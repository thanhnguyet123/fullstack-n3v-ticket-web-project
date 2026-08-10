N3V Ticket — Nền tảng bán vé sự kiện trực tuyến
Hệ thống bán vé sự kiện trực tuyến fullstack, hỗ trợ nhiều loại sơ đồ bố trí chỗ ngồi (sơ đồ ghế, khu vực, phòng trà), quản trị sự kiện, đặt vé và thanh toán. Dự án đồ án nhóm 4 người, xây dựng theo mô hình client–server tách biệt Backend (Spring Boot) và Frontend (React/TypeScript).
📌 Giới thiệu
N3V Ticket mô phỏng một nền tảng bán vé thực tế (kiểu Ticketbox/Eventbrite), cho phép:
Ban quản trị tạo, quản lý sự kiện, danh mục, khu vực chỗ ngồi.
Người dùng tìm kiếm, lọc sự kiện, chọn chỗ ngồi trực quan trên sơ đồ, đặt vé và thanh toán.
Hệ thống xác thực, phân quyền và quản lý đơn hàng theo thời gian thực.
🔗 Demo
Link: https://n3v-ticket.vercel.app/
Tài khoản Admin:
Email: `admin@n3v.com`
Password: `admin@123`
⚙️ Công nghệ sử dụng
Backend
Java 21, Spring Boot (Web, Data JPA, Security)
PostgreSQL (Supabase) — quản lý schema bằng Flyway Migration
JWT Authentication, Spring Security
JPA Specification (lọc động), Hibernate Validation
Frontend
React + TypeScript
Tích hợp API thực (đã thay thế toàn bộ mock data)
🧩 Kiến trúc & Module chính
Dự án được chia thành các module do từng thành viên phụ trách:
Module	Mô tả
Auth	Đăng ký, đăng nhập, phân quyền, JWT
Event Management	Quản lý & hiển thị sự kiện (phụ trách bởi Lê Phạm Thanh Nguyệt)
Booking/Payment	Đặt vé, xử lý thanh toán
Dashboard/Reports	Thống kê, báo cáo quản trị
Module Event Management (chi tiết)
Thiết kế database: Category, Event, EventZone, EventSeat.
Hỗ trợ 3 loại sơ đồ bố trí vé: Seat Map, Zone, Tea Lounge.
Bulk seat generation — sinh hàng loạt ghế theo cấu hình khu vực.
State machine quản lý vòng đời trạng thái sự kiện (EventStatus).
Bộ lọc sự kiện đa tiêu chí bằng JPA Specification.
Trang quản trị CRUD sự kiện, upload hình ảnh, giao diện chọn sơ đồ ghế trực quan.
Xử lý bảo mật: kiểm soát phân quyền, xác thực API theo endpoint.
🚀 Cài đặt & chạy dự án
Yêu cầu
Java 21+, Maven (dùng kèm mvnw)
Node.js 18+ (cho frontend)
PostgreSQL (local hoặc Supabase)
1. Clone dự án
```bash
git clone https://github.com/<your-username>/fullstack-n3v-ticket-web-project.git
cd fullstack-n3v-ticket-web-project
```
2. Cấu hình Backend
Mở `backend/src/main/resources/application-local.properties` và cập nhật:
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/n3vticket
spring.datasource.username=postgres
spring.datasource.password=your\_password
jwt.secret=your\_jwt\_secret\_min\_32\_chars
```
Nếu dùng Supabase, lấy JDBC connection string tại Project Settings → Database:
```properties
spring.datasource.url=jdbc:postgresql://<host>.pooler.supabase.com:6543/postgres?sslmode=require
spring.datasource.username=postgres.xxxxxxxxxxxxxxxxxxxx
spring.datasource.password=your\_database\_password
```
Chạy backend:
```bash
cd backend
./mvnw spring-boot:run        # macOS/Linux
.\\mvnw.cmd spring-boot:run     # Windows PowerShell
```
Nếu database báo thiếu bảng/cột (`roles`, `role\_id`, ...), chạy file `backend/fix\_auth\_schema.sql` trong Supabase SQL Editor hoặc DBeaver.
3. Chạy Frontend
```bash
cd frontend
npm install
npm run dev
```
🔑 API mẫu
Đăng ký
```http
POST /api/auth/register
Content-Type: application/json

{
  "fullName": "Admin Test",
  "email": "admin@test.com",
  "phone": "0900000001",
  "password": "Admin@123"
}
```
Đăng nhập
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "admin@test.com",
  "password": "Admin@123"
}
```
Lấy thông tin cá nhân
```http
GET /api/users/profile
Authorization: Bearer <accessToken>
```
Danh sách sự kiện (module Event Management)
```http
GET /api/events?categoryId=1\&status=PUBLISHED\&keyword=concert
```
👥 Thành viên nhóm
Thành viên	Module phụ trách
Vũ	Authentication & Authorization
Lê Phạm Thanh Nguyệt	Event Management (Quản lý & Hiển thị sự kiện)
Nhung	Booking & Payment
Nguyên	Dashboard & Reports
📄 Giấy phép
Dự án phục vụ mục đích học tập, thực hiện trong khuôn khổ đồ án môn học.
