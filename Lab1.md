1.phân tích kiến trúc:
-Đề xuất kiến trúc: kiến trúc hướng dịch vụ(SOA)
-Lý do lựa chọn:Tính linh hoạt và khả năng mở rộng, tích hợp với hệ thống hiện tại, quản lý phân tán và bảo mật, tái sử dụng dịch vụ.
-Ý nghĩa từng thành phần trong kiến trúc:
Employee Service (Dịch vụ quản lý nhân viên):

Chức năng: Quản lý thông tin cá nhân của nhân viên (tên, địa chỉ, thông tin thanh toán, loại nhân viên: theo giờ, lương cố định, có hoa hồng).
Ý nghĩa: Là dịch vụ cốt lõi để lưu trữ và xử lý thông tin cơ bản của toàn bộ nhân viên trong công ty.
Timecard Service (Dịch vụ quản lý timecard):

Chức năng: Cho phép nhân viên nhập và lưu trữ thông tin về số giờ làm việc, charge numbers, thời gian làm việc.
Ý nghĩa: Đảm bảo rằng tất cả các dữ liệu liên quan đến thời gian làm việc được ghi lại chính xác và có thể sử dụng trong việc tính toán lương.
Payroll Service (Dịch vụ xử lý bảng lương):

Chức năng: Xử lý tính lương cho từng loại nhân viên (theo giờ, cố định, hoa hồng) và tạo các bản sao kê lương.
Ý nghĩa: Đóng vai trò chính trong hệ thống, đảm bảo tính toán chính xác và phát lương cho nhân viên đúng hạn.
Report Service (Dịch vụ báo cáo):

Chức năng: Cho phép nhân viên truy vấn các báo cáo như tổng số giờ làm việc, lương đã nhận, thời gian nghỉ còn lại.
Ý nghĩa: Cung cấp thông tin cần thiết cho nhân viên về tình trạng làm việc và thu nhập của họ.
Project Management Integration Service (Dịch vụ tích hợp quản lý dự án):

Chức năng: Tích hợp với cơ sở dữ liệu DB2 để lấy thông tin về dự án và charge numbers.
Ý nghĩa: Giúp kết nối hệ thống bảng lương mới với hệ thống quản lý dự án cũ mà không cần thay thế cơ sở dữ liệu hiện có.
Payment Method Service (Dịch vụ phương thức thanh toán):

Chức năng: Quản lý và cung cấp các tùy chọn thanh toán (chuyển khoản ngân hàng, gửi qua bưu điện, nhận trực tiếp).
Ý nghĩa: Đảm bảo rằng hệ thống có thể xử lý và gửi tiền lương cho nhân viên theo phương thức mà họ lựa chọn.
Security Service (Dịch vụ bảo mật):

Chức năng: Quản lý quyền truy cập, đảm bảo rằng chỉ những người có quyền mới có thể truy cập hoặc chỉnh sửa dữ liệu.
Ý nghĩa: Đảm bảo an toàn dữ liệu và phân quyền hợp lý cho nhân viên và quản trị viên.

biểu đồ package: https://www.planttext.com/api/plantuml/png/V5JBJiCm4BpxAwnUEFN21w06YX0IbIBA3soTfPWcThJUWYBKB-F09_4BE4zIn-bvPdRMioF_Vl-i70FniSX52Ue0UvIBbD2XOM1jZNo22caXluIKAWVdv7rHvhP2NACxi2sJiXoW52goUPvaXJRQCG5RUZICz0eAnKdyMsoHFhJ2yVG1wmraHshXq7u3nhF98wUn-4KNg82okBX7PyJT_d5j1wPa5Jfd9-9dB2rnNDjY3sYmoMJYI_OT5SjshS9dB-lOzjIU83foVNjzPutniiWyg9eX6-GtEnD5nvb9OelgI9ghkBP7n-BnTTV081DLvtIXFvwq0uSYFCu4y4_j4XeWxtRLP4IWcenso9-8HkQrdHFJaihbycPIdXbQM9CPMdZLY_MF-eUTYhf7IS7v0isPsH1QTD245RpgRAM1D6vVmuZSQ8Kcg_-LFm000F__0m00

2. Cơ chế phân tích
Để giải quyết bài toán thiết kế hệ thống bảng lương cho Acme, Inc., chúng ta cần đề xuất và phân tích một số cơ chế quan trọng:

Cơ chế quản lý quyền truy cập:

Lý do: Hệ thống yêu cầu đảm bảo rằng nhân viên chỉ có thể truy cập và chỉnh sửa thông tin cá nhân của họ (như timecard và phương thức thanh toán). Các tác vụ như thêm mới, xóa hoặc cập nhật thông tin nhân viên chỉ có thể được thực hiện bởi Payroll Administrator.
Cơ chế: Sử dụng các cơ chế phân quyền (role-based access control) để giới hạn quyền truy cập dựa trên vai trò của người dùng. Hệ thống sẽ có các cấp quyền khác nhau cho từng nhóm người dùng.
Cơ chế tính toán lương:

Lý do: Có nhiều loại nhân viên (theo giờ, lương cố định, có hoa hồng), mỗi loại nhân viên có cách tính lương khác nhau. Nhân viên làm thêm giờ cần được trả lương theo mức 1.5 lần so với lương cơ bản.
Cơ chế: Xây dựng một lớp hoặc dịch vụ chuyên xử lý tính toán lương (PayrollProcessor), với các thuật toán khác nhau cho từng loại nhân viên.
Cơ chế ghi nhận và quản lý timecard:

Lý do: Nhân viên cần ghi nhận giờ làm việc của mình hàng ngày. Dữ liệu này được sử dụng để tính toán lương và đánh giá hiệu quả công việc.
Cơ chế: Xây dựng dịch vụ ghi nhận timecard (TimecardService), cho phép lưu trữ thông tin giờ làm việc, charge number, và các thuộc tính khác.
Cơ chế tích hợp với hệ thống quản lý dự án cũ (DB2):

Lý do: Hệ thống mới cần tích hợp với cơ sở dữ liệu DB2 cũ để lấy thông tin dự án và charge numbers.
Cơ chế: Xây dựng lớp tích hợp (DB2Connector) để giao tiếp với cơ sở dữ liệu DB2 bằng các giao thức tương thích, đảm bảo dữ liệu được lấy ra một cách chính xác và không làm ảnh hưởng đến hệ thống hiện có.
Cơ chế báo cáo:

Lý do: Nhân viên cần khả năng truy vấn các báo cáo như tổng số giờ làm việc, tổng lương đã nhận, thời gian nghỉ phép còn lại, v.v.
Cơ chế: Tạo các lớp hoặc dịch vụ tạo báo cáo (ReportService), nơi các báo cáo được sinh ra từ dữ liệu timecard và lương.
Cơ chế thanh toán tự động:

Lý do: Hệ thống cần tự động thực hiện các quy trình thanh toán vào mỗi thứ 6 và ngày làm việc cuối cùng của tháng mà không cần sự can thiệp thủ công.
Cơ chế: Xây dựng lớp quản lý thanh toán (PaymentManager) đảm bảo xử lý thanh toán đúng thời gian và theo phương thức đã được nhân viên lựa chọn.

