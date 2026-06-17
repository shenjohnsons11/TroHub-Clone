# TroHub Web - Hệ Thống Quản Lý Phòng Trọ

## Giới thiệu
TroHub là hệ thống quản lý phòng trọ full-stack, gồm:
- **Backend API**: Node.js + Express + MongoDB
- **Frontend Web Admin**: HTML + Vanilla JS (Vite)
- **Mobile App**: React Native (Expo Router, TypeScript) cho Người Thuê & Chủ Trọ

---

## Cấu trúc dự án

```text
trohub-web-only/                 <-- THƯ MỤC GỐC CHỨA TẤT CẢ
│
├── API_DuAnTotNghiep/           <-- 1. BACKEND API & DATABASE
│   ├── src/
│   │   ├── configs/             # Code kết nối Database (MongoDB)
│   │   ├── controllers/         # Logic xử lý API
│   │   ├── models/              # Schema định nghĩa cấu trúc Database
│   │   └── routes/              # Các đường dẫn API (endpoints)
│   ├── server.js                # Entry point Backend API
│   └── package.json
│
├── src/                         <-- 2. WEB ADMIN (Dành cho Chủ trọ)
│   ├── api.js                   # Code gọi API Backend
│   ├── app.js                   # Code giao diện màn hình Admin chính
│   ├── styles.css               # File CSS giao diện
│   └── (index.html ở ngoài)     # Trang chủ của Web Admin
│
└── TroHub_repo/                 <-- 3. MOBILE APP (Chủ trọ & Người thuê)
    ├── app/                     # File điều hướng màn hình (Expo Router)
    ├── components/              # Các UI Component dùng chung
    ├── screens/                 # Giao diện của App (Login, Hợp đồng, Hóa đơn...)
    ├── services/                # Tương tác API với Backend
    ├── types/                   # Định nghĩa kiểu dữ liệu (TypeScript)
    └── package.json             # Cấu hình dự án Expo
```

---

## Cách chạy dự án (Dành cho thành viên nhóm)

🌟 **DỰ ÁN ĐÃ KẾT NỐI SẴN CLOUD API**
Toàn bộ source code đã được cấu hình trỏ trực tiếp đến máy chủ Render (`https://api-phong-tro.onrender.com/api`).
Bạn **KHÔNG CẦN** phải chạy Database hay chạy Backend API ở máy tính cá nhân. Chỉ cần chạy giao diện Frontend/Mobile là có sẵn dữ liệu chung của cả team!

### CÁCH 1: CHẠY BẰNG DOCKER (NHANH NHẤT 🚀)
Chỉ cần bạn có cài sẵn Docker trên máy, hãy gõ 1 dòng lệnh duy nhất này ở thư mục gốc:
```bash
docker-compose up --build
```
Hệ thống sẽ tự động cài đặt mọi thứ và chạy lên:
- Web Admin: [http://localhost:5173](http://localhost:5173)
- Mobile App: [http://localhost:8081](http://localhost:8081)

---

### CÁCH 2: CHẠY THỦ CÔNG (Nếu không có Docker)

**1. Khởi động Frontend (Web Admin)**
```bash
# Từ thư mục gốc trohub-web-only/
npm run dev
# Web Admin chạy tại: http://localhost:5173
```

**2. Khởi động Mobile App (Expo)**
```bash
# Từ thư mục gốc, di chuyển vào thư mục app
cd TroHub_repo
npm install
npm run android # Mở máy ảo Android
npm run ios     # Mở máy ảo iOS
npm run web     # Mở giao diện trên trình duyệt
# Mobile App chạy tại: http://localhost:8081
```

*(Lưu ý: Nếu bạn muốn test API cục bộ để tự code thêm chức năng backend, hãy tham khảo folder `API_DuAnTotNghiep/README.md`)*



---

## Tài khoản mẫu

| Vai trò | Tên đăng nhập | Mật khẩu |
|---------|--------------|---------|
| Chủ trọ (Admin) | admin@trohub.vn | 123456 |
| Người thuê | tenant@trohub.vn | 123456 |

---

## API Endpoints

### 🔑 Xác thực
| Method | Endpoint | Mô tả |
|--------|---------|-------|
| POST | `/api/auth/register` | Đăng ký tài khoản |
| POST | `/api/auth/login` | Đăng nhập |

### 🏠 Phòng trọ
| Method | Endpoint | Mô tả |
|--------|---------|-------|
| GET | `/api/rooms` | Danh sách phòng |
| POST | `/api/rooms` | Tạo phòng mới |
| PUT | `/api/rooms/:id` | Cập nhật phòng |
| DELETE | `/api/rooms/:id` | Xóa phòng |

### 👥 Khách thuê
| Method | Endpoint | Mô tả |
|--------|---------|-------|
| GET | `/api/tenants` | Danh sách khách thuê |
| POST | `/api/tenants` | Thêm khách thuê (tạo TK + HĐ tự động) |
| PUT | `/api/tenants/:id` | Cập nhật thông tin |
| PUT | `/api/tenants/:id/terminate` | Ngừng thuê |

### 📋 Hợp đồng
| Method | Endpoint | Mô tả |
|--------|---------|-------|
| GET | `/api/contracts` | Danh sách hợp đồng |
| POST | `/api/contracts` | Tạo hợp đồng (Admin mời ký) |
| PUT | `/api/contracts/:id` | Cập nhật hợp đồng |
| PUT | `/api/contracts/:id/sign` | Ký hợp đồng (Admin xác nhận) |

### 💰 Hóa đơn
| Method | Endpoint | Mô tả |
|--------|---------|-------|
| GET | `/api/invoices` | Danh sách hóa đơn |
| POST | `/api/invoices` | Tạo hóa đơn |
| PUT | `/api/invoices/:id/pay` | Đánh dấu đã thanh toán |

### 💳 Lịch sử thanh toán
| Method | Endpoint | Mô tả |
|--------|---------|-------|
| GET | `/api/payments` | Lịch sử giao dịch (Transaction) |

### 🔧 Sửa chữa
| Method | Endpoint | Mô tả |
|--------|---------|-------|
| GET | `/api/repairs` | Danh sách yêu cầu sửa chữa |
| POST | `/api/repairs` | Tạo yêu cầu (kèm tenantId) |
| PUT | `/api/repairs/:id` | Cập nhật trạng thái / độ ưu tiên |

### 👤 Portal Người thuê (yêu cầu JWT)
| Method | Endpoint | Mô tả |
|--------|---------|-------|
| GET | `/api/me` | Lấy toàn bộ dữ liệu của người thuê |
| PUT | `/api/me/sign-contract/:contractId` | Ký hợp đồng |
| PUT | `/api/me/pay-invoice/:invoiceId` | Thanh toán hóa đơn |
| POST | `/api/me/repairs` | Gửi yêu cầu sửa chữa |

### ⚙️ Cài đặt
| Method | Endpoint | Mô tả |
|--------|---------|-------|
| GET | `/api/settings` | Thông tin chủ trọ |
| PUT | `/api/settings` | Cập nhật thông tin chủ trọ |

---

## Luồng dữ liệu chính

### Luồng hợp đồng
```
1. Người thuê đăng ký tài khoản → POST /api/auth/register (role=2)
2. Chủ trọ thêm khách thuê → POST /api/tenants (tạo HĐ tự động status=1)
   HOẶC
   Chủ trọ tạo HĐ mời ký → POST /api/contracts (status=0)
3. Người thuê nhận thông báo HĐ → GET /api/me → contracts[].status=0
4. Người thuê ký HĐ → PUT /api/me/sign-contract/:id → HĐ status=1
5. Chủ trọ thấy HĐ hiệu lực → GET /api/contracts → status=1
```

### Luồng thanh toán → Lịch sử doanh thu
```
1. Chủ trọ tạo hóa đơn → POST /api/invoices
2. Chủ trọ đánh dấu đã TT → PUT /api/invoices/:id/pay
   → Invoice.status = 1 (Đã thanh toán)
   → Transaction mới được tạo (ghi vào collection Transaction)
3. Lịch sử thanh toán reload → GET /api/payments
   → Đọc từ collection Transaction + populate Invoice/Room/Tenant
4. Biểu đồ doanh thu cập nhật dựa trên payments đã thanh toán
```

### Luồng sửa chữa
```
1. Người thuê đăng nhập → GET /api/me (lấy portal data)
2. Người thuê gửi yêu cầu → POST /api/me/repairs
   → Tự động tìm contract hiệu lực của tenant
   → Tạo RepairRequest gắn contractId
3. Chủ trọ thấy yêu cầu → GET /api/repairs (populate room + sender)
4. Chủ trọ cập nhật → PUT /api/repairs/:id {status, priority, note}
5. Người thuê thấy cập nhật → GET /api/me → repairs[]
```

---

## 🌟 Phiên bản Ổn định (Stable Release - Cập nhật 13/06/2026)

**LƯU Ý QUAN TRỌNG:** Đây là phiên bản **Gần như Đầy đủ Chức năng (Near-Full Features)** có thể sử dụng được thực tế trên cả Web Admin và Mobile App. 
Tất cả các luồng nghiệp vụ cốt lõi từ việc Đăng ký, Đăng nhập (có mã hóa bcrypt), Quản lý phòng, Tạo và Ký hợp đồng, Quản lý Hóa đơn và Xử lý sự cố đều đã được hoàn thiện và đồng bộ hóa qua duy nhất 1 Backend API.

### Hướng dẫn sử dụng cốt lõi:
1. **Dành cho Chủ Trọ (Web Admin):**
   - Đăng nhập bằng tài khoản `admin@trohub.vn`.
   - Tạo phòng mới, mời người thuê ký hợp đồng trực tiếp trên giao diện web.
   - Quản lý hóa đơn hàng tháng, nhận yêu cầu sửa chữa và theo dõi doanh thu.
2. **Dành cho Người Thuê (Mobile App / Web App):**
   - Đăng ký tài khoản trên ứng dụng. Hệ thống mã hóa bảo mật mật khẩu.
   - Đăng nhập và xác nhận Hợp đồng từ chủ trọ.
   - Nhận hóa đơn hàng tháng, lấy mã QR thanh toán và xác nhận đã thanh toán.
   - Gửi sự cố sửa chữa kèm hình ảnh để chủ trọ xử lý.

---

## Thay đổi trong các phiên bản trước (cập nhật 07/06/2026)

### Backend (API)
- ✅ **Thêm `/api/me` endpoint** — Portal người thuê: lấy phòng, HĐ, hóa đơn, thanh toán, sửa chữa, stats
- ✅ **Thêm `/api/me/sign-contract/:id`** — Người thuê ký HĐ qua token JWT
- ✅ **Thêm `/api/me/pay-invoice/:id`** — Người thuê thanh toán hóa đơn
- ✅ **Thêm `/api/me/repairs`** — Người thuê gửi yêu cầu sửa chữa (tự tìm contract từ token)
- ✅ **Thêm `/api/payments`** — Lịch sử giao dịch từ collection Transaction
- ✅ **Thêm `PUT /api/contracts/:id`** — Cập nhật hợp đồng (Admin)
- ✅ **Sửa `GET /api/repairs`** — Populate đúng tên phòng và tên người gửi từ contract
- ✅ **Sửa `PUT /api/repairs/:id`** — Nhận đúng status/priority dạng string → number
- ✅ **Thêm `DELETE /api/rooms/:id`** — Xóa phòng (từ phiên bản trước)
- ✅ **Thêm `/api/settings`** — Cài đặt thông tin chủ trọ (từ phiên bản trước)

### Frontend (Web)
- ✅ **Sửa đăng nhập người thuê** — Nhận `role=2` từ JWT, chuyển sang giao diện tenant
- ✅ **Thanh tìm kiếm hoạt động** — Tìm kiếm toàn hệ thống (phòng, khách, hóa đơn)
- ✅ **Nút "Mời ký hợp đồng"** — Tạo hợp đồng status=0 thực sự, người thuê nhận thông báo
- ✅ **Đánh dấu đã thanh toán** — Tự động reload lịch sử thanh toán và biểu đồ doanh thu
- ✅ **Yêu cầu sửa chữa** — Người thuê gửi, Admin thấy + cập nhật, cả 2 role đều thấy
- ✅ **Nút "Hoàn thành sửa chữa"** — Admin click một nút để đánh dấu xong
- ✅ **Portal người thuê** — Xem hợp đồng, hóa đơn, thanh toán, thống kê chi phí
- ✅ **Đăng ký tài khoản** — Tab đăng ký trên màn hình login

---

## Database Schema (MongoDB)

| Collection | Mô tả |
|-----------|-------|
| `accounts` | Tài khoản người dùng (role 1=Chủ trọ, 2=Người thuê) |
| `rooms` | Thông tin phòng trọ |
| `contracts` | Hợp đồng thuê phòng |
| `invoices` | Hóa đơn hàng tháng |
| `transactions` | Lịch sử giao dịch thanh toán |
| `repairrequests` | Yêu cầu sửa chữa |
| `services` | Dịch vụ (điện, nước, wifi...) |

---

## Công nghệ sử dụng

**Backend:**
- Node.js + Express.js
- MongoDB + Mongoose
- JWT (jsonwebtoken)
- bcryptjs
- nodemon (dev)

**Frontend:**
- Vite (build tool)
- Vanilla JavaScript (ES Modules)
- CSS thuần túy (Dark mode)
- VietQR API (QR thanh toán ngân hàng)
