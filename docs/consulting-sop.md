# Quy trình consulting

> Nguồn: trích từ `PLAN.md` mục 5. Khi sửa, sửa file này trước rồi cập nhật PLAN.md.

> Quy trình cho **người vận hành** (bạn), từ lúc có lead đến sau khi bàn giao.
>
> **v2: Mô hình "tư vấn qua tin nhắn + Claude Code làm chuyên môn":**
>
> | Việc | Ai làm |
> |---|---|
> | Nhắn tin với khách, nhận file, gửi file | **Bạn** |
> | Chẩn đoán đề tài, chọn phương pháp, viết giải thích | **Claude Code** soạn → bạn đọc lại → gửi |
> | Trả lời câu hỏi chuyên môn của khách ("Sig. 0.07 thì sao?", "sao EFA ra 6 nhân tố?") | Bạn paste câu hỏi vào Claude Code bằng `/reply <case_id>` → Claude Code soạn câu trả lời giọng thân thiện, dễ hiểu → bạn gửi |
> | Xử lý data, chạy phân tích, xuất file | Claude Code (bạn giám sát) |
> | Kiểm tra cuối | Bạn chạy `/qa`; mục nào Claude Code đánh dấu "cần người kiểm" thì bạn xem |
>
> **Không có cuộc gọi hay buổi họp.** Toàn bộ "buổi 1:1" ở v1 được thay bằng: Analysis Report viết kỹ, video quay màn hình ngắn (tùy chọn, quay lúc chạy lại syntax), và giải đáp qua tin nhắn không giới hạn trong 30 ngày.

## Vòng đời một đơn (case)

```
 Khách nhắn ─► Chẩn đoán ─► Báo giá ─► Cọc ─► Thực hiện (6 bước) ─► QA ─► Bàn giao ─► Hậu mãi ─► Đóng case
  │                                         ▲
  └ Zalo / Facebook / Email (status: NEW)    └ Claude Code làm phần kỹ thuật
```

| Status (lưu trong `case.yaml`) | Ý nghĩa | Ai làm | SLA |
|---|---|---|---|
| `NEW` | Khách vừa nhắn lần đầu | Tư vấn viên | n/a |
| `CONTACTED` | Đã trả lời, đang xin tài liệu | Tư vấn viên | ≤ 24 giờ |
| `DIAGNOSED` | Đã chẩn đoán xong | Tư vấn viên + Claude Code | ≤ 48 giờ |
| `QUOTED` | Đã gửi báo giá và thỏa thuận | Tư vấn viên | Cùng ngày chẩn đoán |
| `DEPOSITED` | Đã nhận cọc 50%, tạo thư mục case | Tư vấn viên | n/a |
| `IN_PROGRESS` | Đang thực hiện các bước | Claude Code + tư vấn viên | Theo gói |
| `QA` | Kiểm tra chất lượng | Tư vấn viên | ≤ 1 ngày |
| `DELIVERED` | Đã bàn giao và gửi tin nhắn giải thích | Tư vấn viên | n/a |
| `REVISION` | Sửa theo góp ý của giảng viên | Claude Code + tư vấn viên | ≤ 2 ngày/lần |
| `CLOSED` | Thanh toán đủ, xin feedback | Tư vấn viên | n/a |
| `LOST` / `REJECTED` | Không chốt / từ chối do vi phạm `service-scope.md` | Tư vấn viên | n/a |

## Chi tiết từng giai đoạn

### Giai đoạn A: Tiếp nhận và chẩn đoán (miễn phí)

1. Khách nhắn qua Zalo (hoặc Facebook/Email). Trả lời trong 24 giờ theo **script mở đầu** ("Script giao tiếp mẫu" cuối file), rồi chạy `/new-case` với thông tin khách để tạo case ở status `NEW`.
2. Xin tài liệu: đề cương, mô hình, bảng hỏi, data (nếu có), yêu cầu của giảng viên. **Hỏi mục đích dùng data** (bài tập luyện / tiểu luận / NCKH / khóa luận) để đánh giá và chọn gói.
3. Chạy **Claude Code `/diagnose <case_id>`**. Claude Code ra 2 thứ: *Research Assessment* (nội bộ) và **tin nhắn tóm tắt cho khách** (ngắn gọn, kèm báo giá đề xuất).
4. Bạn đọc lại rồi gửi tin nhắn đó cho khách.
5. **Phân loại khách theo giai đoạn** để chọn gói:

| Khách đang… | Dịch vụ chính | Gợi ý thêm |
|---|---|---|
| Làm bài tập môn, chưa có data / không đủ người khảo sát | **Mock data** (hoặc combo với Dữ liệu đã công bố) + **03 Phân tích SPSS** (mốc bài tập môn) | 03 trọn bộ |
| Chưa có mô hình / bảng hỏi | Rà soát đề tài, mô hình, bảng hỏi | 01 Tạo dữ liệu khảo sát, Đồng hành trọn đề tài |
| Có bảng hỏi, chưa thu | **01 Tạo dữ liệu khảo sát** (+ Rà soát bảng hỏi nếu cần) | 02 + 03 |
| Có data thô | **02 Xử lý dữ liệu** | 03 |
| Chạy rồi nhưng lỗi | **03 Phân tích SPSS** | AMOS / SmartPLS |
| Cần mô hình SEM | AMOS / SmartPLS | Đồng hành trọn đề tài |
| Có kết quả, cần hiểu | **03 Phân tích SPSS** (mốc cơ bản: review + giải thích) | Câu hỏi bảo vệ |

### Giai đoạn B: Báo giá và chốt

1. Gửi **báo giá 1 trang**: phạm vi, deliverables, thời gian, giá, điều khoản, cam kết học thuật.
2. Khách xác nhận và chuyển cọc 50%. Cập nhật status sang `DEPOSITED`.
3. Điền gói đã chốt vào `case.yaml` và chép tài liệu khách vào `00_intake/`.

### Giai đoạn C: Thực hiện, theo 6 bước chuẩn

| Bước | Tên | Input | Việc chính | Deliverable | Ai |
|---|---|---|---|---|---|
| 1 | Research Diagnosis | Đề tài, mô hình, bảng hỏi, yêu cầu GV | Xác định vấn đề, rủi ro, phạm vi | `01_research_assessment.md` | Claude Code nháp, tư vấn viên duyệt |
| 2 | Research Design | Kết quả bước 1 | Kiểm tra biến, thang đo, cỡ mẫu, chọn phương pháp | `02_analysis_plan.md` | Claude Code nháp, tư vấn viên duyệt |
| 3 | Data Collection | Bảng hỏi đã chốt | Dựng form, kế hoạch tiếp cận, theo dõi tiến độ | Link form, `03_collection_summary.md` | Tư vấn viên (Claude Code soạn form/nội dung). Chỉ thu phiếu từ người trả lời thật |
| 4 | Data Preparation | Data thô (.xlsx/.csv/Sheet) | Kiểm tra, làm sạch, mã hóa, outlier, đảo chiều | `clean.sav`, `data_dictionary.xlsx`, `04_cleaning_log.md` | Claude Code |
| 5 | Statistical Analysis | Data sạch + analysis plan | Chạy các kiểm định theo plan, kiểm tra giả định | `.sps`, output, bảng kết quả, project AMOS/PLS | Claude Code (+ tư vấn viên chạy AMOS/SmartPLS GUI nếu cần) |
| 6 | Interpretation & Handover | Kết quả bước 5 | Giải thích, đối chiếu giả thuyết, dàn ý chương 4, câu hỏi bảo vệ, hướng dẫn tự chạy lại | `06_report/analysis_report.md`, `06_report/tutorial.md`, `06_report/defense_qa.md` | Claude Code nháp, tư vấn viên duyệt và gửi qua tin nhắn |

**Checkpoint với khách**, bắt buộc xác nhận trước khi đi tiếp:

- Sau bước 2: khách đồng ý *Analysis Plan*. Đây là "hợp đồng phương pháp", tránh việc đổi yêu cầu giữa chừng.
- Sau bước 4: khách xem *Cleaning Log*, đồng ý số phiếu cuối cùng.
- Sau bước 5: báo trước kết quả chính (giả thuyết nào được ủng hộ), trước khi viết report.

### Giai đoạn D: QA và bàn giao

1. Tư vấn viên chạy **QA checklist** (QA checklist trong `analysis-standards.md`).
2. Gửi gói bàn giao: một thư mục zip hoặc Drive, có `README` liệt kê từng file.
3. Gửi kèm **tin nhắn hướng dẫn đọc kết quả** (Claude Code soạn: 5–7 ý chính, kết luận giả thuyết) và mời khách hỏi lại bất cứ chỗ nào chưa hiểu.
4. Thu 50% còn lại. Cập nhật status sang `DELIVERED`.

### Giai đoạn E: Hậu mãi

- Hỗ trợ sửa 2 lần trong 30 ngày (`REVISION`).
- Sau khi khách bảo vệ xong: xin feedback (form 3 câu) và xin phép dùng testimonial ẩn danh.
- Sau 90 ngày: **xóa dữ liệu** của khách, ghi ngày xóa vào `case.yaml`.

## Template tài liệu cho khách

| Tài liệu | Khi nào |
|---|---|
| Báo giá + Thỏa thuận dịch vụ (1 trang) | Giai đoạn B |
| Research Assessment | Bước 1 |
| Analysis Plan | Bước 2 |
| Cleaning Log + Data Dictionary | Bước 4 |
| Analysis Report (giải thích từng bảng) | Bước 6 |
| Tutorial "tự chạy lại" | Bước 6 |
| Bộ câu hỏi bảo vệ (Defense Q&A) | Bước 6, dịch vụ 03 mốc trọn bộ trở lên |
| README bàn giao | Bàn giao |
| Form feedback | Đóng case |

## Script giao tiếp mẫu

- **Mở đầu:** "Chào [tên], mình là [X] bên Alpha Lab. Cảm ơn bạn đã nhắn về đề tài *[đề tài]*. Bạn gửi giúp mình bảng hỏi, mô hình và file data (nếu có) để mình chẩn đoán miễn phí nhé. Khoảng [thời gian] mình gửi lại đánh giá và báo giá."
- **Từ chối yêu cầu vi phạm:** "Phần này bên mình không làm được vì sẽ khiến bạn gặp rủi ro gian lận học thuật (có thể bị đình chỉ). Thay vào đó, mình có thể [phương án hợp lệ]…"
