# Phạm vi dịch vụ

> Nguồn: trích từ `PLAN.md` mục 4. Khi sửa, sửa file này trước rồi cập nhật PLAN.md.

> Đây là **quy tắc vận hành nội bộ** (cho bạn và Claude Code), không đưa lên website. Mục đích: giữ chất lượng và tránh rủi ro cho khách.
>
> **(v4) Ai quyết định:** khi tiếp nhận, **tư vấn viên** hỏi sinh viên dùng data vào việc gì (bài tập luyện mô hình, tiểu luận, NCKH, khóa luận…), rồi tự đánh giá và chọn gói phù hợp. Kết quả ghi vào `case.yaml`, mục `muc_dich_su_dung` và `quyet_dinh_tu_van`. Claude Code làm theo gói đã chọn. Các mục ở 4.2 là giới hạn kỹ thuật cố định của Claude Code: gặp yêu cầu loại đó thì Claude Code báo lại để bạn trao đổi với khách.

## Nguyên tắc chung

**Mình lo phần dữ liệu và kỹ thuật. Sinh viên làm chủ phần nội dung và kết luận.**

## Những việc không nằm trong dịch vụ

| # | Không làm | Lý do |
|---|---|---|
| N1 | Trộn phiếu mock vào data khảo sát thật của sinh viên để "đủ mẫu" | Làm hỏng data thật, kết quả không còn đúng |
| N2 | Sửa giá trị trả lời trong data thật để Cronbach, EFA hay hồi quy "đạt" | Như trên |
| N3 | Loại phiếu hoặc loại biến không theo tiêu chí, chỉ để kết quả đẹp | Như trên |
| N4 | Tự viết ra chi tiết của một cuộc khảo sát không diễn ra (địa điểm, thời gian, số người được khảo sát) trong báo cáo | Phần phương pháp do sinh viên tự viết |
| N5 | Viết hộ toàn bộ khóa luận, hoặc làm bài thi / bài kiểm tra thay | Ngoài phạm vi |

## Vùng xám: quy tắc xử lý

| Tình huống | Xử lý |
|---|---|
| Sinh viên xin "viết luôn chương 4" | Giao **Analysis Report** giải thích từng bảng kèm **dàn ý** chương 4 và mẫu câu trình bày. Sinh viên tự viết. Mình review và góp ý bản của họ |
| Alpha thấp, sinh viên muốn "chỉnh" | Chẩn đoán nguyên nhân thật (câu đảo chiều, phiếu kém, thang đo dịch sai). Chỉ loại biến hoặc loại phiếu theo **tiêu chí đã định trước** và **ghi vào Cleaning Log** |
| Thiếu mẫu, chưa có data để chạy | **Mock data** (chạy thử ngay) và/hoặc **Dữ liệu đã công bố** (nhóm "Dịch vụ khác"), hoặc combo cả hai. Không trộn phiếu mock vào data khảo sát thật của sinh viên |
| Mock data trong báo cáo | Báo cáo dùng từ trung tính **"dữ liệu"**, không cần ghi chú "mô phỏng" trong thân bài. Claude Code chỉ **không tự viết thêm** các chi tiết về một cuộc khảo sát không có thật (ví dụ "khảo sát 250 sinh viên tại UEH từ 01–15/11"); phần phương pháp thu thập do sinh viên tự viết |
| Giả thuyết bị bác bỏ | Trình bày trung thực, hướng dẫn cách *giải thích* kết quả không ủng hộ giả thuyết (đây là kết quả hợp lệ) |
| Đặt tên file mock data | Nội bộ, trong thư mục case: `data/mock/` (để không lẫn với data thật khi chạy combo). File giao khách: `mock_data.sav`, tên trung tính, không watermark |
| Khách khăng khăng đòi làm việc thuộc mục "Những việc không nằm trong dịch vụ" | Từ chối lịch sự, đề xuất phương án hợp lệ. Nếu vẫn đòi thì **dừng hợp tác**, hoàn phần phí chưa thực hiện |

## Cơ chế bảo vệ

1. Báo giá gửi qua Zalo có 1 dòng phạm vi dịch vụ: *"Alpha Lab hỗ trợ xử lý & giải thích dữ liệu; nguồn dữ liệu luôn được ghi rõ."*
2. Website không có checkbox hay lời răn đe; tư vấn viên đánh giá từng trường hợp khi nhắn tin.
3. **Cleaning Log bắt buộc:** mọi phiếu hoặc biến bị loại đều có lý do và tiêu chí, nên sinh viên có thể đưa vào phụ lục.
4. **Claude Code bị ràng buộc bởi `CLAUDE.md`:** gặp yêu cầu thuộc 4.2 thì dừng và báo lại, không thực hiện.
5. Mỗi case lưu **Integrity Check** trong file bàn giao (checklist ở QA checklist trong `analysis-standards.md`).
