# Lab A12 – Quản lý sinh viên (SQLite)

- **Họ và tên:** Bùi Quang Duy
- **MSSV:** 231A290127
- **Package:** `vn.edu.vhu.ltdd.a12sqlite`

## Mô tả các bài nâng cao đã thực hiện

### 1. Bài nâng cao NC1: Lưu tên lớp mặc định bằng `SharedPreferences`
- **Mục tiêu:** Tự động ghi nhớ tên lớp của sinh viên vừa thêm để điền sẵn vào ô nhập `Lớp` trong những lần thêm tiếp theo hoặc khi tắt hẳn ứng dụng rồi mở lại.
- **Cách thực hiện:**
  - Sử dụng `getSharedPreferences("cai_dat", MODE_PRIVATE)` với khóa `lop_mac_dinh` trong `MainActivity`.
  - Khi mở ứng dụng (`onCreate`), đọc tên lớp đã lưu từ `SharedPreferences` và gán vào `edtLop.setText(lopMacDinh)`.
  - Sau mỗi lần thêm sinh viên vào CSDL thành công (`themSinhVien`), lưu lại giá trị `lop` vừa nhập bằng `.edit().putString("lop_mac_dinh", lop).apply()`.

### 2. Bài nâng cao NC2: Thống kê số sinh viên đạt (điểm ≥ 5) và điểm cao nhất (`MAX`)
- **Mục tiêu:** Mở rộng dòng thống kê trên giao diện chính để hiển thị thêm số lượng sinh viên đạt (`diem >= 5`) và điểm số cao nhất trong danh sách bằng hàm tổng hợp SQL.
- **Cách thực hiện:**
  - Trong `SinhVienDao`:
    - Bổ sung phương thức `demSinhVienDat()` thực thi `rawQuery("SELECT COUNT(*) FROM sinh_vien WHERE diem >= 5", null)` và đóng `Cursor` an toàn trong khối `try-finally`.
    - Bổ sung phương thức `diemCaoNhat()` thực thi `rawQuery("SELECT MAX(diem) FROM sinh_vien", null)` và đóng `Cursor` an toàn trong khối `try-finally`.
  - Trong `strings.xml` và `MainActivity`:
    - Cập nhật chuỗi định dạng `thong_ke` và hàm `napDanhSach()` để hiển thị đầy đủ: Tổng số sinh viên, Điểm trung bình, Số sinh viên đạt (≥ 5), và Điểm cao nhất.
