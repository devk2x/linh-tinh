# 🧠 PHP Legacy Bug Handling System (JP Production Standard)

## 🎯 Purpose
Standardize bug handling process for PHP legacy systems to ensure:

- No data corruption
- No unintended side effects
- Clear investigation and traceability
- Scalable for team usage

---

# 🔄 Workflow Overview

    Investigate → Fix Plan → QA → Review → Execute

---

# ⚠️ Global Rules (MUST FOLLOW)

- ❗ Do NOT skip steps
- ❗ Do NOT fix without RCA
- ❗ Do NOT deploy without QA
- ❗ Evidence > Assumption
- ❗ Stability > Change

---

# 🧩 Commands (For Developers)

| Command        | Purpose                     |
|----------------|-----------------------------|
| `#investigate` | Find root cause             |
| `#fix`         | Generate fix plan           |
| `#qa`          | Generate test scenarios     |
| `#review`      | (Optional) Validate overall |

---

# 🕵️ 1. Investigate

## Usage

    #investigate
    Bug: <description>
    Log: <error/log>
    Module: <optional>

---

## Output

- Root Cause (with evidence)
- Impact (data / behavior / scope)
- Risk vs Value
- Decision (Fix / No Fix / Workaround)

---

# 🛠️ 2. Fix Plan

## Usage

    #fix
    <paste RCA output>

---

## Output

- Fix strategy (Guard / Patch / Logic Fix)
- Affected file / function
- Risk control
- Rollback plan

---

# 🧪 3. QA

## Usage

    #qa
    <paste Fix Plan>

---

## Output

### Test Coverage

#### ✅ Normal Cases
- Expected usage

#### 🔹 Edge Cases (VALID)
- null / empty
- 0 / negative
- boundary values
- large dataset

#### ⚠️ Abnormal Cases (INVALID)
- wrong data type
- missing field
- inconsistent data
- legacy dirty data
- security input (SQLi / XSS)

---

### 🔁 Regression Test (Impact-based)

#### Direct Impact
- Modified functions / APIs

#### Indirect Impact
- Shared logic
- Batch / cron jobs

#### Data Flow
- Input → Process → Output

#### Integration
- External APIs
- Async jobs

---

### ⚡ Performance
- Query impact
- Loop complexity

---

### 📊 Monitoring
- Logs to track
- Metrics
- Alerts

---

### 🔙 Rollback
- Trigger conditions
- Failure symptoms

---

# 🔍 4. Review (Optional)

## Usage

    #review
    <RCA + Fix + QA>

---

## Output

- Logical consistency
- Risk validation
- Missing cases
- Final decision (Approve / Revise)

---

# 👨‍💻 5. Developer Execution

## Checklist

- [ ] Follow Fix Plan
- [ ] Execute QA Plan
- [ ] Verify rollback
- [ ] Add logging if needed

---

# 📌 Pull Request Template
