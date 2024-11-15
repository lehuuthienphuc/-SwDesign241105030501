# Documentation: Subsystem Context Diagrams, Analysis, and Architectural Layers

## 1. Subsystem Context Diagrams

### BankSystem

**Biểu đồ ngữ cảnh**  
![BankSystem Diagram](https://www.planttext.com/api/plantuml/png/h591JiCm4Bpx5QjUQ2NImhMoeWguz8RW1IRPA5OTE_8wY0Xu6GUUn1U8uxPnqXphY-trpkpChlz-VdVaX7LDfTWDF64XDSApQArHwj5evtUq80W4PE7ECYM8Pf8uFsQaANmowDPc0xRHK8VKvOfziw6Ar0vj8JA4_OFGXzUM75PiDdgaox4s9DrITBMp4hC3RE5qlFLynaEweD_skZ2s4auQFQuRqVQsg7cZSAsj-MZ1bSA1h6g55Mf78tN1UiJ0-GH-zduTiMUmbwgX4oHTEqmWl74UucawiHdHpX5CKZpu1LL_fbBMn2vdlBXRh-yNa2JfQ3vRoAN5p9rS4_JA2DwbO74Y_qgIg7-ZDqyQDUkYWKFNLXUugPKTwjp_wNy0003__mC0)

**Giải thích các mối quan hệ**:
- `PayrollController --> IBankSystem`: Kết nối để gửi phiếu lương qua ngân hàng.
- `IBankSystem <|-- BankSystem`: `BankSystem` kế thừa và hiện thực giao diện `IBankSystem`.
- `IBankSystem o-- Paycheck`: Kết hợp với `Paycheck` để xử lý phiếu lương.
- `IBankSystem o-- BankInformation`: Kết hợp với `BankInformation` để sử dụng thông tin tài khoản.

---

### PrintService

**Biểu đồ ngữ cảnh**  
![PrintService Diagram](https://www.planttext.com/api/plantuml/png/d5512i8m4BplA_QeO3zGGYbuyYRwWbXN2BH9sMoBehxCWq_o2wQ9WYqzUTeiCpipktazdgKNpT8rDLIrzXwtRAoidHLsTKsCIbMfAGgy0c8xu3jg7SjY2NU0q1AVT4MuYRDxujw4RahMgUQOwWh5HJvnZf_7nfuSDrgCir7w9z5NLIdV7Vp52pL1tPqlCx7-Tahyu45MZ2JfSOpH9C3qM5bMJAwGuz4mLP82UkHeuR4t6iPCTSkoqQum8RY0fuGpm5owaknn-DWt0000__y30000)

**Giải thích mối quan hệ**:
- `PrintController --> IPrintService`: Kết nối để in báo cáo.
- `IPrintService <|-- PrintService`: `PrintService` kế thừa `IPrintService` để hiện thực phương thức in.
- `IPrintService o-- Report`: Kết hợp với `Report` để sử dụng nội dung báo cáo.
- `IPrintService o-- PrinterInformation`: Kết hợp với `PrinterInformation` để cấu hình máy in.

---

### ProjectManagementDatabase Subsystems

**Biểu đồ ngữ cảnh**  
![ProjectManagementDatabase Diagram](https://www.planttext.com/api/plantuml/png/r5D1JiCm4BplA_O84lb05KKLoeK3g5B40xRs4XavJkNTW2BeopZm9Bw0qmO4hOkGE76rPqOpixjlBwzBKOewT1x0U1B15OsnzxuPHRd3iZHzqFHGLVW4Y8Qy6JmfD-GfZcURsD-pqHlgU86DHXVQSzW2kA0SxyWmNgtsa6iAr7B7GUlBdLJBEd_LhEIyvCKGoTePc4DSeDtJlrA6ZKqUVsG5VgmFYTlF4euyazAQX5CXCgnbLyvSoR_94PFv5CNfE3l_g_gj76loDFYFFb9fluoQDBylNb5K-TLP81d38YoOt1C-E88ii7mkYjE3X3ofF-J4qxWfFi2IWvtEvnq00F__0m00)

**Giải thích mối quan hệ**:
- `PayrollSystem --> IProjectManagementDB`: Kết nối để truy cập dữ liệu dự án.
- `IProjectManagementDB <|-- ProjectManagementDatabase`: `ProjectManagementDatabase` hiện thực giao diện.
- `ProjectManager` và `User`: Tương tác với cơ sở dữ liệu qua giao diện.

---

## 2. Analysis Class to Design Element Map

| **Lớp phân tích**              | **Lớp thiết kế**                            | **Chức năng trong thiết kế**                                         |
|-------------------------------|--------------------------------------------|--------------------------------------------------------------------|
| **PayrollSystem**              | `PayrollSystem`                            | Tính toán tiền lương từ **ProjectManagementDatabase**               |
| **IProjectManagementDB**       | `IProjectManagementDB`                     | Định nghĩa phương thức thao tác dữ liệu dự án                     |
| **ProjectManagementDatabase**  | `ProjectManagementDatabase`                | Hiện thực thao tác truy xuất/lưu trữ dữ liệu dự án                |
| **ProjectManager**             | `ProjectManager`                           | Quản lý thông tin dự án                                            |
| **User**                       | `User`                                     | Nhập liệu dự án vào cơ sở dữ liệu                                  |

---

## 3. Design Element to Owning Package Map

| **Phần tử thiết kế**            | **Gói chứa**                 | **Mô tả**                                                       |
|---------------------------------|------------------------------|------------------------------------------------------------------|
| **PayrollSystem**               | `com.acme.payroll`           | Tính toán lương, tích hợp **ProjectManagementDatabase**           |
| **IProjectManagementDB**        | `com.acme.database`          | Giao diện thao tác dữ liệu dự án                                |
| **ProjectManagementDatabase**   | `com.acme.database`          | Thực hiện lưu trữ và truy xuất dữ liệu dự án                    |
| **ProjectManager**              | `com.acme.projectmanagement` | Quản lý dự án                                                  |
| **User**                        | `com.acme.user`              | Nhập liệu dự án                                                |

---

## 4. Architectural Layers and Their Dependencies

**Biểu đồ kiến trúc và quan hệ phụ thuộc**  
![Architectural Layers Diagram](https://www.planttext.com/api/plantuml/png/R91B2i9038RtSuguquKNS24-4Q68Y3r0c8bse4xh95MAU38N7iahE2r5hPfT_Z_vydZSxYCMz58SKjKnjBEEO3EVRiUhHJG7dIApKczXxOd92OhDN8GbURWegCDOpbCiusMtroYUDDaJnKn-wV92Wd7zP4qA3jEOesnlTHkM-qm7frNnuYReJ5fZDtGiY7_0CnGSwmhGfkv9Aki5OZnH8uJ-tzFw_U6_9GTWdP17BGndAudwKrErVgyn0AmpOZ31WftF3agDo9dg-Ky0003__mC0)
