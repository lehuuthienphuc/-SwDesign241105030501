1.Subsystem context diagrams
BankSystem:
biểu đồ ngữ cảnh: ![diagram](https://www.planttext.com/api/plantuml/png/T951JiCm44NtFiMeArZa0YnGYzeb4hGIgsoczj2OskDeFA7AsLXm9Aw0qoH2eB3qzv_tlyTV7v_hh2ZQnM24h2AV0i7g2Nj98S2Xpqfn1PXXaaR56BIQ17Qn3QadcewJP-EYPvzLi8ZJrGFoUNP9UYjHZyXueaYiMrGyOYPZPXvKrVtlHBY37Ii9g8zaKHnuVaqr7xfZz0fj9xOf24ZYI7BDpnr93qtg9CCboPbSpI-UBY3K9j5ibhekneuzWUPgO-w-Oy2VMVzEVyaJO40EZo-ahHzM3AxuijVIdTX1Yxrjo9wlt8NPVxTLW1jhAMTeHykL03TxGbSb3lsjCUkIC7pjDm000F__0m00)(https://www.planttext.com/api/plantuml/png/f5512i8m4BplA_QeO3zGGX4zUHDyGKnN3BP9oMx5ehxCWq_o2xQDXPOUlIIxpEpCRF9vlTSiEaXT5c0ApOnxtGHV55llfBife58cDbc6Tq0CjSCgiXPBU09O9nHEsX3kDjfT3WqBbJqrfygpbOLkLSsPp2N5eLfXE-OxVehTkNCd7qejrhjUDAOPwId5zP5ZNGL_Qtvn_lOOsAq3ER4IXISHHeC0ynTAacooUegv3MHaoCRO6p1UhOOnKJsIPBGZJ43VOaEs6J1BjIQNTx_u1G00__y30000)

Giải thích các mối quan hệ trong biểu đồ
PayrollController --> IBankSystem: PayrollController có mối quan hệ phụ thuộc với IBankSystem để thực hiện việc kiểm tra và gửi phiếu lương trực tiếp qua hệ thống ngân hàng (direct deposits checks via).
IBankSystem <|-- BankSystem: BankSystem kế thừa giao diện IBankSystem và hiện thực phương thức deposit.
IBankSystem o-- Paycheck: IBankSystem có mối quan hệ kết hợp với Paycheck, vì nó cần truy cập thông tin phiếu lương để thực hiện giao dịch.
IBankSystem o-- BankInformation: IBankSystem có mối quan hệ kết hợp với BankInformation, vì nó cần thông tin tài khoản ngân hàng để thực hiện gửi phiếu lương vào đúng tài khoản.

PrintService:
biểu đồ ngữ cảnh: ![diagram](https://www.planttext.com/api/plantuml/png/d5512i8m4BplA_QeO3zGGYbuyYRwWbXN2BH9sMoBehxCWq_o2wQ9WYqzUTeiCpipktazdgKNpT8rDLIrzXwtRAoidHLsTKsCIbMfAGgy0c8xu3jg7SjY2NU0q1AVT4MuYRDxujw4RahMgUQOwWh5HJvnZf_7nfuSDrgCir7w9z5NLIdV7Vp52pL1tPqlCx7-Tahyu45MZ2JfSOpH9C3qM5bMJAwGuz4mLP82UkHeuR4t6iPCTSkoqQum8RY0fuGpm5owaknn-DWt0000__y30000)

Giải thích mối quan hệ
PrintController --> IPrintService: PrintController phụ thuộc vào IPrintService để thực hiện in báo cáo.
IPrintService <|-- PrintService: PrintService kế thừa IPrintService và hiện thực phương thức printReport.
IPrintService o-- Report: IPrintService có mối quan hệ kết hợp với Report vì cần truy cập nội dung của báo cáo khi in.
IPrintService o-- PrinterInformation: IPrintService có mối quan hệ kết hợp với PrinterInformation để biết máy in nào sẽ được sử dụng để in báo cáo.

ProjectManagementDatabase subsystems
biểu đồ ngữ cảnh:![diagram](https://www.planttext.com/api/plantuml/png/r5D1JiCm4BplA_O84lb05KKLoeK3g5B40xRs4XavJkNTW2BeopZm9Bw0qmO4hOkGE76rPqOpixjlBwzBKOewT1x0U1B15OsnzxuPHRd3iZHzqFHGLVW4Y8Qy6JmfD-GfZcURsD-pqHlgU86DHXVQSzW2kA0SxyWmNgtsa6iAr7B7GUlBdLJBEd_LhEIyvCKGoTePc4DSeDtJlrA6ZKqUVsG5VgmFYTlF4euyazAQX5CXCgnbLyvSoR_94PFv5CNfE3l_g_gj76loDFYFFb9fluoQDBylNb5K-TLP81d38YoOt1C-E88ii7mkYjE3X3ofF-J4qxWfFi2IWvtEvnq00F__0m00)

Giải thích:
PayrollSystem: Lớp điều khiển (<<control>>) tính toán lương bằng cách truy xuất dữ liệu từ ProjectManagementDatabase.
IProjectManagementDB: Giao diện định nghĩa các phương thức truy xuất và cập nhật dữ liệu trong ProjectManagementDatabase.
ProjectManagementDatabase: Lớp con (<<subsystem>>) thực hiện các hành động quản lý dữ liệu dự án.
ProjectManager và User: Các thực thể (<<entity>>) có thể tương tác với hệ thống ProjectManagementDatabase để cập nhật và nhập liệu.

2.Analysis class to design element map

| **Lớp phân tích**              | **Lớp thiết kế**                            | **Chức năng trong thiết kế**                                         |
|-------------------------------|--------------------------------------------|--------------------------------------------------------------------|
| **PayrollSystem**              | `PayrollSystem`                            | Tính toán tiền lương dựa trên thông tin dự án từ **ProjectManagementDatabase** |
| **IProjectManagementDB**       | `IProjectManagementDB`                     | Giao diện định nghĩa các phương thức để thao tác dữ liệu dự án    |
| **ProjectManagementDatabase**  | `ProjectManagementDatabase`                | Lớp thực thi các phương thức truy xuất và lưu trữ dữ liệu dự án    |
| **ProjectManager**             | `ProjectManager`                           | Quản lý và cập nhật thông tin dự án trong hệ thống                 |
| **User**                       | `User`                                     | Nhập liệu thông tin dự án vào cơ sở dữ liệu                        |


3.Design element to owning package map

| **Phần tử thiết kế**            | **Gói chứa**                 | **Mô tả**                                                       |
|---------------------------------|------------------------------|------------------------------------------------------------------|
| **PayrollSystem**               | `com.acme.payroll`           | Tính toán tiền lương dựa trên thông tin từ **ProjectManagementDatabase** |
| **IProjectManagementDB**        | `com.acme.database`          | Giao diện định nghĩa các phương thức để thao tác dữ liệu dự án |
| **ProjectManagementDatabase**   | `com.acme.database`          | Thực thi các phương thức truy xuất và lưu trữ dữ liệu dự án    |
| **ProjectManager**              | `com.acme.projectmanagement` | Quản lý và cập nhật thông tin dự án trong hệ thống             |
| **User**                        | `com.acme.user`              | Nhập liệu thông tin dự án vào cơ sở dữ liệu                     |


4.Architectural layers and their dependencies
![diagram](https://www.planttext.com/api/plantuml/png/R91B2i9038RtSuguquKNS24-4Q68Y3r0c8bse4xh95MAU38N7iahE2r5hPfT_Z_vydZSxYCMz58SKjKnjBEEO3EVRiUhHJG7dIApKczXxOd92OhDN8GbURWegCDOpbCiusMtroYUDDaJnKn-wV92Wd7zP4qA3jEOesnlTHkM-qm7frNnuYReJ5fZDtGiY7_0CnGSwmhGfkv9Aki5OZnH8uJ-tzFw_U6_9GTWdP17BGndAudwKrErVgyn0AmpOZ31WftF3agDo9dg-Ky0003__mC0)

