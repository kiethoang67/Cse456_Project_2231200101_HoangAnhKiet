# Study Group Project (K2L StudyGroup)

Đây là ứng dụng hỗ trợ học tập nhóm (Study Group) với đầy đủ Backend và Frontend. Dự án được cấu trúc chia thành hai phần riêng rệt và có khả năng triển khai linh hoạt bằng dịch vụ Docker, Render, và Vercel.

## 🚀 Các tính năng chính (Dự kiến)
* **Quản lý nhóm học tập:** Hỗ trợ tạo, tham gia và quản lý các Study Group, phân quyền thành viên.
* **Hỗ trợ thời gian thực (Real-time):** Tính năng tương tác, trò chuyện gửi thông báo trực tiếp nhờ Websocket.
* **Xác thực bảo mật thông tin:** Hỗ trợ tính năng đăng nhập, phân quyền truy cập thông qua JWT và hệ thống OAuth2.
* **Lưu trữ chuyên dụng trên Cloud:** Sử dụng hệ thống lưu trữ đối tượng AWS S3 cho việc đính kèm các tài liệu, hình ảnh.
* **Email thông báo:** Tích hợp với Mailjet SMS/Email API chuyên nghiệp.

## 💻 Công nghệ và Kiến trúc

### 🔙 Backend (Spring Boot)
* **Ngôn ngữ Base:** Java 21
* **Framework:** Spring Boot (Mới nhất: v3.5.x)
* **Database (Hybird):** PostgreSQL (Dữ liệu giao dịch, quan hệ) & MongoDB (Dữ liệu thay đổi nhanh, documents)
* **Security Layer:** Spring Security, OAuth2 Client, JJWT
* **Cloud & External APIs:** Amazon AWS S3 SDK (File Storage), Brevo/Mailjet API (Email)
* **Khác:** Spring Websocket, SpringDoc OpenAPI (Swagger UI), Lombok, Actuator.

### 🎨 Frontend (React + Vite)
* **Core:** React.js, TypeScript (Strict-typed)
* **Công cụ Tối ưu hóa / Build:** Vite, PostCSS
* **Giao diện & UI Framework:** Tailwind CSS
* **Code Standard:** ESLint

## 📁 Cấu trúc thư mục nền tảng

```text
K2L_StudyGroup/
│
├── StudyGroupProject_V2/
│   ├── Backend/             # Mã nguồn Spring Boot, thư mục Maven
│   ├── Frontend/            # Mã nguồn web UI React (package.json, Vite config)
│   ├── render.yaml          # File script chuẩn bị để deploy lên hosting Render.com
│   └── fix_groupview.ps1    # Script sửa chữa / tự động hóa local
├── Dockerfile               # Tệp lệnh cấu hình Image Docker hai giai đoạn (build và chạy backend)
└── ...
```

## 🛠 Hướng dẫn chạy dự án (Local Development)

### Cách 1: Dùng Docker (Cách Nhanh Nhất)
Dự án đã có sẵn file `Dockerfile` ngay ngoài thư mục ngoài để cấu hình các luồng build từ maven xuống chạy JRE.
```bash
# B1: Đứng tại đúng thư mục K2L_StudyGroup có chứa Dockerfile và build image mới
docker build -t k2l-studygroup .

# B2: Chạy container ở cổng 8081
docker run -p 8081:8081 k2l-studygroup
```

### Cách 2: Setup Môi trường Native

**1. Khởi chạy Backend:**
* Yêu cầu bạn phải có sẵn **Java 21**, **Maven** và database **PostgreSQL/MongoDB** đang chạy ngầm.
* Bước vào folder `Backend` cài đặt và khởi động:
```bash
cd StudyGroupProject_V2/Backend
mvn clean install -DskipTests
mvn spring-boot:run
```

**2. Khởi chạy Frontend:**
* Yêu cầu bạn phải cài đặt **Node.js** phiên bản v18+.
* Mở terminal thứ 2 và đi vào folder Frontend:
```bash
cd StudyGroupProject_V2/Frontend
npm install
npm run dev
```
Trang web mặc định sẽ được chạy tải ở địa chỉ: `http://localhost:5173`.

## 🌐 Triển khai Online (Production)
* **Phía Backend:** Ứng dụng tích hợp sẵn luồng CI/CD nhỏ với tập tin cấu hình `render.yaml` - rất thích hợp để host lên các hệ thống PaaS như **Render**.
* **Phía Frontend:** Có sẵn file file config `vercel.json` phục vụ cho việc deploy cực kỳ đơn giản lên host **Vercel** - Môi trường số 1 cho framework frontend.
