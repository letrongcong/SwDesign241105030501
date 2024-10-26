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
![UMLPayroll](https://www.planttext.com/api/plantuml/png/R8_13S8m34Nldi8Bq15GWHvxw0fMi2AhgODYzu0Gat5W95Q0Y0C8ukD_Jq_outRlpQdukYG0cqMnP6C05q-C4uMP8Xjky93830UXM6W1EBq9JeMDrSabwqXdBeWNk7xuVZLHDXjpbD0I1dBQXL2LBmh_tQxRjchGsAhwsuLwFUlnzUaJ003__mC0)

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
###  g. Lưu trữ và Kiểm tra Giao dịch
      - Lưu trữ lịch sử thanh toán và chấm công để hỗ trợ kiểm toán và giải quyết tranh chấp.
      - Kiểm tra bất thường như giờ làm quá mức và mã chi phí không hợp lệ.

##  3. Phân tích ca sử dụng Select Payment
### a. Các lớp phân tích cho ca sử dụng Selected Payment
    -  Lớp Boundary: PaymentMethodSelectionUI
    -  Lớp Controller: SelectPaymentController
    -  Lớp Entities: Employee và Payment
### b. Biểu Sequence của ca sử dụng Select Payment
![PaymentMethod](https://www.planttext.com/api/plantuml/png/j9G_IyD06CRt-nGldNJm2pX8eOY8A88LNEFrw0MlTo6z3Xd5ISIXasjZSL0eABYO31rI-Ztk4_WLV2z9_zacrefPBXnvdz_pFk_bFkDXjQqTNtTQWZXKAn_sMvvG0MFaKdLam_43E7M25fFwc6ck6cTCCAfT9SyF2LLI-qeiVb3BDWNp2UwvUbfFo4GQTlOAHM4Nk6lY6mcQc_WEQ19IyFZuTHpAPhhtJ75n90Ujab2IGY64J87VH7No4G35rtkveBMcGM6Yfs39rAYRz7FHKbC5QQ5kxgYasws9msr27A7XX9je8A6EpLtZOgBGXHfMFH30fuWqCu5GZSb4GssR6dWhs4aFuPK9Q4Qe_8IO2v-csj9gwBBsId5Cj1aSc7ZWGXqbbl75myy6DkhYx9qqvTkqUiMubmAPByewi2vNuOi2NcX-Kxc_X3dBB0-nnZj1-ZSSSMMYFkRic_YDscCK3RtV1ukWTsl1bI2RoQC42swk7R5ENZOhR9kuYzKz5wwoHZOSIed_Vnf9-GHmJB91o7hi2tj1vYTfNH-aYW1xvNy1003__mC0)
### c. Nhiệm vụ của từng lớp phân tích:
   - Boundary: Lớp PaymentMethodSelectionUI tương tác trực tiếp với người dùng, hiển thị các phương thức thanh toán và nhận đầu vào từ nhân viên.
   - Controller: Lớp PaymentMethodController thực hiện các tác vụ liên quan đến việc cập nhật thông tin nhân viên và phương thức thanh toán sau khi nhận đầu vào từ lớp giao diện người dùng.
   - Entities:
      + Employee: Lưu trữ thông tin về nhân viên, bao gồm cả phương thức thanh toán.
      + Payment: Lưu trữ thông tin về phương thức thanh toán cụ thể, bao gồm địa chỉ, tên ngân hàng và số tài khoản (nếu cần).
### d. Một số thuộc tính của các lớp phân tích:
   - Boundary:
      + PaymentMethodSelectionUI: Lớp giao diện người dùng cho phép nhân viên chọn phương thức thanh toán.
      + Phương thức:
         displayPaymentMethods(): Hiển thị các phương thức thanh toán có sẵn.
         getSelectedMethod(): Lấy phương thức thanh toán mà nhân viên đã chọn.
         getAddress(): Lấy địa chỉ nếu phương thức thanh toán là "mail".
         getBankDetails(): Lấy thông tin ngân hàng nếu phương thức thanh toán là "direct deposit".
   - Controller:
      + PaymentMethodController: Lớp điều khiển xử lý logic của ca sử dụng.
      + Phương thức:
         selectPaymentMethod(employee): Cho phép nhân viên chọn phương thức thanh toán và cập nhật thông tin.
   - Entities:
      + Employee: Lớp lưu trữ thông tin nhân viên.
            Thuộc tính:
            employeeId
            name
            paymentMethod
            mailingAddress
            bankName
            accountNumber
      + Payment: Lớp lưu trữ thông tin về phương thức thanh toán.
            Thuộc tính:
            method: Phương thức thanh toán (pick up, mail, direct deposit)
            mailingAddress: Địa chỉ (nếu phương thức thanh toán là "mail")
            bankName: Tên ngân hàng (nếu phương thức thanh toán là "direct deposit")
            accountNumber: Số tài khoản ngân hàng (nếu phương thức thanh toán là "direct deposit")
### e. Biểu đồ lớp mô tả lớp phân tích


