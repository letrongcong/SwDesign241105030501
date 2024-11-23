# Lab4 - Usecase Design 

## 1. Describe interaction among design objects 

### Xác định các đối tượng tham gia và cách chúng tương tác với nhau trong từng ca sử dụng.

#### Trong Payroll System, sự tương tác giữa các đối tượng thiết kế có thể được mô tả như sau:
- Nhân viên (Employee):
  - Gửi thông tin làm việc (giờ làm, ngày làm,...) vào hệ thống thông qua các biểu mẫu.
  - Thông tin này được lưu trữ lại để tính lương.
- Phiếu chấm công (Timecard):
  - Ghi lại chi tiết giờ làm của nhân viên.
  - Được kiểm tra và cập nhật thông tin bởi hệ thống.
- Bộ điều khiển chấm công (TimecardController):
  - Kiểm tra và cập nhật thông tin trên phiếu chấm công.
  - Phân bổ giờ làm cho các dự án khác nhau.
- Bộ điều khiển tính lương (PayrollController):
  - Tính lương cho từng nhân viên dựa trên loại hợp đồng (giờ, tháng, hoa hồng).
  - Sử dụng thông tin từ phiếu chấm công để tính lương.
- Hệ thống ngân hàng (BankSystem):
  - Xử lý việc chuyển lương vào tài khoản nhân viên.
- Biểu mẫu trả lương (Paycheck):
  - Được tạo ra sau khi tính lương.
  - Chứa thông tin về số tiền lương, ngày trả lương,...
- SystemClockInterface là thành phần chịu trách nhiệm xác định thời điểm cần thực hiện tính lương và kích hoạt quy trình tính lương

## 2. Simplify sequence diagrams using subsystems 

### Để đơn giản hóa sequence diagrams, chúng ta có thể nhóm các thành phần liên quan thành các subsystem:
- Subsystem Quản lý nhân viên (Employee Management Subsystem):
  - Thành phần: Employee, TimecardController
  - Chức năng: Xử lý tất cả các hoạt động liên quan đến nhân viên, bao gồm nhập dữ liệu giờ làm và quản lý phiếu chấm công.
- Subsystem Xử lý tính lương (Payroll Processing Subsystem):
  - Thành phần: PayrollController, Paycheck, Timecard
  - Chức năng: Thực hiện tính toán lương, tạo phiếu trả lương và sử dụng dữ liệu từ phiếu chấm công.
- Subsystem Ngân hàng (Banking Subsystem):
  - Thành phần: BankSystem
  - Chức năng: Thực hiện thanh toán lương và giao tiếp với dịch vụ ngân hàng bên ngoài.
- Subsystem Định thời hệ thống (System Timing Subsystem):
  - Thành phần: SystemClockInterface
  - Chức năng: Kích hoạt quy trình tính lương vào các thời điểm được định trước.

### Sequence diagrams đã được đơn giản hóa:
#### Sequence diagrams của ca sử dụng Select Payment Mebthod

![SP](https://www.planttext.com/api/plantuml/png/b9HDReCm48NtFeML5P7I2sHHfMswo29g97A1YPc05MCZUuZ4sRheaNg56Z24dx0eEu_dVNv-3Fn-_-mSWQKoLmm46Si_yqAP2f4LlYo5B40JNtLLVWGDAUReYt5vSPKZp5SSNA_hgsF02IfhbE8dQmGw9tKwqOU61VaxwDjS4weBchYfyRFCvygskEnLP2XkdQzcCMxP0y4574wmNVa1PdroBw_pZFYMErGeo9zIPtf4oamIhTcyqykd4NcrHR8IxnYs3lfg8WpQGx9cCud7p4nwJeha8q41DgctHunv_wANqkeHvhc19re1IfGA26DGOAk81fH5IFDU6lCQhTTsfO7x3NSDi66q_Gi9EBZtW3qIIEL6d2Bi_JUFs7DZ0YfTD3On7Lwla5gIR2zIJqDK3AUYkyg6TxRUX32bfZLZZFjd1dn-25dGxegsJVfi0YMQK1_9BR7xoTvoRKXUgs0xtBOOhjQjnQTZFU1ae9ElEzeFS5dKdSyc7-j2tFv3I5EqOIVyPtpcEzH9_Nlx0m00__y30000)

#### Sequence diagrams của ca sử dụng Maintain Timecard

![MT](https://www.planttext.com/api/plantuml/png/d9H1ReCm44Ntd6B4YaZj1RAeiaWMMKIAGjlzn4nIgyP6zZWIP-kYH-eLQbgW1KpKb8Kb1l_dhy-7ZxVtbMEqx4kLe61ZOLDMojH4IHN6KiWADKFQJM676izKKXZc_kXgnrIcWAxNzTCXO8-rDKh1tXf1pabz7kdR3JFoDJ8UqT58r8r_L4dlzFvXwWcM87Nb-L6M9D0MQsAKocNStGVU8fdA0cliBw0kg6I1J1rjX9aeuXJnGkArGnoyeh4TL0pR4tHRG3fuRavE85onGoQfX5CSNkPyDfYf96xM4dkhym3B6TcxR37h8XQ-DYnFTUv5qu5M6qsxVujBAAIh5DQxe0ZDoz8-XyP5MBzX9wzKdIuIKg4aexIs-d8rhtcd6skDpQXPswhyo_CGGBhuSyLy5ItOjhXh7rtfMgm6Gzw1XBb6lQqLJr_IlXUt9JqG-rytCv_ZVDX3yIgatVpSFW400F__0m00)

#### Sequence diagrams của ca sử dụng Run Payroll

![RP](https://www.planttext.com/api/plantuml/png/f9LDRi8m48NtEON5Yahq0brKKEW2YKf8eGSOd25OE7PaJohbR5tqIBr2JUmGaJXLex8RPzxdDpyatvzVIqjWg2fa0foqOMbj2OkrrFooLOJc11oJqgK8BafGn6Pxg8sMaksDvcYjK3bBgwDjT3C6beM4s-6zV0C4Hx3O4xN78oh7v6Vab_Q29hXFUG5r6Pe9fnqsYLN87fy7jjaJ8oFo74ru4WgUFoJ98DVf1nKuG8wqalArAAMk4G-YG0uckoA6sN4B1gaogbLULNFiuqOCHMWS9Aya4AOWmGYqCTW8gsbvKvD2un3jKOInO3RmlJKl7UcHXOyRQuC4Gjfv6UATi3IrLwdZfGHKJPfKLMQ-fYRRoqiVRRE5Mq0_VCncK_syD-JV7VMtr8bBVw7BBb1HloK9I6BR4mkFsHlIMMTC-8Ld1mFAdj0apFq6yFY553JDQjG7lU9SLyERnuYH-fKcSQg3nQwdNUHfVnsHrFc0rSudWfqsfPtERoD2wLvFqUQkmPudUqQLkMPrW_Hnryr_65LPV9-YxxYsWzVijNR_MIIXbSCi7UVw1VW1003__mC0)

## 3. Describe persistence-related behavior

### Các hành vi persistence-related của hệ thống có thể được mô tả bằng cách tập trung vào cách dữ liệu được lưu trữ và truy xuất:

- Các lớp liên quan đến lưu trữ:
  - Employee: Lưu thông tin cơ bản như tên, địa chỉ, và phương thức thanh toán.
  - Timecard: Ghi lại dữ liệu giờ làm việc của nhân viên làm việc theo giờ.
  - Đối tượng Employee và Timecard được lưu trữ liên tục trong cơ sở dữ liệu. Mỗi Employee có một mã định danh duy nhất (empID), và các bản ghi Timecard liên quan được lưu trong bảng riêng, liên kết thông qua empID.
  - PurchaseOrder: Lưu thông tin các đơn đặt hàng của nhân viên hưởng hoa hồng.
  - Paycheck: Lưu thông tin về các phiếu trả lương đã được tạo.
  - Project: Được lưu trong một bảng riêng và liên kết với Timecard thông qua charge codes.
- Hành vi lưu trữ:
  - Gửi phiếu chấm công (Timecard): Khi nhân viên gửi Timecard, hệ thống lưu thông tin giờ làm việc, mức lương giờ, và trạng thái (draft hoặc submitted) vào cơ sở dữ liệu, đảm bảo dữ liệu luôn chính xác và đồng nhất.
  - Tạo phiếu trả lương (Paycheck): Sau khi tạo Paycheck, hệ thống lưu chi tiết phiếu trả lương vào lịch sử giao dịch, giúp theo dõi và kiểm tra khi cần thiết.
  - Cập nhật thông tin nhân viên (Employee Information): Các thông tin như phương thức thanh toán, tài khoản ngân hàng, và mức lương được cập nhật thường xuyên. Bất kỳ thay đổi nào cũng sẽ được lưu ngay lập tức trong cơ sở dữ liệu để phản ánh đúng tình trạng hiện tại của nhân viên.

 ## 4. Refine the flow of events description 

### Luồng sự kiện trong Hệ thống tính lương có thể được tinh chỉnh, làm mịn thành các bước sau:
- Duy trì Phiếu Chấm Công (Maintain Timecard):
  - Nhân viên truy cập giao diện TimecardForm để nhập dữ liệu.
  - Giao diện TimecardForm hiển thị thông tin phiếu chấm công hiện có và cho phép nhân viên nhập số giờ làm việc.
  - TimecardController xử lý thông tin được gửi từ biểu mẫu, kiểm tra tính hợp lệ của dữ liệu, và cập nhật hồ sơ của nhân viên.
  - Nếu phiếu chấm công đã hoàn chỉnh, nhân viên gửi phiếu qua hệ thống.
      - TimecardController thay đổi trạng thái của phiếu từ draft sang submitted để chuẩn bị cho các bước tiếp theo trong quy trình tính lương.
- Chạy Quy Trình Tính Lương (Run Payroll):
  -SystemClockInterface kích hoạt quy trình tính lương vào ngày đã được định trước (payday).
  - PayrollController thực hiện việc tính lương dựa trên từng loại nhân viên:
    - Nhân viên theo giờ (HourlyEmployee): Lương được tính dựa trên tổng số giờ làm việc được ghi nhận và mức lương theo giờ của nhân viên.
    - Nhân viên lương cố định (SalariedEmployee): Lương tháng được xác định dựa trên mức lương hàng năm, có điều chỉnh các khoản khấu trừ cần thiết.
    - Nhân viên hoa hồng (CommissionedEmployee): Tiền lương được tính dựa trên tỷ lệ hoa hồng và tổng doanh thu bán hàng.
- Hệ thống phân phối lương:
    - Đối với nhân viên sử dụng phương thức chuyển khoản trực tiếp (direct deposit), BankSystem thực hiện các giao dịch chuyển khoản đến tài khoản ngân hàng của họ.
    - Với nhân viên không dùng chuyển khoản, PrinterInterface sẽ tạo và in phiếu trả lương (paycheck).
- Các phiếu trả lương (Paycheck) được lưu trữ và hệ thống hoàn tất quy trình.
- Phiếu trả lương có thể được gửi qua thư hoặc lưu trữ trong lịch sử giao dịch để kiểm tra sau này.

## 5. Unify classes and subsystems 

### Thống nhất các lớp và hệ thống qua biểu đồ sau:

![class](https://www.planttext.com/api/plantuml/png/b5MxRjmm4Epr5OIgf32Gj2eCntSEuiB0mGgGUe_Qqn4Ybm8V1fJ0NvOYdvHV2FMmJhoZBWaB5RkpiyETbVJxvwyxwy0uhsHc6q4j652CIx3satD6xBt3Hwwf5D-HVSYo5dW3DRByGRLITuZi2IW4599ZfT_RpZfKEVkHiN067ZP3n-1uKBMFsuALeGVLYpY1maGOgigWjObC2rtV_0dTKLTH_ZLRYFWg578mLIJ2JS6aaZM5H-sD_QPDWw7TPwd1BP9XcCxRlylOQ796Iuac4lG2KbJWy0tsxdt1xhMM2BH0-VOSyw95jMmsZpp_cBERcrkMAw0kFqsXODnW8B4nl8Sc91RCsm1zNVY_WwvFiftHF1WJBhjc_uHSkJ47oRqCIYPOwZOp3pyYRwBoTWh-buEWj2TNiAtsUucNkxGDSa8sF2zLV0dkoowvqiSXzJmMdwYZyX8a685LaW28FCW1qgrJRBHI8anSqmeDdm5hMYujMHh_PlSwShQYO3KIcdcHql2pcHKdqwzLNOpg7-kIyubgbtjy3zHSMTu-NGxn-CDXWEm1pMvScDJIfiKj-8h08keQJIneoWOphiWQGHkfm-QJGtC0ZcS21-ehBrMIOZBtJ7Z1I3jn4EFexf2g_dVn1m00__y30000)
