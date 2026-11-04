# Hướng dẫn tự chạy lại kết quả trên SPSS

**Mã hồ sơ:** AL-YYMM-NNN

Bạn làm theo các bước dưới đây để ra đúng các bảng trong báo cáo. Nhờ vậy bạn hiểu mình đã chạy gì và trả lời được khi giảng viên hỏi.

## Chuẩn bị

1. Mở SPSS → **File → Open → Data** → chọn file `….sav`.
2. Mở file syntax: **File → Open → Syntax** → chọn file `….sps`.

## Cách 1: chạy toàn bộ bằng syntax (nhanh nhất)

1. Trong cửa sổ Syntax, bấm **Ctrl + A** để chọn hết.
2. Bấm nút ▶ (**Run Selection**).
3. Kết quả hiện trong cửa sổ **Output**, theo đúng thứ tự trong báo cáo.

## Cách 2: chạy từng phân tích bằng menu

| Phân tích | Đường dẫn trong SPSS | Lưu ý |
|---|---|---|
| Thống kê mô tả | Analyze → Descriptive Statistics → Frequencies | |
| Cronbach's Alpha | Analyze → Scale → Reliability Analysis | Statistics → tick "Scale if item deleted" |
| EFA | Analyze → Dimension Reduction → Factor | Extraction: …; Rotation: …; Options: ẩn hệ số < 0.3 |
| Tạo biến đại diện | Transform → Compute Variable | `MEAN(…)` |
| Pearson | Analyze → Correlate → Bivariate | |
| Hồi quy | Analyze → Regression → Linear | Statistics → tick Collinearity diagnostics, Durbin-Watson |
| T-test | Analyze → Compare Means → Independent-Samples T Test | |
| ANOVA | Analyze → Compare Means → One-Way ANOVA | Options → Homogeneity, Welch; Post Hoc → Tukey / Games-Howell |

## Nếu kết quả không khớp

- Kiểm tra đã mở đúng file `.sav` đi kèm chưa (không dùng file cũ).
- Kiểm tra các biến đảo chiều (tên có đuôi `_r`).
- Vẫn lệch thì chụp màn hình gửi Zalo, mình xem giúp.
