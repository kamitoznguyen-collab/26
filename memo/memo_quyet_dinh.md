# Memo quyết định: Trợ lý AI tra cứu tài liệu nội bộ

> Tình huống mẫu (§3.3 đề bài). Các con số là giả định, cần thay bằng dữ liệu đo thật.

## 1. Vấn đề và nguyên nhân gốc
Trợ lý đã triển khai cho nhân viên vận hành (giai đoạn **Deployment**) nhưng nhân viên vẫn tìm file thủ công hoặc hỏi đồng nghiệp. "Ít người dùng" chỉ là triệu chứng. Nguyên nhân gốc:
- **RC1: Thiếu kiến trúc tin cậy.** Câu trả lời không có nguồn và ngày cập nhật, không QA, không có cách báo lỗi, nên người dùng vẫn phải tự kiểm lại.
- **RC2: AI nằm ngoài workflow, không có owner.** Không có bước tra cứu chính thức dùng AI, không data owner, không owner chất lượng.

## 2. Framework và bằng chứng
- **Năm câu hỏi:** Tin cậy và Workflow là GỐC.
- **Gartner-Lite:** Direction ĐẠT; Readiness và Absorption THIẾU, nên chọn pilot nhỏ.
- **ADKAR:** nghẽn ở Desire, nên đào tạo không giải quyết được.
- **Mollick:** AI tìm và tóm tắt; nhân viên kiểm chứng và chịu trách nhiệm; trưởng ca xử lý ngoại lệ; chưa giao bước nào cho AI tự động.
- **Bằng chứng:** E1 case Morgan Stanley (tin cậy đi trước mở rộng); E2 dashboard hiện tại chỉ đo login và số câu hỏi; E3 phỏng vấn người dùng. E2 và E3 sẽ được thu thật bằng log và pulse survey ở tuần 1.

## 3. Thay đổi sau phản biện (v1 → v2)
1. P2: đổi hành động khi xấu thành **cơ chế ngắt mạch** (gỡ SOP lỗi, chuyển 100% cho chuyên gia).
2. W2: chỉ tính câu hỏi thuộc 20 SOP pilot.
3. Thêm **K1** (chu kỳ làm mới tri thức) và **H1** (nhánh chuyển người).
4. Workflow: điều kiện chuyển người đổi từ "confidence < 80%" sang **điều kiện quan sát được**; cổng 0–30 bỏ tiêu chí "100% được đào tạo".

## 4. Quyết định: **SỬA**
Không rollout rộng. Chạy **pilot 90 ngày trên 1 nhóm, 20 SOP** để sửa độ tin cậy và readiness trước.

## 5. Lý do, bước tiếp theo, owner
- **Lý do:** Hướng đi đúng nhưng nền dữ liệu và cơ chế tin cậy còn thiếu. Mở rộng lúc này chỉ nhân rộng việc người dùng không tin AI.
- **Bước tiếp theo:**
  | Giai đoạn | Việc | Owner chính | Qua cổng khi |
  |---|---|---|---|
  | 0–30 | Gắn owner và ngày hiệu lực cho 20 SOP; chạy thử kênh báo lỗi và fallback; đo baseline W1, P1 | Data Owner | 100% SOP có owner và ngày; có baseline |
  | 31–60 | Bắt buộc trích nguồn; QA 50 câu/tuần; theo dõi H1, R1 | Quản lý QA | P1 ≥ 90%, P2 ≤ 5%, R1 ≥ 90%, H1 ≤ 4h, W1 −15% |
  | 61–90 | Đo V1, W2; họp cổng 90 | COO | Mở rộng / Sửa / Dừng theo quy tắc trong dashboard |
