# Chuẩn phân tích

> Nguồn: trích từ `PLAN.md` mục 6.4–6.8. Khi sửa, sửa file này trước rồi cập nhật PLAN.md.

## Chuẩn thống kê mặc định (có thể override theo giảng viên)

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

## Quy tắc làm sạch dữ liệu (mặc định)

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

> Không bao giờ: sửa giá trị trả lời, thêm phiếu, hay loại phiếu vì lý do "để đạt". Xem `service-scope.md`.

## QA checklist (trước khi bàn giao)

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

## Khi nào Claude Code phải dừng và hỏi

1. Yêu cầu chạm vào `service-scope.md` (N1–N5): **dừng và từ chối**, đề xuất phương án hợp lệ.
2. Kết quả không đạt ngưỡng (alpha, KMO, fit…): báo chẩn đoán và các phương án, **không tự loại biến hàng loạt**.
3. Yêu cầu nằm ngoài gói đã mua: báo "ngoài phạm vi" và gợi ý báo giá thêm.
4. Thông tin mâu thuẫn (mô hình trong đề cương khác bảng hỏi…).
5. Trước mỗi checkpoint khách (sau bước 2, 4, 5).

## Công nghệ phân tích

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
