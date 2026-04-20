# 🛡 PHP Legacy Bug Investigation Skill

### JP High-Quality Engineering Edition

---

## 🎯 Overview

**PHP Legacy Bug Investigation Skill** là framework điều tra bug dành cho:

* Hệ thống PHP lâu năm
* Code base phức tạp, thiếu tài liệu
* Hệ thống có nguy cơ domino effect
* Dự án có vấn đề latency
* Khách hàng Nhật yêu cầu chất lượng cao và quản trị rủi ro chặt chẽ

Skill này giúp:

* Chuẩn hóa quy trình điều tra
* Định lượng rủi ro trước khi fix
* Giảm degrade bug
* Minh bạch công số & phạm vi ảnh hưởng
* Tăng uy tín với khách hàng Nhật

---

## 🧠 Engineering Philosophy

Trong hệ thống legacy:

> 1 dòng code có thể ảnh hưởng 10 workflow
> 1 assumption sai có thể mất 1 tháng giải trình

Nguyên tắc:

* Stability > Speed
* Không fix khi assumption chưa xác minh
* Luôn có Risk Score
* Luôn có Regression Impact Matrix
* Luôn có Test Man-hour estimation
* Luôn có Option A/B/C

---

## 🧩 Core Components

### 1️⃣ Root Cause Analysis (RCA)

Phân tích 3 tầng:

1. Surface Cause (triệu chứng)
2. Technical Root Cause (logic / DB / performance)
3. Contextual Cause (vì sao xảy ra trong bối cảnh legacy)

---

### 2️⃣ Assumption & Verification Guardrail

Bắt buộc liệt kê:

* Các điểm chưa rõ ràng
* Các giả định đang tồn tại
* Nội dung cần xác minh
* Rủi ro nếu assumption sai

⚠ Không finalize solution nếu assumption critical còn Pending.

---

### 3️⃣ Proposed Solutions (A/B/C)

| Option | Meaning                      |
| ------ | ---------------------------- |
| A      | Structural / Radical fix     |
| B      | Minimal safe fix             |
| C      | Business adjustment / No fix |

---

### 4️⃣ Risk Scoring Formula

Risk Score = (Impact × Complexity × Data Sensitivity) + Regression Factor

#### Risk Level

| Score | Level    | Action                        |
| ----- | -------- | ----------------------------- |
| 0–7   | Low      | Safe to fix                   |
| 8–14  | Medium   | Extended testing required     |
| 15–20 | High     | Client discussion recommended |
| 21+   | Critical | Avoid direct fix              |

---

### 5️⃣ Regression Impact Matrix

Xác định:

* Module bị ảnh hưởng
* Workflow liên quan
* Loại test cần thực hiện
* Nguy cơ degrade bug

---

### 6️⃣ Effort Estimation

Phải tách rõ:

* Investigation
* Fix implementation
* Unit Test
* Integration Test
* Regression Test
* Buffer risk

⚠ Trong legacy system, test effort thường lớn hơn fix effort.

---

### 7️⃣ QA Strategy

Bao gồm:

* Boundary test
* Full-width character test (全角)
* Legacy data compatibility test
* Performance benchmark before/after
* Production-like data simulation

---

### 8️⃣ Client Communication Strategy (JP)

Nguyên tắc:

* Data-driven
* So sánh Option A/B/C
* Minh bạch công số
* Nhấn mạnh quản trị rủi ro
* Ưu tiên ổn định hơn fix nhanh

---

### 9️⃣ PM Quick One-Page Mode

Tóm tắt gồm:

* Root cause
* Recommended option
* Risk score
* Total cost
* Client discussion required (Yes/No)

---

## 🔎 Assumption Checklist (Auto Apply)

Khi đọc code legacy, luôn xác minh:

### Database

* Data type thực tế
* NULL & default value
* Index & query plan
* Data volume
* Soft delete flag
* Encoding

### Business Logic

* Hidden JP-specific rules
* Workflow dependency
* Batch / cron job
* External API

### Technical

* PHP version
* Deprecated functions
* Transaction boundary
* Cache layer
* Error handling

### Performance

* N+1 query
* Full table scan
* Lock / deadlock
* Blocking I/O

### Regression

* Legacy user behavior dependency
* External integration
* Boundary value / edge cases

---

## 🚀 How to Use in Cursor

### 1️⃣ Installation

Create:

```
.cursor/skills/php-legacy-investigation/SKILL.md
```

Paste the Skill content and commit.

---

### 2️⃣ Basic Usage

```
Use php-legacy-investigation skill.

Bug:
[Bug description]

System: PHP 5.x
DB: MySQL 5.x
```

---

### 3️⃣ Investigation Only Mode

```
Use php-legacy-investigation skill.
Investigation only. Do not finalize solution until assumptions verified.
```

Use when:

* Root cause chưa rõ
* Cần xác minh DB / business rule
* Cần trình PM trước

---

### 4️⃣ After Assumption Verification

```
All assumptions verified.
Regenerate final report.
```

---

### 5️⃣ PM Quick Mode

```
Generate PM Quick One-Page Mode only.
```

---

### 6️⃣ Performance Focus Mode

```
Focus on performance regression risk and query plan impact.
```

Skill sẽ:

* Phân tích index
* Kiểm tra N+1 query
* Đánh giá full table scan
* Phân tích lock/deadlock risk

---

## 🧭 Recommended Workflow (PM / SA)

1. Dev generate Investigation Report
2. PM kiểm tra Risk Score
3. Nếu ≥ 15 → họp nội bộ
4. Nếu > 20 → cân nhắc Option C
5. Soạn communication cho khách hàng nếu cần

---

## 🛑 When NOT to Use This Skill

* UI bug nhỏ
* Không liên quan DB
* Không có workflow dependency
* Dự án mới có test coverage đầy đủ

Skill này dành cho:

> Legacy + High Risk + Japanese Enterprise Projects

---

## 📈 Maturity Levels

| Level      | Usage                           |
| ---------- | ------------------------------- |
| Basic      | Generate report                 |
| Advanced   | Use Risk Score for decision     |
| Expert     | Gatekeeper before merge         |
| Enterprise | Block fix if assumption pending |

---

## 🛡 Governance Rule

* Không fix khi assumption chưa verify
* Không bỏ qua regression matrix
* Không underestimate test effort
* Không quyết định khi chưa định lượng risk

---

## 🏁 Conclusion

Đây không chỉ là template report.

Nó là:

* Hệ thống quản trị rủi ro
* Cơ chế bảo vệ hệ thống legacy
* Công cụ xây dựng niềm tin với khách hàng Nhật
* Framework kiểm soát chất lượng nội bộ

---

**Stability over Speed
Risk visibility over assumption
Quality over quick fix**
