# Alpha Lab: Kế hoạch tổng thể (v5)

> **Trạng thái:** Website đã xong (HTML thuần, `index.html` ở gốc repo, deploy Vercel). Đang chuẩn bị Phase 1 (quy trình vận hành).
>
> **Thay đổi v2 (theo góp ý):**
> 1. **Tư vấn hoàn toàn qua tin nhắn** (Zalo/Messenger), không gọi điện, không họp 1:1. Bạn là người vận hành và xử lý dữ liệu; Claude Code soạn nội dung chuyên môn (giải thích, trả lời câu hỏi), bạn chỉ đọc lại rồi gửi.
> 2. **Giảm nhấn mạnh học thuật trên website.** Khách chính là sinh viên làm **bài tập môn học**, không chỉ khóa luận. Nguyên tắc vẫn giữ, nhưng chỉ dùng nội bộ và nhắc nhẹ trên site.
> 3. **Tách 2 gói dữ liệu chạy song song:** **Mock Data** (data sát thực tế theo mô hình, để sinh viên có data chạy thử ngay) và **Dữ liệu công bố** (tìm bộ khảo sát đã công bố, có nguồn), cùng một combo gộp cả hai.
> 4. **(v3) Bỏ cách gọi "học thuật/đạo đức"** trong tài liệu. Mục 4 đổi thành "Phạm vi dịch vụ".
> 5. **(v4) Website chỉ ghi chung là "Dịch vụ data"** (mock data, dữ liệu công bố, làm sạch, chạy mô hình), không ghi chú thêm gì. **Tư vấn viên (bạn) đánh giá từng trường hợp** sinh viên dùng data vào việc gì, rồi quyết định nhận hay không và chọn gói nào.
> 6. **(v5) Khớp với website đã làm:** tên chốt **Alpha Lab**; web là 1 file HTML thuần (không Next.js, không form); khách liên hệ thẳng qua Zalo (Facebook/Email bổ sung sau). Web có **3 dịch vụ chính + 1 thẻ "Dịch vụ khác"**; các gói còn lại trong plan cũ chuyển vào "Dịch vụ khác", báo giá theo yêu cầu. Bỏ toàn bộ phần form + Google Sheet.
>
> Duyệt xong từng phần (đánh dấu ✅ hoặc ghi góp ý trực tiếp vào file), mình mới triển khai.
> Ngày lập: 04/11/2026

## Mục lục

1. [Kết quả research: sinh viên kinh tế gặp khó khăn gì?](#1-kết-quả-research)
2. [Định vị và thương hiệu](#2-định-vị-và-thương-hiệu)
3. [Gói dịch vụ và bảng giá khởi điểm](#3-gói-dịch-vụ-và-bảng-giá-khởi-điểm)
4. [Phạm vi dịch vụ](#4-phạm-vi-dịch-vụ)
5. [Quy trình consulting (cho người tư vấn)](#5-quy-trình-consulting)
6. [Quy trình thực hiện cho Claude Code](#6-quy-trình-cho-claude-code)
7. [Website (HTML, đã xong)](#7-website--đã-xong)
8. [Tiếp nhận khách](#8-tiếp-nhận-khách)
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

### 2.2 Tên thương hiệu: **Alpha Lab** ✅

Tên lấy từ Cronbach's Alpha, chỉ số đầu tiên sinh viên nào chạy SPSS cũng gặp. Logo là đường cong phân phối chuẩn với vùng đuôi có ý nghĩa.

- Bộ nhận diện: `brand/alpha-lab/` (logo nền sáng/tối, `mark.svg`, avatar 1024×1024, ảnh bìa Facebook 1640×624).
- Slogan trên web: *"Make every number make sense."*
- Các phương án đã loại: Rõ Số, Biến Số, Mẫu Số, Sig.

### 2.3 Kênh liên hệ

- [x] Zalo: `https://zalo.me/0905889328` (kênh chính, có nút nổi trên web)
- [ ] Facebook Page: **pending**
- [ ] Email: **pending**

Link Facebook/Email nằm trong `index.html`, đánh dấu `TODO(pending)` (thẻ liên hệ + footer).

---

## 3. Gói dịch vụ và bảng giá khởi điểm

### 3.1 Logic định giá

- **Neo theo giá thị trường** (mục 1.3), định giá ngang hoặc thấp hơn khoảng 10%, vì mình là thương hiệu mới chưa có review.
- **Không bán phá giá.** Giá trị khác biệt nằm ở bàn giao (syntax, log, buổi 1:1), nên không cần rẻ nhất.
- **Nâng cấp được:** phí gói trước được trừ vào gói sau. Ví dụ đã mua Rà soát 300k, lên SPSS thì trừ 300k.
- Website ghi giá dạng **"từ X"**, "Dịch vụ khác" ghi "báo giá theo yêu cầu". Báo giá cuối cùng gửi sau khi chẩn đoán qua tin nhắn.

### 3.2 Bảng giá (khớp với website)

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
| Thiếu mẫu, chưa có data để chạy | **Mock data** (chạy thử ngay) và/hoặc **Dữ liệu đã công bố** (nhóm "Dịch vụ khác"), hoặc combo cả hai. Không trộn phiếu mock vào data khảo sát thật của sinh viên |
| Mock data trong báo cáo | Báo cáo dùng từ trung tính **"dữ liệu"**, không cần ghi chú "mô phỏng" trong thân bài. Claude Code chỉ **không tự viết thêm** các chi tiết về một cuộc khảo sát không có thật (ví dụ "khảo sát 250 sinh viên tại UEH từ 01–15/11"); phần phương pháp thu thập do sinh viên tự viết |
| Giả thuyết bị bác bỏ | Trình bày trung thực, hướng dẫn cách *giải thích* kết quả không ủng hộ giả thuyết (đây là kết quả hợp lệ) |
| Đặt tên file mock data | Nội bộ, trong thư mục case: `data/mock/` (để không lẫn với data thật khi chạy combo). File giao khách: `mock_data.sav`, tên trung tính, không watermark |
| Khách khăng khăng đòi làm việc thuộc mục 4.2 | Từ chối lịch sự, đề xuất phương án hợp lệ. Nếu vẫn đòi thì **dừng hợp tác**, hoàn phần phí chưa thực hiện |

### 4.4 Cơ chế bảo vệ

1. Báo giá gửi qua Zalo có 1 dòng phạm vi dịch vụ: *"Alpha Lab hỗ trợ xử lý & giải thích dữ liệu; nguồn dữ liệu luôn được ghi rõ."*
2. Website không có checkbox hay lời răn đe; tư vấn viên đánh giá từng trường hợp khi nhắn tin.
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
| `LOST` / `REJECTED` | Không chốt / từ chối do vi phạm mục 4 | Tư vấn viên | n/a |

### 5.2 Chi tiết từng giai đoạn

#### Giai đoạn A: Tiếp nhận và chẩn đoán (miễn phí)

1. Khách nhắn qua Zalo (hoặc Facebook/Email). Trả lời trong 24 giờ theo **script mở đầu** (mục 5.4), rồi chạy `/new-case` với thông tin khách để tạo case ở status `NEW`.
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

#### Giai đoạn B: Báo giá và chốt

1. Gửi **báo giá 1 trang**: phạm vi, deliverables, thời gian, giá, điều khoản, cam kết học thuật.
2. Khách xác nhận và chuyển cọc 50%. Cập nhật status sang `DEPOSITED`.
3. Điền gói đã chốt vào `case.yaml` và chép tài liệu khách vào `00_intake/`.

#### Giai đoạn C: Thực hiện, theo 6 bước chuẩn

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

#### Giai đoạn D: QA và bàn giao

1. Tư vấn viên chạy **QA checklist** (mục 6.6).
2. Gửi gói bàn giao: một thư mục zip hoặc Drive, có `README` liệt kê từng file.
3. Gửi kèm **tin nhắn hướng dẫn đọc kết quả** (Claude Code soạn: 5–7 ý chính, kết luận giả thuyết) và mời khách hỏi lại bất cứ chỗ nào chưa hiểu.
4. Thu 50% còn lại. Cập nhật status sang `DELIVERED`.

#### Giai đoạn E: Hậu mãi

- Hỗ trợ sửa 2 lần trong 30 ngày (`REVISION`).
- Sau khi khách bảo vệ xong: xin feedback (form 3 câu) và xin phép dùng testimonial ẩn danh.
- Sau 90 ngày: **xóa dữ liệu** của khách, ghi ngày xóa vào `case.yaml`.

### 5.3 Template tài liệu cho khách

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

### 5.4 Script giao tiếp mẫu

- **Mở đầu:** "Chào [tên], mình là [X] bên Alpha Lab. Cảm ơn bạn đã nhắn về đề tài *[đề tài]*. Bạn gửi giúp mình bảng hỏi, mô hình và file data (nếu có) để mình chẩn đoán miễn phí nhé. Khoảng [thời gian] mình gửi lại đánh giá và báo giá."
- **Từ chối yêu cầu vi phạm:** "Phần này bên mình không làm được vì sẽ khiến bạn gặp rủi ro gian lận học thuật (có thể bị đình chỉ). Thay vào đó, mình có thể [phương án hợp lệ]…"

---

## 6. Quy trình cho Claude Code

> Mục tiêu: bạn chỉ cần nói *"làm đơn AL-2611-001 phân tích SPSS trọn bộ"*. Claude Code đọc đơn, tự chọn bước, làm theo SOP, dừng ở checkpoint, và **linh hoạt** với yêu cầu riêng của từng đề tài.

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
cases/AL-2611-001/
├── case.yaml                 # thông tin đơn + mô hình nghiên cứu + gói + status (nguồn sự thật)
├── 00_intake/                # tài liệu khách gửi (bảng hỏi, đề cương, yêu cầu GV)
├── 01_assessment.md
├── 02_analysis_plan.md
├── 03_collection_summary.md
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
case_id: AL-2611-001
status: IN_PROGRESS
client: { name: "Nguyễn Văn A", contact: "zalo", school: "UEH", level: "Đại học", deadline: 2026-12-15 }
packages: [xu_ly_du_lieu, phan_tich_spss]   # + spss_tier: bai_tap | co_ban | tron_bo
spss_tier: tron_bo
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
| `/new-case` | n/a | Bạn paste thông tin khách (tin nhắn Zalo/Facebook/Email), Claude Code cấp mã `AL-YYMM-NNN`, tạo thư mục từ template, điền `case.yaml` | Không |
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

## 7. Website ✅ Đã xong

### 7.1 Stack

- **1 file `index.html`** ở gốc repo: HTML + CSS + JS thuần, không build step. Chỉ load Google Fonts (Be Vietnam Pro, JetBrains Mono).
- Ảnh và logo: `brand/alpha-lab/`.
- Deploy: **Vercel** (Framework Preset: Other, Root Directory `./`), tự deploy khi push lên `main`. File `.vercelignore` chặn `PLAN.md`, `README.md`, `CLAUDE.md`, `docs/`, `templates/` để tài liệu nội bộ không lên web.
- Có chế độ sáng/tối (mặc định tối, nhớ lựa chọn của người xem).

### 7.2 Cấu trúc trang

| # | Section | Nội dung |
|---|---|---|
| 0 | Navbar | Logo Alpha Lab, link Dịch vụ / Quy trình / Hỏi đáp / Liên hệ, nút đổi theme |
| 1 | Hero (`#top`) | "Make every number make sense." + CTA |
| 2 | Dịch vụ (`#dich-vu`) | 4 thẻ ngang hàng: 01 → 02 → 03 (thẻ 03 "Phổ biến nhất") + 04 **"Dịch vụ khác"** (báo giá theo yêu cầu). Desktop 4 cột, tablet 2 cột, mobile 1 cột |
| 3 | Quy trình (`#quy-trinh`) | Timeline dọc 6 bước, mỗi bước có nhãn đầu ra; đường kẻ tô dần khi cuộn |
| 4 | Hỏi đáp (`#hoi-dap`) | 7 câu FAQ dạng xổ xuống (`<details>`) |
| 5 | Liên hệ (`#lien-he`) | Zalo (chính), Facebook, Email |
| 6 | Footer | Logo, link liên hệ |
| n/a | Nút nổi | "Chat Zalo" góc dưới phải |

### 7.3 Việc còn lại

- [ ] Link Facebook và Email (đang `href="#"`, có ghi chú `TODO(pending)`).
- [x] SEO cơ bản: title, meta description, Open Graph, schema `ProfessionalService`, `robots.txt`.
- [ ] Khi có link Vercel / domain: đổi `og:image` sang URL tuyệt đối, thêm `og:url`, `canonical`, `sitemap.xml`, đăng ký Google Search Console.
- [ ] (Tùy chọn) Google Analytics 4 / Meta Pixel nếu chạy quảng cáo.

---

## 8. Tiếp nhận khách

Không có form trên web. Khách nhắn thẳng qua **Zalo** (chính), Facebook hoặc Email.

```
Khách nhắn Zalo ──► Tư vấn viên trả lời (script 5.4) ──► /new-case (paste thông tin) ──► cases/AL-YYMM-NNN/case.yaml
```

- Mọi thông tin đơn và status lưu trong `case.yaml` của từng case. `/status` liệt kê toàn bộ case và deadline.
- Thông tin cần hỏi khi tiếp nhận: tên, trường, bậc học, loại bài, deadline, đề tài, mô hình, giai đoạn hiện tại, tình trạng dữ liệu, mục đích dùng data, phần mềm GV yêu cầu.
- Khi khách đông (> 10 case/tháng) mới cân nhắc thêm form + Google Sheet hoặc Supabase.

---

## 9. Cấu trúc thư mục dự án

```
Economic_Consulting/            # repo github.com/Anhhuhi123/SPSS
├── index.html                   # website (deploy Vercel)
├── brand/alpha-lab/             # logo, avatar, ảnh bìa
├── .vercelignore                # không deploy tài liệu nội bộ (PLAN, CLAUDE, docs, templates)
├── PLAN.md                      # file này
├── CLAUDE.md                    # hiến pháp cho Claude Code (mục 4 + 6)
├── README.md
├── docs/
│   ├── PROMPT_redesign.md       # prompt thiết kế web (đã dùng)
│   ├── services-pricing.md      # mục 3
│   ├── service-scope.md         # mục 4
│   ├── consulting-sop.md        # mục 5
│   ├── analysis-standards.md    # mục 6.4–6.5
│   └── test-selection.md        # cây chọn kiểm định
├── .claude/skills/              # new-case, diagnose, design, build-form, clean, analyze, interpret, qa, deliver, revise, reply, mock-data, find-dataset, status
├── templates/
│   ├── case/                    # khung thư mục + case.yaml + các file .md mẫu
│   └── client-docs/             # báo giá, README bàn giao, form feedback
├── toolkit/                     # Python: config, data_engine, stats_engine, export, report
└── cases/                       # dữ liệu khách (gitignore)
```

---

## 10. Lộ trình triển khai

| Phase | Nội dung | Đầu ra | Trạng thái |
|---|---|---|---|
| **0. Duyệt** | Chốt tên, dịch vụ, giá | PLAN.md v5 | ✅ |
| **2. Website** | `index.html` + brand + deploy Vercel | Web chạy online | ✅ (còn link FB/Email, OG) |
| **1. Nền tảng tài liệu** | `CLAUDE.md`, `docs/*`, `templates/*` | Quy trình sẵn sàng, nhận khách thủ công được | ✅ |
| **3. Skills cho Claude Code** | `.claude/skills/*` | Các lệnh `/new-case` … `/deliver` | ⏭️ **Làm tiếp theo** |
| **4. Toolkit Python** | Cài `.venv`, viết module, test bằng mock data | Pipeline cleaning → SPSS → report chạy được | Chờ Phase 1, bạn duyệt cài môi trường |
| **5. Pilot** | 3–5 khách đầu (ưu đãi), thu feedback | Điều chỉnh giá và quy trình | Chờ Phase 1–4 |
| **Song song** | Khảo sát xác thực nhu cầu (50–100 sinh viên kinh tế) | Số liệu thật về pain point, dùng làm content | Bất kỳ lúc nào |

Phase 3 và 4 có thể làm song song.

---

## 11. Câu hỏi cần bạn chốt

**Đã chốt:** framework (HTML thuần, không Next.js) · tên **Alpha Lab** · 3 dịch vụ chính + "Dịch vụ khác" và giá trên web · không form/Google Sheet · testimonial: chưa có section.

**Còn mở:**

1. **Mốc giá nội bộ** ở mục 3.2 (mốc dịch vụ 03 và "Dịch vụ khác"): giữ như vậy hay chỉnh?
2. **Ưu đãi ra mắt** giảm 20% cho 10 khách đầu: có làm không?
3. **Chẩn đoán miễn phí** qua tin nhắn: đồng ý không?
4. **Cộng tác viên:** sau này có thêm người không?
5. **AMOS/SmartPLS:** máy bạn có cài sẵn không? (Cần GUI, Claude Code chỉ hướng dẫn và kiểm tra chéo.)
6. **Khảo sát xác thực nhu cầu:** có muốn mình soạn bộ câu hỏi không?
