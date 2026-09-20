# MOD01 - Quản lý Tài khoản & Định danh (Account & Auth)

## Scenario: Đăng ký tài khoản

| Test Case ID | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- |
| TC-REG-001 | Gửi mã OTP thành công với SĐT hợp lệ chưa đăng ký | Đang ở màn hình Đăng ký | 1. Mở màn hình Đăng ký<br>

<br>2. Nhập SĐT<br>

<br>3. Nhấn 'Gửi mã OTP' | SĐT: 0901234567 | Hệ thống gửi OTP qua SMS thành công trong vòng 5 giây; hiển thị màn hình nhập OTP | High |
| TC-REG-002 | Xác thực OTP hợp lệ và tạo tài khoản Customer | OTP đã được gửi tới thiết bị | 1. Nhập mã OTP<br>

<br>2. Nhấn 'Xác nhận' | SĐT: 0901234567<br>

<br>OTP: 482913 | Xác thực thành công; tạo user role=CUSTOMER, status=ACTIVE; trả về JWT Token và vào giao diện Khách hàng | High |
| TC-REG-003 | Đăng ký tài khoản Tài xế và điều hướng đúng giao diện Driver | Đang ở màn hình Chọn loại tài khoản | 1. Chọn loại tài khoản 'Tài xế'<br>

<br>2. Hoàn tất xác thực OTP | SĐT: 0908889999 | Tạo user role=DRIVER, status=PENDING_APPROVAL; chuyển sang màn hình nộp hồ sơ tài xế | High |
| TC-REG-004 | Gửi lại mã OTP sau khi hết hiệu lực | Đã hết thời gian chờ 60 giây của OTP cũ | 1. Nhấn nút 'Gửi lại mã OTP'<br>

<br>2. Kiểm tra SMS | SĐT: 0901234567 | Mã OTP mới được gửi thành công; mã OTP cũ bị vô hiệu hóa | Medium |
| TC-REG-005 | Hoàn tất thông tin Họ tên, Email sau khi xác thực OTP | Đã xác thực OTP thành công | 1. Nhập Họ tên, Email<br>

<br>2. Nhập Mật khẩu hợp lệ<br>

<br>3. Nhấn 'Hoàn tất' | Name: Nguyen Van A<br>

<br>Email: ana@gmail.com<br>

<br>Pass: Abc@1234 | Cập nhật thông tin tài khoản thành công; chuyển sang Trang chủ | High |
| TC-REG-006 | Đăng ký bằng SĐT đã tồn tại | SĐT 0901234567 đã có trong DB | 1. Nhập SĐT đã tồn tại<br>

<br>2. Nhấn 'Gửi mã OTP' | SĐT: 0901234567 | Hiển thị lỗi 'Số điện thoại đã được sử dụng. Vui lòng đăng nhập hoặc dùng SĐT khác' | High |
| TC-REG-007 | Nhập sai mã OTP | Đã bấm gửi OTP thành công | 1. Nhập sai mã OTP<br>

<br>2. Nhấn 'Xác nhận' | OTP sai: 000000 | Báo lỗi 'Mã OTP không chính xác. Vui lòng thử lại'; giữ nguyên màn hình OTP | High |
| TC-REG-008 | Nhập OTP đã hết hiệu lực | Quá 3 phút kể từ khi gửi OTP | 1. Nhập mã OTP cũ<br>

<br>2. Nhấn 'Xác nhận' | OTP hết hạn | Báo lỗi 'Mã OTP đã hết hiệu lực. Vui lòng yêu cầu mã mới' | High |
| TC-REG-009 | Nhập sai OTP quá số lần cho phép | Nhập sai OTP 4 lần liên tiếp | 1. Nhập sai OTP lần thứ 5 | OTP sai | Khóa tính năng xác thực OTP của SĐT trong 15 phút; hiển thị thông báo khóa tạm thời | High |
| TC-REG-010 | Đăng ký với Email đã được tài khoản khác sử dụng | Email 'exist@gmail.com' đã đăng ký | 1. Hoàn tất OTP<br>

<br>2. Nhập Email trùng<br>

<br>3. Bấm 'Hoàn tất' | Email: exist@gmail.com | Báo lỗi 'Email đã được sử dụng bởi tài khoản khác' | Medium |
| TC-REG-011 | SĐT ngắn hơn độ dài tối thiểu (9 số) | Đang ở màn hình Đăng ký | 1. Nhập SĐT 9 chữ số<br>

<br>2. Nhấn 'Gửi mã OTP' | SĐT: 090123456 | Nút 'Gửi mã OTP' bị disable hoặc hiển thị lỗi 'Số điện thoại phải đủ 10 chữ số' | Medium |
| TC-REG-012 | Để trống SĐT khi gửi OTP | Đang ở màn hình Đăng ký | 1. Để trống ô SĐT<br>

<br>2. Nhấn 'Gửi mã OTP' | SĐT: [rỗng] | Hiển thị thông báo 'Vui lòng nhập số điện thoại' | High |
| TC-REG-013 | Để trống ô nhập OTP | Đã gửi OTP thành công | 1. Để trống ô OTP<br>

<br>2. Nhấn 'Xác nhận' | OTP: [rỗng] | Hiển thị thông báo 'Vui lòng nhập mã OTP' | High |
| TC-REG-014 | SĐT chứa ký tự chữ và ký tự đặc biệt | Đang ở màn hình Đăng ký | 1. Nhập SĐT chứa chữ/ký tự<br>

<br>2. Nhấn 'Gửi mã OTP' | SĐT: 09012abc#$ | Bàn phím không cho nhập chữ/ký tự đặc biệt hoặc báo 'SĐT chỉ được chứa số' | Medium |
| TC-REG-015 | Spam nút 'Gửi mã OTP' liên tục | Đang ở màn hình Đăng ký | 1. Nhấn nút 'Gửi mã OTP' 5 lần liên tiếp trong 2 giây | SĐT: 0901234567 | Chỉ xử lý 1 request gửi OTP đầu tiên; disable nút bấm trong 60 giây (Rate limiting) | Medium |
| TC-REG-016 | Request đăng ký thiếu trường phone_number | Gọi API POST /api/v1/auth/register-otp | 1. Gửi payload thiếu field 'phone_number' | Payload: {} | API trả về HTTP Status 400 Bad Request; message 'phone_number is required' | High |
| TC-REG-017 | Mật khẩu được mã hóa khi lưu xuống DB | Đăng ký tài khoản mới thành công | 1. Kiểm tra trực tiếp bảng `users` trong CSDL | User ID vừa tạo | Mật khẩu được lưu dưới dạng chuỗi Hash (Bcrypt/Argon2), không lưu xâu rõ (plaintext) | High |
| TC-REG-018 | Họ tên đúng độ dài tối đa cho phép (100 ký tự) | Đang điền hồ sơ sau OTP | 1. Nhập Họ tên 100 ký tự hợp lệ<br>

<br>2. Lưu thông tin | Name: 100 ký tự | Lưu thành công; hiển thị đủ 100 ký tự trên trang thông tin | Low |

---

## Scenario: Đăng nhập Email-Mật khẩu & phân quyền theo Role

| Test Case ID | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- |
| TC-AUTH-001 | Đăng nhập thành công bằng Email và mật khẩu hợp lệ | Tài khoản Customer active | 1. Mở màn hình Đăng nhập<br>

<br>2. Nhập Email, Mật khẩu<br>

<br>3. Nhấn 'Đăng nhập' | Email: customer@cab.com<br>

<br>Pass: Pass123! | Đăng nhập thành công; trả về Bearer JWT Token; chuyển về Trang chủ Khách hàng | High |
| TC-AUTH-002 | Đăng nhập tài khoản Driver và điều hướng đúng Role | Tài khoản Driver active | 1. Nhập Email/Pass Driver<br>

<br>2. Nhấn 'Đăng nhập' | Email: driver@cab.com<br>

<br>Pass: Pass123! | Đăng nhập thành công; điều hướng đến Màn hình Tài xế (Sẵn sàng nhận chuyến) | High |
| TC-AUTH-003 | Đăng nhập tài khoản Admin vào Admin Portal | Tài khoản Admin active | 1. Truy cập Admin Portal<br>

<br>2. Đăng nhập tài khoản Admin | Email: admin@cab.com<br>

<br>Pass: Pass123! | Đăng nhập thành công; điều hướng đến Màn hình Quản trị Admin Dashboard | High |
| TC-AUTH-004 | JWT Token chứa đúng thông tin Role và thời hạn | Đã đăng nhập thành công | 1. Giải mã chuỗi JWT Token (Payload) | JWT Token | Claim chứa đúng `user_id`, `role` (CUSTOMER/DRIVER/ADMIN) và `exp` validity (e.g. 24h) | High |
| TC-AUTH-005 | Truy cập API được bảo vệ bằng token hợp lệ | Token còn hạn | 1. Gọi API `GET /api/v1/profile` đính kèm Header `Authorization: Bearer <token>` | Token hợp lệ | HTTP 200 OK; Trả về đúng thông tin hồ sơ của user sở hữu token | High |
| TC-AUTH-006 | Đăng xuất và vô hiệu hóa phiên | Đang đăng nhập | 1. Nhấn nút 'Đăng xuất'<br>

<br>2. Dùng token cũ gọi API bảo vệ | Token vừa logout | Đăng xuất thành công; API trả về HTTP 401 Unauthorized do Token đã bị ngắt phiên | Medium |
| TC-AUTH-007 | Đăng nhập với Email không tồn tại | Email chưa từng đăng ký | 1. Nhập Email chưa có trong hệ thống<br>

<br>2. Nhấn 'Đăng nhập' | Email: notexist@cab.com<br>

<br>Pass: Pass123! | Báo lỗi 'Email hoặc mật khẩu không chính xác' (không chỉ định rõ email chưa tồn tại để bảo mật) | High |
| TC-AUTH-008 | Đăng nhập với mật khẩu sai | Email có trong hệ thống | 1. Nhập đúng Email<br>

<br>2. Nhập sai Mật khẩu<br>

<br>3. Nhấn 'Đăng nhập' | Email: customer@cab.com<br>

<br>Pass: WrongPass123 | Báo lỗi 'Email hoặc mật khẩu không chính xác' | High |
| TC-AUTH-009 | Đăng nhập bằng tài khoản bị khóa (LOCKED) | User status = LOCKED | 1. Nhập Email/Pass của tài khoản đã bị khóa | Email: locked@cab.com<br>

<br>Pass: Pass123! | Báo lỗi 'Tài khoản của bạn đã bị khóa. Vui lòng liên hệ bộ phận hỗ trợ' | High |
| TC-AUTH-010 | Tài xế PENDING_APPROVAL đăng nhập | Tài xế chưa được duyệt hồ sơ | 1. Đăng nhập tài khoản Driver PENDING | Email: pending_driver@cab.com | Đăng nhập thành công nhưng chỉ hiển thị màn hình 'Hồ sơ đang chờ duyệt' | High |
| TC-AUTH-011 | Đăng nhập sai mật khẩu nhiều lần liên tiếp | Đang ở màn hình Đăng nhập | 1. Nhập sai mật khẩu 5 lần liên tiếp | Email: customer@cab.com | Tự động tạm khóa tài khoản trong 15 phút hoặc yêu cầu giải CAPTCHA | High |
| TC-AUTH-012 | Customer gọi API dành riêng cho Admin | Đã đăng nhập vai trò CUSTOMER | 1. Gọi API `GET /api/v1/admin/users` dùng Token Customer | Token Customer | API trả về HTTP status 403 Forbidden | High |
| TC-AUTH-013 | Sử dụng JWT Token đã hết hạn | Token đã quá thời hạn `exp` | 1. Gọi API đính kèm Token hết hạn | Expired Token | API trả về HTTP status 401 Unauthorized; message 'Token has expired' | High |
| TC-AUTH-014 | Sử dụng JWT Token bị chỉnh sửa chữ ký | Modded Signature Token | 1. Sửa payload của JWT (e.g. đổi role thành ADMIN) nhưng giữ nguyên signature | Tampered Token | API trả về HTTP status 401 Unauthorized; message 'Invalid signature' | High |
| TC-AUTH-015 | Mật khẩu ngắn hơn tối thiểu (7 ký tự) | Màn hình Đăng nhập | 1. Nhập mật khẩu 7 ký tự<br>

<br>2. Nhấn 'Đăng nhập' | Pass: 1234567 | Báo lỗi validation 'Mật khẩu phải chứa ít nhất 8 ký tự' | Medium |
| TC-AUTH-016 | Để trống Email khi đăng nhập | Màn hình Đăng nhập | 1. Để trống Email, nhập Mật khẩu<br>

<br>2. Bấm 'Đăng nhập' | Email: [rỗng] | Báo lỗi 'Vui lòng nhập Email' | High |
| TC-AUTH-017 | Email sai định dạng và chuỗi SQL Injection | Màn hình Đăng nhập | 1. Nhập `' OR '1'='1` vào ô Email<br>

<br>2. Bấm 'Đăng nhập' | Email: ' OR '1'='1 | Hiển thị lỗi định dạng Email không hợp lệ; hệ thống an toàn không bị lọt qua đăng nhập | High |
| TC-AUTH-018 | Thời gian phản hồi API đăng nhập | Mạng ổn định | 1. Gửi request `POST /api/v1/auth/login`<br>

<br>2. Đo response time | Request chuẩn | API phản hồi thành công trong thời gian < 2000ms (NFR) | High |

---

## Scenario: Cập nhật hồ sơ cá nhân

| Test Case ID | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- |
| TC-PROF-001 | Cập nhật Họ tên thành công | Đã đăng nhập, ở màn Hồ sơ | 1. Sửa Họ tên mới<br>

<br>2. Nhấn 'Lưu thay đổi' | Name: Nguyen Van B | Thông tin được lưu thành công; hiển thị Họ tên mới trên ứng dụng | High |
| TC-PROF-002 | Cập nhật Email thành công | Đã đăng nhập, ở màn Hồ sơ | 1. Nhập Email mới hợp lệ<br>

<br>2. Nhấn 'Lưu' | Email: newemail@gmail.com | Lưu thành công; gửi mail xác nhận đến địa chỉ email mới | Medium |
| TC-PROF-003 | Tải lên ảnh đại diện hợp lệ | File ảnh PNG/JPG < 5MB | 1. Chọn file ảnh avatar hợp lệ<br>

<br>2. Nhấn 'Tải lên' | File: avatar.jpg (2MB) | Ảnh đại diện cập nhật thành công và hiển thị rõ nét | Medium |
| TC-PROF-004 | Tài xế cập nhật thông tin phương tiện | Tài xế đã đăng nhập | 1. Cập nhật Hãng xe, Dòng xe, Màu xe<br>

<br>2. Bấm 'Lưu' | Xe: Honda City, Đen | Thông tin xe được lưu cập nhật thành công | Medium |
| TC-PROF-005 | Xem lại hồ sơ sau khi đăng nhập lại | Đã lưu hồ sơ mới thành công | 1. Đăng xuất<br>

<br>2. Đăng nhập lại<br>

<br>3. Vào màn hình Hồ sơ | Tài khoản vừa sửa | Các thông tin mới lưu vẫn giữ nguyên đúng dữ liệu | Medium |
| TC-PROF-006 | Cập nhật Email trùng với người dùng khác | Email 'other@gmail.com' đã tồn tại | 1. Nhập Email trùng<br>

<br>2. Nhấn 'Lưu' | Email: other@gmail.com | Báo lỗi 'Email này đã được sử dụng bởi người dùng khác' | High |
| TC-PROF-007 | Người dùng A sửa hồ sơ của người dùng B | Dùng API `PUT /api/v1/profile` | 1. User A truyền `user_id` của User B vào request body | User_id của B | Hệ thống chỉ cập nhật hồ sơ của chính User A dựa theo Token (hoặc báo 403 Forbidden) | High |
| TC-PROF-008 | Sửa trực tiếp trường role qua API | Dùng API `PUT /api/v1/profile` | 1. Gửi payload cập nhật kèm `"role": "ADMIN"` | Role: ADMIN | Hệ thống bỏ qua field `role` hoặc trả về lỗi 400/403; Role của user không bị thay đổi | High |
| TC-PROF-009 | Tải lên file avatar vượt dung lượng cho phép | File > 5MB | 1. Chọn file ảnh 8MB<br>

<br>2. Nhấn 'Tải lên' | File: big_photo.png (8MB) | Báo lỗi 'Dung lượng ảnh vượt quá giới hạn tối đa 5MB' | Medium |
| TC-PROF-010 | Xóa trắng Họ tên rồi lưu | Màn hình Chỉnh sửa hồ sơ | 1. Xóa toàn bộ ký tự trong ô Họ tên<br>

<br>2. Nhấn 'Lưu' | Name: [rỗng] | Báo lỗi 'Họ và tên không được để trống' | High |
| TC-PROF-011 | Email sai định dạng | Màn hình Chỉnh sửa hồ sơ | 1. Nhập `abc@xyz`<br>

<br>2. Nhấn 'Lưu' | Email: abc@xyz | Báo lỗi 'Định dạng Email không hợp lệ' | Medium |
| TC-PROF-012 | Tải lên avatar sai định dạng file | File PDF/EXE | 1. Chọn file document.pdf<br>

<br>2. Bấm 'Tải lên' | File: document.pdf | Báo lỗi 'Định dạng file không hỗ trợ. Chỉ chấp nhận JPG, PNG' | High |
| TC-PROF-013 | Họ tên chứa mã script (XSS) | Màn hình Chỉnh sửa hồ sơ | 1. Nhập `<script>alert('xss')</script>` vào Họ tên<br>

<br>2. Nhấn 'Lưu' | Name: `<script>...` | Hệ thống Encode/Sanitize chuỗi nhập vào; hiển thị dưới dạng văn bản thường, không thực thi script | High |
| TC-PROF-014 | Cập nhật hồ sơ khi mất kết nối mạng | Thiết bị offline | 1. Tắt mạng internet<br>

<br>2. Nhấn 'Lưu thay đổi' | Không có mạng | Báo lỗi 'Kết nối mạng bị gián đoạn. Vui lòng kiểm tra lại internet' | Medium |

---

## Scenario: Tài xế tải giấy tờ & gửi hồ sơ xét duyệt

| Test Case ID | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
| --- | --- | --- | --- | --- | --- | --- |
| TC-DOCS-001 | Tài xế tải đầy đủ Bằng lái, Giấy tờ xe, Biển số và gửi xét duyệt | Tài xế tài khoản PENDING | 1. Tải ảnh Bằng lái (GTLX)<br>

<br>2. Tải ảnh Đăng ký xe<br>

<br>3. Nhập Biển số xe<br>

<br>4. Nhấn 'Gửi xét duyệt' | Biển số: 29A-123.45<br>

<br>Ảnh hợp lệ | Hồ sơ chuyển sang trạng thái PENDING_APPROVAL thành công; hiển thị màn hình chờ Admin duyệt | High |
| TC-DOCS-002 | Admin phê duyệt hồ sơ hợp lệ | Admin đăng nhập Portal, có hồ sơ tài xế chờ duyệt | 1. Xem chi tiết hồ sơ tài xế<br>

<br>2. Nhấn 'Phê duyệt' | Driver ID: 102 | Hồ sơ tài xế đổi sang status APPROVED/ACTIVE; gửi thông báo Push/SMS cho tài xế | High |
| TC-DOCS-003 | Tài xế bật trạng thái Sẵn sàng sau khi được duyệt | Tài xế status = APPROVED | 1. Mở ứng dụng Driver<br>

<br>2. Bật công tắc 'Sẵn sàng đón khách' | Status: APPROVED | Trạng thái chuyển sang ONLINE; tài xế bắt đầu nhận được cuốc xe từ hệ thống | High |
| TC-DOCS-004 | Tài xế nộp lại hồ sơ sau khi bị từ chối | Hồ sơ tài xế status = REJECTED | 1. Xem lý do từ chối<br>

<br>2. Tải lại ảnh giấy tờ mờ<br>

<br>3. Nhấn 'Gửi lại' | Hồ sơ bổ sung | Trạng thái hồ sơ chuyển lại thành PENDING_APPROVAL | High |
| TC-DOCS-005 | Tải lên nhiều ảnh giấy tờ trong một lần gửi | Màn hình nộp giấy tờ | 1. Chọn 2 ảnh mặt trước/sau bằng lái<br>

<br>2. Nhấn 'Tải lên' | 2 files ảnh JPG | Cả 2 ảnh đều được lưu và hiển thị xem trước đầy đủ | Medium |
| TC-DOCS-006 | Gửi hồ sơ khi thiếu Bằng lái | Thiếu ảnh Bằng lái | 1. Tải Giấy đăng ký xe<br>

<br>2. Để trống Bằng lái<br>

<br>3. Bấm 'Gửi xét duyệt' | Thiếu GTLX | Báo lỗi 'Vui lòng tải lên hình ảnh Bằng lái xe' | High |
| TC-DOCS-007 | Admin từ chối hồ sơ không hợp lệ kèm lý do | Admin portal | 1. Chọn tài xế cần duyệt<br>

<br>2. Nhấn 'Từ chối'<br>

<br>3. Nhập lý do 'Ảnh bằng lái bị mờ'<br>

<br>4. Xác nhận | Lý do: Ảnh mờ | Hồ sơ chuyển trạng thái REJECTED; thông báo gửi về cho Tài xế kèm đúng lý do | High |
| TC-DOCS-008 | Tài xế chưa duyệt cố bật trạng thái Sẵn sàng | Driver status = PENDING_APPROVAL | 1. Cố bật nút 'Sẵn sàng' khi chưa duyệt | Status: PENDING | Công tắc bị disable hoặc hiển thị popup 'Hồ sơ của bạn đang chờ phê duyệt' | High |
| TC-DOCS-009 | Đăng ký biển số xe đã được tài xế khác sử dụng | Biển số 30F-999.99 đã active | 1. Nhập biển số 30F-999.99<br>

<br>2. Nhấn 'Gửi xét duyệt' | Biển số: 30F-999.99 | Báo lỗi 'Biển số xe này đã được đăng ký bởi tài xế khác' | High |
| TC-DOCS-010 | Tài xế tự phê duyệt hồ sơ qua API | Dùng tài khoản DRIVER | 1. Gọi API `POST /api/v1/admin/drivers/{id}/approve` bằng Token Driver | Token Driver | API trả về lỗi 403 Forbidden | High |
| TC-DOCS-011 | Ảnh giấy tờ vượt dung lượng tối đa | File ảnh > 5MB | 1. Chọn file 10MB<br>

<br>2. Tải lên | File 10MB | Báo lỗi 'Dung lượng file vượt quá 5MB' | Medium |
| TC-DOCS-012 | Gửi hồ sơ khi chưa tải bất kỳ giấy tờ nào | Form trống | 1. Bấm 'Gửi xét duyệt' ngay | Form trống | Báo lỗi yêu cầu tải lên đầy đủ tất cả tài liệu bắt buộc | High |
| TC-DOCS-013 | Để trống ô Biển số xe | Chưa nhập biển số | 1. Tải đủ ảnh<br>

<br>2. Để trống ô Biển số<br>

<br>3. Bấm 'Gửi' | Biển số: [rỗng] | Báo lỗi 'Vui lòng nhập Biển số xe' | High |
| TC-DOCS-014 | Biển số sai định dạng | Nhập sai định dạng | 1. Nhập `@@-12345678`<br>

<br>2. Bấm 'Gửi' | Biển số sai | Báo lỗi 'Biển số xe không đúng định dạng (Ví dụ hợp lệ: 29A-123.45)' | Medium |
| TC-DOCS-015 | Tải lên giấy tờ sai định dạng file | File đính kèm .ZIP/.PDF | 1. Chọn file `doc.zip`<br>

<br>2. Bấm 'Tải lên' | File doc.zip | Báo lỗi 'Định dạng file không hỗ trợ. Chỉ nhận file ảnh PNG, JPG, JPEG' | High |
