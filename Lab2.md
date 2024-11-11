# Phân Tích Các Ca Sử Dụng trong Hệ Thống Payroll System

## 1. **Record Timecard Information (Ghi nhận thông tin thẻ thời gian)**
   - **Mô tả**: Nhân viên nhập thời gian làm việc vào hệ thống.
   - **Người dùng chính**: Nhân viên.
   - **Dữ liệu đầu vào**: Ngày làm việc, số giờ làm việc, số charge (charge number).
   - **Quy tắc kinh doanh**:
     - Với nhân viên tính lương theo giờ, nếu thời gian làm việc vượt quá 8 giờ/ngày, giờ làm thêm sẽ được tính với hệ số 1.5.
     - Các nhân viên salaried vẫn phải ghi lại thời gian làm việc để thống kê.
   - **Kết quả**: Hệ thống lưu thông tin thời gian làm việc của nhân viên.

## 2. **Enter Purchase Orders (Nhập đơn đặt hàng)**
   - **Mô tả**: Nhân viên bán hàng nhập thông tin đơn hàng để tính hoa hồng.
   - **Người dùng chính**: Nhân viên bán hàng.
   - **Dữ liệu đầu vào**: Ngày đơn hàng, số tiền bán hàng.
   - **Quy tắc kinh doanh**:
     - Tính hoa hồng theo tỷ lệ phần trăm (10%, 15%, 25%, hoặc 35%).
   - **Kết quả**: Lưu trữ thông tin đơn hàng để tính toán hoa hồng.

## 3. **Change Employee Preferences (Thay đổi tùy chọn của nhân viên)**
   - **Mô tả**: Nhân viên có thể thay đổi phương thức nhận lương và một số tùy chọn cá nhân khác.
   - **Người dùng chính**: Nhân viên.
   - **Tùy chọn**: Nhận lương qua thư, gửi tiền vào tài khoản ngân hàng hoặc nhận trực tiếp tại văn phòng.
   - **Kết quả**: Hệ thống cập nhật tùy chọn cá nhân của nhân viên.

## 4. **Generate Paycheck (Tạo phiếu lương)**
   - **Mô tả**: Hệ thống tự động tạo phiếu lương cho nhân viên theo thời gian biểu (thứ sáu hàng tuần hoặc ngày làm việc cuối cùng của tháng).
   - **Người dùng chính**: Payroll Administrator (quản trị viên).
   - **Quy tắc kinh doanh**:
     - Tính toán dựa trên số giờ làm việc (cho nhân viên tính theo giờ), hoặc dựa trên lương cố định và hoa hồng (cho nhân viên salaried).
   - **Kết quả**: Phiếu lương được tạo và thanh toán.

## 5. **Run Payroll Automatically (Chạy hệ thống lương tự động)**
   - **Mô tả**: Hệ thống lương sẽ tự động chạy theo lịch mà không cần can thiệp.
   - **Người dùng chính**: Payroll Administrator, nhưng việc thực thi là tự động.
   - **Quy tắc kinh doanh**:
     - Cập nhật từ dữ liệu thời gian làm việc và đơn hàng từ lần thanh toán trước đến ngày thanh toán hiện tại.
   - **Kết quả**: Tất cả nhân viên được trả lương đúng hạn.

## 6. **Query Employee Reports (Truy vấn báo cáo của nhân viên)**
   - **Mô tả**: Nhân viên có thể truy vấn thông tin liên quan đến giờ làm, lương, thời gian nghỉ phép còn lại.
   - **Người dùng chính**: Nhân viên.
   - **Kết quả**: Hệ thống trả về báo cáo theo yêu cầu.

## 7. **Manage Employee Information (Quản lý thông tin nhân viên)**
   - **Mô tả**: Payroll Administrator quản lý thông tin nhân viên, bao gồm thêm mới, xoá, và cập nhật thông tin.
   - **Người dùng chính**: Payroll Administrator.
   - **Dữ liệu**: Thông tin cá nhân (tên, địa chỉ, vị trí công việc, loại lương).
   - **Kết quả**: Thông tin nhân viên được quản lý chặt chẽ và cập nhật thường xuyên.

## 8. **Run Administrative Reports (Chạy báo cáo quản trị)**
   - **Mô tả**: Payroll Administrator có thể tạo báo cáo thống kê, ví dụ như tổng chi phí lương, số lượng nhân viên theo từng vị trí.
   - **Người dùng chính**: Payroll Administrator.
   - **Kết quả**: Hệ thống tạo ra các báo cáo quản trị theo yêu cầu để hỗ trợ phân tích.


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
