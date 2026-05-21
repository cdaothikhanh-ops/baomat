# Ứng Dụng Quản Lý Đơn Hàng Có Tính Năng Bảo Mật

## 📝 Tổng Quan Dự Án
Trong kỷ nguyên số, dữ liệu thương mại điện tử và thông tin khách hàng luôn là mục tiêu hàng đầu của các cuộc tấn công mạng. Dự án **Ứng dụng quản lý đơn hàng có tính năng bảo mật** được xây dựng nhằm cung cấp giải pháp toàn diện để quản lý quy trình vận hành đơn hàng, đồng thời triển khai các cơ chế phòng thủ chuyên sâu chống lại rủi ro rò rỉ, thao túng hoặc phá hoại dữ liệu.

Hệ thống kết hợp chặt chẽ giữa các giải pháp mã hóa ở tầng ứng dụng và các tính năng bảo mật nâng cao trực tiếp trên hệ quản trị cơ sở dữ liệu **Oracle Database**.

---

## 🛠️ Các Tính Năng Bảo Mật Hệ Thống

### 1. Mã Hóa Dữ Liệu Chuyên Sâu (Application & Data Encryption)
Để bảo vệ thông tin trước các nguy cơ tấn công đánh cắp dữ liệu tĩnh (Data-at-Rest), hệ thống áp dụng linh hoạt các thuật toán mã hóa hiện đại:
* **Mã hóa đối xứng (AES):** Sử dụng thuật toán AES với độ dài khóa an toàn để mã hóa các thông tin cá nhân nhạy cảm của khách hàng như *Địa chỉ (Address)* và *Số điện thoại (Phone Number)* trước khi lưu xuống đĩa cứng.
* **Mã hóa bất đối xứng (RSA) & Mã hóa lai (Hybrid Encryption):** Kết hợp tốc độ của mã hóa đối xứng và sự an toàn trong quản lý khóa của mã hóa bất đối xứng, phục vụ cho các tiến trình truyền tải dữ liệu hoặc xác thực bảo mật cao.
* **Băm dữ liệu bảo mật (Hashing):** Sử dụng các hàm băm một chiều an toàn để băm mật khẩu người dùng (kèm cơ chế Salt). Điều này đảm bảo ngay cả khi quản trị viên hệ thống hoặc kẻ tấn công chiếm được bảng cơ sở dữ liệu cũng không thể khôi phục lại mật khẩu gốc.

### 2. Bảo Mật Mức Cơ Sở DỮ Liệu (Oracle Database Security)
Hệ thống tận dụng tối đa các công nghệ bảo mật mạnh mẽ tích hợp sẵn trong Oracle Database để thiết lập các lớp phòng thủ:
* **Phân quyền và Kiểm soát truy cập (RBAC):** Định nghĩa rõ ràng quyền hạn chi tiết (System/Object Privileges) cho từng nhóm vai trò (Roles) như Nhân viên bán hàng, Quản lý kho, Kế toán, và Khách hàng. Thiết lập `Profile` và `Session` để giới hạn tài nguyên, chống tấn công từ chối dịch vụ (DoS) nội bộ.
* **Chính sách VPD (Virtual Private Database):** Triển khai bảo mật mức dòng (Row-level security). Cơ chế này tự động đính kèm điều kiện `WHERE` vào các truy vấn SQL dựa trên ngữ cảnh người dùng (Application Context), đảm bảo nhân viên vùng nào chỉ thấy đơn hàng vùng đó, khách hàng chỉ thấy đơn hàng của chính mình.
* **Giám sát hệ thống chi tiết (FGA - Fine-Grained Auditing):** Triển khai cơ chế kiểm toán thông minh để theo dõi, ghi nhận lại chính xác hành vi, thời gian và địa chỉ IP của bất kỳ ai cố tình truy cập hoặc chỉnh sửa các vùng dữ liệu nhạy cảm thông qua hệ thống `Audit Log`.
* **Khôi phục dữ liệu nâng cao (Oracle Flashback):** Cấu hình tính năng Flashback cho phép quản trị viên quay ngược thời gian cơ sở dữ liệu về trạng thái trước khi xảy ra lỗi logic hoặc bị tấn công phá hoại, giúp giảm thiểu tối đa thời gian gián đoạn hệ thống (Downtime).

---

## 🏗️ Kiến Trúc Hệ Thống & Công Nghệ Sử Dụng
* **Hệ Quản Trị CSDL:** Oracle Database (Hỗ trợ VPD, FGA, Flashback, Cryptographic Toolkit).
* **Tầng Ứng Dụng:** [Điền ngôn ngữ/framework ví dụ: Java/C#/PHP/Python] tích hợp các thư viện mật mã chuẩn để xử lý mã hóa AES, RSA và Hashing.
* **Mô hình triển khai:** Client-Server / Web-based Application bảo mật qua các phân vùng truy cập được kiểm soát chặt chẽ.

---

## 🧪 Kết Quả Đạt Được & Thực Nghiệm
* **Tính toàn vẹn dữ liệu:** Toàn bộ mật khẩu và thông tin liên lạc được mã hóa hoàn toàn khi kiểm tra trực tiếp bằng lệnh `SELECT` trong SQL*Plus hay Oracle Developer.
* **Tính bảo mật phân quyền:** Kiểm thử đăng nhập giữa tài khoản nhân viên kinh doanh và khách hàng cho thấy dữ liệu được phân tách hoàn hảo, không xảy ra hiện tượng rò rỉ dữ liệu chéo (IDOR).
* **Khả năng truy vết:** Mọi thao tác bất thường trên bảng Đơn hàng (Orders) đều kích hoạt FGA và lưu vết rõ ràng trong bảng log hệ thống, phục vụ công tác điều tra sự cố.

---

## 👥 Thành Viên Thực Hiện (Nhóm 15)
Dự án được hoàn thành bởi các thành viên thuộc Khoa Công nghệ Thông tin - Trường Đại học Công thương TP. HCM, dưới sự hướng dẫn chuyên môn của **GVHD: Đinh Thị Mận**:

1. **Đào Thị Khánh Chi** – *MSSV: 2033230035*
2. **Phạm Nhật Minh** – *MSSV: 2001230513*
3. **Trương Lê Trúc Quỳnh** – *MSSV: 2033230246*
