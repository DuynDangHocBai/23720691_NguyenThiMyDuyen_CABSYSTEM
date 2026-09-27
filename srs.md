# Software Requirements Specification (SRS) - CAB System

## 1. Stakeholder List & Roles (Danh sách & Vai trò Bên liên quan)

| Stakeholder | Vai trò chính |
| :--- | :--- |
| **Ban Giám đốc** | Ra quyết định chiến lược, duyệt ngân sách và phê duyệt các quy tắc nghiệp vụ. |
| **Khách hàng** | Đặt xe, theo dõi chuyến đi, thanh toán và đánh giá chất lượng dịch vụ. |
| **Tài xế** | Bật trạng thái sẵn sàng, nhận/từ chối chuyến và cập nhật tiến trình chuyến đi. |
| **Nhân viên vận hành** | Theo dõi hệ thống, hỗ trợ xử lý sự cố chuyến đi và quản trị dữ liệu. |
| **Business Analyst** | Làm rõ yêu cầu chưa chốt và chi tiết hóa quy trình nghiệp vụ cho team. |
| **Nhóm Phát triển** | Thiết kế kiến trúc, lập trình và hoàn thiện hệ thống trong 7 tuần. |
| **Đối tác Thanh toán** | Tích hợp xử lý giao dịch điện tử. |

---

## 2. Stakeholder Matrix (Ma trận Bên liên quan)

```mermaid
quadrantChart
    title Stakeholder Matrix - CAB System
    x-axis Low Interest --> High Interest
    y-axis Low Power --> High Power

    quadrant-1 Manage Closely
    quadrant-2 Keep Satisfied
    quadrant-3 Monitor
    quadrant-4 Keep Informed

    "Ban Giam doc": [0.85, 0.95]
    "Business Analyst": [0.75, 0.70]
    "Nhom Phat trien": [0.80, 0.60]
    "Nhan vien Van hanh": [0.90, 0.75]
    "Khach hang": [0.95, 0.55]
    "Tai xe": [0.90, 0.45]
    "Doi tac Thanh toan": [0.35, 0.65]
```
---

## 3. Business Goals (Mục tiêu Kinh doanh)

| ID | Tên Mục tiêu | Mô tả Chi tiết |
| :--- | :--- | :--- |
| **BG01** | Tự động hóa & Mở rộng Vận hành | Tự động hóa quy trình phân công tài xế và tối ưu hóa vận hành nhằm giảm thiểu sự can thiệp thủ công, sẵn sàng mở rộng quy mô hệ thống phục vụ lượng lớn khách hàng và tài xế trong tương lai. |
| **BG02** | Tối ưu Doanh thu & Chuyến đi | Nâng cao doanh thu, tỷ lệ hoàn thành chuyến đi và giảm tỷ lệ hủy chuyến thông qua việc tối ưu cơ chế đề xuất, ghép nối tài xế gần nhất theo thời gian thực. |
| **BG03** | Nâng cao Trải nghiệm Khách hàng | Tăng cường trải nghiệm và độ hài lòng của khách hàng bằng việc minh bạch hóa thông tin trạng thái chuyến đi, vị trí tài xế, thời gian dự kiến đến và đa dạng hóa phương thức thanh toán an toàn. |
| **BG04** | Tối ưu Hiệu quả cho Tài xế | Tăng hiệu quả hoạt động và thu nhập cho tài xế nhờ cơ chế thông báo nhận chuyến chủ động, minh bạch tiến trình chuyến đi và quy trình hỗ trợ vận hành rõ ràng. |
| **BG05** | Nâng cao Năng lực Quản trị | Nâng cao năng lực quản trị, hỗ trợ và xử lý sự cố kịp thời thông qua hệ thống theo dõi trực quan, phân quyền chặt chẽ và công cụ báo cáo hoạt động chuyên sâu. |
| **BG06** | Kiến trúc Nền tảng Linh hoạt | Xây dựng kiến trúc nền tảng ổn định, bảo mật cao, có khả năng mở rộng độc lập và linh hoạt tích hợp/bổ sung các loại hình dịch vụ, đối tác thanh toán hay thông báo mới trong tương lai mà không ảnh hưởng tới hệ thống đang chạy. |
---

## 4. Minimum Viable Product (MVP) Modules

| ID | Tên Module | Mô tả Chức năng chính |
| :--- | :--- | :--- |
| **MOD01** | Quản lý Tài khoản & Định danh (*Account & Auth Module*) | Đăng ký, đăng nhập, quản lý hồ sơ (Khách hàng, Tài xế) và phân quyền quản trị (Nhân viên vận hành). |
| **MOD02** | Đặt xe & Phân công (*Booking & Matching Module*) | Tạo chuyến, định vị thời gian thực, thuật toán tự động ghép nối/tìm tài xế gần nhất và xử lý chuyển tiếp khi từ chối. |
| **MOD03** | Quản lý Tiến trình Chuyến đi (*Trip Management Module*) | Cập nhật/theo dõi trạng thái chuyến đi theo thời gian thực (ETA, vị trí), lịch sử chuyến và đánh giá tài xế. |
| **MOD04** | Tính cước & Thanh toán (*Pricing & Payment Module*) | Tính tiền tự động, hỗ trợ tiền mặt và tích hợp Payment Gateway bên ngoài xử lý thanh toán điện tử. |
| **MOD05** | Vận hành & Báo cáo (*Admin & Analytics Module*) | Giao diện quản trị theo dõi chuyến đi, hỗ trợ xử lý sự cố và xuất báo cáo doanh thu, hiệu suất cho Ban giám đốc. |
---

## 5. Business Requirements (Yêu cầu Nghiệp vụ)

| ID | Tên Yêu cầu | Mô tả Chi tiết |
| :--- | :--- | :--- |
| **BR01** | Quản lý Định danh & Xét duyệt Hồ sơ | Hỗ trợ đăng ký, đăng nhập và phân quyền (Khách hàng, Tài xế, Quản trị viên); cung cấp quy trình tải lên và xét duyệt giấy tờ, phương tiện của Tài xế trước khi kích hoạt hoạt động. |
| **BR02** | Đặt xe & Đề xuất Điều phối | Cho phép Khách hàng chọn lộ trình, xem cước phí dự kiến và tạo chuyến; hệ thống định vị GPS để tự động quét, đề xuất và chuyển tiếp chuyến đi tới Tài xế sẵn sàng gần nhất |
| **BR03** | Quản lý Vòng đời Chuyến đi | Cung cấp máy trạng thái để Tài xế cập nhật liên tục tiến trình chuyến (Đã đến, Đang di chuyển, Hoàn thành); hỗ trợ theo dõi vị trí real-time và cho phép xử lý hủy chuyến theo chính sách. |
| **BR04** | Tính cước, Thanh toán & Hoa hồng | Tự động chốt cước phí thực tế sau chuyến đi; hỗ trợ thanh toán tiền mặt/ví điện tử và tự động tính tỷ lệ chiết khấu hoa hồng cho hệ thống/tài xế |
| **BR05** | Giám sát & Hỗ trợ Vận hành | Cung cấp giao diện trực quan cho Nhân viên vận hành giám sát các chuyến đi đang chạy thời gian thực, hỗ trợ xử lý sự cố (mất GPS, kẹt đơn, khóa tài khoản) |
| **BR06** | Báo cáo & Đánh giá Dịch vụ | Cho phép Khách hàng đánh giá chất lượng phục vụ sau chuyến đi; đồng thời tổng hợp báo cáo kinh doanh (doanh thu, số chuyến, tỷ lệ hủy, hiệu suất) phục vụ Ban Giám đốc |

---
## 6. Business Process Modeling (Mô hình hóa Quy trình Nghiệp vụ)

### 6.1. Biểu đồ Tổng quan Toàn bộ Quy trình Nghiệp vụ (Overall Process Map)

```mermaid
flowchart LR
    %% Style definitions
    classDef step fill:#f0f7ff,stroke:#0284c7,stroke-width:2px,color:#0f172a,rx:8,ry:8;
    classDef highlight fill:#ecfdf5,stroke:#059669,stroke-width:2px,color:#064e3b,rx:8,ry:8;

    S1("<b>1. Đặt xe & Chọn tuyến</b><br/>Khách chọn điểm đón/đến, loại xe & xem giá cước"):::step
    S2("<b>2. Xác thực & Quét tài xế</b><br/>Hệ thống verify token & quét tài xế READY (bán kính 3-5km)"):::step
    S3("<b>3. Đề xuất nhận chuyến</b><br/>Gửi offer kèm đếm ngược 15s tới tài xế gần nhất"):::step
    S4("<b>4. Phản hồi nhận chuyến</b><br/>Tài xế bấm Chấp nhận (hoặc Chuyển tiếp nếu từ chối/timeout)"):::step
    S5("<b>5. Khởi tạo Chuyến đi</b><br/>Khóa tài xế, tạo chuyến & trả thông tin tài xế cho Khách"):::highlight
    S6("<b>6. Thực hiện chuyến đi</b><br/>Cập nhật tiến trình: ARRIVED ➔ IN_PROGRESS"):::step
    S7("<b>7. Hoàn thành & Tính cước</b><br/>Chốt lộ trình thực tế, tính tổng tiền & trích hoa hồng 15%"):::step
    S8("<b>8. Xử lý Thanh toán</b><br/>Thanh toán tiền mặt hoặc qua Cổng thanh toán điện tử"):::step
    S9("<b>9. Đánh giá chất lượng</b><br/>Khách hàng chấm điểm 1-5 sao & gửi phản hồi"):::step
    S10("<b>10. Vận hành & Giám sát</b><br/>Ghi nhận báo cáo doanh thu & giám sát sự cố real-time"):::highlight

    S1 --> S2 --> S3 --> S4 --> S5 --> S6 --> S7 --> S8 --> S9 --> S10
```

```mermaid
sequenceDiagram
    autonumber
    actor C as Khách hàng (Customer)
    actor D as Tài xế (Driver)
    participant GW as API Gateway
    participant Auth as Auth & Identity
    participant Match as Matching Service (Redis)
    participant Trip as Trip Service
    participant Pay as Pricing & Payment
    participant MB as Event Broker (Kafka/EventBus)
    participant Ops as Admin & Analytics

    %% Bước 1 & 2: Tạo yêu cầu & Quét điều phối
    Note over C, Match: 1. Đặt xe & Quét điều phối tự động
    C->>GW: POST /api/bookings (Điểm đón, Điểm đến, Loại xe)
    GW->>Auth: Xác thực Token (JWT Verification)
    Auth-->>GW: Token hợp lệ (uid, role=Customer)
    GW->>Match: Yêu cầu tìm tài xế (Quét Redis GEO bán kính 3-5km)
    
    %% Bước 3 & 4: Đề xuất và Nhận chuyến
    Note over Match, D: 2. Đề xuất nhận chuyến (15s Timeout)
    Match->>D: Gửi thông báo nhận chuyến (Push Socket + Đếm ngược 15s)
    alt Tài xế chấp nhận
        D->>Match: Bấm "Chấp nhận chuyến"
    else Từ chối hoặc Hết 15 giây
        Match->>Match: Chuyển tiếp đề xuất tới Tài xế tiếp theo
    end

    %% Bước 5: Tạo chuyến đi
    Note over Match, Trip: 3. Khởi tạo chuyến đi
    Match->>Trip: Yêu cầu tạo chuyến (Customer_id, Driver_id)
    Trip->>Trip: Lưu bản ghi Trip (Status = ACCEPTED)
    Trip-->>GW: Trả về thông tin Chuyến đi & Tài xế
    GW-->>C: Hiển thị thông tin xe, tài xế & vị trí real-time

    %% Bước 6: Tiến trình chuyến đi
    Note over D, C: 4. Cập nhật tiến trình chuyến đi
    D->>Trip: Cập nhật "Đã đến điểm đón" (Status = ARRIVED)
    Trip->>C: Thông báo: Tài xế đã tới điểm đón (Push Notification)
    D->>Trip: Bắt đầu di chuyển (Status = IN_PROGRESS)
    loop Cập nhật GPS (mỗi 3-5 giây)
        D->>Trip: Bắn tọa độ GPS thực tế
        Trip->>C: Cập nhật vị trí di chuyển trên bản đồ
    end

    %% Bước 7 & 8: Hoàn thành & Thanh toán
    Note over D, Pay: 5. Kết thúc & Thanh toán
    D->>Trip: Bấm "Hoàn thành chuyến đi" (Status = COMPLETED)
    Trip->>Pay: Kích hoạt tính cước (Quãng đường thực tế)
    Pay->>Pay: Tính cước + Trích hoa hồng hệ thống 15%
    Pay-->>C: Hiển thị hóa đơn & Yêu cầu thanh toán
    alt Thanh toán Điện tử (Payment Gateway)
        C->>Pay: Thanh toán qua Cổng điện tử / Ví
        Pay-->>C: Xác nhận thanh toán thành công
    else Thanh toán Tiền mặt (Cash)
        C->>D: Trả tiền mặt cho Tài xế
        D->>Pay: Xác nhận đã nhận đủ tiền
    end
    Pay->>Trip: Cập nhật trạng thái thanh toán (PAID)

    %% Bước 9: Đánh giá
    Note over C, Trip: 6. Đánh giá chất lượng
    C->>Trip: Gửi đánh giá (Rating 1-5 sao + Nhận xét)
    Trip->>Trip: Cập nhật điểm uy tín trung bình cho Tài xế

    %% Bước 10: Đồng bộ Báo cáo & Vận hành
    Note over Trip, Ops: 7. Báo cáo & Giám sát Vận hành
    Trip-)MB: Publish sự kiện `TripCompletedEvent`
    MB-)Ops: Consume sự kiện: Cập nhật Dashboard & Thống kê doanh thu
```

---
## 7. Functional Requirements (Yêu cầu Chức năng)


### 7.1. MOD01 - Module Quản lý Tài khoản & Định danh (Account & Auth)

| ID | Tên Chức năng | Đối tượng | Mô tả Chi tiết |
| :--- | :--- | :--- | :--- | 
| **FR01.1** | Đăng ký & Đăng nhập phân quyền | KH, TX, NVVH | Cho phép người dùng đăng ký, đăng nhập hệ thống và phân quyền theo Role (Customer, Driver, Admin). |
| **FR01.2** | Cập nhật Hồ sơ cá nhân | KH, TX | Cho phép người dùng xem và chỉnh sửa thông tin cá nhân (họ tên, số điện thoại, thông tin xe đối với tài xế). |

---

### 7.2. MOD02 - Module Đặt xe & Điều phối (Booking & Matching)

| ID | Tên Chức năng | Đối tượng | Mô tả Chi tiết | 
| :--- | :--- | :--- | :--- | 
| **FR02.1** | Tạo Yêu cầu Đặt xe | KH | Khách hàng chọn điểm đón/đến trên bản đồ, xem giá cước dự kiến và nhấn nút gửi yêu cầu đặt xe. |
| **FR02.2** | Định vị & Điều phối Chuyến | Hệ thống tự động quét tìm tài xế "Sẵn sàng" gần nhất theo bán kính (3–5km) và gửi lời mời nhận chuyến kèm đồng hồ đếm ngược 15 giây |
| **FR02.3** | Phản hồi & Chuyển tiếp chuyến | Cho phép Tài xế bấm nhận/từ chối; nếu từ chối hoặc hết 15 giây, hệ thống tự động chuyển tiếp sang tài xế tiếp theo.  |

---

### 7.3. MOD03 - Module Quản lý Tiến trình Chuyến đi (Trip Management)

| ID | Tên Chức năng | Đối tượng | Mô tả Chi tiết | 
| :--- | :--- | :--- | :--- | 
| **FR03.1** | Cập nhật Trạng thái Chuyến đi | TX | Cho phép Tài xế cập nhật lần lượt các mốc tiến trình của chuyến: Đã đến điểm đón $\rightarrow$ Bắt đầu di chuyển $\rightarrow$ Hoàn thành  |
| **FR03.2** | Theo dõi Vị trí Xe thời gian thực | KH | Khách hàng theo dõi vị trí GPS của tài xế di chuyển trên bản đồ theo thời gian thực (real-time). |
| **FR03.3** | Hủy chuyến đi | KH, TX | Cho phép Khách hàng hoặc Tài xế chủ động hủy chuyến khi chuyến đi chưa hoàn thành. |

---

### 7.4. MOD04 - Module Tính cước & Thanh toán (Pricing & Payment)

| ID | Tên Chức năng | Đối tượng | Mô tả Chi tiết | 
| :--- | :--- | :--- | :--- | 
| **FR04.1** | Tự động Tính cước phí | Hệ thống | Hệ thống tự động chốt tổng cước phí chuyến đi dựa trên loại xe và khoảng cách thực tế khi tài xế bấm hoàn thành. |
| **FR04.2** | Thanh toán Chuyến đi | TX, KH | Hỗ trợ thanh toán bằng Tiền mặt (tài xế xác nhận nhận tiền) hoặc thanh toán qua Cổng điện tử Sandbox. |


---

### 7.5. MOD05 - Module Vận hành & Báo cáo (Notification & Feedback)

| ID | Tên Chức năng | Đối tượng | Mô tả Chi tiết |
| :--- | :--- | :--- | :--- | 

---

## 8. Business Rules & Exception Handling (Quy tắc Nghiệp vụ & Xử lý Ngoại lệ)

### 8.1. Business Rules (Quy tắc Nghiệp vụ)

| ID | Quy tắc Nghiệp vụ | Mô tả & Logic Áp dụng | Áp dụng cho |
| :--- | :--- | :--- | :--- |
| **BR-RL01** | **Thời gian Phản hồi Nhận chuyến** | Tài xế có tối đa **15 giây** để bấm "Chấp nhận" hoặc "Từ chối" từ khi nhận thông báo. Quá 15 giây không phản hồi, hệ thống coi như "Từ chối" (Timeout). | Booking & Matching |
| **BR-RL02** | **Bán kính & Số lượng Tìm kiếm** | Ưu tiên quét Tài xế trong bán kính **3km** gần nhất; nếu không có, mở rộng tối đa lên **5km** và đề xuất lần lượt cho tối đa **5 Tài xế** liên tiếp. | Booking & Matching |
| **BR-RL03** | **Chính sách Hủy chuyến & Phí phạt** | • **Khách hàng:** Hủy miễn phí trong vòng **2 phút** sau khi Tài xế nhận chuyến. Hủy sau 2 phút hoặc khi Tài xế đã tới điểm đón sẽ chịu phí phạt **10,000 VNĐ**.<br>• **Tài xế:** Tự ý hủy chuyến mà không có lý do chính đáng sẽ bị trừ **2 điểm uy tín** và tạm khóa nhận chuyến trong **15 phút**. | Trip Management |
| **BR-RL04** | **Thời gian Chờ tại Điểm đón** | Tài xế có trách nhiệm đợi Khách hàng tối đa **5 phút** tại điểm đón. Sau 5 phút nếu không liên lạc được Khách, Tài xế có quyền hủy chuyến với lý do *"Khách không xuất hiện"*. | Trip Management |
| **BR-RL05** | **Tỷ lệ Chiết khấu & Đối soát** | Hệ thống thu phí hoa hồng cố định **15%** trên tổng giá trị cước phí mỗi chuyến đi hoàn thành. Dữ liệu đối soát được chốt tự động vào **23:59:59 hàng ngày**. | Pricing & Payment |

### 8.2. Exception Handling (Xử lý Ngoại lệ & Sự cố)

| ID | Kịch bản Ngoại lệ / Sự cố | Nguyên nhân Phát sinh | Phương án Xử lý Tự động & Vận hành |
| :--- | :--- | :--- | :--- |
| **BR-EX01** | **Không tìm thấy Tài xế (No Driver Found)** | Không có tài xế sẵn sàng trong bán kính 5km hoặc tất cả tài xế đề xuất đều từ chối/timeout. | Hệ thống hiển thị thông báo gửi Khách hàng: *"Hiện tại các tài xế đều đang bận, vui lòng thử lại sau ít phút"*, đồng thời gợi ý Khách hàng tăng/đổi loại xe hoặc chọn lại điểm đón. |
| **BR-EX02** | **Mất kết nối GPS / Mất mạng (Connection Lost)** | App Khách hàng hoặc Tài xế bị rớt mạng/mất tín hiệu GPS trong quá trình diễn ra chuyến đi. | • **App Tài xế:** Lưu vết tọa độ offline tạm thời trên thiết bị, tự động đồng bộ lại ngay khi có kết nối.<br>• **Hệ thống:** Nếu mất kết nối > 3 phút, gửi cảnh báo tới màn hình Vận hành (Admin) để NVVH chủ động gọi điện xác minh. |
| **BR-EX03** | **Thanh toán Điện tử Lỗi (Payment Failure)** | Cổng thanh toán bị timeout, tài khoản Khách hàng không đủ số dư hoặc giao dịch ngân hàng bị chối bỏ. | Hệ thống chuyển trạng thái thanh toán sang *"Thất bại"*, gửi Push Notification yêu cầu Khách hàng chọn phương thức thanh toán thay đổi (Chuyển sang Tiền mặt / Ví khác) để hoàn tất chuyến đi. |
| **BR-EX04** | **Tranh chấp Cước phí / Sự cố Đường dài** | Xe gặp sự cố kỹ thuật (hỏng xe, va chạm) giữa đường hoặc Lộ trình di chuyển thực tế lệch quá **20%** so với dự kiến. | Tài xế hoặc Khách hàng bấm nút *"Báo cáo Sự cố"* trên App. Hệ thống tạm dừng tính cước tự động, đóng băng giao dịch và chuyển chuyến đi sang trạng thái *"Chờ NVVH xử lý thủ công"*. |

---
## 9. Non-Functional Requirements (Yêu cầu Phi chức năng)

| ID | Nhóm Yêu cầu | Tiêu chí & Thông số Kỹ thuật |
| :--- | :--- | :--- |
| **NFR01** | **Hiệu năng (Performance)** | • Thời gian phản hồi API < **200ms** cho 95% các tác vụ thông thường.<br>• Thời gian tìm kiếm và đề xuất tài xế gần nhất < **2 giây**.<br>• Độ trễ cập nhật vị trí GPS real-time trên bản đồ từ **3 - 5 giây**. |
| **NFR02** | **Bảo mật (Security)** | • Mã hóa toàn bộ dữ liệu truyền tải qua **HTTPS/TLS 1.3**.<br>• Xác thực và phân quyền truy cập thông qua **JWT (JSON Web Token)** & OAuth 2.0.<br>• Mã hóa mật khẩu người dùng bằng thuật toán bcrypt/Argon2.<br>• Tuân thủ tiêu chuẩn PCI-DSS (không lưu trữ thông tin thẻ thanh toán nhạy cảm trên hệ thống CAB). |
| **NFR03** | **Độ tin cậy & Khả dụng (Availability)** | • Thời gian hoạt động của hệ thống (Uptime) đạt tối thiểu **99.9%** (24/7/365).<br>• Tự động sao lưu (Backup) cơ sở dữ liệu định kỳ 1 lần/ngày và lưu trữ tối thiểu 30 ngày. |
| **NFR04** | **Khả năng mở rộng (Scalability)** | • Kiến trúc Microservices/Modular Monolith hỗ trợ mở rộng chiều ngang (Horizontal Scaling).<br>• Đáp ứng tối thiểu **10,000 người dùng hoạt động đồng thời (DAU)** và xử lý **1,000 chuyến đi/phút** trong giờ cao điểm mà không gây gián đoạn. |
| **NFR05** | **Tính Dễ sử dụng (Usability)** | • Giao diện di động tối ưu cho thao tác 1 tay, thân thiện trên cả 2 nền tảng iOS và Android.<br>• Hiển thị thông báo trạng thái rõ ràng, hỗ trợ ngôn ngữ Tiếng Việt và Tiếng Anh. |

---

## 10. Data modeling 
**Mô hình Dữ liệu ERD**
```mermaid
erDiagram
    USERS ||--o{ TRIPS : "places (Customer)"
    USERS ||--o| DRIVER_PROFILES : "has profile (Driver)"
    DRIVER_PROFILES ||--o| VEHICLES : "drives"
    DRIVER_PROFILES ||--o{ TRIPS : "accepts (Driver)"
    TRIPS ||--|| PAYMENTS : "generates"
    TRIPS ||--o| RATINGS : "receives"

    USERS {
        bigint id PK
        string phone_number
        string password_hash
        string full_name
        string email
        string role
        string status
        timestamp created_at
    }

    DRIVER_PROFILES {
        bigint id PK
        bigint user_id FK
        string license_number
        string identity_card_number
        string status
        decimal rating_avg
        timestamp created_at
    }

    VEHICLES {
        bigint id PK
        bigint driver_id FK
        string license_plate
        string vehicle_type
        string model
        string color
    }

    TRIPS {
        bigint id PK
        bigint customer_id FK
        bigint driver_id FK
        string pickup_address
        decimal pickup_lat
        decimal pickup_lng
        string dropoff_address
        decimal dropoff_lat
        decimal dropoff_lng
        decimal fare_amount
        string status
        timestamp created_at
        timestamp completed_at
    }

    PAYMENTS {
        bigint id PK
        bigint trip_id FK
        decimal amount
        string payment_method
        string payment_status
        string transaction_id
        timestamp paid_at
    }

    RATINGS {
        bigint id PK
        bigint trip_id FK
        int score
        text comment
        timestamp created_at
    }
```
---

## 11. Use Cases 
*** Use Case Diagram

```mermaid
graph LR
    %% Actors
    KH["👤 Khách hàng"]
    TX["🚗 Tài xế"]
    NVVH["💻 Nhân viên Vận hành / Admin"]

    subgraph CAB_System [Hệ thống CAB System]
        %% MOD01: Account & Auth
        UC01("(UC01: Đăng ký, Đăng nhập & Phân quyền)")
        UC02("(UC02: Quản lý Hồ sơ & Phương tiện)")

        %% MOD02: Booking & Matching
        UC03("(UC03: Tạo Yêu cầu Đặt xe)")
        UC04("(UC04: Điều phối GPS & Nhận/Từ chối Chuyến)")

        %% MOD03: Trip Management
        UC05("(UC05: Cập nhật & Theo dõi Tiến trình Chuyến đi)")
        UC06("(UC06: Hủy chuyến đi)")
        UC07("(UC07: Tra cứu Lịch sử Chuyến đi)")

        %% MOD04: Pricing & Payment
        UC08("(UC08: Tính cước & Thanh toán Chuyến đi)")

        %% MOD05: Notification & Rating
        UC09("(UC09: Nhận Thông báo Push Notification)")
        UC10("(UC10: Đánh giá & Phản hồi Chuyến đi)")

        %% MOD06: Admin & Operations
        UC11("(UC11: Giám sát Vận hành & Xem Báo cáo)")
        UC12("(UC12: Quản lý Tài khoản & Can thiệp Hỗ trợ)")
    end

    %% Mối quan hệ Khách hàng
    KH --> UC01
    KH --> UC02
    KH --> UC03
    KH --> UC05
    KH --> UC06
    KH --> UC07
    KH --> UC08
    KH --> UC09
    KH --> UC10

    %% Mối quan hệ Tài xế
    TX --> UC01
    TX --> UC02
    TX --> UC04
    TX --> UC05
    TX --> UC06
    TX --> UC07
    TX --> UC08
    TX --> UC09

    %% Mối quan hệ NVVH / Admin
    NVVH --> UC01
    NVVH --> UC11
    NVVH --> UC12
```
---
## 12. Acceptance Criteria (Tiêu chí Chấp nhận - AC)

**Bảng Tiêu chí Chấp nhận theo Module**

| Mã FR | Tên Chức năng | Mã AC | Given (Điều kiện tiên quyết) | When (Hành động kích hoạt) | Then (Kết quả kỳ vọng) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **FR01.1** | Đăng ký, Đăng nhập & Phân quyền | **AC-FR01.1a** | Người dùng nhập SĐT chính xác trên giao diện Đăng ký/Đăng nhập. | Nhấn nút "Gửi mã OTP". | Hệ thống gửi mã OTP xác thực qua SMS/Notification thành công trong vòng 5 giây. |
| | | **AC-FR01.1b** | Mã OTP đã được gửi đến thiết bị người dùng. | Người dùng nhập mã OTP hợp lệ và nhấn "Xác nhận". | Hệ thống xác thực thành công, trả về JWT Token và đăng nhập người dùng vào đúng giao diện theo Role (Customer/Driver/Admin). |
| **FR01.2** | Quản lý Hồ sơ & Phương tiện | **AC-FR01.2a** | Khách hàng/Tài xế đã đăng nhập và mở trang Thông tin cá nhân. | Thay đổi thông tin (Họ tên, Email, Avatar) và nhấn "Lưu thay đổi". | Dữ liệu hồ sơ trong DB được cập nhật thành công và hiển thị ngay trên giao diện. |
| | | **AC-FR01.2b** | Tài xế đăng tải đầy đủ hình ảnh Bằng lái, Giấy tờ xe và Biển số xe. | Tài xế nhấn "Gửi hồ sơ xét duyệt". | Trạng thái tài khoản chuyển thành `PENDING_APPROVAL`; tài xế chưa thể bật trạng thái Sẵn sàng cho đến khi Admin phê duyệt. |
| **FR02.1** | Tạo Yêu cầu Đặt xe | **AC-FR02.1** | Khách hàng chọn xong Điểm đón, Điểm đến và loại phương tiện. | Khách hàng nhấn nút "Đặt xe". | Hệ thống tạo chuyến đi ở trạng thái `PENDING`, hiển thị đúng bản đồ lộ trình và cước phí tạm tính. |
| **FR02.2** | Định vị GPS & Điều phối Chuyến | **AC-FR02.2a** | Có chuyến đi mới ở trạng thái `PENDING`. | Thuật toán điều phối của hệ thống được kích hoạt. | Hệ thống quét bán kính 3km (mở rộng tối đa 5km) và gửi thông báo nhận chuyến kèm đếm ngược 15s tới Tài xế Sẵn sàng gần nhất. |
| | | **AC-FR02.2b** | Tài xế nhận đề xuất chuyến đi nhưng không bấm chọn hoặc từ chối sau 15s. | Đồng hồ đếm ngược chạm mốc 0s hoặc Tài xế bấm "Từ chối". | Hệ thống tự động chuyển tiếp yêu cầu đặt xe tới tài xế phù hợp tiếp theo trong danh sách. |
| **FR03.1** | Cập nhật & Theo dõi Chuyến đi | **AC-FR03.1a** | Tài xế đã chấp nhận chuyến đi (`ACCEPTED`). | Tài xế nhấn lần lượt các nút trạng thái trên App. | Trạng thái chuyến đi trong hệ thống cập nhật đúng tiến trình: `ARRIVED` (Đã đến) $\rightarrow$ `IN_PROGRESS` (Đã đón/Đang di chuyển) $\rightarrow$ `COMPLETED` (Hoàn thành). |
| | | **AC-FR03.1b** | Chuyến đi đang ở trạng thái `IN_PROGRESS`. | App Tài xế truyền dữ liệu GPS định kỳ mỗi 3–5 giây. | Giao diện Khách hàng hiển thị chính xác vị trí tài xế di chuyển mượt mà trên bản đồ kèm ETA cập nhật liên tục. |
| **FR03.2** | Hủy chuyến đi | **AC-FR03.2** | Chuyến đi ở trạng thái `PENDING` hoặc `ACCEPTED`. | Khách hàng hoặc Tài xế nhấn "Hủy chuyến" và chọn lý do hủy. | Chuyến đi chuyển trạng thái `CANCELLED`, giải phóng trạng thái sẵn sàng cho các bên và áp dụng chính sách phí phạt hủy chuyến (nếu có). |
| **FR03.3** | Lịch sử Chuyến đi | **AC-FR03.3** | Người dùng truy cập tab "Lịch sử chuyến đi". | Chọn một chuyến đi bất kỳ trong danh sách. | Màn hình hiển thị đầy đủ thông tin: Mã chuyến, Điểm đón/trả, Ngày giờ, Giá tiền, Phương thức thanh toán và Trạng thái chuyến. |
| **FR04.1** | Tự động Tính cước & Thanh toán | **AC-FR04.1a** | Tài xế nhấn "Hoàn thành chuyến đi" tại điểm đến. | Hệ thống chốt quãng đường di chuyển thực tế. | Tổng cước phí được tự động tính toán chính xác theo công thức và hiển thị lên màn hình của cả Khách hàng và Tài xế. |
| | | **AC-FR04.1b** | Khách hàng chọn thanh toán Tiền mặt hoặc Thanh toán qua Cổng điện tử. | Tài xế xác nhận nhận tiền mặt HOẶC Cổng thanh toán trả kết quả giao dịch thành công. | Trạng thái thanh toán chuyển thành `PAID`, hệ thống trích xuất % chiết khấu tài xế và gửi hóa đơn điện tử cho khách hàng. |
| **FR05.1** | Push Notification | **AC-FR05.1** | Trạng thái chuyến đi có sự thay đổi (đã nhận chuyến, đã đến, hoàn thành, hủy chuyến). | Sự kiện thay đổi trạng thái phát sinh trên server. | Thiết bị của Khách hàng/Tài xế nhận được Push Notification tương ứng tức thì với độ trễ dưới 2 giây. |
| **FR05.2** | Đánh giá Chuyến đi | **AC-FR05.2** | Chuyến đi hoàn thành (`COMPLETED`) và khách hàng mở màn hình Đánh giá. | Khách hàng chọn số sao (1-5) và nhập nhận xét rồi bấm "Gửi". | Điểm đánh giá được ghi nhận vào DB, tính lại điểm `rating_avg` cho Tài xế; nếu đánh giá $\le$ 2 sao, hệ thống tự động tạo cảnh báo hỗ trợ. |
| **FR06.1** | Giám sát & Báo cáo Vận hành | **AC-FR06.1a** | NVVH mở màn hình "Giám sát Vận hành" trên Admin Portal. | Đăng nhập hệ thống quản trị. | Bản đồ hiển thị toàn bộ các chuyến đi đang diễn ra theo thời gian thực và tự động cảnh báo đỏ đối với các chuyến mất GPS trên 3 phút. |
| | | **AC-FR06.1b** | Admin chọn khoảng thời gian báo cáo và bấm "Xuất báo cáo". | Yêu cầu kết xuất báo cáo được gửi. | Hệ thống tạo và tải xuống file (Excel/PDF) thống kê chi tiết tổng doanh thu, số lượng chuyến đi, tỷ lệ hủy và chiết khấu. |
| **FR06.2** | Khóa/Mở tài khoản & Hỗ trợ | **AC-FR06.2** | Quản trị viên chọn một tài khoản tài xế vi phạm hoặc một chuyến đi đang gặp sự cố/kẹt. | Thực hiện hành động "Khóa tài khoản" hoặc "Hủy chuyến thủ công" kèm nhập lý do. | Trạng thái tài khoản/chuyến đi được cập nhật lập tức, thông báo gửi tới người dùng và toàn bộ thao tác được lưu vết vào Audit Log. |
---

## 13. Traceability Matrix (Bảng Truy vết Nghiệp vụ & Kỹ thuật)

Bảng truy vết đảm bảo tính khép kín và nhất quán từ Mục tiêu Kinh doanh (BG) cho đến Tiêu chí Nghiệm thu (AC):

| Mã BG | Mã BR | Mã BPM (Quy trình) | Mã FR | Mã UC | Mã AC |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **BG01** | **BR01** | **BPM6.4** (Onboarding) | **FR01.1** | UC01 | **AC-FR01.1a, AC-FR01.1b** |
| | **BR02** | **BPM6.1** (Đặt xe & Điều phối) | **FR02.2** | UC04 | **AC-FR02.2a, AC-FR02.2b** |
| **BG02** | **BR02** | **BPM6.1** (Đặt xe & Điều phối) | **FR02.1** | UC03 | **AC-FR02.1** |
| | | **BPM6.1** (Đặt xe & Điều phối) | **FR02.2** | UC04 | **AC-FR02.2a, AC-FR02.2b** |
| | **BR03** | **BPM6.5** (Hủy chuyến) | **FR03.2** | UC06 | **AC-FR03.2** |
| **BG03** | **BR03** | **BPM6.2** (Thực hiện chuyến) | **FR03.1** | UC05 | **AC-FR03.1a, AC-FR03.1b** |
| | | **BPM6.2** (Thực hiện chuyến) | **FR03.3** | UC07 | **AC-FR03.3** |
| | **BR04** | **BPM6.2** (Thực hiện & Thanh toán) | **FR04.1** | UC08 | **AC-FR04.1a, AC-FR04.1b** |
| | **BR06** | **BPM6.2** (Thực hiện chuyến) | **FR05.2** | UC10 | **AC-FR05.2** |
| **BG04** | **BR01** | **BPM6.4** (Onboarding) | **FR01.2** | UC02 | **AC-FR01.2a, AC-FR01.2b** |
| | **BR02** | **BPM6.1** (Đặt xe & Điều phối) | **FR02.2** | UC04 | **AC-FR02.2a** |
| | **BR03** | **BPM6.2** (Thực hiện chuyến) | **FR03.1** | UC05 | **AC-FR03.1a** |
| | **BR04** | **BPM6.2** (Thực hiện & Thanh toán) | **FR04.1** | UC08 | **AC-FR04.1a, AC-FR04.1b** |
| **BG05** | **BR05** | **BPM6.6** (Can thiệp & Vận hành) | **FR06.1** | UC11 | **AC-FR06.1a** |
| | | **BPM6.6** (Can thiệp & Vận hành) | **FR06.2** | UC12 | **AC-FR06.2** |
| | **BR06** | **BPM6.6** (Đối soát & Báo cáo) | **FR06.1** | UC11 | **AC-FR06.1b** |
| **BG06** | **BR01** | **BPM6.4** (Onboarding) | **FR01.1** | UC01 | **AC-FR01.1a, AC-FR01.1b** |
| | **BR02, BR03** | **BPM6.1, BPM6.2** (Các luồng chính) | **FR05.1** | UC09 | **AC-FR05.1** |
