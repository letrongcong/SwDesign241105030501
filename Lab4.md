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
