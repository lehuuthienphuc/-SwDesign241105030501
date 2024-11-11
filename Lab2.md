# 1. Phân Tích Kiến Trúc

## Đề xuất kiến trúc: Kiến trúc hướng dịch vụ (SOA)
- **Lý do lựa chọn**:
  - Tính linh hoạt và khả năng mở rộng.
  - Dễ dàng tích hợp với hệ thống hiện tại.
  - Quản lý phân tán và bảo mật hiệu quả.
  - Tái sử dụng dịch vụ cho các yêu cầu khác nhau.

### Ý Nghĩa Từng Thành Phần Trong Kiến Trúc

- **Employee Service (Dịch vụ quản lý nhân viên)**
  - **Chức năng**: Quản lý thông tin cá nhân của nhân viên (tên, địa chỉ, thông tin thanh toán, loại nhân viên: theo giờ, lương cố định, có hoa hồng).
  - **Ý nghĩa**: Là dịch vụ cốt lõi để lưu trữ và xử lý thông tin cơ bản của toàn bộ nhân viên trong công ty.

- **Timecard Service (Dịch vụ quản lý timecard)**
  - **Chức năng**: Cho phép nhân viên nhập và lưu trữ thông tin về số giờ làm việc, charge numbers, thời gian làm việc.
  - **Ý nghĩa**: Đảm bảo rằng tất cả dữ liệu liên quan đến thời gian làm việc được ghi lại chính xác để phục vụ tính toán lương.

- **Payroll Service (Dịch vụ xử lý bảng lương)**
  - **Chức năng**: Xử lý tính lương cho từng loại nhân viên và tạo các bản sao kê lương.
  - **Ý nghĩa**: Đóng vai trò chính trong hệ thống, đảm bảo tính toán chính xác và phát lương đúng hạn.

- **Report Service (Dịch vụ báo cáo)**
  - **Chức năng**: Cung cấp báo cáo về tổng số giờ làm việc, lương đã nhận, thời gian nghỉ còn lại.
  - **Ý nghĩa**: Giúp nhân viên dễ dàng truy vấn thông tin về thu nhập và tình trạng làm việc của họ.

- **Project Management Integration Service (Dịch vụ tích hợp quản lý dự án)**
  - **Chức năng**: Tích hợp với cơ sở dữ liệu DB2 để lấy thông tin về dự án và charge numbers.
  - **Ý nghĩa**: Kết nối hệ thống bảng lương mới với hệ thống quản lý dự án cũ mà không cần thay đổi cơ sở dữ liệu.

- **Payment Method Service (Dịch vụ phương thức thanh toán)**
  - **Chức năng**: Quản lý các tùy chọn thanh toán như chuyển khoản, gửi qua bưu điện, nhận trực tiếp.
  - **Ý nghĩa**: Đảm bảo hệ thống xử lý thanh toán linh hoạt theo yêu cầu của nhân viên.

- **Security Service (Dịch vụ bảo mật)**
  - **Chức năng**: Quản lý quyền truy cập để đảm bảo an toàn dữ liệu.
  - **Ý nghĩa**: Bảo vệ dữ liệu và phân quyền hợp lý cho từng nhóm nhân viên.

![Biểu Đồ Package](https://www.planttext.com/api/plantuml/png/Z5H1RjGm5Dtd55-p0HRTS03KJe8AObeL6bLiZSTCGXCxift527N1YaLN725K5GXfL91O9K9THEezV0Akm4-6feadddQLI7x_lUVt__VVwdfNQI9rdYPUHkWfMJ2OXARynXUm7nC1GMogptm27pq0cX2bO6AgxtWQcEeIFuTH_PN3ILp_G11Hy3pD4h5aB63gL8jiBylk2dk4y3etvGM7K9hg76OtFsyAlcW9ZiXIYYJPcwSnZvMMH0lvacictnFAl3DlmoOQEQSHdA2VjSqEq3iP-cnGdQl_JcRr7-Tb3WX7GebLPov-FpBbPGf-_RkvXqjWY4A5C4uP9NB-08MmNl7eBgg1n5jJhLg1aIIFfA1CAR6LV5eN0cqLmYB6ZF6WTugyRrWcfDvddBNDkSSp_humrKK6lHWGyWlgJtOdNfdoMiEXgRx444oVjcBuzGNdZDwd515C9nHriQM_0z0wePHn_O3mfyWXuC2KA-sc7u2G_fZHNCPwsUSV6U1GvalmiIfhWhc2MRCX-M3b_EDWvbureiaxefW5TywQ0t_R57YCcJ-v3H-dvmE6tzMW_qSGhgSCT5rGMA3TAmAq-TVjZRpDHm1sTfvjh9C3Pk-40sQFuTQ7OrJVNf1HzL6GDJXMpK2iIswKQ0DbtMfWgGFrbw95Z3Hgb_5vywh_0m00__y30000)

---

# 2. Cơ Chế Phân Tích

## Cơ chế quản lý quyền truy cập
- **Lý do**: Đảm bảo nhân viên chỉ có quyền truy cập và chỉnh sửa thông tin cá nhân của họ.
- **Cơ chế**: Phân quyền theo vai trò (RBAC).

## Cơ chế tính toán lương
- **Lý do**: Có nhiều loại nhân viên (theo giờ, lương cố định, hoa hồng).
- **Cơ chế**: Sử dụng lớp `PayrollProcessor` với các thuật toán riêng cho từng loại.

## Cơ chế ghi nhận và quản lý timecard
- **Lý do**: Nhân viên cần ghi nhận giờ làm việc để tính toán lương.
- **Cơ chế**: `TimecardService` lưu trữ thời gian làm việc và các thuộc tính liên quan.

## Cơ chế tích hợp với hệ thống quản lý dự án cũ (DB2)
- **Lý do**: Lấy thông tin dự án từ hệ thống DB2.
- **Cơ chế**: Sử dụng lớp `DB2Connector` giao tiếp với DB2.

## Cơ chế báo cáo
- **Lý do**: Nhân viên cần truy vấn báo cáo về giờ làm, lương, nghỉ phép.
- **Cơ chế**: Sử dụng lớp `ReportService` để tạo báo cáo từ dữ liệu.

## Cơ chế thanh toán tự động
- **Lý do**: Tự động thực hiện thanh toán định kỳ.
- **Cơ chế**: Lớp `PaymentManager` đảm bảo thanh toán đúng thời gian và phương thức đã chọn.

---

# 3. Phân Tích Ca Sử Dụng "Payment"
- **Lớp phân tích**:
  - Nhân viên: Thông tin cá nhân và phương thức thanh toán.
  - Bộ xử lý lương: Tính toán lương dựa trên loại hình nhân viên.
  - Quản lý thanh toán: Xử lý và gửi thanh toán.
  - Ngân hàng: Xử lý thanh toán qua chuyển khoản.

### Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/T98nQiD044LxdM8ku0ke22Ofui8O0Y8uvKOntWLbf2YpXqddJOg0GU32bOH9CU1xx0boXSpQmRBmkfx_t_m_p6_tCtudLPDzBHALKrd3JFCdFXfUOrB9mEIcKaXmwxkFkU-QAU-c-ytUuN8mVh2-_K8PPbgXpafsG_jiATG9hyIMz1jWT1C1f_34QmkvRxyj43UeeVXVUIaEYCZo5Ev5Pe0qRqL41a-CY3f0-eGfX1LGy4xi8W4wQDwi0WmYq8SUlG56rqBCsUM0shSDdhFY6QuSuqxSrH52GBLlGslfvSm06JjDg7KwTWhPyHZFx4hGfIGFc5KWd7762tm9t_07003__mC0)

---

# 4. Phân Tích Ca Sử Dụng "Maintain Timecard"
- **Lớp phân tích**:
  - Nhân viên: Ghi nhận giờ làm việc hàng ngày.
  - Quản lý Timecard: Lưu trữ thông tin timecard của nhân viên.
  - Bộ xử lý lương: Sử dụng thông tin timecard để tính lương.

### Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aO9Vnk55UM6PXrVbSHK09JAJCmiIyqeK0aiVxbgSvtDuRqXcRcfoOb4AYgpJmzqp8nxkNWkKzpcsuTZ2l7GkSjc7W26RJsySa2u8TkWSmt6SDw0Y6o2LqK3xRXZRCrwINHY4IZy8tPChU8A_6mGE0c1sZtr5TwsiupbGA7MFrbGrwtQzBiE5MGHdIp7hQKrDdJGT-KEvP9MJifDcbN9Dg3tbXUm0D1tpHyBkTc3GwOYABUJ4OcsfBbGGg3nKl4n6hBaO9np7HrAk5bclRBqGQ80Lbrpy7oeNQCTax2uwuhsZ-lOrOCTC1FYwOwAEoVjQ0v90Bz0sz9)

---

# 5. Các Yêu Cầu Phi Chức Năng

## Bảo mật
- **Yêu cầu**: Cần phân quyền truy cập theo vai trò để bảo vệ dữ liệu nhạy cảm.
- **Giải pháp**: Sử dụng dịch vụ bảo mật Security Service và cơ chế RBAC (Role-Based Access Control) để chỉ định quyền truy cập dựa trên vai trò nhân viên.

## Khả năng mở rộng
- **Yêu cầu**: Hệ thống cần dễ dàng mở rộng khi số lượng nhân viên và dự án tăng.
- **Giải pháp**: Áp dụng kiến trúc hướng dịch vụ (SOA) để có thể bổ sung thêm các dịch vụ mới hoặc tích hợp với các hệ thống khác mà không ảnh hưởng đến cấu trúc hiện tại.

## Tích hợp với hệ thống cũ
- **Yêu cầu**: Cần tích hợp hệ thống bảng lương mới với hệ thống quản lý dự án cũ (DB2).
- **Giải pháp**: Sử dụng lớp `DB2Connector` như một cầu nối để truy xuất thông tin dự án mà không cần thay đổi hệ thống hiện tại.

## Hiệu năng
- **Yêu cầu**: Hệ thống phải xử lý các yêu cầu về lương và timecard một cách nhanh chóng để đáp ứng nhu cầu của nhân viên.
- **Giải pháp**: Tối ưu hóa các dịch vụ như Payroll Service và Timecard Service để đảm bảo thời gian xử lý nhanh chóng và sử dụng bộ nhớ hiệu quả.

## Tính ổn định và khả năng khôi phục
- **Yêu cầu**: Đảm bảo hệ thống không bị gián đoạn và có khả năng khôi phục nhanh chóng khi gặp sự cố.
- **Giải pháp**: Áp dụng các cơ chế sao lưu và phục hồi, và sử dụng các công cụ giám sát để phát hiện và xử lý các vấn đề kịp thời.

---

# 6. Bản Mô Tả Chi Tiết Quy Trình Ca Sử Dụng

## Ca sử dụng "Payment" (Thanh Toán)
1. **Bắt đầu**: Hệ thống khởi động dịch vụ Payroll Service để tính toán lương của nhân viên vào cuối tháng.
2. **Xác minh nhân viên**: Dịch vụ kiểm tra thông tin và phương thức thanh toán của nhân viên.
3. **Tính toán lương**:
   - **Nhân viên theo giờ**: Tính lương dựa trên số giờ làm việc đã ghi trong Timecard Service.
   - **Nhân viên lương cố định**: Sử dụng mức lương cố định đã lưu trong Employee Service.
   - **Nhân viên có hoa hồng**: Tính lương cơ bản cộng hoa hồng dựa trên dữ liệu bán hàng.
4. **Xử lý thanh toán**: Chuyển thông tin thanh toán tới Payment Method Service.
5. **Kết thúc**: Gửi thông báo tới nhân viên sau khi thanh toán hoàn tất.

## Ca sử dụng "Maintain Timecard" (Quản Lý Timecard)
1. **Bắt đầu**: Nhân viên đăng nhập vào hệ thống và chọn chức năng quản lý timecard.
2. **Nhập dữ liệu**: Nhân viên nhập số giờ làm việc và charge number cho từng ngày.
3. **Lưu thông tin**: Hệ thống xác nhận và lưu thông tin vào Timecard Service.
4. **Xác minh và thông báo**: Gửi thông báo xác nhận đã ghi nhận timecard thành công cho nhân viên.

---

# 7. Tổng Kết và Đề Xuất Cải Tiến

Hệ thống bảng lương Acme, Inc. được thiết kế với kiến trúc hướng dịch vụ, cho phép quản lý hiệu quả dữ liệu nhân viên, thông tin về thời gian làm việc và thanh toán lương. Các cơ chế bảo mật và phân quyền giúp đảm bảo tính an toàn, đồng thời tích hợp dễ dàng với hệ thống cũ.

### Đề xuất cải tiến:
1. **Áp dụng công nghệ lưu trữ đám mây** để tăng khả năng mở rộng.
2. **Cải thiện giao diện người dùng** để tăng tính dễ sử dụng cho nhân viên.
3. **Tự động hóa nhiều quy trình** như tạo báo cáo và gửi email nhắc nhở.
4. **Theo dõi hiệu năng hệ thống** qua công cụ giám sát để phát hiện kịp thời các lỗi hoặc điểm nghẽn.

---

# 8. Tài Liệu và Biểu Đồ Hỗ Trợ

### Biểu Đồ Thành Phần
- Giúp mô tả các thành phần chính của hệ thống và cách chúng tương tác với nhau.
  
### Biểu Đồ Sequence cho "Payment" và "Maintain Timecard"
- Minh họa quy trình xử lý chi tiết cho từng ca sử dụng.

### Tài Liệu Tham Khảo
1. Hướng dẫn kiến trúc hướng dịch vụ (SOA).
2. Các mẫu thiết kế hệ thống bảng lương phổ biến.
3. Tài liệu sử dụng các công cụ quản lý timecard và tích hợp hệ thống DB2.

---

## Java Code for Maintain Timecard

### Code Example
The following Java code demonstrates a basic structure for handling timecard entries, tracking hours, and submitting timecards.

java
package lab2;

import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class ThoiGianLamViec {
    private String maNhanVien;
    private Map<String, Integer> gioLamViec;

    public ThoiGianLamViec(String maNhanVien) {
        this.maNhanVien = maNhanVien;
        this.gioLamViec = new HashMap<>();
    }

    public void themGioLam(String maDuAn, int gio) {
        gioLamViec.put(maDuAn, gioLamViec.getOrDefault(maDuAn, 0) + gio);
    }

    public void hienThiBangChamCong() {
        System.out.println("Bảng chấm công của Nhân viên: " + maNhanVien);
        gioLamViec.forEach((maDuAn, gio) -> {
            System.out.println("Mã Dự Án: " + maDuAn + ", Giờ Làm Việc: " + gio);
        });
    }

    public void nopBangChamCong() {
        System.out.println("Bảng chấm công đã nộp thành công cho Nhân viên: " + maNhanVien);
    }
}

class HeThongBangLuong {
    private Map<String, ThoiGianLamViec> bangChamCong;

    public HeThongBangLuong() {
        bangChamCong = new HashMap<>();
    }

    public ThoiGianLamViec layHoacTaoBangChamCong(String maNhanVien) {
        return bangChamCong.computeIfAbsent(maNhanVien, ThoiGianLamViec::new);
    }
}

public class mainTainTimeCard {
    public static void main(String[] args) {
        HeThongBangLuong heThongBangLuong = new HeThongBangLuong();
        Scanner scanner = new Scanner(System.in);
        System.out.println("Nhập Mã Nhân Viên:");
        String maNhanVien = scanner.nextLine();

        ThoiGianLamViec bangChamCong = heThongBangLuong.layHoacTaoBangChamCong(maNhanVien);

        boolean hoanTat = false;
        while (!hoanTat) {
            System.out.println("1. Thêm Giờ Làm");
            System.out.println("2. Hiển Thị Bảng Chấm Công");
            System.out.println("3. Nộp Bảng Chấm Công");
            System.out.println("4. Thoát");
            int luaChon = scanner.nextInt();
            scanner.nextLine();  

            switch (luaChon) {
                case 1:
                    System.out.println("Nhập Mã Dự Án:");
                    String maDuAn = scanner.nextLine();
                    System.out.println("Nhập Giờ Làm Việc:");
                    int gio = scanner.nextInt();
                    bangChamCong.themGioLam(maDuAn, gio);
                    break;
                case 2:
                    bangChamCong.hienThiBangChamCong();
                    break;
                case 3:
                    bangChamCong.nopBangChamCong();
                    break;
                case 4:
                    hoanTat = true;
                    break;
                default:
                    System.out.println("Lựa chọn không hợp lệ, vui lòng thử lại.");
            }
        }

        scanner.close();
    }
}
