Bạn là senior web designer + front-end developer. Hãy thiết kế lại giao diện cho landing page dưới đây. Nội dung và cấu trúc đã chốt, chỉ cần làm cho nó ĐẸP, có cá tính và đáng tin hơn.

## Bối cảnh
- Thương hiệu: **Rõ Số**, dịch vụ thu thập, xử lý và phân tích dữ liệu SPSS cho sinh viên kinh tế Việt Nam (tiểu luận, NCKH, khóa luận, luận văn).
- Khách hàng: sinh viên 19–26 tuổi, đang lo deadline, không giỏi thống kê, xem chủ yếu trên điện thoại (>70% mobile), liên hệ chủ yếu qua Zalo.
- Cảm giác cần truyền tải: **rõ ràng, chính xác, bình tĩnh, đáng tin**, như một người anh/chị khóa trên giỏi số liệu. Tagline: "Hiểu rõ từng con số trong bài nghiên cứu của bạn."
- Trang chỉ có 1 mục tiêu: cho người xem hiểu **3 dịch vụ** và **liên hệ** để nhận báo giá. Trang ngắn, gọn, không thêm section nào khác.

## Vấn đề của bản hiện tại (tránh lặp lại)
- Trông như template SaaS do AI tạo: blob gradient mờ, nền chấm bi, chữ gradient, bóng đổ khắp nơi.
- Hero căn giữa, chỉ có chữ, không có hình ảnh gì nói lên "dữ liệu / bảng kết quả SPSS".
- 3 thẻ dịch vụ trông giống nhau, chưa thể hiện được đây là 3 bước nối tiếp (thu thập → xử lý → phân tích).
- Màu navy + teal + cam khá chung chung, không nhớ được.

## Hướng thiết kế mong muốn
- Lấy cảm hứng từ chính chất liệu của nghề: Google Form, bảng tính Excel, bảng output SPSS (Cronbach's Alpha, hệ số hồi quy, Sig.), giấy kẻ ô, ghi chú bút đỏ. Dùng chúng làm visual chính (vẽ bằng HTML/CSS/SVG inline). Ví dụ hero minh họa hành trình dữ liệu: form khảo sát → bảng dữ liệu được làm sạch → bảng kết quả SPSS có chú thích giải thích bằng tiếng Việt.
- 3 dịch vụ nên được trình bày như một pipeline 01 → 02 → 03 (khách có thể mua riêng từng bước), mỗi dịch vụ có minh họa nhỏ riêng phù hợp nội dung.
- Typography là điểm nhấn: font hỗ trợ đầy đủ dấu tiếng Việt (Be Vietnam Pro, Inter, Lexend, Manrope, hoặc kết hợp 1 font serif như Fraunces/Lora cho tiêu đề). Có thể dùng 1 font mono (JetBrains Mono / IBM Plex Mono) cho số thứ tự, tên file (.xlsx, .sav, .sps), tên kiểm định.
- Bảng màu riêng, tối đa 1 màu chính + 1 màu nhấn + các tông trung tính. Gợi ý thử: nền giấy ngà, mực xanh đậm, nhấn đỏ/cam "bút phê", hoặc xanh lá "Sig. < 0.05". Tương phản đạt WCAG AA.
- Icon: SVG nét mảnh đồng bộ (vẽ inline, phong cách Lucide/Phosphor), KHÔNG dùng emoji.
- Phần "Bàn giao" trình bày như danh sách file thật (icon file + đuôi file).
- Phần liên hệ: Zalo là kênh chính, nổi bật nhất; Facebook và Email là phụ.
- Animation tiết chế: reveal khi cuộn, hover tinh tế. Tôn trọng `prefers-reduced-motion`.
- Mobile-first: đẹp ở 375px, không cuộn ngang, nút bấm ≥ 44px, có nút "Chat Zalo" nổi cố định góc dưới phải.

## Ràng buộc kỹ thuật
- Xuất **1 file `index.html` duy nhất**, HTML + CSS + JS thuần (không React, không Tailwind, không build step). Chỉ được load Google Fonts từ bên ngoài.
- Khai báo màu/khoảng cách/bo góc bằng CSS variables trong `:root`.
- **Giữ nguyên toàn bộ nội dung chữ và thứ tự section** như bên dưới (có thể sửa câu chữ nhỏ cho hợp bố cục, nhưng không bỏ thông tin và không thêm giá tiền).
- Giữ các anchor: `#top`, `#dich-vu`, `#lien-he`.
- Code sạch, có comment chia section, class đặt tên theo BEM.

## Nội dung (giữ nguyên)

**Nav:** Rõ Số (logo) · Dịch vụ · [Liên hệ]

**Hero**
- Eyebrow: Dịch vụ dữ liệu & SPSS cho sinh viên kinh tế
- H1: Hiểu rõ từng con số trong bài nghiên cứu của bạn.
- Mô tả: Từ thu thập khảo sát, xử lý dữ liệu đến phân tích SPSS, kèm giải thích kết quả dễ hiểu.
- CTA: [Liên hệ nhận báo giá →] [Xem dịch vụ]
- Dòng tóm tắt: 01 Tạo dữ liệu khảo sát → 02 Xử lý dữ liệu → 03 Phân tích SPSS
- Dải chạy "Hỗ trợ các môn & loại bài phổ biến": Phương pháp nghiên cứu · Kinh tế lượng · Nghiên cứu Marketing · Thống kê kinh doanh · Tiểu luận · NCKH sinh viên · Khóa luận tốt nghiệp · Luận văn thạc sĩ

**Dịch vụ** (`#dich-vu`): "3 dịch vụ chính, từ dữ liệu đến kết quả" / "Chọn đúng phần bạn đang cần hỗ trợ."

01 – Tạo dữ liệu khảo sát (Data Collection Support)
- Hỗ trợ xây dựng Google Form
- Hỗ trợ triển khai khảo sát và thu thập phản hồi thực tế
- Theo dõi số lượng phản hồi theo yêu cầu
- Xuất dữ liệu Excel
- Bàn giao: Excel (.xlsx)
- Báo giá theo: số lượng phản hồi và phạm vi công việc
- Nút: Hỏi báo giá

02 – Xử lý dữ liệu (Data Processing)
- Kiểm tra dữ liệu
- Làm sạch dữ liệu
- Mã hóa biến
- Xử lý dữ liệu thiếu và bất thường theo tiêu chí thống nhất
- Chuẩn hóa dữ liệu để đưa vào SPSS
- Bàn giao: Excel, SPSS (.sav), Cleaning log
- Báo giá theo: số lượng mẫu, số biến và độ phức tạp
- Nút: Hỏi báo giá

03 – Hỗ trợ phân tích SPSS (Statistical Analysis)
- Thống kê mô tả
- Cronbach's Alpha
- EFA
- Pearson Correlation
- Linear Regression
- T-test / ANOVA
- Kiểm tra các giả định thống kê
- Giải thích kết quả và hướng dẫn đọc output
- Bàn giao: File dữ liệu, Syntax SPSS (.sps), Báo cáo kết quả
- Báo giá theo: số lượng phép kiểm định và độ phức tạp mô hình
- Nút: Hỏi báo giá

Ghi chú dưới phần dịch vụ: Báo giá cụ thể sau khi xem yêu cầu của bạn.

**Liên hệ** (`#lien-he`): "Nhắn cho bên mình để nhận báo giá" / "Chọn kênh bạn tiện nhất. Bên mình sẽ xem yêu cầu và báo giá rõ phạm vi trước khi làm."
- Khung "Khi nhắn, gửi kèm giúp bên mình:" Đề tài và mô hình nghiên cứu · Bảng hỏi / file dữ liệu (nếu có) · Dịch vụ cần hỗ trợ (01, 02, 03) · Deadline
- Kênh liên hệ (link đặt `#` tạm):
  - Zalo – 09xx xxx xxx – "Nhắn ngay →" (kênh chính)
  - Facebook – facebook.com/roso – "Mở →"
  - Email – lienhe@roso.vn – "Gửi →"

**Footer:** Rõ Số – Dịch vụ thu thập, xử lý và phân tích dữ liệu SPSS cho sinh viên kinh tế. Hiểu rõ từng con số trong bài của bạn. | Dịch vụ: Tạo dữ liệu khảo sát, Xử lý dữ liệu, Phân tích SPSS | Liên hệ: Zalo, Facebook, Email | © 2026 Rõ Số · Bảo mật dữ liệu

## Cách trả lời
1. Trước khi code, mô tả ngắn concept thiết kế (bảng màu, font, ý tưởng visual chính) trong 5–8 dòng.
2. Sau đó xuất toàn bộ file `index.html` hoàn chỉnh, chạy được ngay khi mở bằng trình duyệt.
