# Analysis Plan: AL-YYMM-NNN

> Bước 2. **Checkpoint với khách:** khách xác nhận plan này trước khi làm tiếp. Đây là "hợp đồng phương pháp": đổi yêu cầu sau khi đã xác nhận thì tính là phát sinh.
> Chọn kiểm định theo `docs/test-selection.md`; ngưỡng theo `docs/analysis-standards.md`, trừ khi GV yêu cầu khác.

## 1. Mô hình và giả thuyết

| Giả thuyết | Quan hệ | Chiều kỳ vọng |
|---|---|---|
| H1 | | (+) |

## 2. Dữ liệu

- **Nguồn:** khảo sát của khách / data khách gửi / mock data / dữ liệu công bố (ghi rõ nguồn)
- **Cỡ mẫu:** hiện có … / yêu cầu tối thiểu … (công thức: max(5 × số item, 50 + 8 × số IV))
- **Thang đo:** Likert … điểm
- **Câu đảo chiều:**

## 3. Các phân tích sẽ chạy

| # | Phân tích | Mục đích | Tiêu chí đánh giá | Ghi chú |
|---|---|---|---|---|
| 1 | Thống kê mô tả | Mô tả mẫu | n/a | |
| 2 | Cronbach's Alpha | Độ tin cậy thang đo | α ≥ 0.6; item-total ≥ 0.3 | |
| 3 | EFA (IV, DV riêng) | Giá trị hội tụ, phân biệt | KMO ≥ 0.5; Bartlett p < 0.05; Eigen ≥ 1; TVE ≥ 50%; loading ≥ 0.5 | Phép trích / xoay: |
| 4 | Pearson | Tương quan | p < 0.05 | |
| 5 | Hồi quy bội | Kiểm định giả thuyết | F p < 0.05; β p < 0.05; VIF < 10 | Giả định: phần dư, DW, phương sai sai số |
| 6 | T-test / ANOVA | Khác biệt theo nhóm | Levene → F / Welch | Biến nhóm: |

## 4. Yêu cầu riêng của giảng viên

-

## 5. Xử lý khi không đạt ngưỡng (thống nhất trước với khách)

- Alpha < 0.6 hoặc item-total < 0.3: xem câu đảo chiều, mã hóa trước; chỉ loại item theo tiêu chí, tối đa … item / nhân tố, ghi log.
- Item tải chéo / loading thấp: loại từng item một, chạy lại, ghi log.
- Giả thuyết không được ủng hộ: giữ nguyên kết quả, hướng dẫn cách giải thích.

## 6. Bàn giao

- [ ] File dữ liệu (.sav / .xlsx)
- [ ] Syntax SPSS (.sps)
- [ ] Bảng kết quả (.xlsx)
- [ ] Báo cáo kết quả (giải thích từng bảng)
- [ ] (Trọn bộ) Câu hỏi bảo vệ, hướng dẫn tự chạy lại
