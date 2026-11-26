# Báo cáo Day 14 — Lê Đức Tường — 2A202603066

- Mã học viên dùng với `--student`: `066`
- `seed_tag` trong `frames_A.txt`: `AC-_MUFc`

## 1. Dự đoán trước sweep (bước 5b)

Ghi **trước** khi chạy `scripts/pp_sweep.py`, rồi commit và push ngay (lịch sử commit là bằng chứng thời điểm viết). Không sửa phần này sau khi có kết quả.

- Tham số tôi nghĩ giảm công sửa nhiều nhất: Tăng `score_thr` từ `0.1` lên `0.3` (hoặc `0.4`) kết hợp đặt `min_points=5` (hoặc `10`).
- Vì sao (nhìn ảnh BEV tập A: box thừa nhiều hay box sót nhiều?): 
  - Qua đo đạc chi phí công sửa ở cấu hình gốc trên tập A (3 frame), tổng chi phí sửa là **35.2**, mô hình dự đoán tới **98 hộp** nhưng nhãn thực tế sau khi sửa tay chỉ có **33 hộp**.
  - Mô hình KITTI bị nhiễu và dự đoán thừa tới **69 hộp** (chiếm đa số chi phí sửa), trong khi chỉ bỏ sót **4 hộp**. Do đó, việc tăng `score_thr` và lọc bớt các chùm điểm quá thưa (`min_points`) sẽ giúp loại bỏ phần lớn các box nhiễu/nhiễu nền xa, từ đó giảm mạnh chi phí xóa hộp thừa mà ít làm gia tăng số box bị bỏ sót.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | | | | |
| `best_config.json` | | | | |

- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_066/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_066/frames_B.txt --config d14_066/best_config.json --gt d14_066/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...