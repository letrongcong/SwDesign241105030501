## LAB 1
## PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG

## 1. Phân tích kiến trúc 
   - Lựa chọn kiến trúc: Kiến trúc phân lớp (Layered Architecture)
   - Lý do lựa chọn:
    + Tách biệt nhiệm vụ: Dễ bảo trì, mỗi lớp chỉ thực hiện một nhiệm vụ cụ thể.
    + Dễ mở rộng và bảo trì: Thay đổi logic, giao diện hoặc truy xuất dữ liệu không ảnh hưởng đến các lớp khác.
    + Bảo mật tốt hơn: Kiểm soát quyền truy cập dữ liệu qua từng lớp.
    + Dễ kiểm thử và phát triển song song: Từng lớp kiểm thử độc lập, tăng hiệu quả phát triển.
    + Tái sử dụng mã nguồn: Logic tính toán và nghiệp vụ có thể dùng lại trong các hệ thống khác
   - Ý nghĩa từng thành phần trong kiến trúc:
    + Presentation Layer: Đảm bảo tương tác của người dùng dễ dàng, mọi giao diện và API đều truy xuất qua lớp này.
    + Business Logic Layer: Kiểm soát các quy tắc nghiệp vụ phức tạp và đảm bảo hệ thống hoạt động đúng như mong đợi.
    + Data Access Layer: Cung cấp các phương thức để truy vấn và cập nhật dữ liệu từ cơ sở dữ liệu một cách hiệu quả và an toàn.
  - Biểu đồ UML Package cho Hệ thống Payroll:
!(UMLPayroll)(https://www.planttext.com/api/plantuml/png/R8_13S8m34Nldi8Bq15GWHvxw0fMi2AhgODYzu0Gat5W95Q0Y0C8ukD_Jq_outRlpQdukYG0cqMnP6C05q-C4uMP8Xjky93830UXM6W1EBq9JeMDrSabwqXdBeWNk7xuVZLHDXjpbD0I1dBQXL2LBmh_tQxRjchGsAhwsuLwFUlnzUaJ003__mC0)

## 2. Danh sách các cơ chế phân tích trong hệ thống Payroll:
###  a. Quản lý Nhân viên và Thông tin Lương
      - Payroll Administrator quản lý thêm, xoá, cập nhật thông tin nhân viên (tên, địa chỉ, loại lương: giờ, cố định, hoa hồng) và phương thức thanh toán (gửi bưu điện, chuyển khoản, nhận tại văn phòng).
      - Phân loại nhân viên theo giờ làm, lương cố định, hoặc lương có hoa hồng.
###  b. Chấm công và Quản lý Hoá đơn
      - Ghi nhận bảng chấm công (giờ làm, mã chi phí) và tính lương làm thêm cho nhân viên tính theo giờ (>8 giờ trả 1.5 lần).
      - Quản lý hoá đơn bán hàng để tính hoa hồng dựa trên tỷ lệ quy định (10%, 15%, 25%, 35%).
###  c. Quản lý Phương thức Thanh toán
      - Nhân viên chọn phương thức nhận lương: bưu điện, chuyển khoản ngân hàng, hoặc nhận tại văn phòng.
###  d. Báo cáo và Thông tin Nghỉ Phép
      - Nhân viên xem báo cáo về tổng giờ làm, lương nhận, giờ làm từng dự án, và số ngày nghỉ phép còn lại.
      - Payroll Administrator truy cập báo cáo tổng quan và báo cáo tuỳ chỉnh theo nhu cầu.
###  e. Tích hợp và Tự động hoá
      - Kết nối với cơ sở dữ liệu dự án DB2 (không chỉnh sửa) để lấy mã chi phí.
      - Tự động chạy quy trình trả lương mỗi thứ Sáu và ngày làm việc cuối tháng.
###  f. An ninh và Phân quyền
      - Chỉ Payroll Administrator xem thông tin toàn bộ nhân viên; nhân viên chỉ truy cập thông tin cá nhân.
      - Sử dụng xác thực đa yếu tố (MFA) để tăng cường bảo mật.
###  g. Báo cáo:
      - Nhân viên: Xem tổng giờ làm, tổng giờ cho từng dự án, tổng lương nhận năm, ngày nghỉ còn lại.
      - Payroll Administrator: Lập báo cáo quản trị, theo dõi lịch sử thanh toán, tạo báo cáo tùy chỉnh theo phòng ban, loại nhân viên, hoặc thời gian.



