# Tài Liệu Phân Tích Hệ Thống "Payroll System"

## 1. Phân Tích Kiến Trúc

### Đề xuất kiến trúc
**Kiến trúc hướng dịch vụ (SOA)**

### Lý do lựa chọn
- Tính linh hoạt và khả năng mở rộng.
- Dễ dàng tích hợp với hệ thống hiện tại.
- Quản lý phân tán và bảo mật hiệu quả.
- Tái sử dụng dịch vụ cho các yêu cầu khác nhau.

### Ý Nghĩa Từng Thành Phần Trong Kiến Trúc

#### Employee Service (Dịch vụ quản lý nhân viên)
- **Chức năng**: Quản lý thông tin cá nhân của nhân viên (tên, địa chỉ, thông tin thanh toán, loại nhân viên: theo giờ, lương cố định, có hoa hồng).
- **Ý nghĩa**: Là dịch vụ cốt lõi để lưu trữ và xử lý thông tin cơ bản của toàn bộ nhân viên trong công ty.

#### Timecard Service (Dịch vụ quản lý timecard)
- **Chức năng**: Cho phép nhân viên nhập và lưu trữ thông tin về số giờ làm việc, charge numbers, thời gian làm việc.
- **Ý nghĩa**: Đảm bảo rằng tất cả các dữ liệu liên quan đến thời gian làm việc được ghi lại chính xác để phục vụ tính toán lương.

#### Payroll Service (Dịch vụ xử lý bảng lương)
- **Chức năng**: Xử lý tính lương cho từng loại nhân viên và tạo các bản sao kê lương.
- **Ý nghĩa**: Đóng vai trò chính trong hệ thống, đảm bảo tính toán chính xác và phát lương đúng hạn.

#### Report Service (Dịch vụ báo cáo)
- **Chức năng**: Cung cấp báo cáo về tổng số giờ làm việc, lương đã nhận, thời gian nghỉ còn lại.
- **Ý nghĩa**: Giúp nhân viên dễ dàng truy vấn thông tin về thu nhập và tình trạng làm việc của họ.

#### Project Management Integration Service (Dịch vụ tích hợp quản lý dự án)
- **Chức năng**: Tích hợp với cơ sở dữ liệu DB2 để lấy thông tin về dự án và charge numbers.
- **Ý nghĩa**: Kết nối hệ thống bảng lương mới với hệ thống quản lý dự án cũ mà không cần thay đổi cơ sở dữ liệu.

#### Payment Method Service (Dịch vụ phương thức thanh toán)
- **Chức năng**: Quản lý các tùy chọn thanh toán như chuyển khoản, gửi qua bưu điện, nhận trực tiếp.
- **Ý nghĩa**: Đảm bảo rằng hệ thống xử lý thanh toán linh hoạt theo yêu cầu của nhân viên.

#### Security Service (Dịch vụ bảo mật)
- **Chức năng**: Quản lý quyền truy cập để đảm bảo an toàn dữ liệu.
- **Ý nghĩa**: Bảo vệ dữ liệu và phân quyền hợp lý cho từng nhóm nhân viên.

### Biểu Đồ Package
![Diagram](https://www.planttext.com/api/plantuml/png/Z5H1RjGm5Dtd55-p0HRTS03KJe8AObeL6bLiZSTCGXCxift527N1YaLN725K5GXfL91O9K9THEezV0Akm4-6feadddQLI7x_lUVt__VVwdfNQI9rdYPUHkWfMJ2OXARynXUm7nC1GMogptm27pq0cX2bO6AgxtWQcEeIFuTH_PN3ILp_G11Hy3pD4h5aB63gL8jiBylk2dk4y3etvGM7K9hg76OtFsyAlcW9ZiXIYYJPcwSnZvMMH0lvacictnFAl3DlmoOQEQSHdA2VjSqEq3iP-cnGdQl_JcRr7-Tb3WX7GebLPov-FpBbPGf-_RkvXqjWY4A5C4uP9NB-08MmNl7eBgg1n5jJhLg1aIIFfA1CAR6LV5eN0cqLmYB6ZF6WTugyRrWcfDvddBNDkSSp_humrKK6lHWGyWlgJtOdNfdoMiEXgRx444oVjcBuzGNdZDwd515C9nHriQM_0z0wePHn_O3mfyWXuC2KA-sc7u2G_fZHNCPwsUSV6U1GvalmiIfhWhc2MRCX-M3b_EDWvbureiaxefW5TywQ0t_R57YCcJ-v3H-dvmE6tzMW_qSGhgSCT5rGMA3TAmAq-TVjZRpDHm1sTfvjh9C3Pk-40sQFuTQ7OrJVNf1HzL6GDJXMpK2iIswKQ0DbtMfWgGFrbw95Z3Hgb_5vywh_0m00__y30000)

## 2. Cơ chế phân tích

Để giải quyết bài toán thiết kế hệ thống bảng lương, chúng ta cần đề xuất và phân tích một số cơ chế quan trọng:

### Cơ chế quản lý quyền truy cập
- **Lý do**: Hệ thống yêu cầu đảm bảo rằng nhân viên chỉ có thể truy cập và chỉnh sửa thông tin cá nhân của họ (như timecard và phương thức thanh toán). Các tác vụ như thêm mới, xóa hoặc cập nhật thông tin nhân viên chỉ có thể được thực hiện bởi Payroll Administrator.
- **Cơ chế**: Sử dụng các cơ chế phân quyền (role-based access control) để giới hạn quyền truy cập dựa trên vai trò của người dùng. Hệ thống sẽ có các cấp quyền khác nhau cho từng nhóm người dùng.

### Cơ chế tính toán lương
- **Lý do**: Có nhiều loại nhân viên (theo giờ, lương cố định, có hoa hồng), mỗi loại nhân viên có cách tính lương khác nhau. Nhân viên làm thêm giờ cần được trả lương theo mức 1.5 lần so với lương cơ bản.
- **Cơ chế**: Xây dựng một lớp hoặc dịch vụ chuyên xử lý tính toán lương (PayrollProcessor), với các thuật toán khác nhau cho từng loại nhân viên.

### Cơ chế ghi nhận và quản lý timecard
- **Lý do**: Nhân viên cần ghi nhận giờ làm việc của mình hàng ngày. Dữ liệu này được sử dụng để tính toán lương và đánh giá hiệu quả công việc.
- **Cơ chế**: Xây dựng dịch vụ ghi nhận timecard (TimecardService), cho phép lưu trữ thông tin giờ làm việc, charge number, và các thuộc tính khác.

### Cơ chế tích hợp với hệ thống quản lý dự án cũ (DB2)
- **Lý do**: Hệ thống mới cần tích hợp với cơ sở dữ liệu DB2 cũ để lấy thông tin dự án và charge numbers.
- **Cơ chế**: Xây dựng lớp tích hợp (DB2Connector) để giao tiếp với cơ sở dữ liệu DB2 bằng các giao thức tương thích, đảm bảo dữ liệu được lấy ra một cách chính xác và không làm ảnh hưởng đến hệ thống hiện có.

### Cơ chế báo cáo
- **Lý do**: Nhân viên cần khả năng truy vấn các báo cáo như tổng số giờ làm việc, tổng lương đã nhận, thời gian nghỉ phép còn lại, v.v.
- **Cơ chế**: Tạo các lớp hoặc dịch vụ tạo báo cáo (ReportService), nơi các báo cáo được sinh ra từ dữ liệu timecard và lương.

### Cơ chế thanh toán tự động
- **Lý do**: Hệ thống cần tự động thực hiện các quy trình thanh toán vào mỗi thứ 6 và ngày làm việc cuối cùng của tháng mà không cần sự can thiệp thủ công.
- **Cơ chế**: Xây dựng lớp quản lý thanh toán (PaymentManager) đảm bảo xử lý thanh toán đúng thời gian và theo phương thức đã được nhân viên lựa chọn.

## 3. Phân tích ca sử dụng "Payment"

### Lớp phân tích
- **Nhân viên**: Lưu thông tin cá nhân và phương thức thanh toán.
- **Bộ xử lý lương**: Tính toán lương dựa trên loại hình nhân viên.
- **Quản lý thanh toán**: Xử lý và gửi thanh toán.
- **Ngân hàng**: Xử lý thanh toán qua chuyển khoản.

### Biểu đồ Sequence:
  ![Diagram] (https://www.planttext.com/api/plantuml/png/T98nQiD044LxdM8ku0ke22Ofui8O0Y8uvKOntWLbf2YpXqddJOg0GU32bOH9CU1xx0boXSpQmRBmkfx_t_m_p6_tCtudLPDzBHALKrd3JFCdFXfUOrB9mEIcKaXmwxkFkU-QAU-c-ytUuN8mVh2-_K8PPbgXpafsG_jiATG9hyIMz1jWT1C1f_34QmkvRxyj43UeeVXVUIaEYCZo5Ev5Pe0qRqL41a-CY3f0-eGfX1LGy4xi8W4wQDwi0WmYq8SUlG56rqBCsUM0shSDdhFY6QuSuqxSrH52GBLlGslfvSm06JjDg7KwTWhPyHZFx4hGfIGFc5KWd7762tm9t_07003__mC0)

### Biểu đồ phân tích:
![Diagram]
(https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9Vnk55UM6PXrVbALHpAIWeb01P8Fh8n8UxknCLaZCUxku4yGioZcqujZ0lFGGei38v92CnBoCa__32FAvQBgX9JWztpunuk7kjp-6zFX2rC1FNvcL0HJGGrcaYT0QMFjorE0-e3s4iH6i5n3Y4C7RzVkb0GO_32s0sGhKvPvHMFjpTdEUTaGyo7rqlaizrTUsmE9yBYuz0Ah4ubmkR5q1g4KxZSaZDIm65Em000F__0m00)
## 4. Phân tích ca sử dụng "Maintain Timecard"

### Lớp phân tích:
- **Nhân viên:** Ghi nhận và cập nhật thời gian làm việc.
- **Dịch vụ timecard:** Xử lý việc lưu trữ và truy xuất thông tin timecard.
- **Quản lý thời gian làm việc:** Đảm bảo thông tin được ghi nhận đúng và chính xác.

### Biểu đồ Sequence:
 ![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aO9Vnk55UM6PXrVbSHK09JAJCmiIyqeK0aiVxbgSvtDuRqXcRcfoOb4AYgpJmzqp8nxkNWkKzpcsuTZ2l7GkBeH12hfscFgj5DmpCXNoCXxkMfkda9xvSFTSXPp32t8Loe3CzcGk3FKAka1J46PQAKGSNfWCqtzauk752Zd7DfHoORe4X-q-3tSjhLGeoJYy1QYa93CFYA4Umsurfi5M2Y55fPKFTpVcAQGytBrU8GVaybA4EGwfUIcWS0K0003__mC0)
### Biểu đồ phân tích:
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9Vnk55UM6PXrVbALHpAIWeb01P83ep1SpBp4rDJYnAuQhbWgeFB7suQt6Up-6z8L0fgBQCmwjoOK8Q24CrGP8v3tSjhSGg2JVMwU7kcH4FTwy56knpRCEnXNdfCEUipSk0Yg3hH7AwhguTfikuCDqAKeTf5PT3QbuAA4W00000__y30000)

---

## 5. Hợp nhất kết quả phân tích:
### Biểu đồ tổng hợp:
  ![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niO9Vnk55UM6PXrVbALHpAIWeb01P8Fh8n8UxknCLaZCUxku4yGioZcqujZ0lFGGei38v92CnBoCa__12iDgIpDpKvCIY5AvQBgYfJWztpunuk7kjp-6zFX1zCDFNvcL0HJGGLciYT0QMFjorE0-e3s45H6i5n3Y4C27zK4T1BSuul2eN9eIY4oYPyt3Nqagiad1Z_TA1WXw75y0y0dMDSqPfvSFTpNdU6VaWQz7r8WMkhguTbb11Lu7XUYui8Ocg414Js88Ef1RXTYw7rBmKKDm30000__y30000)
### Tổng kết
Hệ thống bảng lương của Acme, Inc. đã được phân tích và thiết kế dựa trên các yêu cầu cụ thể của công ty. Các cơ chế và kiến trúc được đề xuất sẽ đảm bảo rằng hệ thống có thể hoạt động hiệu quả, linh hoạt, và dễ dàng tích hợp với các hệ thống hiện có.

### Lợi ích
- **Quản lý thời gian và lương hiệu quả.**
- **Tăng cường độ chính xác trong tính toán lương.**
- **Cung cấp thông tin báo cáo nhanh chóng cho nhân viên.**
- **Đảm bảo an toàn dữ liệu và bảo mật thông tin.**


