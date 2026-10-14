# Báo cáo Lab Day 26: Áp dụng AI (Track 01)
## Đề tài: Tái thiết kế Workflow & Dashboard Hành động cho Trợ lý AI Tra cứu Quy trình Nội bộ (SOP)

---

### 1. Bảng thành viên & Đóng góp
| Họ và tên | MSSV | Phần phụ trách | Góp ý cho nhóm bạn (Nhóm ...) |
|---|---|---|---|
| *(Điền Họ tên 1)* | *(Điền MSSV 1)* | Bước 0–2: Phạm vi & Chẩn đoán; Bước 5: Dashboard v1 | *(Điền góp ý cụ thể cho nhóm bạn)* |
| *(Điền Họ tên 2)* | *(Điền MSSV 2)* | Bước 3–4: Thiết kế TO-BE & Lộ trình 30–60–90; Bước 7: Dựng Repo | *(Điền góp ý cụ thể cho nhóm bạn)* |
| *(Điền Họ tên 3)* | *(Điền MSSV 3)* | Bước 6: Phản biện chéo, Memo quyết định & Dashboard v2 | *(Điền góp ý cụ thể cho nhóm bạn)* |

> *Ghi chú:* Quá trình phản biện chéo 2 chiều (Claude ↔ Anti) đã hoàn thành tại outbox trao đổi nội bộ. Mục "Góp ý cho nhóm bạn" dành để ghi nhận góp ý cho nhóm lớp theo đúng yêu cầu §6.3.

---

### 2. Phạm vi khoá (Scope)
- **Sản phẩm:** Trợ lý AI tra cứu tài liệu nội bộ (kho 20 SOP vận hành cốt lõi *(giả định)*).
- **Người dùng:** Nhóm nhân viên vận hành nòng cốt (15 nhân sự pilot *(giả định)*).
- **Workflow:** (1) Tra cứu SOP qua AI → (2) AI trích nguồn + ngày hiệu lực → (3) Nhân viên kiểm chứng nhanh ≤ 30s trước khi áp dụng.

---

### 3. Nguyên nhân gốc (Root Causes)
- **RC1 (Thiếu kiến trúc tin cậy):** AI trả lời không trích nguồn, không ngày cập nhật, không QA mẫu, không kênh báo lỗi khiến nhân viên phải kiểm chứng lại thủ công.
- **RC2 (AI nằm ngoài workflow, thiếu Governance):** Không có bước tra cứu bắt buộc dùng AI, thiếu Data Owner quản lý kho tri thức và thiếu Owner chịu trách nhiệm chất lượng câu trả lời.

---

### 4. Cách làm mới (TO-BE & Phân công Mollick)
- **3 thay đổi bắt buộc:** (1) Bắt buộc trích dẫn văn bản + điều khoản + ngày cập nhật gần nhất; (2) Nhân viên xử lý ca chịu trách nhiệm kết quả cuối; (3) Fallback quan sát được (tự động chuyển chuyên gia SOP khi thiếu nguồn/mâu thuẫn/ngoài 20 SOP) + nút báo lỗi 1-click SLA 48h.
- **Phân công Mollick:** Con người giữ quyền (duyệt ca, duyệt SOP); AI hỗ trợ tìm & trích nguồn; **tuyệt đối không** dùng AI tự động hoàn toàn ở bài toán này.

---

### 5. Chỉ số hành động (Dashboard v2)
Theo dõi 8 chỉ số trên 5 tầng, mốc đầu đo bằng dữ liệu thực chứng (log ca và QA mẫu tuần 1):
- **Chất lượng & Tin cậy:** P1 (Trích nguồn hợp lệ ≥ 90%), P2 (Câu trả lời sai/cũ ≤ 5% kèm cơ chế ngắt mạch), H1 (Tỷ lệ chuyển người ≤ 20%, phản hồi ≤ 4h), R1 (Xử lý lỗi ≤ 48h đạt ≥ 90%), K1 (Làm mới SOP vào kho ≤ 5 ngày).
- **Hành vi & Năng suất & Giá trị:** W2 (Tỷ lệ tra cứu qua AI ≥ 60% trên 20 SOP pilot), W1 (Thời gian tra cứu giảm 15% ở ngày 60 và giảm 30% ở ngày 90), V1 (Sự cố nghiệp vụ do sai SOP giảm).

---

### 6. Quyết định & Thay đổi so với v1
- **Quyết định:** **SỬA** (chạy pilot 90 ngày trên 1 nhóm nòng cốt và 20 SOP; chưa mở rộng rollout toàn công ty).
- **5 thay đổi cốt lõi so với v1:**
  1. **P2:** Đổi từ "thu hẹp kho" chung chung thành **cơ chế ngắt mạch** (tự động gỡ tag active của SOP lỗi, chuyển 100% câu hỏi sang chuyên gia).
  2. **W2:** Loại trừ các câu hỏi ngoài 20 SOP pilot khỏi mẫu số đánh giá tuân thủ quy trình.
  3. **Thêm K1:** Đo chu kỳ làm mới tri thức từ lúc báo lỗi đến khi cập nhật vào kho SOP.
  4. **Thêm H1:** Bổ sung chỉ số đo lường nhánh chuyển người (Fallback).
  5. **Khoá phạm vi:** Chốt cứng 20 SOP có Data Owner và bổ sung mốc kiểm soát W1 trung gian ngày 60.

---

## Cấu trúc thư mục Repo
```
├── README.md
├── dashboard/
│   └── dashboard_hanh_dong_v2.xlsx
├── memo/
│   └── memo_quyet_dinh.md
└── v1/
    └── dashboard_hanh_dong_v1.xlsx
```
