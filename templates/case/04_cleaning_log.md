# Cleaning Log: AL-YYMM-NNN

> Bước 4. **Checkpoint với khách:** khách đồng ý số phiếu cuối cùng trước khi phân tích. Khách có thể đưa file này vào phụ lục.
> Quy tắc mặc định: `docs/analysis-standards.md`. Không bao giờ sửa giá trị trả lời; `data/raw/` không bị đụng tới.

## 1. Thông tin file

| | |
|---|---|
| File gốc | `data/raw/...` |
| Số phiếu gốc | |
| Số biến gốc | |
| File sạch | `data/clean/clean.sav`, `data/clean/clean.xlsx` |

## 2. Các bước làm sạch

| # | Quy tắc | Tiêu chí | Số phiếu bị ảnh hưởng | Xử lý | Còn lại |
|---|---|---|---|---|---|
| 1 | Phiếu trùng | Trùng toàn bộ câu trả lời / timestamp | | Loại bản sau | |
| 2 | Không đúng đối tượng | Câu lọc … | | Loại | |
| 3 | Sai câu kiểm tra chú ý | Câu … phải chọn … | | Loại | |
| 4 | Straight-lining | Cùng 1 đáp án ≥ 90% câu Likert | | Đề xuất loại, **chờ duyệt** | |
| 5 | Làm quá nhanh | < 1/3 trung vị thời gian | | Đề xuất loại | |
| 6 | Missing | ≥ 20% câu trong phiếu | | Đề xuất loại | |
| 7 | Outlier đa biến | Mahalanobis p < 0.001 | | Đánh dấu, **không tự loại** | |

**Số phiếu cuối cùng: N = …**

## 3. Mã hóa biến

| Biến gốc | Tên mới | Nhãn biến | Nhãn giá trị | Ghi chú |
|---|---|---|---|---|

## 4. Câu đảo chiều

| Biến | Công thức | Biến mới |
|---|---|---|
| | `(max + 1) − x` | `..._r` (giữ biến gốc) |

## 5. Ghi chú khác
