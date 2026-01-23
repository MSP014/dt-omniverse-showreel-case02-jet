# Pre-commit Hooks Troubleshooting Guide

**Date:** 2026-01-23
**Case:** 02 - Jet Engine
**Issue:** System Python leakage and pip-audit performance degradation

---

## 🔍 Problem Description

### Issue #1: System Python Leakage

- All `local` hooks in `.pre-commit-config.yaml` configured with `language: system` and `entry: python -m <tool>`
- When executing `git commit`, pre-commit resolved `python` to **system Python** (``C:\Python310\``) instead of the isolated `case01-env`
- System Python had incompatible/broken dependencies:
  - `pytest`: Old version → `ImportError: cannot import name 'FixtureDef'`
  - `bandit`: Missing/corrupted → `ModuleNotFoundError: No module named 'pbr'`
  - `pip-audit`: Running from wrong environment

### Issue #2: pip-audit Performance Degradation

- `pip-audit -r requirements.txt` (file-based audit) **hung for 5+ minutes** without results
- Root cause: Excessive API calls to fetch vulnerability descriptions and progress rendering
- Other projects may have had different pip-audit configurations or cached data

---

## 🩺 Diagnostics Process

### Step 1: Verify Environment

```powershell
python -c "import sys; print(sys.executable)"
# Output: C:\Users\SpeLL\anaconda3\python.exe  ← BASE, NOT case01-env!
```

### Step 2: Analyse Pre-commit Errors

Errors clearly pointed to system Python paths:

```text
C:\Python310\lib\site-packages\_pytest\config\__init__.py:331
C:\Python310\lib\site-packages\bandit\__init__.py
```

### Step 3: Isolate pip-audit Issue

Series of tests from correct environment:

```powershell
# Test 1: File-based audit
C:\Users\SpeLL\anaconda3\envs\case01-env\python.exe -m pip_audit -r requirements.txt
# Result: HANG (>5 minutes)

# Test 2: With --no-deps flag
C:\Users\SpeLL\anaconda3\envs\case01-env\python.exe -m pip_audit -r requirements.txt --no-deps
# Result: HANG

# Test 3: Network check
C:\Users\SpeLL\anaconda3\envs\case01-env\python.exe -c "import requests; print(requests.get('https://api.osv.dev/v1/query').status_code)"
# Result: 405 (network operational)

# Test 4: File-based audit with performance flags
C:\Users\SpeLL\anaconda3\envs\case01-env\python.exe -m pip_audit -r requirements.txt --desc=off --progress-spinner=off
# Result: "No known vulnerabilities found" ← ~10 seconds!
```

**Diagnostic Conclusion:**

1. `language: system` in pre-commit ignores active conda environment
2. File-based `pip-audit -r requirements.txt` hangs when fetching vulnerability descriptions
3. Performance flags (`--desc=off --progress-spinner=off`) resolve the issue

---

## 💡 Solution

### Solution #1: Explicit Project Interpreter Binding

- Replace all `entry: python -m <tool>` with **absolute path**:

  ```yaml
  entry: C:/Users/SpeLL/anaconda3/envs/case01-env/python.exe -m <tool>
  ```

- Use forward slashes (`/`) instead of backslashes (`\`) for Windows path compatibility in YAML

### Solution #2: Optimise pip-audit Performance

- Keep file-based audit (`-r requirements.txt`) for proper lock-file validation
- Add performance flags:
  - `--desc=off`: Skip fetching vulnerability descriptions (reduces API calls)
  - `--progress-spinner=off`: Disable interactive progress rendering

### Solution #3: Use Local Hooks with Explicit Paths

- Remote repositories still had environment conflicts
- Final solution: all tools via `local` hooks with explicit interpreter paths

---

## 🔧 Implementation

**Final `.pre-commit-config.yaml` structure:**

```yaml
# Pre-commit Guardrails - Cross-Platform Path Enforcement
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files
        args: ['--maxkb=10240'] # 10MB limit

  - repo: local
    hooks:
      - id: black
        name: black
        entry: C:/Users/SpeLL/anaconda3/envs/case01-env/python.exe -m black
        language: system
        types: [python]

      - id: isort
        name: isort
        entry: C:/Users/SpeLL/anaconda3/envs/case01-env/python.exe -m isort
        language: system
        types: [python]

      - id: flake8
        name: flake8
        entry: C:/Users/SpeLL/anaconda3/envs/case01-env/python.exe -m flake8
        language: system
        types: [python]

      - id: bandit
        name: bandit
        entry: C:/Users/SpeLL/anaconda3/envs/case01-env/python.exe -m bandit
        language: system
        types: [python]
        args: ["-r", "src", "tools"]
        exclude: "tests/"

      - id: pip-compile-check
        name: pip-compile-check
        entry: C:/Users/SpeLL/anaconda3/envs/case01-env/python.exe -m piptools compile --no-header --quiet --dry-run requirements.in
        language: system
        files: ^requirements\.(in|txt)$
        pass_filenames: false
        always_run: false

      # KEY CHANGE: Performance flags --desc=off --progress-spinner=off
      - id: pip-audit
        name: pip-audit
        entry: C:/Users/SpeLL/anaconda3/envs/case01-env/python.exe -m pip_audit -r requirements.txt --desc=off --progress-spinner=off
        language: system
        pass_filenames: false
        always_run: true

      - id: pytest
        name: pytest
        entry: C:/Users/SpeLL/anaconda3/envs/case01-env/python.exe -m pytest
        language: system
        pass_filenames: false
        always_run: true
```

**Reinstall hooks:**

```powershell
C:\Users\SpeLL\anaconda3\envs\case01-env\python.exe -m pre_commit install --overwrite
```

---

## ✅ Verification

### Step 1: Manual Run of All Hooks

```powershell
C:\Users\SpeLL\anaconda3\envs\case01-env\python.exe -m pre_commit run --all-files
```

**Result:**

```text
trim trailing whitespace.................................................Passed
fix end of files.........................................................Passed
check yaml...............................................................Passed
check for added large files..............................................Passed
black....................................................................Passed
isort....................................................................Passed
flake8...................................................................Passed
bandit...................................................................Passed
pip-compile-check........................................................Passed
pip-audit................................................................Passed  ← INSTANT!
pytest...................................................................Passed

Exit code: 0
```

### Step 2: Real Git Commit

```powershell
git add .pre-commit-config.yaml README.md docs/img/Moskovskiy_av_150/
git commit -m "docs: optimise README aesthetics and repair pre-commit hooks"
```

**Result:**

- All hooks executed correctly
- `pip-audit` completed instantly (instead of hanging)
- Commit created: `e1ba02a`

### Step 3: Push to GitHub

```powershell
git push origin main
```

**Result:**

```text
To github.com:MSP014/dt-omniverse-showreel-case01-msk.git
   761a72c..e1ba02a  main -> main
```

---

## 📊 Before/After Comparison

| Aspect | Before Fix | After Fix |
| --- | --- | --- |
| **Hook Environment** | System Python (``C:\Python310``) | Isolated `case01-env` |
| **pip-audit Mode** | `-r requirements.txt` (hang >5 min) | `-r requirements.txt --desc=off --progress-spinner=off` (~10 sec) |
| **pytest** | ImportError (incompatible version) | ✅ Pass |
| **bandit** | ModuleNotFoundError | ✅ Pass |
| **Commit Time** | Impossible (hang) | ~10 seconds |

---

## 🔄 Applying to Other Cases

For Case 02, 03, 04:

1. **Identify the environment name:**

   ```powershell
   conda env list
   # Look for: case02-env, case03-env, case04-env
   ```

2. **Get absolute Python path:**

   ```powershell
   C:\Users\SpeLL\anaconda3\envs\case0X-env\python.exe -c "import sys; print(sys.executable)"
   ```

3. **Update `.pre-commit-config.yaml`:**
   - Replace `python -m` with `C:/Users/SpeLL/anaconda3/envs/case0X-env/python.exe -m`
   - Update `pip-audit` to use `-r requirements.txt --desc=off --progress-spinner=off`

4. **Reinstall hooks:**

   ```powershell
   C:\Users\SpeLL\anaconda3\envs\case0X-env\python.exe -m pre_commit install --overwrite
   ```

5. **Verify:**

   ```powershell
   C:\Users\SpeLL\anaconda3\envs\case0X-env\python.exe -m pre_commit run --all-files
   ```

---

## 🎯 Key Takeaways

1. **`language: system` is unreliable** with conda environments on Windows
2. **Absolute interpreter paths** ensure correct environment isolation
3. **File-based pip-audit is essential** for proper lock-file validation
4. **Performance flags** (`--desc=off --progress-spinner=off`) resolve pip-audit hangs
5. **Forward slashes** in paths prevent YAML parsing issues on Windows
