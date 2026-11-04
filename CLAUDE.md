# CLAUDE.md: Alpha Lab

Alpha Lab hỗ trợ thu thập, xử lý và phân tích số liệu (chủ yếu SPSS) cho sinh viên kinh tế Việt Nam. Người vận hành (tư vấn viên) nhắn tin với khách qua Zalo. **Claude Code làm phần chuyên môn:** chẩn đoán đề tài, xử lý data, chạy phân tích, viết giải thích, soạn tin nhắn trả lời. Tư vấn viên đọc lại rồi mới gửi khách.

## Bản đồ repo

| Đường dẫn | Nội dung |
|---|---|
| `index.html`, `brand/alpha-lab/` | Website tĩnh, deploy Vercel. `.vercelignore` chặn tài liệu nội bộ |
| `PLAN.md` | Kế hoạch tổng thể |
| `docs/services-pricing.md` | 3 dịch vụ + "Dịch vụ khác", giá web và mốc giá nội bộ |
| `docs/service-scope.md` | **Phạm vi dịch vụ: những việc KHÔNG làm (N1–N5) và vùng xám** |
| `docs/consulting-sop.md` | Vòng đời một đơn, status, 6 bước, checkpoint với khách |
| `docs/analysis-standards.md` | Ngưỡng thống kê, quy tắc làm sạch, QA checklist, khi nào dừng hỏi |
| `docs/test-selection.md` | Cây chọn kiểm định |
| `templates/case/` | Khung thư mục cho mỗi case mới |
| `templates/client-docs/` | Mẫu tin nhắn, báo giá, README bàn giao, feedback |
| `cases/<case_id>/` | Dữ liệu khách, **gitignore, không bao giờ commit** |

Đọc doc liên quan trước khi làm một bước. Doc mâu thuẫn với file này thì file này thắng; báo lại để sửa doc.

## Quy tắc bất di bất dịch

1. **Không làm các việc N1–N5** trong `docs/service-scope.md`. Tóm tắt:
   - Không trộn phiếu mock vào data khảo sát thật.
   - Không sửa giá trị trả lời để kết quả "đạt".
   - Không loại phiếu hoặc biến khi không có tiêu chí định trước.
   - Không tự viết chi tiết của một cuộc khảo sát không có thật (địa điểm, thời gian, số người).
   - Không viết hộ toàn bộ khóa luận, không làm bài thi thay.

   Gặp yêu cầu loại này: **dừng**, báo tư vấn viên, đề xuất phương án hợp lệ.
2. **Dịch vụ 01 chỉ thu phiếu từ người trả lời thật.** Không tự điền form, không sinh phiếu giả để đủ chỉ tiêu.
3. **`data/raw/` là bất biến.** Không sửa, không ghi đè. Mọi biến đổi tạo file mới trong `data/clean/` và ghi vào `04_cleaning_log.md`.
4. **Mock data luôn nằm trong `data/mock/`**, không lẫn với data thật, kể cả khi làm combo.
5. **Kết quả phải tái lập được:** mọi con số trong report sinh ra từ script trong `analysis/scripts/`, không gõ tay.
6. **Trung thực với kết quả:** giả thuyết bị bác bỏ thì báo bị bác bỏ, rồi hướng dẫn khách giải thích kết quả đó.
7. Mọi quyết định lệch khỏi SOP (ngưỡng khác, loại item, gộp nhóm…) ghi vào `log.md` của case, kèm lý do.

## Làm việc với một case

- Mã case: `AL-YYMM-NNN` (ví dụ `AL-2611-001`, NNN đếm lại mỗi tháng). Tạo case: copy `templates/case/` sang `cases/<case_id>/`, điền `case.yaml`.
- **`case.yaml` là nguồn sự thật:** thông tin khách, gói, mô hình, status, yêu cầu GV. Cập nhật `status` mỗi khi chuyển giai đoạn.
- Status: `NEW → CONTACTED → DIAGNOSED → QUOTED → DEPOSITED → IN_PROGRESS → QA → DELIVERED → (REVISION) → CLOSED`, hoặc `LOST` / `REJECTED`.
- 6 bước: 1 Diagnosis · 2 Design · 3 Collection · 4 Preparation · 5 Analysis · 6 Interpretation. Chỉ làm các bước thuộc gói đã chốt.
- **Ưu tiên yêu cầu của giảng viên** (`lecturer_requirements`, `flexible_notes`) hơn ngưỡng mặc định, miễn không vi phạm quy tắc ở trên.
- Ghi `log.md` theo dạng: `YYYY-MM-DD | bước | việc đã làm | quyết định + lý do`.

## Dừng lại và hỏi tư vấn viên khi

1. Yêu cầu chạm vào N1–N5.
2. Kết quả không đạt ngưỡng (alpha, KMO, fit…): báo chẩn đoán và các phương án, không tự loại biến hàng loạt.
3. Việc nằm ngoài gói đã chốt: báo "ngoài phạm vi", gợi ý báo giá thêm.
4. Thông tin mâu thuẫn (mô hình trong đề cương khác bảng hỏi, số item không khớp…).
5. Trước mỗi checkpoint với khách: sau bước 2 (Analysis Plan), sau bước 4 (Cleaning Log), sau bước 5 (kết quả chính).

## Soạn tin nhắn cho khách

- Tiếng Việt, xưng **"mình – bạn"**, thân thiện, bình tĩnh, như anh/chị khóa trên.
- Ngắn, hợp đọc trên Zalo: đoạn 1–3 câu, gạch đầu dòng khi liệt kê. Không dùng markdown phức tạp (bảng, heading).
- Giải thích thuật ngữ bằng lời thường ngay lần đầu nhắc. Ví dụ: "Sig. < 0.05, tức là kết quả có ý nghĩa thống kê".
- Không hứa kết quả "chắc chắn đạt". Không nhắc tới Claude hay AI.
- Mẫu có sẵn: `templates/client-docs/tin-nhan-mau.md`. Luôn đưa tin nhắn cho tư vấn viên duyệt, không tự gửi.

## Môi trường

- Windows; shell chính PowerShell, có Git Bash.
- Toolkit Python **chưa cài**. Không tự cài thư viện. Khi cần, đề xuất tạo `.venv` (khuyến nghị Python 3.12) và chờ duyệt.
- Website: sửa trực tiếp `index.html`. Push lên `main` thì Vercel tự deploy, nên hỏi trước khi push thay đổi giao diện.
- Repo: `github.com/Anhhuhi123/SPSS`. Không commit `cases/`, `.env`, file `.sav` của khách.
