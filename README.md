# Báo cáo Lab Day 26: Áp dụng AI (Track 01)
## Đề tài: Tái thiết kế Workflow & Dashboard Hành động cho Trợ lý AI Tra cứu Quy trình Nội bộ (SOP)
**Nhóm:** `<Ten_Nhom>` *(Tạm thời, chờ điền tên nhóm chính thức)*

---

### 1. Bảng thành viên & Đóng góp
| Họ và tên | MSSV | Phần phụ trách | Góp ý cho nhóm bạn (Ghi rõ nhóm nào) |
|---|---|---|---|
| *(Điền Họ tên 1)* | *(Điền MSSV 1)* | Bước 0–2: Phạm vi & Chẩn đoán; Bước 5: Dashboard v1 | *(Điền góp ý cụ thể cho nhóm bạn)* |
| *(Điền Họ tên 2)* | *(Điền MSSV 2)* | Bước 3–4: Thiết kế TO-BE & Lộ trình 30–60–90; Bước 7: Dựng Repo | *(Điền góp ý cụ thể cho nhóm bạn)* |
| *(Điền Họ tên 3)* | *(Điền MSSV 3)* | Bước 6: Phản biện chéo, Memo quyết định & Dashboard v2 | *(Điền góp ý cụ thể cho nhóm bạn)* |

> *Lưu ý (§6.3):* Bảng thành viên trên là mẫu khung *(số lượng thành viên điền theo thực tế nhóm)*. Quá trình trao đổi, phản biện nội bộ Claude ↔ Anti không thay thế yêu cầu phản biện chéo với nhóm bạn trong lớp.

---

### 2. Phạm vi khoá (Scope)
- **Sản phẩm:** Trợ lý AI tra cứu tài liệu nội bộ (giới hạn trong kho 20 SOP vận hành cốt lõi *(giả định)*).
- **Người dùng:** Nhóm nhân viên vận hành nòng cốt (15 nhân sự pilot *(giả định)*).
- **Workflow:** (1) Tra cứu SOP qua AI → (2) AI trích nguồn + ngày hiệu lực → (3) Nhân viên kiểm chứng nhanh ≤ 30s trước khi áp dụng vào ca xử lý.

---

### 3. Nguyên nhân gốc (Root Causes)
- **RC1 (Thiếu kiến trúc tin cậy):** AI trả lời không trích nguồn, không ngày cập nhật, không QA mẫu, không kênh báo lỗi khiến nhân viên phải tự kiểm lại thủ công.
  - *Framework:* Năm câu hỏi (Trục Tin cậy = GỐC) + ADKAR (Nghẽn chính ở Desire, đào tạo không giải quyết được).
  - *Bằng chứng:* E1 (Case tham khảo Morgan Stanley: độ tin cậy đi trước mở rộng); E3 *(giả định, sẽ thu bằng Pulse Survey tuần 1 với 5 nhân sự)*: "không biết bản nào mới, vẫn phải tự mở file kiểm tra".
- **RC2 (AI nằm ngoài workflow, thiếu Governance):** Chưa có bước tra cứu chính thức bằng AI trong luồng xử lý ca, thiếu Data Owner quản lý kho tri thức và thiếu Owner chịu trách nhiệm chất lượng.
  - *Framework:* Năm câu hỏi (Trục Workflow = GỐC) + Gartner-Lite (Direction ĐẠT; Readiness & Absorption THIẾU, cần pilot sửa nền trước).
  - *Bằng chứng:* E2 *(giả định, sẽ thu từ log dashboard hiện trạng ở tuần 1)*: hiện chỉ đo số lần đăng nhập và số lượng câu hỏi tầng 1, không đo chất lượng.

---

### 4. Cách làm mới (TO-BE & Phân công Mollick)
- **3 thay đổi bắt buộc:** (1) Bắt buộc trích dẫn văn bản + số điều khoản + ngày cập nhật gần nhất; (2) Nhân viên xử lý ca chịu trách nhiệm kết quả cuối; (3) Fallback quan sát được (tự động chuyển chuyên gia SOP khi thiếu nguồn/mâu thuẫn/ngoài 20 SOP) + nút báo lỗi 1-click SLA 48h.
- **Phân công Mollick:** Con người giữ quyền (duyệt ca, duyệt phát hành SOP); AI hỗ trợ tìm kiếm & trích nguồn; **tuyệt đối không** dùng AI tự động hoàn toàn ở bài toán này do rủi ro sai lệch quy trình cao.

---

### 5. Chỉ số hành động (Dashboard v2)
*Mốc đầu (Baseline) sẽ đo ở tuần 1 bằng log ca và QA mẫu 50 câu.* Hệ thống theo dõi 8 chỉ số trên 5 tầng (Dashboard chi tiết tại `dashboard/dashboard_hanh_dong_v2.xlsx`):

| ID | Chỉ số | Loại | Mốc đầu (Baseline tuần 1) | Mục tiêu | Nguồn dữ liệu | Phụ trách (Owner) |
|---|---|---|---|---|---|---|
| **P1** | % câu trả lời có trích nguồn + ngày hợp lệ (20 SOP pilot) | Product (Tầng 4) | Đo mẫu 50 câu, tuần 1 | ≥ 90% (ngày 60) | QA mẫu hằng tuần | Phụ trách AI/QA |
| **P2** | % câu trả lời sai hoặc lỗi thời (kèm cơ chế ngắt mạch) | Product (Tầng 4) | Đo mẫu 50 câu, tuần 1 | ≤ 5% | QA mẫu + log lỗi | Quản lý QA |
| **W1** | Thời gian hoàn thành 1 lượt tra cứu ca | Workflow (Tầng 3) | Log ca tuần 1 (AS-IS) | −15% (ngày 60), −30% (ngày 90) | Log tác vụ / ticket | Chủ quy trình vận hành |
| **W2** | % lượt tra cứu đi qua luồng AI (chỉ tính 20 SOP pilot) | Workflow (Tầng 2) | Đo tuần 1 pilot | ≥ 60% | Log quy trình + trợ lý | Trưởng nhóm pilot |
| **H1** | Tỷ lệ chuyển người & thời gian phản hồi chuyên gia SOP | Workflow (Tầng 4) | Đo từ khi bật fallback | Phản hồi ≤ 4h; chuyển ≤ 20% | Log fallback | Quản lý QA |
| **R1** | % báo lỗi được xử lý trong 2 ngày làm việc | Workflow (Tầng 4) | 0 (chưa có kênh) | ≥ 90% | Log báo lỗi | Phụ trách AI |
| **K1** | Thời gian từ báo lỗi đến khi SOP sửa phát hành vào kho | Workflow (Tầng 4) | Đo từ lỗi đầu tiên | ≤ 5 ngày làm việc | Log lỗi + phiên bản SOP | Data Owner |
| **V1** | Sự cố nghiệp vụ do áp dụng tài liệu lỗi thời / tháng | Workflow (Tầng 5) | Số hiện tại hệ thống sự cố | Giảm so với mốc đầu | Hệ thống sự cố/nghiệp vụ | Giám đốc Vận hành (COO) |

---

### 6. Quyết định & Thay đổi so với v1
- **Quyết định:** **SỬA** (chạy pilot 90 ngày trên 1 nhóm nòng cốt và 20 SOP; sửa độ tin cậy và hoàn thiện readiness trước khi tính chuyện mở rộng).
- **5 thay đổi cốt lõi so với v1:**
  1. **P2 (Hành động khi xấu):** Đổi từ "thu hẹp kho" chung chung thành **cơ chế ngắt mạch** (tự động gỡ tag active của SOP lỗi, chuyển 100% câu hỏi sang chuyên gia SOP).
  2. **W2 (Chỉ số):** Loại trừ câu hỏi ngoài 20 SOP pilot khỏi mẫu số đánh giá tỷ lệ áp dụng AI.
  3. **Thêm K1 (Chỉ số):** Đo chu kỳ làm mới tri thức từ lúc báo lỗi đến khi SOP cập nhật được phát hành vào kho.
  4. **Thêm H1 (Chỉ số):** Theo dõi nhánh chuyển người (Fallback) và thời gian phản hồi của chuyên gia SOP.
  5. **Khoá phạm vi & Lộ trình:** Khoá cứng 20 SOP có Data Owner và bổ sung mốc kiểm soát W1 trung gian ngày 60 (−15%) khớp với cổng 31–60.

---

## Cấu trúc thư mục Repo nộp bài
```
├── README.md
├── dashboard/
│   └── dashboard_hanh_dong_v2.xlsx
├── memo/
│   └── memo_quyet_dinh.md
└── v1/
    └── dashboard_hanh_dong_v1.xlsx
```
