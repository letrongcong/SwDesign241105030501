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
![lopPhanTich](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3XTNKdvfNafYKQL2G69bRcfUYMzgIKP-Id1gJcfoIMP-NgYdGcAnWYDNSdvUIL5-3gegPuXWJceHI94J5r0YiwHImJMt82U_CZKL9EWC4uHg18cvS74vAkZgAZWfS3c1Q6SexQB0nUMGcfS2SXS0003__mC0)
#### Giải thích:
      - Mối quan hệ sử dụng giữa PaymentMethodSelectionUI và PaymentMethodController cho phép giao diện người dùng gửi yêu cầu đến lớp điều khiển để xử lý logic.
      - Mối quan hệ thao tác giữa PaymentMethodController và các thực thể EmployeeEntity và Payment cho phép lớp điều khiển cập nhật và quản lý thông tin liên quan đến nhân viên và phương thức thanh toán.
## 4. Phân tích ca sử dụng Maintain Timecard
### a. Các lớp phân tích cho ca sử dụng Selected Payment
    -  Lớp Boundary: TimecardUI
    -  Lớp Controller: TimecardController
    -  Lớp Entities: Timecard, Employee, ChargeNumber
### b. Biểu Sequence của ca sử dụng Select Payment
![MaintainTimecard](https://www.planttext.com/api/plantuml/png/Z5CnQiCm5DrrYa_sNA13QU9uA8LExG4KsLW2MmwE7EgnTCXGEcJeL08neHGAWOPsieOE2hs7Jj0hLB9ZfmbrYGTZVR_t_lllsz_oysmiS2BIA4IOY3W1Dng5SURxQ1YdtCD91bSiyWbElEjpm6Fe8H9paSHXKtUgS-WdzdqV-LmmaJL2jkZKnPfZYuEww52S1Fvb6Wqh2HUXXjmzXHwSGAPUKo2wU4c1KrsiHX0mBUSGgaK44_Cu9QXdmNq3fkPynq5GBU_B-vmPEEQ_qILeQa2wo1dgMwfZgA4kdZF3KHyy0C5u6ntXKC151IFglHK6vYh51qRSzefR3KLQFZ4JYLUvSHit7kOKnYed52Ar14_BDQYS8nUwsu55eeibJBIyRGNtwoJtmjdNEyYS6CW3tyF0H2sEM42WvOhz0MYI2B_UqjRC_jbz9Tn6FEX_oDkr5nHdi9bf-SZAx7AxRAfoAwqM9i3EPcQcBbcT7Ut6n5esNvDM3yUDs6oZb2m3vLkJP-OBi7_Z3m000F__0m00)
### c. Nhiệm vụ của từng lớp phân tích:
      - TimecardUI (Boundary): Chứa các phương thức để hiển thị thông tin thời gian làm việc, nhập giờ làm việc và gửi thời gian làm việc.
      - TimecardController (Controller): Chứa các phương thức để xử lý việc lấy thời gian làm việc, tạo mới, xác thực và gửi thời gian làm việc.
      - Employee (Entity): Lớp này chứa thông tin của nhân viên và phương thức để lấy thông tin thời gian làm việc.
      - Timecard (Entity): Lưu trữ thông tin về số giờ làm việc và mã dự án. Nó có các phương thức để thiết lập giờ làm việc và gửi thời gian làm việc.
      - ChargeNumber (Entity): Chứa thông tin về mã dự án, cho phép hệ thống quản lý các mã dự án mà nhân viên có thể ghi nhận giờ làm việc.
### d. Một số thuộc tính của các lớp phân tích:
      - TimecardUI (Boundary)
            displayCurrentTimecard(): Phương thức hiển thị thời gian làm việc hiện tại cho nhân viên.
            enterWorkedHours(): Phương thức cho phép nhân viên nhập số giờ làm việc.
            submitTimecard(): Phương thức để gửi thời gian làm việc lên hệ thống.
      - TimecardController (Controller)
            retrieveTimecard(): Nhận một đối tượng Employee và trả về Timecard hiện tại của nhân viên.
            createNewTimecard(): Nhận một đối tượng Employee và tạo một Timecard mới nếu chưa có.
            validateWorkedHours(): Nhận số giờ làm việc và mã dự án, trả về true nếu hợp lệ, ngược lại trả về false.
            submitTimecard(): Nhận một đối tượng Timecard và xử lý việc gửi thời gian làm việc.
      - Employee (Entity)
            id: String: ID duy nhất của nhân viên.
            name: String: Tên của nhân viên.
            getTimecard(): Timecard: Phương thức để lấy Timecard của nhân viên.
      - Timecard (Entity)
            hoursWorked: Map<Date, int>: Bản đồ lưu trữ số giờ làm việc cho từng ngày (khóa là ngày, giá trị là số giờ).
            chargeNumbers: List<ChargeNumber>: Danh sách mã dự án liên quan đến thời gian làm việc.
            status: String: Trạng thái của thời gian làm việc (ví dụ: "chưa gửi", "đã gửi").
            setHours(date: Date, hours: int): Phương thức để thiết lập số giờ làm việc cho một ngày cụ thể.
            submit(): Phương thức để gửi thời gian làm việc.
      - ChargeNumber (Entity)
            code: String: Mã của dự án.
            description: String: Mô tả của mã dự án.
### e. Biểu đồ lớp mô tả lớp phân tích
![lopPhanTich](https://www.planttext.com/api/plantuml/png/H8wx3SCm34HxJi45l8CjMaMQLCa0j4Ka1lG9QAdmR2uoKbO81Cj9zN3lS0G_-xjVCsikmGDCgKJ7kk5j2JApkli5USK1vXIp9l_pT6GlMdi34lEI_xCgwPGsl7pQHAeSJqbFreTSIvYE4nPWmAv3Ws0ggN5ij0ZK2Br4Lz_z0W00__y30000)
#### Giải thích:
      - MMối quan hệ sử dụng giữa TimecardUI và TimecardController: Cho phép giao diện người dùng gửi yêu cầu nhập và gửi thông tin thời gian làm việc đến lớp điều khiển để xử lý.
      - Mối quan hệ thao tác giữa TimecardController và các thực thể Timecard và Employee: Cho phép lớp điều khiển cập nhật và quản lý thông tin thời gian làm việc của nhân viên, cũng như liên kết với thông tin của nhân viên.
      - Mối quan hệ thao tác giữa TimecardController và ChargeNumber: Cho phép lớp điều khiển truy xuất danh sách mã dự án để nhân viên ghi nhận giờ làm việc.

## 5. Hợp nhất kết quả phân tích
![hopnhat](https://www.planttext.com/api/plantuml/png/L93D3OCm34RldY8Bi0EG0Eg1gbBR0GAn2b9-gX0EpDP3H-eAnKgWvVIIvo-sbS_hdKz1-Z0R3T2vsIhf5tOR3VRIg_k9oOaLq3iRlDExv_6kqLEz1BHX3Bzd9FacA_FKRa4aAJR91-aVU9vD5rjKVyClSZ5hhCKmE7L5ZNqOdOshrFigXzHndsQRaZBaMe2QPTbQQmWYOhLGqA5aK19veaYi6F14oD4g-gOl0000__y30000)
#### Tài Liệu Mô Tả Ca Sử Dụng
   - Ca Sử Dụng: Quản Lý Thông Tin Nhân Viên và Thời Gian Làm Việc
   - Mô tả ngắn gọn: Ca sử dụng này cho phép nhân viên cập nhật thông tin phương thức thanh toán và ghi nhận thời gian làm việc. Nhân viên có thể chọn phương thức thanh toán (nhận trực tiếp, qua bưu điện hoặc chuyển khoản) và ghi lại tất cả giờ làm việc hàng tuần cho các dự án mà họ đã làm việc. Nhân viên chỉ có thể thay đổi thông tin thời gian làm việc cho kỳ thanh toán hiện tại và trước khi thời gian làm việc đã được gửi.
   - Luồng sự kiện
      + Luồng cơ bản
         1. Nhân viên đăng nhập vào hệ thống.
         2. Nhân viên chọn phương thức thanh toán mong muốn:
            Hệ thống hiển thị các tùy chọn phương thức thanh toán.
            Nhân viên chọn một phương thức thanh toán và cung cấp thông tin cần thiết (địa chỉ nhận séc hoặc thông tin tài khoản ngân hàng nếu cần).
            Hệ thống cập nhật thông tin nhân viên với phương thức thanh toán đã chọn.
         3. Nhân viên muốn nhập thời gian làm việc cho kỳ thanh toán hiện tại:
            Hệ thống lấy và hiển thị thời gian làm việc hiện tại cho nhân viên. Nếu không có thời gian làm việc cho kỳ thanh toán hiện tại, hệ thống tạo mới.
            Hệ thống lấy và hiển thị danh sách các số tài khoản dự án từ cơ sở dữ liệu quản lý dự án.
            Nhân viên chọn số tài khoản và nhập số giờ làm việc cho bất kỳ ngày nào trong khoảng thời gian.
            Hệ thống lưu thời gian làm việc.
         4. Gửi thời gian làm việc
            Nhân viên yêu cầu hệ thống gửi thời gian làm việc.
            Hệ thống gán ngày hiện tại cho thời gian làm việc và thay đổi trạng thái thành “đã gửi”.
            Hệ thống xác thực số giờ làm việc, đảm bảo không vượt quá giới hạn cho phép.
            Hệ thống lưu thời gian làm việc và làm cho nó trở nên chỉ đọc.
      + Luồng thay thế
         1. Số giờ không hợp lệ: Nếu số giờ không hợp lệ được nhập (>24) hoặc vượt quá giới hạn, hệ thống hiển thị thông báo lỗi và yêu cầu nhập lại.
         2. Thời gian làm việc đã được gửi: Nếu thời gian làm việc đã được gửi, hệ thống hiển thị bản sao chỉ đọc và thông báo cho nhân viên.
         3. Cơ sở dữ liệu quản lý dự án không khả dụng: Hệ thống hiển thị thông báo lỗi về danh sách số tài khoản không khả dụng.
   - Yêu cầu đặc biệt: Không có.
   - Điều kiện trước: Nhân viên phải đăng nhập vào hệ thống trước khi bắt đầu ca sử dụng này.
   - Điều kiện sau: Nếu ca sử dụng thành công, phương thức thanh toán và thông tin thời gian làm việc của nhân viên sẽ được cập nhật trong hệ thống. Nếu không, trạng thái hệ thống không thay đổi.
