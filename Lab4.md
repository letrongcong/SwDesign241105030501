# Lab4 - Usecase Design 

## 1. Describe interaction among design objects 

### Xác định các đối tượng tham gia và cách chúng tương tác với nhau trong từng ca sử dụng.

#### Trong Payroll System, sự tương tác giữa các đối tượng thiết kế có thể được mô tả như sau:
a. Nhân viên (Employee):
  - Gửi thông tin làm việc (giờ làm, ngày làm,...) vào hệ thống thông qua các biểu mẫu.
  - Thông tin này được lưu trữ lại để tính lương.
b. Phiếu chấm công (Timecard):
  - Ghi lại chi tiết giờ làm của nhân viên.
  - Được kiểm tra và cập nhật thông tin bởi hệ thống.
c. Bộ điều khiển chấm công (TimecardController):
  - Kiểm tra và cập nhật thông tin trên phiếu chấm công.
  - Phân bổ giờ làm cho các dự án khác nhau.
d. Bộ điều khiển tính lương (PayrollController):
  - Tính lương cho từng nhân viên dựa trên loại hợp đồng (giờ, tháng, hoa hồng).
  - Sử dụng thông tin từ phiếu chấm công để tính lương.
e. Hệ thống ngân hàng (BankSystem):
  - Xử lý việc chuyển lương vào tài khoản nhân viên.
f. Biểu mẫu trả lương (Paycheck):
  - Được tạo ra sau khi tính lương.
  - Chứa thông tin về số tiền lương, ngày trả lương,...
g. SystemClockInterface là thành phần chịu trách nhiệm xác định thời điểm cần thực hiện tính lương và kích hoạt quy trình tính lương

## 2. Simplify sequence diagrams using subsystems 

### Để đơn giản hóa sequence diagrams, chúng ta có thể nhóm các thành phần liên quan thành các subsystem:
a. Subsystem Quản lý nhân viên (Employee Management Subsystem):
  - Thành phần: Employee, TimecardController
  - Chức năng: Xử lý tất cả các hoạt động liên quan đến nhân viên, bao gồm nhập dữ liệu giờ làm và quản lý phiếu chấm công.
b. Subsystem Xử lý tính lương (Payroll Processing Subsystem):
  - Thành phần: PayrollController, Paycheck, Timecard
  - Chức năng: Thực hiện tính toán lương, tạo phiếu trả lương và sử dụng dữ liệu từ phiếu chấm công.
c. Subsystem Ngân hàng (Banking Subsystem):
  - Thành phần: BankSystem
  - Chức năng: Thực hiện thanh toán lương và giao tiếp với dịch vụ ngân hàng bên ngoài.
d. Subsystem Định thời hệ thống (System Timing Subsystem):
  - Thành phần: SystemClockInterface
  - Chức năng: Kích hoạt quy trình tính lương vào các thời điểm được định trước.
