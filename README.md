# Đấu trường trí nhớ

Website game trí nhớ tiếng Việt, responsive cho điện thoại/máy tính, gồm 6 vòng:
1. Nhận diện hình ảnh
2. Ghi nhớ chuỗi số
3. Ghi nhớ từ ngữ
4. Ghi nhớ chuỗi màu
5. Nhận diện biểu tượng
6. Thử thách tổng hợp

## Chạy thử nhanh
Mở `index.html` trong trình duyệt. Game có thể chơi thử ngay. Khi chưa cấu hình Supabase, kết quả chỉ lưu trên trình duyệt hiện tại (không đồng bộ giữa thiết bị).

## Để có bảng xếp hạng chung giữa 50+ người

### A. Tạo cơ sở dữ liệu Supabase
1. Tạo tài khoản/dự án tại https://supabase.com/
2. Trong dự án, mở **SQL Editor** → **New query**.
3. Sao chép toàn bộ nội dung `supabase-schema.sql`, chạy (Run).
4. Mở **Project Settings → API** (hoặc phần API keys theo giao diện hiện tại).
5. Sao chép **Project URL** và **anon/public key**. Chỉ dùng public/anon key trên trình duyệt. Tuyệt đối không đưa `service_role` hoặc secret key vào website.

### B. Điền cấu hình
Mở `index.html`, tìm:
```js
const SUPABASE_URL = "YOUR_SUPABASE_URL";
const SUPABASE_ANON_KEY = "YOUR_SUPABASE_ANON_KEY";
```
Thay bằng Project URL và anon/public key của dự án Supabase. Lưu lại.

### C. Đưa website lên mạng bằng Vercel
Cách đơn giản:
1. Tạo tài khoản tại https://vercel.com/
2. Tạo một repository GitHub mới tại https://github.com/ rồi tải 3 file của thư mục này lên (ít nhất cần `index.html`; thêm SQL và README để tiện quản lý).
3. Trong Vercel chọn **Add New → Project**, kết nối repository GitHub.
4. Framework preset chọn **Other** nếu được hỏi; không cần build command, output directory để mặc định/trống theo hướng dẫn của Vercel.
5. Nhấn **Deploy**. Sau khi thành công, Vercel cấp URL dạng `https://ten-du-an.vercel.app`.
6. Mở URL đó trên điện thoại bằng mạng di động để kiểm tra game. Chơi thử, hoàn thành 6 vòng, rồi xem bảng xếp hạng có nhận điểm hay chưa.

Có thể dùng dịch vụ static hosting khác, miễn website được xuất bản công khai qua HTTPS.

## Tạo mã QR
Sau khi deploy:
1. Mở URL website công khai trên trình duyệt.
2. Ở trang chủ game bấm **Hiện mã QR**. QR được tạo từ chính URL hiện tại.
3. Quét thử bằng một điện thoại khác. Nếu QR mở đúng website, chụp/lưu mã hoặc dùng chức năng chia sẻ/in trang để đưa lên slide.
4. Bạn cũng có thể sao chép URL bằng nút **Sao chép link game**.

Không tạo QR từ `file:///...` hoặc URL localhost vì người khác sẽ không truy cập được.

## Lưu ý quan trọng
- Cần cấu hình Supabase và deploy mới có bảng xếp hạng chung giữa các thiết bị.
- Chính sách SQL mẫu cho phép công khai gửi điểm và xem bảng xếp hạng; phù hợp demo lớp học nhưng người am hiểu có thể giả mạo kết quả. Nếu cần thi chính thức, nên thêm xác thực hoặc server-side scoring/rate limiting.
- Chỉ dùng biệt danh; tránh yêu cầu người chơi nhập số điện thoại, email hoặc dữ liệu cá nhân.
- Trò chơi là hoạt động giáo dục/giải trí, không phải công cụ chẩn đoán y khoa.
