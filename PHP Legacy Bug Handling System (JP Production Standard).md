# 🧠 PHP Legacy Bug Handling System (JP Production Standard)

## 🎯 Mục tiêu
Thiết lập quy trình chuẩn để xử lý bug trong hệ thống PHP legacy:

- Không phá dữ liệu cũ
- Không introduce bug mới
- Có thể audit / trace / scale cho team

---

# 🔄 Tổng quan Pipeline

    Investigate → Fix Plan → QA → Review → Execute

| Phase | Agent            | Mục tiêu                          |
|------|------------------|-----------------------------------|
| 1    | Investigator     | Tìm nguyên nhân + quyết định      |
| 2    | Fix Planner      | Thiết kế cách sửa an toàn         |
| 3    | QA Generator     | Tạo test bảo vệ hệ thống          |
| 4    | Reviewer (opt)   | Validate lần cuối                 |
| 5    | Developer        | Code + Test + Deploy              |

---

# ⚠️ Global Rules (BẮT BUỘC)

- ❗ Không được skip phase  
- ❗ Không fix khi chưa có RCA  
- ❗ Không deploy khi chưa có QA  
- ❗ Evidence > Assumption  
- ❗ Stability > Change  

---

# 🕵️ 1. Investigator Agent

## 🎯 Responsibility
- Root Cause Analysis (RCA)
- Impact Analysis
- Risk vs Value Decision

## ❌ Not Allowed
- Không viết code fix
- Không thiết kế solution chi tiết

---

## 📥 Input
- Symptom  
- Logs / Error  
- Reproduce steps (optional)  

Nếu thiếu:

    ⚠️ Insufficient data for investigation

---

## 📤 Output

### 🔍 RCA Report

#### 1. Root Cause
- Cause:
- Evidence:
  - Log:
  - SQL:
  - Data sample:

#### 2. Impact (Triple-A)
- Data:
- Behavior:
- Scope:

#### 3. Risk vs Value
- Risk:
- Value:
- Decision: (No Fix / Workaround / Fix)

#### 4. Options (High-level only)
- A: Permanent Fix  
- B: Workaround  

---

# 🛠️ 2. Fix Planner Agent

## 🎯 Responsibility
- Convert RCA → Fix Plan
- Ensure backward compatibility

---

## 📥 Input
- RCA Report

---

## 🔍 Checklist

### 1. Validate Decision
- Nếu No Fix → STOP

### 2. Fix Strategy
- Guard (if condition)
- Data patch
- Minimal logic change

### 3. Legacy Safety
- Không break data cũ  
- Không refactor lớn  
- Không đổi schema nếu không cần  

---

## 📤 Output

### 🛠️ Fix Plan

#### 1. Strategy
- Type: (Guard / Patch / Logic Fix)

#### 2. Implementation
- File:
- Function:
- Change detail:

#### 3. Risk Control
- Backward compatibility:
- Failure scenario:

#### 4. Rollback Plan
- Steps:

#### 5. Notes
- Lý do chọn solution (JP mindset)

---

# 🧪 3. QA Generator Agent

## 🎯 Responsibility
- Generate test scenarios
- Cover edge + abnormal + regression

---

## 📥 Input
- Fix Plan / RCA

Nếu thiếu:

    ⚠️ Insufficient context for QA generation

---

## 📤 Output

### 🧪 QA Test Plan

#### 1. Summary
- Affected Area:
- Risk Level:

---

## 2. Test Cases

### ✅ Normal Cases
- TC01:
- TC02:

---

### 🔹 Edge Cases (VALID)
- null / ""
- 0 / negative
- boundary values
- large dataset
- date boundary

---

### ⚠️ Abnormal Cases (INVALID)
- Wrong data type
- Missing required field
- Inconsistent data
- Legacy dirty data
- Security input (SQLi / XSS)

---

## 3. Regression Test (Impact-based)

### Direct Impact
- Function / API bị sửa

### Indirect Impact
- Shared logic
- Batch / cron

### Data Flow
- Input → Process → Output

### Historical Data
- Data cũ có bị ảnh hưởng không

### Integration
- External API
- Async job

---

## 4. Performance
- Query impact
- Loop impact

---

## 5. Monitoring
- Logs:
- Metrics:
- Alert:

---

## 6. Rollback Condition
- Trigger:
- Symptom:

---

# 🔍 4. Reviewer Agent (Optional)

## 🎯 Responsibility
- Validate toàn bộ pipeline trước khi dev code

---

## 📥 Input
- RCA
- Fix Plan
- QA Plan

---

## 📤 Output

### 🔍 Review Result
- Logical consistency:
- Risk acceptable:
- Missing cases:
- Final decision: (Approve / Revise)

---

# 👨‍💻 5. Developer Execution

## Checklist

- [ ] Code theo Fix Plan  
- [ ] Test theo QA Plan  
- [ ] Verify rollback  
- [ ] Add logging nếu cần  

---

# 🔄 Workflow thực tế

## Step 1 — Investigate

    #investigate
    <bug description + log>

## Step 2 — Fix Plan

    #fix
    <RCA output>

## Step 3 — QA

    #qa
    <Fix Plan>

## Step 4 — Review (optional)

    #review
    <RCA + Fix + QA>

## Step 5 — Execute
- Dev implement  
- QA verify  
- Deploy  

---

# 📌 PR Template

    ## 🧠 RCA
    (paste từ Investigator)

    ## 🛠️ Fix Plan
    (paste từ Fix Planner)

    ## 🧪 QA Plan
    (paste từ QA Generator)

    ## ✅ Checklist
    - [ ] Tested normal case
    - [ ] Tested edge cases
    - [ ] Tested abnormal cases
    - [ ] Regression verified

---

# ⚠️ Anti-Patterns (CẤM)

- ❌ Fix ngay không RCA  
- ❌ Test mỗi happy path  
- ❌ Ignore legacy data  
- ❌ Refactor lớn khi fix bug nhỏ  
- ❌ Không có rollback plan  

---

# 🚀 Advanced (Optional)

## Auto Guard Rule
Nếu Abnormal case có thể crash → MUST add validation

## Coverage Rule
Mỗi function phải có:
- 1 normal test
- 1 edge test
- 1 abnormal test

## Risk Priority

| Risk | Action     |
|------|------------|
| High | Full test  |
| Medium | Focus test |
| Low | Sanity test |

---

# 🎯 Kết luận

Hệ thống này đảm bảo:

- Bug được hiểu đúng trước khi sửa  
- Fix không phá hệ thống legacy  
- QA có chiều sâu, không hời hợt  
- Team làm việc theo chuẩn, không cảm tính  
