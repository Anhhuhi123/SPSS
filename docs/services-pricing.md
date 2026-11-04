# Gói dịch vụ và bảng giá khởi điểm

> Nguồn: trích từ `PLAN.md` mục 3. Khi sửa, sửa file này trước rồi cập nhật PLAN.md.

## Logic định giá

- **Neo theo giá thị trường** (`PLAN.md` mục 1.3), định giá ngang hoặc thấp hơn khoảng 10%, vì mình là thương hiệu mới chưa có review.
- **Không bán phá giá.** Giá trị khác biệt nằm ở bàn giao (syntax, log, buổi 1:1), nên không cần rẻ nhất.
- **Nâng cấp được:** phí gói trước được trừ vào gói sau. Ví dụ đã mua Rà soát 300k, lên SPSS thì trừ 300k.
- Website ghi giá dạng **"từ X"**, "Dịch vụ khác" ghi "báo giá theo yêu cầu". Báo giá cuối cùng gửi sau khi chẩn đoán qua tin nhắn.

## Bảng giá (khớp với website)

**3 dịch vụ chính** (hiện trên web, đi theo luồng 01 → 02 → 03, khách mua riêng từng bước được):

| # | Dịch vụ | Nội dung (như trên web) | Bàn giao | Giá trên web |
|---|---|---|---|---|
| 01 | **Tạo dữ liệu khảo sát** (Data Collection Support) | Dựng Google Form; triển khai khảo sát, thu phản hồi thực tế; theo dõi số phản hồi theo yêu cầu; xuất Excel | Excel (.xlsx) | **từ 1.000đ / phiếu** (tính trên mỗi phiếu trả lời thu được) |
| 02 | **Xử lý dữ liệu** (Data Processing) | Kiểm tra, làm sạch, mã hóa biến; xử lý thiếu và bất thường theo tiêu chí thống nhất; chuẩn hóa để đưa vào SPSS | Excel + SPSS (.sav) + Cleaning log | **từ 300.000đ** |
| 03 | **Hỗ trợ phân tích SPSS** (Statistical Analysis) ⭐ Phổ biến nhất | Thống kê mô tả, Cronbach's Alpha, EFA, Pearson, hồi quy tuyến tính, T-test/ANOVA, kiểm tra giả định, giải thích kết quả và hướng dẫn đọc output | File dữ liệu + Syntax (.sps) + Báo cáo kết quả | **từ 500.000đ** |

**Mốc báo giá nội bộ cho dịch vụ 03** (không ghi trên web, dùng khi báo giá qua tin nhắn):

| Phạm vi | Giá tham khảo |
|---|---|
| Bài tập môn: mô hình nhỏ (≤ 5 biến), mô tả + Cronbach + EFA + hồi quy, giải thích ngắn | 500.000đ |
| Cơ bản: Cronbach + EFA *hoặc* Pearson + hồi quy | 700.000đ |
| Trọn bộ: tất cả kiểm định ở trên + giải đáp qua tin nhắn | 1.800.000đ |

**Dịch vụ khác** (thẻ thứ 4 trên web, ghi "Báo giá theo yêu cầu"). Giá dưới đây là mốc nội bộ:

| Dịch vụ | Nội dung | Bàn giao | Giá tham khảo |
|---|---|---|---|
| **Mock data** | Sinh data sát thực tế theo đúng mô hình (số biến, item, thang Likert, cỡ mẫu, tương quan hợp lý) để chạy thử mô hình ngay | `mock_data.sav` + `.xlsx` + codebook | 150.000đ |
| **Dữ liệu đã công bố** | Tìm bộ khảo sát đã công bố cùng chủ đề (Kaggle, Mendeley Data, OSF, Harvard Dataverse, GSO, World Bank…), chuẩn hóa cho SPSS, kèm trích dẫn | Dataset + trích dẫn | 250.000đ |
| Combo Mock + Công bố | Dựng mô hình trên mock trước, có bộ công bố thì chạy lại | Cả hai bộ + pipeline | 350.000đ |
| **Rà soát đề tài, mô hình, bảng hỏi** | Góp ý mô hình, giả thuyết, thang đo, bảng hỏi; đề xuất cỡ mẫu và phương pháp | Research Assessment + Analysis Plan | 300.000đ |
| **AMOS / SmartPLS** | CFA (CR, AVE, HTMT), SEM/PLS-SEM, trung gian/điều tiết, bootstrap | Project file + Report + hướng dẫn | 1.800.000đ (CFA) · 2.800.000đ (CFA + SEM) |
| **Đồng hành trọn đề tài** | Cả 6 bước, dàn ý chương 3–4, câu hỏi bảo vệ soạn sẵn, hỗ trợ Zalo đến ngày bảo vệ | Toàn bộ deliverables | 3.500.000đ |
| Yêu cầu khác về số liệu | Đánh giá từng trường hợp | n/a | Báo giá riêng |

## Điều khoản chung

| Mục | Đề xuất |
|---|---|
| Chẩn đoán ban đầu | **Miễn phí**, qua tin nhắn Zalo: khách gửi file, nhận đánh giá + báo giá trong 24 giờ |
| Đặt cọc | 50% khi chốt phạm vi, 50% khi bàn giao |
| Gấp (< 48 giờ) | +30% |
| Phụ phí độ phức tạp | Trung gian / điều tiết / biến bậc hai: +20–40%. Trên 8 biến tiềm ẩn: báo giá riêng |
| Chỉnh sửa | Miễn phí 2 lần trong 30 ngày, *trong phạm vi gói*, theo góp ý của giảng viên |
| Hoàn tiền | Hoàn 100% cọc nếu mình chưa bắt đầu; hoàn theo tỷ lệ nếu không giao được đúng phạm vi |
| Bảo mật | Không chia sẻ dữ liệu; xóa sau 90 ngày kể từ bàn giao hoặc theo yêu cầu |
| Ưu đãi ra mắt (tùy chọn) | Giảm 20% cho 10 khách đầu tiên, đổi lấy feedback hoặc testimonial |
