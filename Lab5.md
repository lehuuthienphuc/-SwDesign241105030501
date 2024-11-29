# Thiết Kế Hệ Thống Con trong Payroll System

Dựa trên các ca sử dụng và yêu cầu hệ thống, Payroll System được chia thành các hệ thống con (subsystems) để quản lý hiệu quả và tăng khả năng mở rộng.

---

## **1. Timecard Management Subsystem**
### **Chức năng chính**
- Ghi chép và quản lý thông tin thời gian làm việc của nhân viên.

### **Ca sử dụng liên quan**
- Ghi chép thời gian làm việc (Record Timecard).

### **Thành phần chính**
- **Timecard Entry Module**: Nhận và lưu thông tin thời gian làm việc từ nhân viên.
- **Validation Module**: Kiểm tra tính hợp lệ của dữ liệu nhập (số giờ, mã dự án).
- **Database Interface**: Kết nối và lưu dữ liệu vào cơ sở dữ liệu.

### **Dữ liệu quản lý**
- **Timecard**: 
  - *employee_id*
  - *project_id*
  - *hours_worked*
  - *date*

---

## **2. Payroll Calculation Subsystem**
### **Chức năng chính**
- Tính toán và tạo phiếu lương cho nhân viên dựa trên thời gian làm việc và các chính sách.

### **Ca sử dụng liên quan**
- Tạo phiếu lương (Generate Paycheck).

### **Thành phần chính**
- **Payroll Rules Engine**: Áp dụng các quy tắc tính lương (lương cơ bản, giờ làm thêm, hoa hồng).
- **Timecard Integration Module**: Lấy thông tin từ **Timecard Management Subsystem**.
- **Paycheck Generator**: Tạo phiếu lương dưới dạng tệp hoặc bản ghi.

### **Dữ liệu quản lý**
- **Paycheck**: 
  - *employee_id*
  - *basic_salary*
  - *overtime_pay*
  - *commission*
  - *total_salary*

---

## **3. Payment Processing Subsystem**
### **Chức năng chính**
- Xử lý thanh toán lương qua ngân hàng hoặc dịch vụ in ấn.

### **Ca sử dụng liên quan**
- Xử lý thanh toán (Process Payment).

### **Thành phần chính**
- **Bank Interface Module**: Kết nối và gửi yêu cầu thanh toán tới hệ thống ngân hàng.
- **Print Service Interface**: Tạo lệnh in cho phiếu lương.
- **Error Handling Module**: Xử lý các lỗi liên quan đến giao dịch ngân hàng hoặc in ấn.

### **Dữ liệu quản lý**
- **Payment Record**: 
  - *employee_id*
  - *amount*
  - *payment_method*
  - *status*

---

## **4. Employee Management Subsystem**
### **Chức năng chính**
- Quản lý thông tin nhân viên trong hệ thống.

### **Ca sử dụng liên quan**
- Quản lý thông tin nhân viên (Manage Employee Information).

### **Thành phần chính**
- **Employee CRUD Module**: Cung cấp chức năng thêm, sửa, xóa, và đọc thông tin nhân viên.
- **Access Control Module**: Đảm bảo chỉ quản trị viên mới có quyền thay đổi dữ liệu.
- **Database Interface**: Lưu trữ thông tin nhân viên trong cơ sở dữ liệu.

### **Dữ liệu quản lý**
- **Employee**: 
  - *employee_id*
  - *name*
  - *address*
  - *role*
  - *salary_type*
  - *bank_account*

---

## **5. Reporting Subsystem**
### **Chức năng chính**
- Tạo báo cáo cho quản trị viên và nhân viên.

### **Ca sử dụng liên quan**
- Xem báo cáo cá nhân (View Personal Report).
- Tạo báo cáo quản trị (Generate Administrative Reports).

### **Thành phần chính**
- **Report Generator**: Xử lý và tạo báo cáo theo yêu cầu.
- **Visualization Module**: Hiển thị báo cáo dưới dạng bảng hoặc biểu đồ.
- **Data Aggregation Module**: Tích hợp dữ liệu từ các hệ thống con khác.

### **Dữ liệu quản lý**
- **Report**: 
  - *report_type*
  - *employee_id*
  - *time_period*
  - *summary_data*

---

## **6. Integration Subsystem**
### **Chức năng chính**
- Kết nối Payroll System với các hệ thống bên ngoài.

### **Ca sử dụng liên quan**
- Cơ sở dữ liệu quản lý dự án (Project Management Database).
- Hệ thống ngân hàng (Bank System).

### **Thành phần chính**
- **Project Management Integration**: Truy xuất thông tin dự án từ hệ thống DB2.
- **Bank API Adapter**: Kết nối với API của ngân hàng.
- **Data Transformation Module**: Đảm bảo dữ liệu phù hợp định dạng giữa các hệ thống.

---

## **Tổng Hợp Kiến Trúc Hệ Thống**
Hệ thống được thiết kế theo mô hình **Microservices** hoặc **Modular Architecture**, trong đó mỗi hệ thống con hoạt động độc lập và giao tiếp thông qua API hoặc các giao thức được định nghĩa trước.

### **Các thành phần chính**
1. **Frontend Layer**: Giao diện người dùng (Windows desktop interface).
2. **Backend Layer**: Các hệ thống con đã được thiết kế.
3. **Database Layer**: Quản lý dữ liệu cho toàn bộ hệ thống.
4. **External Systems**: Tích hợp ngân hàng và cơ sở dữ liệu DB2.

---

## **Lý Do Thiết Kế**
1. **Tính rõ ràng**: Các chức năng được chia nhỏ, giúp quản lý dễ dàng hơn.
2. **Khả năng mở rộng**: Dễ dàng bổ sung hoặc chỉnh sửa các hệ thống con khi yêu cầu thay đổi.
3. **Tính độc lập**: Hạn chế sự phụ thuộc giữa các hệ thống con, giúp giảm thiểu lỗi khi bảo trì.
4. **Khả năng tích hợp**: Tích hợp linh hoạt với hệ thống hiện có (DB2, ngân hàng).

