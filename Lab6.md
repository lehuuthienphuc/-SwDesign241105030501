
# **Chi tiết các lớp với 4 tiêu chí phân tích**

## 1. **Employee (Nhân viên)**

### **1.1 Xác định các operations và methods**
- `viewPersonalDetails()`: Hiển thị thông tin cá nhân.
- `updateContactInfo(newContact: String)`: Cập nhật thông tin liên lạc.
- `assignPaymentMethod(method: String)`: Gán phương thức thanh toán.

### **1.2 Xác định trạng thái và sự thay đổi trạng thái**
- Trạng thái:  
  - `Active`: Nhân viên đang làm việc.  
  - `OnLeave`: Nhân viên đang nghỉ phép.  
  - `Inactive`: Nhân viên không còn làm việc.
- Sự thay đổi:
  - Khi nghỉ phép -> chuyển từ `Active` sang `OnLeave`.
  - Khi nghỉ việc -> chuyển từ `Active` hoặc `OnLeave` sang `Inactive`.

### **1.3 Xác định thuộc tính và mô tả rõ ràng**
- `employeeId` (String): Mã nhân viên duy nhất.
- `name` (String): Tên nhân viên.
- `position` (String): Vị trí công việc.
- `department` (String): Phòng ban.
- `contact` (String): Số điện thoại hoặc email.
- `paymentMethod` (String): Phương thức thanh toán (VD: Chuyển khoản, tiền mặt).

### **1.4 Xác định phụ thuộc và quan hệ kết hợp**
- Liên kết với `Timecard`: Một nhân viên có thể có nhiều bảng chấm công.
- Liên kết với `Payroll`: Một nhân viên có nhiều bảng lương.
- Liên kết với `Payment`: Thông tin nhân viên được dùng để thực hiện thanh toán.

---

## 2. **Timecard (Bảng chấm công)**

### **2.1 Xác định các operations và methods**
- `recordTime(employeeId: String, date: Date, hours: Double)`: Ghi nhận giờ làm việc.
- `getTimeDetails(employeeId: String, date: Date)`: Lấy thông tin giờ làm việc.

### **2.2 Xác định trạng thái và sự thay đổi trạng thái**
- Trạng thái:  
  - `Pending`: Bảng chấm công chưa hoàn tất.  
  - `Completed`: Đã ghi nhận đủ thông tin.
- Sự thay đổi:
  - Khi nhân viên cập nhật đủ giờ làm việc -> chuyển từ `Pending` sang `Completed`.

### **2.3 Xác định thuộc tính và mô tả rõ ràng**
- `timecardId` (String): Mã bảng chấm công.
- `employeeId` (String): Mã nhân viên liên quan.
- `projectId` (String): Mã dự án (nếu có).
- `date` (Date): Ngày làm việc.
- `hoursWorked` (Double): Số giờ làm việc.

### **2.4 Xác định phụ thuộc và quan hệ kết hợp**
- Liên kết với `Employee`: Một bảng chấm công thuộc về một nhân viên duy nhất.
- Dùng bởi `Payroll` để tính lương dựa trên giờ làm việc.

---

## 3. **Payroll (Bảng lương)**

### **3.1 Xác định các operations và methods**
- `calculateNetSalary()`: Tính toán lương thực nhận.
- `generatePaycheck(employeeId: String)`: Tạo phiếu lương.

### **3.2 Xác định trạng thái và sự thay đổi trạng thái**
- Trạng thái:  
  - `Draft`: Bảng lương đang được tính toán.  
  - `Finalized`: Bảng lương đã hoàn thành và không thể chỉnh sửa.  
  - `Paid`: Lương đã được thanh toán.
- Sự thay đổi:
  - Sau khi hoàn thành tính toán -> chuyển từ `Draft` sang `Finalized`.
  - Sau khi thanh toán xong -> chuyển từ `Finalized` sang `Paid`.

### **3.3 Xác định thuộc tính và mô tả rõ ràng**
- `payrollId` (String): Mã bảng lương.
- `employeeId` (String): Mã nhân viên liên quan.
- `basicSalary` (Double): Lương cơ bản.
- `overtimeHours` (Double): Số giờ làm thêm.
- `bonus` (Double): Thưởng.
- `deductions` (Double): Khấu trừ.
- `netSalary` (Double): Lương thực nhận sau tính toán.

### **3.4 Xác định phụ thuộc và quan hệ kết hợp**
- Liên kết với `Employee`: Mỗi bảng lương thuộc về một nhân viên.
- Liên kết với `Payment`: Thông tin từ bảng lương được dùng để thực hiện thanh toán.

---

## 4. **Payment (Thanh toán)**

### **4.1 Xác định các operations và methods**
- `processPayment(payrollId: String)`: Thực hiện thanh toán lương.
- `generatePaymentReceipt(paymentId: String)`: Tạo biên lai thanh toán.

### **4.2 Xác định trạng thái và sự thay đổi trạng thái**
- Trạng thái:  
  - `Pending`: Đang chờ thanh toán.  
  - `Completed`: Thanh toán đã hoàn tất.
- Sự thay đổi:
  - Khi thanh toán thành công -> chuyển từ `Pending` sang `Completed`.

### **4.3 Xác định thuộc tính và mô tả rõ ràng**
- `paymentId` (String): Mã giao dịch thanh toán.
- `payrollId` (String): Mã bảng lương liên quan.
- `paymentDate` (Date): Ngày thanh toán.
- `paymentAmount` (Double): Số tiền thanh toán.
- `paymentMethod` (String): Phương thức thanh toán (VD: Chuyển khoản, tiền mặt).

### **4.4 Xác định phụ thuộc và quan hệ kết hợp**
- Liên kết với `Payroll`: Thực hiện thanh toán dựa trên thông tin lương.
- Dùng bởi `AccessControl` để đảm bảo chỉ admin hoặc người có quyền mới thực hiện thanh toán.

---

## 5. **AccessControl (Kiểm soát truy cập)**

### **5.1 Xác định các operations và methods**
- `grantPermission(roleId: String, permission: String)`: Gán quyền cho vai trò.
- `checkAccess(userId: String, resource: String)`: Kiểm tra quyền truy cập của người dùng.

### **5.2 Xác định trạng thái và sự thay đổi trạng thái**
- Trạng thái:  
  - `Active`: Người dùng có quyền truy cập.  
  - `Suspended`: Người dùng bị tạm dừng quyền truy cập.
- Sự thay đổi:
  - Khi người dùng vi phạm hoặc bị khóa tài khoản -> chuyển từ `Active` sang `Suspended`.

### **5.3 Xác định thuộc tính và mô tả rõ ràng**
- `roleId` (String): Mã vai trò (admin, nhân viên, quản lý).
- `permissions` (List<String>): Danh sách quyền truy cập.

### **5.4 Xác định phụ thuộc và quan hệ kết hợp**
- Liên kết với toàn hệ thống: Mọi lớp sử dụng để kiểm tra quyền truy cập.
- Đảm bảo bảo mật dữ liệu và phân quyền hợp lý.
