# Cây chọn kiểm định

> Dùng ở bước 2 (Research Design) để viết `02_analysis_plan.md`. Yêu cầu của giảng viên (`lecturer_requirements` trong `case.yaml`) luôn được ưu tiên hơn cây này. Ngưỡng cụ thể xem `analysis-standards.md`.

## Bước 0: Xác định mục tiêu của câu hỏi nghiên cứu

| Mục tiêu | Ví dụ câu hỏi | Nhánh |
|---|---|---|
| **Đo lường** (thang đo có tin cậy, có hội tụ không?) | "Thang đo Niềm tin có đáng tin cậy không?" | A |
| **Quan hệ / tác động** giữa các biến | "Giá cả ảnh hưởng thế nào đến Ý định mua?" | B |
| **So sánh nhóm** | "Ý định mua có khác nhau giữa nam và nữ?" | C |
| **Mô tả** mẫu | "Đặc điểm nhân khẩu học của mẫu?" | D |

## A. Đo lường

```
Thang đo Likert nhiều item
 ├─ Bước 1: Cronbach's Alpha cho từng nhân tố (loại item có item-total < 0.3, ghi log)
 ├─ Bước 2: EFA
 │    ├─ Chỉ đi tiếp hồi quy        → PCA + Varimax
 │    └─ Sẽ đi tiếp CFA / SEM       → PAF + Promax
 │    EFA chạy riêng cho biến độc lập và biến phụ thuộc (thông lệ ở VN), trừ khi GV yêu cầu khác
 └─ Bước 3 (nếu SEM): CFA → CR, AVE, HTMT → AMOS / SmartPLS
```

## B. Quan hệ / tác động

| Biến phụ thuộc (DV) | Biến độc lập (IV) | Phương pháp |
|---|---|---|
| Định lượng (trung bình Likert, số) | 1 biến định lượng | Pearson (+ hồi quy đơn nếu cần hệ số) |
| Định lượng | Nhiều biến | **Hồi quy tuyến tính bội (OLS)**: kiểm tra VIF, phần dư, Durbin-Watson, phương sai sai số |
| Định lượng | Có biến định danh | Hồi quy với biến giả (dummy) |
| Nhị phân (có/không) | Bất kỳ | **Hồi quy Logistic** (ngoài SOP chuẩn: đề xuất trong Analysis Plan, chờ duyệt) |
| Thứ bậc (1 item, không lấy trung bình) | Bất kỳ | Spearman / hồi quy thứ bậc (chờ duyệt) |
| Có biến trung gian / điều tiết | Mô hình nhiều tầng | **SEM (AMOS)** hoặc **PLS-SEM (SmartPLS)**; điều tiết đơn giản có thể dùng hồi quy có biến tương tác |
| Dữ liệu bảng (panel), DiD, chuỗi thời gian | n/a | Ngoài SOP: đề xuất Stata/Eviews, chờ duyệt |

**Chọn AMOS hay SmartPLS:**

- Mẫu ≥ 200, dữ liệu gần chuẩn, mục tiêu kiểm định lý thuyết → **AMOS (CB-SEM)**.
- Mẫu nhỏ, phân phối lệch, mô hình phức tạp, mục tiêu dự báo → **SmartPLS (PLS-SEM)**.
- GV chỉ định phần mềm nào thì dùng phần mềm đó.

## C. So sánh nhóm

```
Biến phụ thuộc định lượng?
 ├─ Có
 │   ├─ 2 nhóm độc lập (nam/nữ)
 │   │    └─ Independent Samples T-test (đọc Levene: vi phạm → dòng "Equal variances not assumed")
 │   ├─ ≥ 3 nhóm độc lập (thu nhập, năm học)
 │   │    └─ One-way ANOVA
 │   │         ├─ Levene p ≥ 0.05 → F-test, post-hoc Tukey
 │   │         └─ Levene p < 0.05 → Welch, post-hoc Games-Howell
 │   ├─ 2 lần đo trên cùng người (trước/sau) → Paired Samples T-test
 │   └─ Nhóm quá nhỏ (< 30 / nhóm) và lệch nặng → Mann-Whitney U / Kruskal-Wallis
 └─ Không (cả 2 biến định danh) → Chi-square (Crosstabs); ô kỳ vọng < 5 quá 20% → Fisher
```

Nhóm có < 5 quan sát: đề xuất gộp nhóm (ghi log), không chạy post-hoc trên nhóm quá nhỏ.

## D. Mô tả

- Biến định danh / thứ bậc: tần số, tỷ lệ % (Frequencies).
- Biến định lượng, item Likert: Mean, SD, Min, Max (Descriptives).
- Luôn báo N cuối cùng, khớp với Cleaning Log.

## Thứ tự chạy chuẩn cho mô hình hồi quy (dịch vụ 03)

1. Thống kê mô tả mẫu
2. Cronbach's Alpha từng nhân tố
3. EFA (IV riêng, DV riêng)
4. Tạo biến đại diện (trung bình các item còn lại)
5. Tương quan Pearson
6. Hồi quy bội + kiểm tra giả định
7. T-test / ANOVA theo biến nhân khẩu học (nếu có trong plan)
8. Bảng tổng hợp kết quả kiểm định giả thuyết
