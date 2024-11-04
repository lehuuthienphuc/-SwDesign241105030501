# Phân Tích Các Ca Sử Dụng Trong Hệ Thống *Payroll System*

Hệ thống **Payroll System** bao gồm nhiều ca sử dụng (use cases) phục vụ việc quản lý nhân sự và tính toán lương cho nhân viên. Các ca sử dụng quan trọng gồm có:

## 1. **Quản Lý Nhân Viên**
   - **Mô tả**: Chức năng cho phép tạo mới, cập nhật và xóa thông tin nhân viên.
   - **Diễn biến**:
     - *Tạo mới nhân viên*: Nhập thông tin cá nhân, vị trí công việc, và thông tin liên quan khác.
     - *Cập nhật thông tin*: Sửa đổi thông tin cá nhân hoặc vị trí công việc.
     - *Xóa nhân viên*: Xóa hồ sơ khi nhân viên nghỉ việc.
   - **Kết quả mong muốn**: Nhân viên được thêm, sửa, hoặc xóa khỏi hệ thống.

## 2. **Chấm Công Hàng Ngày**
   - **Mô tả**: Theo dõi giờ làm việc hàng ngày của từng nhân viên.
   - **Diễn biến**:
     - Nhân viên hoặc quản lý chọn ngày, giờ làm việc và công việc cụ thể.
   - **Kết quả mong muốn**: Giờ làm việc của nhân viên được cập nhật.

## 3. **Quản Lý Bảng Chấm Công (*Maintain Timecard*)**
   - **Mô tả**: Tạo, cập nhật, và nộp bảng chấm công.
   - **Diễn biến**:
     - *Thêm giờ làm*: Nhập mã dự án và số giờ đã làm.
     - *Hiển thị bảng chấm công*: Xem bảng tổng hợp giờ làm.
     - *Nộp bảng chấm công*: Gửi bảng chấm công lên hệ thống.
   - **Kết quả mong muốn**: Bảng chấm công của nhân viên được lưu và nộp thành công.

## 4. **Tính Toán Lương**
   - **Mô tả**: Tự động tính toán lương hàng tháng dựa trên giờ làm và hệ số lương.
   - **Diễn biến**:
     - Dữ liệu từ bảng chấm công và hệ số lương được lấy để tính lương.
   - **Kết quả mong muốn**: Bảng lương cuối tháng của nhân viên được tạo.

## 5. **Phê Duyệt Bảng Lương**
   - **Mô tả**: Kiểm tra và phê duyệt bảng lương trước khi thanh toán.
   - **Diễn biến**:
     - Kiểm tra bảng lương dựa trên số giờ làm và mức lương.
   - **Kết quả mong muốn**: Bảng lương của nhân viên được phê duyệt.

## 6. **Thanh Toán Lương**
   - **Mô tả**: Xử lý việc thanh toán lương sau khi bảng lương được phê duyệt.
   - **Diễn biến**:
     - Thực hiện thanh toán qua ngân hàng hoặc tiền mặt.
     - Gửi thông báo thanh toán thành công đến nhân viên.
   - **Kết quả mong muốn**: Nhân viên nhận được lương theo quy định.

## 7. **Báo Cáo và Phân Tích**
   - **Mô tả**: Tổng hợp báo cáo lương, giờ làm việc hoặc chi phí khác.
   - **Diễn biến**:
     - Tạo báo cáo định kỳ hoặc theo yêu cầu (PDF, Excel).
   - **Kết quả mong muốn**: Báo cáo chính xác cho bộ phận nhân sự và quản lý.

## 8. **Quản Lý và Phân Quyền Người Dùng**
   - **Mô tả**: Phân quyền sử dụng hệ thống cho các vai trò khác nhau.
   - **Diễn biến**:
     - Cấp quyền truy cập và chỉnh sửa dữ liệu cho từng loại người dùng.
   - **Kết quả mong muốn**: Quyền hạn truy cập rõ ràng và bảo mật.

