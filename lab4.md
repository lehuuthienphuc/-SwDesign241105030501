# Hệ thống bảng lương

## I. Xác định tác nhân (Actor)
### Các tác nhân chính:
1. **Nhân viên (Employee):**
   - Ghi chép thời gian làm việc.
   - Kiểm tra thông tin cá nhân và nhận bảng lương.

2. **Quản trị viên bảng lương (Payroll Administrator):**
   - Quản lý thông tin nhân viên.
   - Tạo phiếu lương và báo cáo quản trị.

3. **Hệ thống ngân hàng (Bank System):**
   - Xử lý chuyển khoản tiền lương cho nhân viên.

4. **Dịch vụ in ấn (Print Service):**
   - Hỗ trợ in phiếu lương và báo cáo.

5. **Cơ sở dữ liệu quản lý dự án (Project Management Database):**
   - Cung cấp thông tin về dự án để hỗ trợ tính toán lương.

---

## II. Xác định chức năng (Use Case)
### Danh sách các chức năng chính:
1. Ghi chép thời gian làm việc (Record Timecard).
2. Tạo phiếu lương (Generate Paycheck).
3. Xử lý thanh toán (Process Payment).
4. Xem báo cáo cá nhân (View Personal Report).
5. Quản lý thông tin nhân viên (Manage Employee Information).
6. Tạo báo cáo quản trị (Generate Administrative Reports).

---

## III. Mô tả sơ bộ các ca sử dụng
### **Use Case 1: Ghi chép thời gian làm việc (Record Timecard)**
- **Tác nhân:** Nhân viên.
- **Mục tiêu:** Lưu trữ thông tin thời gian làm việc của nhân viên để sử dụng trong tính lương.
- **Quy trình:**
  1. Nhân viên đăng nhập vào hệ thống.
  2. Chọn chức năng "Ghi chép thời gian làm việc".
  3. Nhập thông tin về số giờ làm việc, mã dự án.
  4. Lưu thông tin vào cơ sở dữ liệu.

### **Use Case 2: Tạo phiếu lương (Generate Paycheck)**
- **Tác nhân:** Quản trị viên bảng lương.
- **Mục tiêu:** Tính toán và tạo phiếu lương cho nhân viên.
- **Quy trình:**
  1. Quản trị viên đăng nhập vào hệ thống.
  2. Chọn chức năng "Tạo phiếu lương".
  3. Hệ thống lấy dữ liệu từ các thời gian làm việc và thông tin dự án từ cơ sở dữ liệu.
  4. Tính toán lương bao gồm: lương cơ bản, giờ làm thêm, và hoa hồng (nếu có).
  5. Lưu phiếu lương vào cơ sở dữ liệu.

### **Use Case 3: Xử lý thanh toán (Process Payment)**
- **Tác nhân:** Hệ thống ngân hàng, dịch vụ in ấn.
- **Mục tiêu:** Thanh toán tiền lương cho nhân viên qua chuyển khoản hoặc phiếu lương in.
- **Quy trình:**
  1. Lấy thông tin từ phiếu lương.
  2. Nếu thanh toán qua ngân hàng, hệ thống gửi yêu cầu chuyển khoản đến ngân hàng.
  3. Nếu thanh toán trực tiếp, hệ thống gửi phiếu lương đến dịch vụ in.

### **Use Case 4: Xem báo cáo cá nhân (View Personal Report)**
- **Tác nhân:** Nhân viên.
- **Mục tiêu:** Cho phép nhân viên kiểm tra thông tin cá nhân về giờ làm việc và lương.
- **Quy trình:**
  1. Nhân viên đăng nhập vào hệ thống.
  2. Chọn chức năng "Xem báo cáo cá nhân".
  3. Hệ thống hiển thị báo cáo chi tiết.

### **Use Case 5: Quản lý thông tin nhân viên (Manage Employee Information)**
- **Tác nhân:** Quản trị viên bảng lương.
- **Mục tiêu:** Thêm, sửa hoặc xóa thông tin nhân viên trong cơ sở dữ liệu.
- **Quy trình:**
  1. Quản trị viên đăng nhập vào hệ thống.
  2. Chọn chức năng "Quản lý nhân viên".
  3. Thực hiện các thao tác thêm, sửa hoặc xóa.

### **Use Case 6: Tạo báo cáo quản trị (Generate Administrative Reports)**
- **Tác nhân:** Quản trị viên bảng lương.
- **Mục tiêu:** Tạo báo cáo tổng hợp phục vụ quản trị.
- **Quy trình:**
  1. Quản trị viên chọn loại báo cáo cần tạo.
  2. Hệ thống xử lý dữ liệu và tạo báo cáo.

---

## IV. Biểu đồ ca sử dụng (Use Case Diagram)
![Use Case Diagram](https://www.planttext.com/api/plantuml/png/V98xJWCn48PxdsAqVGf2ae82XV0I1LAK0Ft87eZ9sbwDdQ0z6mL7uWfuizxrYaJfxFc_UVWV_tx_p7r03ZjJ2fJ1CToRgdGrKRekiMPNbZVAQAjzO8p192tGRjUr3sGwbhKDQ-Azbdqwkq-IuHajVf0X6-uMGkmyIVG4nOgaOmKlsiG0gmBGm-ljHGOUoL9iISqOSaDocv1nHc87ITutH5C_0PSPUDFq1KjYxooMiABASKTDCjLEsByUdkoxOuD1EvlWwOcn1hReFQNYFYNCXEZBZKRNXvVz2qp4AN-JE3udJi-9Cn6p3-Uy8xZANYdDSIcWuhXUXwAdXmji-NY7glD-m1rjjS4VACWDLAq8EZfOY3bPrNokFm000F__0m00)

---

## V. Lý do thiết kế
1. **Đáp ứng yêu cầu bài toán:**
   - Các ca sử dụng được xây dựng dựa trên các chức năng chính mà hệ thống yêu cầu, đảm bảo rằng mọi quy trình được mô phỏng và quản lý.

2. **Hỗ trợ nhiều tác nhân:**
   - Hệ thống được thiết kế để hỗ trợ tất cả các bên liên quan (nhân viên, quản trị viên, hệ thống ngân hàng, máy in, v.v.).

3. **Tính linh hoạt và mở rộng:**
   - Mỗi ca sử dụng có thể dễ dàng mở rộng thêm các tính năng hoặc tích hợp với hệ thống khác.

4. **Tăng hiệu quả quản lý:**
   - Cung cấp các chức năng tự động hóa như tính lương, tạo báo cáo, và thanh toán giúp giảm tải công việc quản trị viên.

5. **Thân thiện với người dùng:**
   - Hệ thống đơn giản hóa quy trình cho nhân viên và quản trị viên, hỗ trợ truy cập và cập nhật thông tin nhanh chóng.
