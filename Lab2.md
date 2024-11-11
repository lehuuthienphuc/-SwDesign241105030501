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
