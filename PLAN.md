# Rõ Số: Kế hoạch tổng thể (bản duyệt v3)

> **Trạng thái:** Chờ duyệt. Chưa code, chưa cài môi trường.
>
> **Thay đổi v2 (theo góp ý):**
> 1. **Tư vấn hoàn toàn qua tin nhắn** (Zalo/Messenger), không gọi điện, không họp 1:1. Bạn là người vận hành và xử lý dữ liệu; Claude Code soạn nội dung chuyên môn (giải thích, trả lời câu hỏi), bạn chỉ đọc lại rồi gửi.
> 2. **Giảm nhấn mạnh học thuật trên website.** Khách chính là sinh viên làm **bài tập môn học**, không chỉ khóa luận. Nguyên tắc vẫn giữ, nhưng chỉ dùng nội bộ và nhắc nhẹ trên site.
> 3. **Tách 2 gói dữ liệu chạy song song:** **Mock Data** (data sát thực tế theo mô hình, để sinh viên có data chạy thử ngay) và **Dữ liệu công bố** (tìm bộ khảo sát đã công bố, có nguồn), cùng một combo gộp cả hai.
> 4. **(v3) Bỏ cách gọi "học thuật/đạo đức"** trong tài liệu. Mục 4 đổi thành "Phạm vi dịch vụ".
> 5. **(v4) Website chỉ ghi chung là "Dịch vụ data"** (mock data, dữ liệu công bố, làm sạch, chạy mô hình), không ghi chú thêm gì. **Tư vấn viên (bạn) đánh giá từng trường hợp** sinh viên dùng data vào việc gì, rồi quyết định nhận hay không và chọn gói nào.
> Duyệt xong từng phần (đánh dấu ✅ hoặc ghi góp ý trực tiếp vào file), mình mới triển khai.
> Ngày lập: 04/11/2026

## Mục lục

1. [Kết quả research: sinh viên kinh tế gặp khó khăn gì?](#1-kết-quả-research)
2. [Định vị và thương hiệu](#2-định-vị-và-thương-hiệu)
3. [Gói dịch vụ và bảng giá khởi điểm](#3-gói-dịch-vụ-và-bảng-giá-khởi-điểm)
4. [Phạm vi dịch vụ](#4-phạm-vi-dịch-vụ)
5. [Quy trình consulting (cho người tư vấn)](#5-quy-trình-consulting)
6. [Quy trình thực hiện cho Claude Code](#6-quy-trình-cho-claude-code)
7. [Website (Next.js, frontend)](#7-website)
8. [Tiếp nhận đơn qua Google Sheet](#8-tiếp-nhận-đơn-qua-google-sheet)
9. [Cấu trúc thư mục dự án](#9-cấu-trúc-thư-mục-dự-án)
10. [Lộ trình triển khai](#10-lộ-trình-triển-khai)
11. [Câu hỏi cần bạn chốt](#11-câu-hỏi-cần-bạn-chốt)

---

## 1. Kết quả research

### 1.1 Kết luận nhanh

| # | Vấn đề (theo tài liệu của bạn) | Có bằng chứng xác nhận? | Mức độ tin cậy |
|---|---|---|---|
| 01 | Không đủ mẫu khảo sát | **Có.** Thu dữ liệu mất 3–4 tuần, nhiều phiếu bị loại; sinh viên tự chịu chi phí khảo sát | Trung bình (blog, tham luận) |
| 02 | Không biết chọn kiểm định | **Có.** "Khó khăn trong lựa chọn mô hình phù hợp với đề tài", "thiếu nền tảng thống kê" | Trung bình |
| 03 | Không biết làm sạch dữ liệu | **Có, và quan trọng hơn mình nghĩ.** Phiếu trả lời qua loa và không làm sạch trước khi chạy là lý do chính khiến "kết quả không đạt bất kỳ kiểm định nào" | Trung bình |
| 04 | Cronbach / EFA lỗi | **Có, rất rõ.** Đối thủ liệt kê đúng các lỗi: alpha < 0.6, ma trận xoay lộn xộn, loại quá nhiều biến | Cao (đối thủ xây dịch vụ quanh lỗi này) |
| 05 | Không biết AMOS / SmartPLS | **Có.** Đối thủ đều tách thành gói riêng, giá cao hơn | Trung bình |
| 06 | Có kết quả nhưng không hiểu | **Có.** Trên Fiverr có hẳn gig "interpret your SPSS output for your thesis" | Trung bình |
| 07 | Deadline, không ai review | **Có.** Đối thủ bán phụ phí "gấp" 20–40% | Cao |

**Nhận định:** cả 7 vấn đề trong tài liệu của bạn đều có dấu hiệu là thật. Tuy nhiên:

- **Chưa có nghiên cứu học thuật nào khảo sát định lượng riêng sinh viên kinh tế Việt Nam về khó khăn với SPSS.** Bằng chứng hiện tại chủ yếu đến từ blog, tham luận và trang của đối thủ. Nguồn học thuật gần nhất là bài trên tạp chí ĐH Hà Nội, nhưng lại về nghiên cứu *định tính*.
- Vì vậy mình đề xuất **tự kiểm chứng bằng một khảo sát nhỏ** khoảng 50–100 sinh viên kinh tế, qua Google Form, trước hoặc song song với lúc ra mắt (xem 10. Lộ trình). Kết quả khảo sát này vừa giúp xác nhận nhu cầu, vừa dùng làm nội dung marketing.

### 1.2 Phát hiện mới, ngoài tài liệu của bạn

1. **Bảng hỏi kém là gốc rễ của nhiều lỗi về sau.** Câu hỏi khó hiểu khiến người trả lời chọn bừa, dẫn đến Cronbach/EFA không đạt. → Gói *Research Starter* (rà soát bảng hỏi trước khi phát) có giá trị thật, và nên bán như một biện pháp phòng ngừa.
2. **Nhiều đối thủ công khai "cung cấp data".** Ví dụ: một trang có gói "Chưa có số liệu: 3–6 triệu, cung cấp data", một trang khác "hỗ trợ dữ liệu phù hợp với môi trường nghiên cứu". Đây chính là bịa số liệu. → **Đây là điểm khác biệt lớn nhất của mình: minh bạch và dữ liệu thật** (xem mục 4).
3. **Đối thủ bàn giao rất mỏng.** Thường chỉ gồm file SPSS, Excel và một file Word "nhận xét cơ bản". Gần như không ai giao syntax (.sps), cleaning log hay buổi hướng dẫn tự chạy lại. → Mình cạnh tranh bằng **chất lượng bàn giao và sự minh bạch**, không cạnh tranh bằng giá rẻ.
4. **Học phí đào tạo SPSS ở trường rất rẻ.** Ví dụ CENTREC ĐH Cần Thơ: 300–400k mỗi module, 2–3 buổi. → Đừng định vị là "khóa học SPSS". Định vị là **giải quyết đúng đề tài của bạn**.
5. **Rủi ro pháp lý cho khách hàng là có thật.** Nhờ người làm hộ khóa luận bị xếp vào nhóm gian lận và có thể bị đình chỉ học. Dùng tài liệu giả để tốt nghiệp có thể bị thu hồi bằng. → Quy tắc vận hành nội bộ ở mục 4 giúp khách tránh những rủi ro này.

### 1.3 Giá thị trường (đã kiểm tra trên website đối thủ, tháng 11/2026)

| Đơn vị | Gói | Giá |
|---|---|---|
| Phạm Lộc Blog | Pearson + hồi quy | 600.000đ |
| | ANOVA / T-test | 700.000đ |
| | Cronbach + EFA | 800.000đ |
| | Cronbach + EFA + Pearson + hồi quy | 1.400.000đ |
| | + Thống kê mô tả | 2.000.000đ |
| | + ANOVA / T-test (trọn bộ) | 2.600.000đ |
| Luận Văn Uy Tín | Đã có số liệu, trọn bộ SPSS | 1–3 triệu |
| | "Chưa có số liệu" (cung cấp data ⚠️) | 3–6 triệu |
| | Phụ phí gấp | +20–40% |
| Luanvan24 | Cronbach + EFA + Pearson + hồi quy | 4–6 triệu (trang cũ, cần kiểm tra lại) |
| Tài liệu bạn gửi | AMOS CFA/SEM | 1,5–2,5 triệu |
| | AMOS nâng cao | 2,6–5,3 triệu |
| CENTREC ĐH Cần Thơ (đào tạo) | Module SPSS/AMOS | 300–400k/module |
| Freelance quốc tế (Khamsat) | Phân tích + viết kết quả | 30–100 USD |

**Bàn giao điển hình của đối thủ:** file SPSS và Excel đã xử lý, file Word bảng kết quả và nhận xét cơ bản, sửa theo góp ý của giảng viên.

### 1.4 Nguồn

- [Phạm Lộc Blog: Bảng giá dịch vụ SPSS](https://www.phamlocblog.com/p/dich-vu-spss.html)
- [Luận Văn Uy Tín: Bảng giá SPSS](https://luanvanuytin.com/bang-gia-dich-vu-spss-xu-ly-so-lieu-du-lieu/)
- [Luanvan24: Dịch vụ SPSS](https://luanvan24.org/spss/dich-vu-xu-ly-so-lieu/)
- [Khoa học trẻ: Lý do số liệu không xử lý được](https://khoahoctre.com.vn/mot-so-ly-do-khien-so-lieu-thu-thap-trong-nghien-cuu-khoa-hoc-khong-xu-ly-duoc/)
- [Nhận Việc: Xử lý số liệu trong NCKH](https://nhanviec.com/xu-ly-so-lieu-trong-nghien-cuu-khoa-hoc/)
- [Tham luận: Khó khăn của sinh viên khi làm NCKH](https://nguyentuanduong.wordpress.com/2012/06/18/tham-luan-nhung-kho-khan-cua-sinh-vien-khi-thuc-hien-de-tai-nghien-cuu-khoa-hoc/)
- [Tạp chí ĐH Hà Nội: Thách thức nghiên cứu định tính của sinh viên](https://journals.hanu.edu.vn/tckhnn/article/view/935)
- [Tạp chí Thiết bị Giáo dục: Công cụ xử lý số liệu cho SV kinh tế – xã hội](https://vjol.info.vn/tctbgd/article/view/87966)
- [CENTREC ĐH Cần Thơ: Học phí SPSS/AMOS](https://cse.ctu.edu.vn/images/upload/tttv/2025/MoTaCacKhoa/CN/CN_VI1_SPSS.pdf)
- [Khamsat: Gói phân tích thống kê](https://khamsat.com/data/data-analytics/4229228-%D8%A7%D9%84%D8%AA%D8%AD%D9%84%D9%8A%D9%84-%D8%A7%D9%84%D8%A7%D8%AD%D8%B5%D8%A7%D8%A6%D9%8A-%D9%84%D9%84%D8%B1%D8%B3%D8%A7%D8%A6%D9%84-%D8%A7%D9%84%D8%B9%D9%84%D9%85%D9%8A%D8%A9)
- [Fiverr: Interpret SPSS output for thesis](https://fiverr.com/elias_sadat/interpret-your-spss-output-and-explain-results-for-your-thesis)
- [Hệ thống pháp luật: Làm hộ đồ án có thể bị đình chỉ](https://hethongphapluat.com/phap-luat/huong-dan/sinh-vien-thi-ho-lam-ho-do-coi-chung-bi-dinh-chi-hoc-ngay-lan-dau-vi-pham.html)
- [Thư viện pháp luật: Hành vi vi phạm bị kỷ luật](https://thuvienphapluat.vn/hoi-dap-phap-luat/hanh-vi-nao-cua-sinh-vien-duoc-cho-la-vi-pham-bi-xu-ly-ky-luat-138099984.html)
- [Luật Minh Khuê: Thu hồi văn bằng khi dùng tài liệu giả](https://luatminhkhue.vn/sinh-vien-bi-lap-bien-ban-khi-su-dung-tai-lieu-khi-thi-co-bi-ha-bang.aspx)

---

## 2. Định vị và thương hiệu

### 2.1 Định vị

> **Research & Data Analysis Consulting cho sinh viên kinh tế.**
> Đồng hành từ bảng hỏi đến khi *bạn hiểu và tự trình bày được* kết quả.
> Không gửi file rồi nhận file, mà là minh bạch, có hướng dẫn, và bạn tự chạy lại được.

**Khách hàng chính (thứ tự ưu tiên):**

1. Sinh viên làm **bài tập / tiểu luận môn học** có phần SPSS (Phương pháp nghiên cứu, Kinh tế lượng, Thống kê, Nghiên cứu Marketing…). Đây là nhóm đông nhất, cần nhanh, giá mềm, và thường thiếu người khảo sát.
2. Sinh viên làm NCKH / khóa luận.
3. Học viên cao học (AMOS / SmartPLS).

**3 điểm khác biệt:**

1. **Nhanh và dễ:** gửi file qua Zalo, nhận kết quả kèm giải thích bằng tiếng Việt dễ hiểu; hỏi lại qua tin nhắn bao nhiêu lần cũng được.
2. **Hiểu được bài mình:** report giải thích từng bảng, có dàn ý trình bày và câu hỏi giảng viên hay hỏi, nên sinh viên không bị "đứng hình" khi thuyết trình.
3. **Minh bạch:** giao kèm syntax (.sps) và log xử lý, nên chạy lại ra đúng kết quả.

### 2.2 Gợi ý tên thương hiệu

| Tên | Ý nghĩa | Ưu | Nhược |
|---|---|---|---|
| **Rõ Số** ⭐ | "Hiểu rõ từng con số" | Ngắn, tiếng Việt, dễ nhớ, đúng định vị "giải thích" | Dấu tiếng Việt, domain sẽ là `roso.vn` / `roso.edu.vn` |
| **Biến Số Lab** | "Biến số" là thuật ngữ quen thuộc với dân nghiên cứu | Có chất học thuật | Hơi dài |
| **Sig. Lab** | Sig. là chỉ số ai chạy SPSS cũng biết | Rất "đúng dân" | Người ngoài ngành không hiểu |
| **Mentora Research** | Mentor + Research | Nghe quốc tế | Chung chung, khó nổi bật |
| **Luận Data** | Luận văn + Data | Rõ ngay là làm gì | Dễ bị gắn với "làm hộ luận văn" |

**Đề xuất: Rõ Số**, slogan: *"Hiểu rõ từng con số trong nghiên cứu của bạn."*
(Cần kiểm tra trùng tên trên Facebook, Zalo OA và domain trước khi chốt.)

### 2.3 Kênh liên hệ (bạn gửi link sau)

- [ ] Zalo (cá nhân hoặc Zalo OA)
- [ ] Facebook Page
- [ ] Email

Trên website, các link này nằm trong một file cấu hình (`site.config.ts`) nên đổi rất dễ.

---

## 3. Gói dịch vụ và bảng giá khởi điểm

### 3.1 Logic định giá

- **Neo theo giá thị trường** (mục 1.3), định giá ngang hoặc thấp hơn khoảng 10%, vì mình là thương hiệu mới chưa có review.
- **Không bán phá giá.** Giá trị khác biệt nằm ở bàn giao (syntax, log, buổi 1:1), nên không cần rẻ nhất.
- **Nâng cấp được:** phí gói trước được trừ vào gói sau. Ví dụ đã mua Starter 300k, lên SPSS thì trừ 300k.
- Website ghi giá dạng **"từ X"**. Báo giá cuối cùng gửi sau buổi chẩn đoán.

### 3.2 Bảng giá đề xuất

| Gói | Nội dung | Bàn giao | Thời gian | Giá khởi điểm |
|---|---|---|---|---|
| **Research Starter** | Rà soát đề tài, mô hình, giả thuyết, thang đo, bảng hỏi; đề xuất cỡ mẫu và phương pháp; góp ý qua tin nhắn | Research Assessment + Analysis Plan | 1–2 ngày | **từ 300.000đ** |
| **Mock Data** (mới) | Sinh bộ mock data **sát thực tế** theo đúng mô hình của sinh viên (số biến, số item, thang Likert, cỡ mẫu, phân phối và tương quan hợp lý, nhân khẩu học), để sinh viên **có data chạy thử mô hình** ngay, không phải chờ khảo sát. Có thể dựa trên cấu trúc của nghiên cứu tương tự | `mock_data.sav` + `.xlsx` + codebook | Trong ngày | **từ 150.000đ** |
| **Dữ liệu công bố** (mới) | Tìm bộ dữ liệu khảo sát đã công bố cùng chủ đề (Kaggle, Mendeley Data, OSF, Harvard Dataverse, GSO, World Bank…), chuẩn hóa lại cho SPSS, kèm trích dẫn nguồn | Dataset + trích dẫn | 1–3 ngày | **từ 250.000đ** |
| **Combo Mock + Công bố** | Chạy song song: có mock data để dựng và thử mô hình ngay; khi tìm được dữ liệu công bố phù hợp thì chạy lại trên bộ đó | Cả hai bộ + pipeline chạy sẵn | 1–3 ngày | **từ 350.000đ** |
| **Data Collection Support** | Dựng Google Form chuẩn (câu lọc, câu kiểm tra chú ý), kế hoạch tiếp cận đối tượng, theo dõi tiến độ và chất lượng phiếu | Form + Kế hoạch thu mẫu + Collection Summary | Theo tiến độ thu | **từ 400.000đ** |
| **Data Cleaning** | Missing, trùng, phiếu không hợp lệ, straight-lining, câu đảo chiều, mã hóa, gán nhãn, xuất .sav | Clean dataset + Data Dictionary + Cleaning Log | 1–2 ngày | **từ 400.000đ** |
| **SPSS Consulting: Cơ bản** | Cronbach + EFA *hoặc* Pearson + hồi quy | .sav + .sps + output + Report | 1–2 ngày | **từ 700.000đ** |
| **SPSS Consulting: Trọn bộ** | Mô tả + Cronbach + EFA + Pearson + hồi quy + T-test/ANOVA + kiểm tra giả định + giải đáp qua tin nhắn | .sav + .sps + output + Analysis Report | 2–4 ngày | **từ 1.800.000đ** |
| **Gói Bài tập môn** (mới) | Cho tiểu luận / bài tập môn: một mô hình nhỏ (≤ 5 biến), chạy mô tả + Cronbach + EFA + hồi quy, kèm giải thích ngắn gọn | .sav + .sps + bảng kết quả + giải thích | 1–2 ngày | **từ 500.000đ** |
| **AMOS / SmartPLS (SEM)** | CFA (CR, AVE, HTMT), SEM/PLS-SEM, trung gian/điều tiết, bootstrap | Project file + Report + hướng dẫn | 4–7 ngày | **từ 1.800.000đ** (CFA) · **từ 2.800.000đ** (CFA + SEM) |
| **Full Research Mentoring** | Đồng hành cả 6 bước, dàn ý trình bày chương 3–4, bộ câu hỏi bảo vệ soạn sẵn, nhóm chat Zalo hỗ trợ đến ngày bảo vệ | Toàn bộ deliverables | Theo tiến độ đề tài | **từ 3.500.000đ** |

### 3.3 Điều khoản chung

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

---

## 4. Phạm vi dịch vụ

> Đây là **quy tắc vận hành nội bộ** (cho bạn và Claude Code), không đưa lên website. Mục đích: giữ chất lượng và tránh rủi ro cho khách.
>
> **(v4) Ai quyết định:** khi tiếp nhận, **tư vấn viên** hỏi sinh viên dùng data vào việc gì (bài tập luyện mô hình, tiểu luận, NCKH, khóa luận…), rồi tự đánh giá và chọn gói phù hợp. Kết quả ghi vào `case.yaml`, mục `muc_dich_su_dung` và `quyet_dinh_tu_van`. Claude Code làm theo gói đã chọn. Các mục ở 4.2 là giới hạn kỹ thuật cố định của Claude Code: gặp yêu cầu loại đó thì Claude Code báo lại để bạn trao đổi với khách.

### 4.1 Nguyên tắc chung

**Mình lo phần dữ liệu và kỹ thuật. Sinh viên làm chủ phần nội dung và kết luận.**

### 4.2 Những việc không nằm trong dịch vụ

| # | Không làm | Lý do |
|---|---|---|
| N1 | Trộn phiếu mock vào data khảo sát thật của sinh viên để "đủ mẫu" | Làm hỏng data thật, kết quả không còn đúng |
| N2 | Sửa giá trị trả lời trong data thật để Cronbach, EFA hay hồi quy "đạt" | Như trên |
| N3 | Loại phiếu hoặc loại biến không theo tiêu chí, chỉ để kết quả đẹp | Như trên |
| N4 | Tự viết ra chi tiết của một cuộc khảo sát không diễn ra (địa điểm, thời gian, số người được khảo sát) trong báo cáo | Phần phương pháp do sinh viên tự viết |
| N5 | Viết hộ toàn bộ khóa luận, hoặc làm bài thi / bài kiểm tra thay | Ngoài phạm vi |

### 4.3 Vùng xám: quy tắc xử lý

| Tình huống | Xử lý |
|---|---|
| Sinh viên xin "viết luôn chương 4" | Giao **Analysis Report** giải thích từng bảng kèm **dàn ý** chương 4 và mẫu câu trình bày. Sinh viên tự viết. Mình review và góp ý bản của họ |
| Alpha thấp, sinh viên muốn "chỉnh" | Chẩn đoán nguyên nhân thật (câu đảo chiều, phiếu kém, thang đo dịch sai). Chỉ loại biến hoặc loại phiếu theo **tiêu chí đã định trước** và **ghi vào Cleaning Log** |
| Thiếu mẫu, chưa có data để chạy | Gói **Mock Data** (chạy thử ngay) và/hoặc **Dữ liệu công bố**, hoặc combo cả hai. Không trộn phiếu mock vào data khảo sát thật của sinh viên |
| Mock data trong báo cáo | Báo cáo dùng từ trung tính **"dữ liệu"**, không cần ghi chú "mô phỏng" trong thân bài. Claude Code chỉ **không tự viết thêm** các chi tiết về một cuộc khảo sát không có thật (ví dụ "khảo sát 250 sinh viên tại UEH từ 01–15/11"); phần phương pháp thu thập do sinh viên tự viết |
| Giả thuyết bị bác bỏ | Trình bày trung thực, hướng dẫn cách *giải thích* kết quả không ủng hộ giả thuyết (đây là kết quả hợp lệ) |
| Đặt tên file mock data | Nội bộ, trong thư mục case: `data/mock/` (để không lẫn với data thật khi chạy combo). File giao khách: `mock_data.sav`, tên trung tính, không watermark |
| Khách khăng khăng đòi làm việc thuộc mục 4.2 | Từ chối lịch sự, đề xuất phương án hợp lệ. Nếu vẫn đòi thì **dừng hợp tác**, hoàn phần phí chưa thực hiện |

### 4.4 Cơ chế bảo vệ

1. Một dòng nhỏ dưới nút gửi form: *"Rõ Số hỗ trợ xử lý & giải thích dữ liệu; nguồn dữ liệu luôn được ghi rõ."* Không có checkbox răn đe.
2. Báo giá gửi qua Zalo có 1 dòng phạm vi dịch vụ.
3. **Cleaning Log bắt buộc:** mọi phiếu hoặc biến bị loại đều có lý do và tiêu chí, nên sinh viên có thể đưa vào phụ lục.
4. **Claude Code bị ràng buộc bởi `CLAUDE.md`:** gặp yêu cầu thuộc 4.2 thì dừng và báo lại, không thực hiện.
5. Mỗi case lưu **Integrity Check** trong file bàn giao (checklist ở mục 6.6).

---

## 5. Quy trình consulting

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

### 5.1 Vòng đời một đơn (case)

```
 Lead ─► Chẩn đoán ─► Báo giá ─► Cọc ─► Thực hiện (6 bước) ─► QA ─► Bàn giao ─► Hậu mãi ─► Đóng case
  │                                         ▲
  └ form web → Google Sheet (status: NEW)    └ Claude Code làm phần kỹ thuật
```

| Status trong Sheet | Ý nghĩa | Ai làm | SLA |
|---|---|---|---|
| `NEW` | Form vừa gửi | (tự động) | n/a |
| `CONTACTED` | Đã nhắn Zalo | Tư vấn viên | ≤ 24 giờ |
| `DIAGNOSED` | Đã chẩn đoán xong | Tư vấn viên + Claude Code | ≤ 48 giờ |
| `QUOTED` | Đã gửi báo giá và thỏa thuận | Tư vấn viên | Cùng ngày chẩn đoán |
| `DEPOSITED` | Đã nhận cọc 50%, tạo thư mục case | Tư vấn viên | n/a |
| `IN_PROGRESS` | Đang thực hiện các bước | Claude Code + tư vấn viên | Theo gói |
| `QA` | Kiểm tra chất lượng | Tư vấn viên | ≤ 1 ngày |
| `DELIVERED` | Đã bàn giao và có buổi giải thích | Tư vấn viên | n/a |
| `REVISION` | Sửa theo góp ý của giảng viên | Claude Code + tư vấn viên | ≤ 2 ngày/lần |
| `CLOSED` | Thanh toán đủ, xin feedback | Tư vấn viên | n/a |
| `LOST` / `REJECTED` | Không chốt / từ chối do vi phạm mục 4 | Tư vấn viên | n/a |

### 5.2 Chi tiết từng giai đoạn

#### Giai đoạn A: Tiếp nhận và chẩn đoán (miễn phí)

1. Nhận thông báo đơn mới (email từ Apps Script). Nhắn Zalo trong 24 giờ theo **script mở đầu** (mục 5.4).
2. Xin tài liệu: đề cương, mô hình, bảng hỏi, data (nếu có), yêu cầu của giảng viên. **Hỏi mục đích dùng data** (bài tập luyện / tiểu luận / NCKH / khóa luận) để đánh giá và chọn gói.
3. Chạy **Claude Code `/diagnose <case_id>`**. Claude Code ra 2 thứ: *Research Assessment* (nội bộ) và **tin nhắn tóm tắt cho khách** (ngắn gọn, kèm báo giá đề xuất).
4. Bạn đọc lại rồi gửi tin nhắn đó cho khách.
5. **Phân loại khách theo giai đoạn** để chọn gói:

| Khách đang… | Gói chính | Upsell tự nhiên |
|---|---|---|
| Làm bài tập môn, chưa có data / không đủ người khảo sát | **Mock Data (hoặc Combo) + Gói Bài tập môn** | SPSS Trọn bộ |
| Chưa có mô hình / bảng hỏi | Research Starter | Data Collection, Full Mentoring |
| Có bảng hỏi, chưa thu | Research Starter (rà bảng hỏi) + Data Collection | Cleaning + SPSS |
| Có data thô | Data Cleaning | SPSS |
| Chạy rồi nhưng lỗi | SPSS Consulting | AMOS, buổi luyện bảo vệ |
| Cần mô hình SEM | AMOS / SmartPLS | Full Mentoring |
| Có kết quả, cần hiểu | SPSS Cơ bản (review + giải thích) | Luyện bảo vệ |

#### Giai đoạn B: Báo giá và chốt

1. Gửi **báo giá 1 trang**: phạm vi, deliverables, thời gian, giá, điều khoản, cam kết học thuật.
2. Khách xác nhận và chuyển cọc 50%. Cập nhật Sheet sang `DEPOSITED`.
3. Chạy **`/new-case <case_id>`** để tạo thư mục case từ template.

#### Giai đoạn C: Thực hiện, theo 6 bước chuẩn

| Bước | Tên | Input | Việc chính | Deliverable | Ai |
|---|---|---|---|---|---|
| 1 | Research Diagnosis | Đề tài, mô hình, bảng hỏi, yêu cầu GV | Xác định vấn đề, rủi ro, phạm vi | `01_research_assessment.md` | Claude Code nháp, tư vấn viên duyệt |
| 2 | Research Design | Kết quả bước 1 | Kiểm tra biến, thang đo, cỡ mẫu, chọn phương pháp | `02_research_plan.md`, `02_analysis_plan.md` | Claude Code nháp, tư vấn viên duyệt |
| 3 | Data Collection | Bảng hỏi đã chốt | Dựng form, kế hoạch tiếp cận, theo dõi tiến độ | Link form, `03_collection_summary.md` | Tư vấn viên (Claude Code soạn form/nội dung) |
| 4 | Data Preparation | Data thô (.xlsx/.csv/Sheet) | Kiểm tra, làm sạch, mã hóa, outlier, đảo chiều | `clean.sav`, `data_dictionary.xlsx`, `04_cleaning_log.md` | Claude Code |
| 5 | Statistical Analysis | Data sạch + analysis plan | Chạy các kiểm định theo plan, kiểm tra giả định | `.sps`, output, bảng kết quả, project AMOS/PLS | Claude Code (+ tư vấn viên chạy AMOS/SmartPLS GUI nếu cần) |
| 6 | Interpretation & Handover | Kết quả bước 5 | Giải thích, đối chiếu giả thuyết, dàn ý chương 4, câu hỏi bảo vệ, hướng dẫn tự chạy lại | `06_analysis_report.docx/.md`, `06_tutorial.md`, `06_defense_qa.md` | Claude Code nháp, tư vấn viên duyệt và dạy 1:1 |

**Checkpoint với khách**, bắt buộc xác nhận trước khi đi tiếp:

- Sau bước 2: khách đồng ý *Analysis Plan*. Đây là "hợp đồng phương pháp", tránh việc đổi yêu cầu giữa chừng.
- Sau bước 4: khách xem *Cleaning Log*, đồng ý số phiếu cuối cùng.
- Sau bước 5: báo trước kết quả chính (giả thuyết nào được ủng hộ), trước khi viết report.

#### Giai đoạn D: QA và bàn giao

1. Tư vấn viên chạy **QA checklist** (mục 6.6).
2. Gửi gói bàn giao: một thư mục zip hoặc Drive, có `README` liệt kê từng file.
3. Gửi kèm **tin nhắn hướng dẫn đọc kết quả** (Claude Code soạn: 5–7 ý chính, kết luận giả thuyết) và mời khách hỏi lại bất cứ chỗ nào chưa hiểu.
4. Thu 50% còn lại. Cập nhật Sheet sang `DELIVERED`.

#### Giai đoạn E: Hậu mãi

- Hỗ trợ sửa 2 lần trong 30 ngày (`REVISION`).
- Sau khi khách bảo vệ xong: xin feedback (form 3 câu) và xin phép dùng testimonial ẩn danh.
- Sau 90 ngày: **xóa dữ liệu** của khách, ghi ngày xóa vào Sheet.

### 5.3 Template tài liệu cho khách

| Tài liệu | Khi nào |
|---|---|
| Báo giá + Thỏa thuận dịch vụ (1 trang) | Giai đoạn B |
| Research Assessment | Bước 1 |
| Analysis Plan | Bước 2 |
| Cleaning Log + Data Dictionary | Bước 4 |
| Analysis Report (giải thích từng bảng) | Bước 6 |
| Tutorial "tự chạy lại" | Bước 6 |
| Bộ câu hỏi bảo vệ (Defense Q&A) | Bước 6, gói SPSS Trọn bộ trở lên |
| README bàn giao | Bàn giao |
| Form feedback | Đóng case |

### 5.4 Script giao tiếp mẫu

- **Mở đầu:** "Chào [tên], mình là [X] bên Rõ Số. Mình đã nhận yêu cầu về đề tài *[đề tài]*. Bạn gửi giúp mình bảng hỏi, mô hình và file data (nếu có) để mình chẩn đoán miễn phí nhé. Khoảng [thời gian] mình gửi lại đánh giá và báo giá."
- **Từ chối yêu cầu vi phạm:** "Phần này bên mình không làm được vì sẽ khiến bạn gặp rủi ro gian lận học thuật (có thể bị đình chỉ). Thay vào đó, mình có thể [phương án hợp lệ]…"

---

## 6. Quy trình cho Claude Code

> Mục tiêu: bạn chỉ cần nói *"làm đơn RC-001 gói SPSS trọn bộ"*. Claude Code đọc đơn, tự chọn bước, làm theo SOP, dừng ở checkpoint, và **linh hoạt** với yêu cầu riêng của từng đề tài.

### 6.1 Thành phần

| Thành phần | Vai trò |
|---|---|
| `CLAUDE.md` (gốc dự án) | "Hiến pháp": vai trò, phạm vi dịch vụ (mục 4), cấu trúc case, quy tắc đặt tên, chuẩn thống kê, khi nào phải dừng hỏi |
| `docs/` | SOP chi tiết, ngưỡng thống kê, cây chọn kiểm định, template report |
| `.claude/skills/` | Các lệnh tắt cho từng bước (mục 6.3) |
| `templates/case/` | Khung thư mục và file cho mỗi case mới |
| `toolkit/` (Python) | Module xử lý: cleaning, Cronbach, EFA, hồi quy…, xuất .sav và .sps |
| `cases/<case_id>/` | Mỗi khách một thư mục, độc lập |

### 6.2 Cấu trúc một case

```
cases/RC-2611-001/
├── case.yaml                 # thông tin đơn + mô hình nghiên cứu + gói + status (nguồn sự thật)
├── 00_intake/                # tài liệu khách gửi (bảng hỏi, đề cương, yêu cầu GV)
├── 01_assessment.md
├── 02_research_plan.md
├── 02_analysis_plan.md
├── data/
│   ├── raw/                  # BẤT BIẾN: không bao giờ sửa file gốc
│   ├── clean/                # clean.sav, clean.xlsx
│   └── data_dictionary.xlsx
├── 04_cleaning_log.md
├── analysis/
│   ├── scripts/              # .py chạy thực tế (tái lập được)
│   ├── spss/                 # .sps để khách tự chạy
│   ├── amos_smartpls/        # hướng dẫn hoặc project
│   └── output/               # bảng kết quả .xlsx, hình .png
├── 06_report/
│   ├── analysis_report.md / .docx
│   ├── tutorial.md
│   └── defense_qa.md
├── deliverables/             # bản đóng gói cuối giao khách + README
└── log.md                    # nhật ký: ai làm gì, khi nào, quyết định gì
```

**`case.yaml` mẫu:**

```yaml
case_id: RC-2611-001
status: IN_PROGRESS
client: { name: "Nguyễn Văn A", school: "UEH", level: "Đại học", deadline: 2026-12-15 }
packages: [data_cleaning, spss_full]
topic: "Các yếu tố ảnh hưởng đến ý định mua hàng online của Gen Z"
model:
  type: regression            # regression | sem | pls_sem | group_comparison
  constructs:
    GC: { name: "Giá cả",        items: [GC1, GC2, GC3, GC4], role: IV }
    CL: { name: "Chất lượng",    items: [CL1, CL2, CL3, CL4, CL5], role: IV }
    NT: { name: "Niềm tin",      items: [NT1, NT2, NT3, NT4], role: IV, reverse: [NT3] }
    YD: { name: "Ý định mua",    items: [YD1, YD2, YD3], role: DV }
  hypotheses:
    H1: "GC → YD (+)"
    H2: "CL → YD (+)"
    H3: "NT → YD (+)"
  controls: [gioi_tinh, thu_nhap]
scale: { type: likert, points: 5 }
sample: { required: 250, current: 268 }
lecturer_requirements: "Bắt buộc có EFA, hồi quy, ANOVA theo thu nhập"
flexible_notes: "GV yêu cầu bảng theo mẫu APA, làm tròn 3 chữ số"
```

### 6.3 Bộ lệnh (skills)

| Lệnh | Bước | Việc Claude Code làm | Dừng để duyệt? |
|---|---|---|---|
| `/new-case <id>` | n/a | Lấy đơn từ Google Sheet (hoặc paste), tạo thư mục từ template, điền `case.yaml` | Không |
| `/diagnose <id>` | 1 | Đọc tài liệu khách, phát hiện vấn đề (mô hình, thang đo, cỡ mẫu, bảng hỏi), viết Assessment, gợi ý gói và giá | **Có** |
| `/design <id>` | 2 | Chọn kiểm định theo cây quyết định, tính cỡ mẫu, viết Research Plan + Analysis Plan | **Có** (checkpoint khách) |
| `/build-form <id>` | 3 | Soạn nội dung Google Form (câu lọc, attention check, thứ tự), checklist phát khảo sát | Có |
| `/clean <id>` | 4 | Kiểm tra data, áp dụng quy tắc làm sạch, mã hóa đảo chiều, xuất .sav + dictionary + log | **Có** (checkpoint khách) |
| `/analyze <id>` | 5 | Chạy các phân tích theo Analysis Plan, kiểm tra giả định, xuất bảng và syntax .sps | Có, nếu có kết quả bất thường |
| `/interpret <id>` | 6 | Viết Analysis Report, đối chiếu giả thuyết, dàn ý chương 4, Defense Q&A, Tutorial | Có |
| `/qa <id>` | QA | Chạy checklist 6.6, tái lập kết quả từ script, kiểm tra phạm vi | n/a |
| `/deliver <id>` | Bàn giao | Đóng gói `deliverables/`, viết README, cập nhật status | Có |
| `/revise <id> "<góp ý GV>"` | Sửa | Phân tích góp ý, xác định có thuộc phạm vi không, thực hiện và ghi log | Có |
| `/reply <id> "<tin nhắn khách>"` | Mọi lúc | Đọc ngữ cảnh case, soạn câu trả lời tiếng Việt thân thiện, dễ hiểu để bạn copy gửi Zalo | Bạn đọc trước khi gửi |
| `/mock-data <id>` | 3 (thay thế) | Sinh mock data sát thực tế theo `case.yaml`: Likert có lệch phân phối tự nhiên, tương quan giữa các item theo cấu trúc nhân tố, hệ số đường dẫn theo hướng giả thuyết, có một ít nhiễu và missing tự nhiên; xuất .sav + .xlsx + codebook. Tham số chỉnh được: cỡ mẫu, độ mạnh quan hệ, giả thuyết nào ủng hộ / không | Không |
| `/find-dataset <id>` | 3 (thay thế) | Tìm bộ dữ liệu khảo sát đã công bố cùng chủ đề, đánh giá độ khớp với mô hình, chuẩn hóa sang .sav, kèm trích dẫn | Có (chọn bộ) |
| `/status` | n/a | Liệt kê các case, status và deadline gần nhất | Không |

**"Flexible" được thực hiện thế nào:**

- `case.yaml` có mục `lecturer_requirements` và `flexible_notes`. Claude Code **ưu tiên yêu cầu của giảng viên** hơn mặc định của SOP (ví dụ ngưỡng loading 0.4 thay vì 0.5, hoặc bắt buộc dùng Varimax), miễn là không vi phạm mục 4.
- Mô hình không chuẩn (logistic, panel, DiD, Stata/Eviews, phân tích định tính…): Claude Code **đề xuất phương án** trong Analysis Plan, rồi chờ duyệt.
- Mọi quyết định lệch khỏi SOP đều ghi vào `log.md` kèm lý do.

### 6.4 Chuẩn thống kê mặc định (có thể override theo giảng viên)

| Phân tích | Tiêu chí mặc định | Nguồn trích dẫn gợi ý |
|---|---|---|
| Cronbach's Alpha | α ≥ 0.6 (chấp nhận), ≥ 0.7 (tốt); item-total ≥ 0.3 | Nunnally & Bernstein (1994); Hair et al. |
| EFA | KMO ≥ 0.5; Bartlett p < 0.05; Eigenvalue ≥ 1; tổng phương sai trích ≥ 50%; loading ≥ 0.5; chênh lệch tải chéo ≥ 0.3 | Hair et al. (2019) |
| Phép trích / xoay | PCA + Varimax (phổ biến ở VN), hoặc PAF + Promax nếu đi tiếp CFA/SEM | Ghi rõ lựa chọn trong Analysis Plan |
| Tương quan | Pearson, p < 0.05; cảnh báo |r| > 0.8 giữa các IV | n/a |
| Hồi quy | F-test p < 0.05; hệ số p < 0.05; VIF < 2 (tốt), < 10 (chấp nhận); kiểm tra phân phối phần dư, phương sai sai số (Breusch-Pagan), Durbin-Watson 1.5–2.5 | Hair et al. |
| T-test / ANOVA | Levene trước; Welch nếu vi phạm; post-hoc Tukey / Games-Howell | n/a |
| CFA (AMOS) | CMIN/df < 3; CFI, TLI ≥ 0.9; RMSEA < 0.08; SRMR < 0.08; CR ≥ 0.7; AVE ≥ 0.5; HTMT < 0.85 | Hu & Bentler (1999); Fornell & Larcker (1981); Henseler et al. (2015) |
| PLS-SEM | Outer loading ≥ 0.7; CR ≥ 0.7; AVE ≥ 0.5; HTMT < 0.85; VIF < 3–5; bootstrap 5000 | Hair et al. (2022) |
| Cỡ mẫu | Max(5 × số biến quan sát, 50 + 8 × số IV); SEM ≥ 200 | Hair et al.; Tabachnick & Fidell |

**Cây chọn kiểm định** (sẽ có file riêng `docs/test-selection.md`):
mục tiêu (so sánh nhóm / quan hệ / dự báo / đo lường) → loại biến (định danh, thứ bậc, khoảng) → số nhóm → giả định → kiểm định.

### 6.5 Quy tắc làm sạch dữ liệu (mặc định)

| Quy tắc | Xử lý | Ghi log |
|---|---|---|
| Phiếu trùng (timestamp hoặc toàn bộ câu trả lời giống nhau) | Loại bản sau | ✓ |
| Không đúng đối tượng (câu lọc) | Loại | ✓ |
| Sai câu attention check | Loại | ✓ |
| Straight-lining (cùng một đáp án cho ≥ 90% câu Likert) | Đánh dấu, đề xuất loại, **chờ duyệt** | ✓ |
| Thời gian làm quá nhanh (< 1/3 trung vị, nếu có dữ liệu thời gian) | Đánh dấu, đề xuất loại | ✓ |
| Missing < 5% một phiếu | Giữ, xử lý theo Analysis Plan | ✓ |
| Missing ≥ 20% một phiếu | Đề xuất loại | ✓ |
| Câu đảo chiều | Recode `(max + 1) − x`, giữ biến gốc | ✓ |
| Outlier (Mahalanobis p < 0.001) | Đánh dấu, **không tự loại**, báo cáo | ✓ |

> Không bao giờ: sửa giá trị trả lời, thêm phiếu, hay loại phiếu vì lý do "để đạt". Xem mục 4.

### 6.6 QA checklist (trước khi bàn giao)

**Kỹ thuật**
- [ ] `data/raw/` không bị sửa (so sánh hash).
- [ ] Chạy lại `analysis/scripts/` từ raw, ra đúng kết quả trong report.
- [ ] File `.sps` chạy được trên SPSS (tư vấn viên test, hoặc so sánh số liệu).
- [ ] N cuối cùng khớp giữa Cleaning Log, bảng mô tả và report.
- [ ] Mọi bảng có tiêu đề, đơn vị, làm tròn đúng yêu cầu của giảng viên.

**Học thuật**
- [ ] Kết luận về giả thuyết khớp với p-value và hướng của hệ số.
- [ ] Đã kiểm tra giả định và báo cáo, kể cả khi bị vi phạm.
- [ ] Có ghi chú hạn chế (cỡ mẫu, phương pháp chọn mẫu…).

**Phạm vi**
- [ ] Combo: kết quả trên data mock và data công bố được tách riêng, không lẫn file.
- [ ] Mọi phiếu hoặc biến bị loại đều có lý do trong log.
- [ ] Report là *giải thích và dàn ý*, không phải chương 4 viết sẵn để nộp.

### 6.7 Khi nào Claude Code phải dừng và hỏi

1. Yêu cầu chạm vào mục 4.2: **dừng và từ chối**, đề xuất phương án hợp lệ.
2. Kết quả không đạt ngưỡng (alpha, KMO, fit…): báo chẩn đoán và các phương án, **không tự loại biến hàng loạt**.
3. Yêu cầu nằm ngoài gói đã mua: báo "ngoài phạm vi" và gợi ý báo giá thêm.
4. Thông tin mâu thuẫn (mô hình trong đề cương khác bảng hỏi…).
5. Trước mỗi checkpoint khách (sau bước 2, 4, 5).

### 6.8 Công nghệ phân tích

| Việc | Công cụ | Ghi chú |
|---|---|---|
| Xử lý dữ liệu | Python: `pandas`, `openpyxl` | n/a |
| Cronbach, EFA | `pingouin`, `factor_analyzer` | n/a |
| Hồi quy, ANOVA, kiểm định | `statsmodels`, `scipy` | n/a |
| CFA / SEM | `semopy` (để kiểm tra chéo) | Khách thường cần project **AMOS/SmartPLS gốc**. Claude Code viết hướng dẫn từng bước, còn tư vấn viên dựng project trên GUI (2 phần mềm này không có API để tự động hóa) |
| Xuất .sav | `pyreadstat` | Giữ nhãn biến và nhãn giá trị |
| Sinh .sps | Template syntax do toolkit sinh | Để khách tự chạy và kiểm chứng |
| Report | Markdown, rồi `.docx` (`python-docx` hoặc pandoc) | n/a |

> ⚠️ Máy hiện có Python 3.14 nhưng chưa có các thư viện này. **Chỉ cài khi bạn duyệt** (dùng `.venv` riêng trong dự án). Nên cân nhắc Python 3.12 để tương thích tốt với `pyreadstat` và `factor_analyzer`.

---

## 7. Website

### 7.1 Stack đề xuất

> Bạn nói "Nest". Mình hiểu là **Next.js**: NestJS là framework backend, không dùng để làm giao diện. Nếu đúng là Next.js thì stack như sau:

| Lớp | Lựa chọn | Lý do |
|---|---|---|
| Framework | **Next.js 15 (App Router) + TypeScript**, `output: 'export'` (static) | Chỉ có frontend, deploy free lên Vercel |
| Styling | **Tailwind CSS** | Nhanh, đồng bộ |
| UI components | **shadcn/ui** (Accordion, Dialog, Form, Select, Toast) | Đẹp, tùy biến được |
| Animation | **Framer Motion** (reveal on scroll, stagger, layout animation) + **Lenis** (smooth scroll) | Mượt, "xịn" |
| Hiệu ứng nổi bật | Count-up số liệu, timeline vẽ dần theo scroll, card nghiêng nhẹ khi hover, marquee logo trường, mockup bảng SPSS "đang chạy" ở hero | Tạo cảm giác chuyên nghiệp, đúng chủ đề |
| Icon | `lucide-react` | n/a |
| Font | **Be Vietnam Pro** (hiển thị tiếng Việt chuẩn) | n/a |
| Form | `react-hook-form` + `zod` để validate, POST lên Google Apps Script | Không cần backend |
| Deploy | Vercel (free) + domain riêng | n/a |
| Analytics | Vercel Analytics hoặc Google Analytics 4 + Meta Pixel (nếu chạy ads) | Đo nguồn khách |

### 7.2 Cấu trúc trang: one-page, cuộn dọc

| # | Section | Nội dung | Animation |
|---|---|---|---|
| 0 | **Navbar** (sticky, mờ nền khi cuộn) | Logo, menu anchor, nút "Gửi yêu cầu" | Thu nhỏ khi cuộn, active theo section |
| 1 | **Hero** | Headline "Hiểu rõ từng con số trong nghiên cứu của bạn", subtext, 2 CTA, 3 điểm tin cậy; bên phải là mockup bảng Cronbach có chỉ số "chạy" | Chữ hiện từng dòng; số đếm lên; chip KMO/R² trôi nhẹ |
| 2 | **Dải số liệu** | 6 gói · 6 bước · 3 phần mềm · 100% có syntax | Count-up khi vào khung nhìn |
| 3 | **7 vấn đề** | Grid 7 thẻ (số thứ tự, tiêu đề, mô tả) | Stagger fade-up; hover nâng thẻ |
| 4 | **Dịch vụ** | Các thẻ gói: đối tượng, nội dung, bàn giao, giá "từ X"; gói SPSS nổi bật. Nhóm dữ liệu gộp thành một thẻ **"Dịch vụ Data"** (mock data · dữ liệu công bố · làm sạch), không ghi chú thêm | Thẻ nổi bật có viền gradient chuyển động |
| 5 | **Quy trình 6 bước** | Timeline dọc: tên bước, mô tả, deliverable | Đường timeline vẽ dần theo scroll |
| 6 | **So sánh** (mới) | Bảng "Dịch vụ thông thường vs Rõ Số": syntax, log, buổi 1:1, cam kết data thật | Check/cross hiện lần lượt |
| 7 | **Cách làm việc** (nền tối) | 4 bước: Nhắn Zalo / gửi file → Nhận báo giá trong 24h → Nhận kết quả + giải thích → Hỏi lại thoải mái 30 ngày. *(v2: thay cho section "Cam kết học thuật")* | Các bước hiện lần lượt |
| 8 | **Feedback** | Testimonial (để trống lúc ra mắt, ẩn section nếu chưa có) | Carousel |
| 9 | **FAQ** | 6–8 câu (data, chỉnh số, bàn giao, thời gian, thanh toán, bảo mật) | Accordion mượt |
| 10 | **Form gửi yêu cầu** | Xem 7.3 | Chia thành 3 bước (stepper) với thanh tiến độ |
| 11 | **Footer** | Logo, slogan, Zalo / Facebook / Email, link cam kết | n/a |
| n/a | **Nút nổi** | Nút Zalo nổi góc phải, và "Gửi yêu cầu" trên mobile | Pulse nhẹ |

**Trang phụ (tùy chọn, có thể làm sau):** `/cam-ket` (chính sách học thuật đầy đủ), `/bao-mat`.

### 7.3 Form gửi yêu cầu, gồm 3 bước

| Bước | Trường | Bắt buộc |
|---|---|---|
| **1. Liên hệ** | Họ tên · SĐT/Zalo · Email · Trường · Ngành · Bậc học (ĐH/ThS/TS) | Tên, SĐT, Trường, Bậc |
| **2. Nghiên cứu** | Loại bài (tiểu luận/NCKH/KLTN/luận văn/bài báo) · Deadline · Tên đề tài · Mô hình (text) · **Giai đoạn hiện tại** (6 lựa chọn) · Số mẫu hiện có / yêu cầu · Phần mềm (SPSS/AMOS/SmartPLS/Stata/Chưa rõ) | Loại bài, Deadline, Đề tài, Giai đoạn |
| **3. Nhu cầu** | Gói quan tâm (chọn nhiều) · **Tình trạng dữ liệu** (đã có đủ / có nhưng thiếu / cần mock data để chạy thử / cần tìm dữ liệu công bố) · Link Google Drive tài liệu · Mô tả vấn đề · Biết đến qua đâu | Gói, Tình trạng dữ liệu |

- Tạo **mã đơn** phía client theo dạng `RC-YYMM-XXXX` và hiển thị sau khi gửi thành công ("Mã đơn của bạn: RC-2611-0042").
- Chống spam: honeypot + giới hạn 1 lần gửi mỗi 60 giây.
- Upload file: **không** upload trực tiếp. Dùng link Google Drive, cho đơn giản và an toàn.

### 7.4 Thiết kế

- **Màu:** navy đậm `#0B1F3A` (tin cậy, học thuật), teal `#0FB5A6` (dữ liệu, tươi), cam nhấn `#FF7A45` (CTA); nền trắng ngà; section cam kết dùng nền navy.
- **Phong cách:** sạch, nhiều khoảng trắng, bo góc 16px, đổ bóng mềm, có các chi tiết "data" (lưới chấm, bảng số, biểu đồ cột nhỏ làm logo).
- **Responsive:** ưu tiên mobile, vì sinh viên chủ yếu vào từ Facebook và Zalo trên điện thoại.
- **Hiệu năng:** Lighthouse ≥ 90; animation tôn trọng `prefers-reduced-motion`.
- **SEO:** metadata tiếng Việt, Open Graph image (để share lên Facebook/Zalo có ảnh đẹp), `sitemap.xml`.

---

## 8. Tiếp nhận đơn qua Google Sheet

### 8.1 Luồng

```
Website form ──POST──► Google Apps Script (Web App) ──► Google Sheet "Don_Hang"
                                │
                                ├──► Email thông báo cho bạn (MailApp)
                                └──► (tùy chọn) tin nhắn Telegram/Zalo bot
Claude Code ──GET + token──► Apps Script ──► trả JSON của 1 đơn  (dùng cho /new-case)
```

### 8.2 Cột trong Sheet

`ma_don · thoi_gian · ho_ten · sdt_zalo · email · truong · nganh · bac_hoc · loai_bai · deadline · de_tai · mo_hinh · giai_doan · so_mau · so_mau_yeu_cau · phan_mem · goi_dich_vu · link_tai_lieu · mo_ta · nguon · cam_ket · status · nguoi_phu_trach · bao_gia · da_coc · ngay_ban_giao · ngay_xoa_du_lieu · ghi_chu`

(Các cột từ `status` trở đi do bạn cập nhật tay hoặc Claude Code cập nhật.)

### 8.3 Bảo mật

- Apps Script `doGet` (cho Claude Code đọc đơn) yêu cầu **token bí mật**. Token lưu trong `.env` local và không commit.
- Sheet chỉ chia sẻ cho bạn và cộng tác viên.
- Khi có khách đông hơn, nâng cấp lên Supabase mà không phải sửa giao diện form.

---

## 9. Cấu trúc thư mục dự án

```
Economic_Consulting/
├── PLAN.md                      # file này
├── CLAUDE.md                    # hiến pháp cho Claude Code (mục 4 + 6)
├── README.md
├── .env.example                 # APPS_SCRIPT_URL, APPS_SCRIPT_TOKEN
├── docs/
│   ├── market-research.md       # mục 1
│   ├── services-pricing.md      # mục 3
│   ├── academic-integrity.md    # mục 4 (bản đầy đủ, dùng làm thỏa thuận dịch vụ)
│   ├── consulting-sop.md        # mục 5
│   ├── analysis-standards.md    # mục 6.4–6.5
│   └── test-selection.md        # cây chọn kiểm định
├── .claude/skills/              # new-case, diagnose, design, build-form, clean, analyze, interpret, qa, deliver, revise, status
├── templates/
│   ├── case/                    # khung thư mục + case.yaml + các file .md mẫu
│   └── client-docs/             # báo giá, thỏa thuận, README bàn giao, form feedback
├── toolkit/                     # Python: config, data_engine, stats_engine, export, report
├── apps-script/
│   └── Code.gs                  # nhận form → Sheet, email, doGet có token
├── web/                         # Next.js site
└── cases/                       # dữ liệu khách (gitignore)
```

---

## 10. Lộ trình triển khai

| Phase | Nội dung | Đầu ra | Phụ thuộc |
|---|---|---|---|
| **0. Duyệt** | Bạn duyệt file này, chốt các câu ở mục 11 | PLAN.md v2 | n/a |
| **1. Nền tảng tài liệu** | `CLAUDE.md`, `docs/*`, `templates/*` | Quy trình sẵn sàng, có thể làm khách thủ công ngay | Phase 0 |
| **2. Website** | Next.js + animation + form + Apps Script + Sheet | Site chạy local, rồi deploy Vercel | Phase 0, link 3 kênh |
| **3. Skills cho Claude Code** | `.claude/skills/*` | Các lệnh `/new-case` … `/deliver` | Phase 1 |
| **4. Toolkit Python** | Cài `.venv`, viết module, test bằng mock data | Pipeline cleaning → SPSS → report chạy được | Phase 1, bạn duyệt cài môi trường |
| **5. Pilot** | 3–5 khách đầu (ưu đãi), thu feedback | Điều chỉnh giá và quy trình | Phase 1–4 |
| **Song song** | Khảo sát xác thực nhu cầu (50–100 sinh viên kinh tế) | Số liệu thật về pain point, dùng làm content | Bất kỳ lúc nào |

Phase 2 và Phase 3–4 có thể làm song song.

---

## 11. Câu hỏi cần bạn chốt

0. **(v3) Gói Mock Data (150k), Dữ liệu công bố (250k), Combo (350k)** ở mục 3.2: mức giá ổn chưa?
1. **Framework:** "Nest" là **Next.js** đúng không?
2. **Tên thương hiệu:** chọn **Rõ Số** hay tên khác ở mục 2.2?
3. **Bảng giá** ở mục 3.2: đồng ý chưa, có chỉnh mức nào không?
4. **Ưu đãi ra mắt** giảm 20% cho 10 khách đầu: có làm không?
5. **Chẩn đoán miễn phí** qua tin nhắn: đồng ý không?
6. **Ai thực hiện?** (v2: đã rõ là bạn vận hành, Claude Code làm chuyên môn.) Sau này có thêm cộng tác viên không?
7. **AMOS/SmartPLS:** máy bạn có cài sẵn không? (Phần này cần GUI, Claude Code chỉ hướng dẫn và kiểm tra chéo.)
8. **Khảo sát xác thực nhu cầu** (mục 10): có muốn mình soạn bộ câu hỏi không?
9. **Section testimonial:** ẩn lúc ra mắt, hay dùng nội dung mẫu có ghi rõ "minh họa"? (Đề xuất: **ẩn**, vì testimonial giả trái với định vị minh bạch.)
