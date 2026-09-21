# BTL_TKWeb
## I. MÔ TẢ CHUNG VỀ DỰ ÁN (PROJECT OVERVIEW)

### 1. Bối cảnh & Lý do ra đời
Trong đời sống sinh viên, chi phí ăn uống luôn chiếm tỷ trọng lớn nhất trong ngân sách hàng tháng. Tuy nhiên, phần lớn sinh viên thường gặp phải các vấn đề:
- Chi tiêu cảm tính: Ăn uống tự do vào đầu tháng, chọn các món đắt đỏ hoặc đặt app không kiểm soát dẫn đến tình trạng "vỡ quỹ" và "cháy túi" vào cuối tháng.
- Rào cản phí giao hàng (Phí ship)* Phí ship đơn lẻ cao khiến chi phí một bữa ăn bị đội lên đáng kể.
- Khó khăn khi đặt chung nhóm: Việc gom đơn đặt cơm/trà sữa chung phòng trọ hay nhóm học bài để chia ship thường gây rắc rối khi phải tính toán tiền món lẻ, mã giảm giá và phí ship thủ công cho từng người.

### 2. Sứ mệnh & Giải pháp của FINFood
FINFood là nền tảng Web Front-End được thiết kế riêng cho sinh viên Học viện Ngân hàng và giới trẻ. Dự án kết hợp độc đáo giữa Trực quan hóa Thực đơn F&B và Công cụ Quản lý Tài chính Cá nhân, giúp sinh viên:
1. Duy trì thói quen chi tiêu kỷ luật: Tự động tính toán hạn mức tiền ăn mỗi ngày dựa trên số dư thực tế.
2. Gợi ý món ăn thông minh: Tự động đề xuất các món ăn ngon - bổ - rẻ nằm đúng trong tầm giá sinh viên được phép chi tiêu.
3. Tối ưu chi phí nhóm: Cung cấp công cụ tính chia tiền bill và phí ship đơn nhóm nhanh chóng, chính xác đến từng đồng.

> **Ghi chú:** Dự án là Bài tập lớn thuộc học phần **Thiết kế Web (IS19A)** - Học viện Ngân hàng. Toàn bộ dữ liệu món ăn, ngân sách và trạng thái đơn hàng là dữ liệu mô phỏng Front-End phục vụ học tập.
## II. DANH SÁCH CHI TIẾT CÁC CHỨC NĂNG (FEATURE LIST)

### 1. Khung Giao Diện & Điều Hướng Chung (Global UI & Navigation)
- **Hệ thống điều hướng Semantic:** Thanh Header/Footer đồng nhất trên toàn bộ 06 trang, có nhận diện trang hiện tại (`aria-current="page"`).
- **Thiết kế Đáp ứng (Responsive Design):** Hiển thị tối ưu và mượt mà trên 03 thiết bị: Desktop (1200px+), Tablet (768px+) và Mobile (360px+) bằng Bootstrap 4 Grid.

### 2. Trang Chủ (`index.html`)
- **Hero Banner Khuyến Mãi:** Trình bày thông điệp thương hiệu và lối tắt dẫn ngay tới công cụ tính tiền ăn.
- **Khối Món HOT Bán Chạy (Flash Sale):** Hiển thị danh sách các món ăn bán chạy nhất tuần dạng Card trực quan.
- **Bảng So Sánh Chi Phí:** Bảng dữ liệu HTML so sánh khả năng tiết kiệm chi phí giữa việc đặt app tự do và dùng FINSTART Food.

### 3. Trang Thực Đơn & Lọc Món Thông Minh (`pages/products.html`)
- **Nạp Dữ Liệu Động (AJAX/Fetch):** Tải danh sách thực đơn từ file dữ liệu `products.json` mà không cần reload trang.
- **Tìm Kiếm Realtime:** Tìm kiếm món ăn theo tên không phân biệt chữ hoa/chữ thường.
- **Bộ Lọc Đa Tiêu Chí:** Lọc món theo danh mục (Cơm sinh viên, Bún/Phở, Trà sữa/Đồ uống, Combo tiết kiệm) và khoảng giá.
- **Sắp Xếp Giá:** Sắp xếp danh sách món ăn theo giá tăng dần hoặc giảm dần.
- **Tích Hợp Gợi Ý Theo Ngân Sách (US01):** Tự động nhận hạn mức tiền ăn từ `localStorage` để lọc ra danh sách các món ăn có giá $\le$ hạn mức.

### 4. Trang Chi Tiết Món Ăn (`pages/product-detail.html`)
- **Trình Bày Món Ăn Chi Tiết:** Hiển thị hình ảnh chất lượng cao, giá tiền và mô tả thành phần món ăn.
- **Tùy Chọn Topping & Số Lượng:** Cho phép người dùng chọn thêm Topping (trứng ốp, thêm sườn...) và điều chỉnh số lượng suất ăn.
- **Bảng Giá Trị Dinh Dưỡng:** Bảng thống kê chi tiết hàm lượng Calories, Protein, Carbs của từng suất ăn.

### 5. Trang Quản Lý Ngân Sách & Chia Ship (`pages/calculator.html`)
- **Tab 1 - Tính Hạn Mức Tiền Ăn Cá Nhân:** 
  - Nhập tổng tiền ăn còn lại + số ngày còn lại + số bữa/ngày.
  - Tính toán hạn mức tối đa cho từng bữa ăn và hiển thị thanh Progress Bar % quỹ tiền còn lại.
  - Lưu hạn mức vào `localStorage` và cung cấp nút "Gợi ý thực đơn hôm nay" chuyển trực tiếp qua trang Thực đơn.
- **Tab 2 - Công Cụ Chia Tiền Bill Nhóm (Split Ship - US06):**
  - Nhập tổng tiền món lẻ từng người + phí ship chung + tiền voucher giảm giá.
  - Tự động chia chính xác số tiền lẻ mà mỗi bạn trong nhóm phải trả.

### 6. Trang Đặt Hàng & Thanh Toán (`pages/contact.html`)
- **Biểu Mẫu Đặt Hàng Chuẩn Form:** Nhập thông tin khách hàng, số điện thoại, địa chỉ giao hàng và ghi chú cho quán.
- **Bắt Lỗi Form Realtime (Validation):** Kiểm tra bắt buộc nhập, kiểm tra định dạng Số điện thoại và Email, hiển thị thông báo lỗi ngay cạnh ô nhập liệu.
- **Cảnh Báo Vượt Quỹ (US05):** Kiểm tra tổng tiền đơn hàng với hạn mức trong `localStorage`; hiển thị cảnh báo đỏ nếu người dùng chọn món vượt ngân sách.
- **Trừ Quỹ Tự Động:** Tự động trừ số tiền vừa mua vào tổng quỹ ăn còn lại trong `localStorage` ngay khi đặt hàng thành công.
- **Modal Thanh Toán Mã QR (US07):** Tự động bật Modal hiện mã QR VietQR / Ví MoMo tĩnh khi chọn phương thức thanh toán online.
- **Mô Phỏng Trạng Thái Đơn Hàng (Timeline UI - US08):** Thanh tiến trình 4 bước (Chờ xác nhận $\rightarrow$ Đang nấu $\rightarrow$ Đang giao $\rightarrow$ Đã giao) tự động chuyển màu để mô phỏng đơn hàng realtime.

### 7. Trang Giới Thiệu & Hồ Sơ Nhóm (`pages/about.html`)
- **Nghiên Cứu Người Dùng:** Trình bày chi tiết 03 Persona (An - Quản lý quỹ, Bình - Tìm quán rẻ, Cường - Gom đơn chia ship) và 08 User Story.
- **Thẻ Thông Tin Nhóm (Team Cards):** Hiển thị thông tin 5 thành viên, phân công vai trò kỹ thuật và liên kết đến file nhật ký `AI_USAGE.md`.

---

## III. DANH SÁCH THÀNH VIÊN & PHÂN CÔNG TỔ CHỨC

| STT | Họ và Tên | Mã Sinh Viên | Vai trò | Phụ trách kỹ thuật chính |
| :---: | :--- | :---: | :--- | :--- |
| 1 | Trịnh Quốc Đại | 27A4043282 | Product Owner / Lead | Quản lý Git, Deploy, Trang chủ (`index.html`), Design System (`main.css`) |
| 2 | Đoàn Thị Minh Ánh | 27A4043271 | Dev Thực đơn & Data | Trang Thực đơn (`products.html`), Chi tiết món (`product-detail.html`), `products.json`, `main.js` |
| 3 | Nguyễn Thị Thảo Ly | 27A4043313 | Dev Đặt hàng & Form | Trang Đặt hàng (`contact.html`), Form Validation, Modal Mã QR (`validation.js`) |
| 4 | Nguyễn Thị Kim Huệ | 27A4043296 | Dev Logic Chi Tiêu | Trang Tính ngân sách & Chia ship (`calculator.html`), `localStorage` (`calculator.js`) |
| 5 | Nguyễn Quốc Khánh | 27A4043304 | UI/UX & Quality Control | Trang Giới thiệu (`about.html`), Wireframe, Báo cáo PDF, `AI_USAGE.md` |

---

## IV. CÔNG NGHỆ SỬ DỤNG (TECH STACK)

- **Front-End Core:** HTML5 Semantic, CSS3 (Flexbox/CSS Grid), JavaScript (ES6+).
- **Framework & Thư viện:** Bootstrap 4, jQuery.
- **Xử lý dữ liệu & Lưu trữ:** AJAX/Fetch API, JSON, Browser `localStorage`.
- **Công cụ quản lý & Triển khai:** Git, GitHub, VS Code, Live Server.