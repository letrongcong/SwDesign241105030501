#LAB 2 PHÂN TÍCH CÁC CA SỬ DỤNG TRONG PAYROLL SYSTEM

## Phần 1 : Create Administrative Report

### a. Các lớp phân tích
-  Lớp Controller: ReportController
-  Lớp Entities: Report, Employee, ReportData
-  Lớp Boundary: ReportUI, ErrorMessageDisplay, ReportDisplay

### b. Biểu đồ sequence
![BieuDoSequence](https://www.planttext.com/api/plantuml/png/h5N1Qjj04BthA-ReWFi31fSubY6XJZ72EUGeoy8IaLQgj3BHiVIGGmx5Xz9JmQufWQGcXXOAqY67DVwF_OB-GcVNShnoh9vo4MZdpRmtRsUal_dJSKpDY2Q-fsccHOC8UcOQ1PxN6lekSMCQcUBGZA7Nqa94kfORceI2OOT1HDi1eG9jIuZHFW2HWT9vnm-z8BLj4UaSoD1DQiei_K3muao4BixA5QCeYCxjE3P7jkx6eMUcilZveGeA01cqPXDEUFP8OJNXsLq27n8s0ngndyI1PbFhjU3DM-Hhm2MxJy2I6CgpMG03XWyB7ngAGb2lrO1Jb-UV2527vxSm42y9-3nxI80uF5k4G5rPnc4B9LzXQITa95X-8DHXl_65kcG7XLetG79tTrA7zoCsJM6WDB4zk-BP4nLrCgiEVNPFK0NxJc2C8iXH8TjeDw0V9IdFFn8OylmHFDHzawXINvDLEDul6oYCDjfIJED5x3Mv3S7HQK0N3KvBpIemg5bEWBUMVtNBsPsjmeXdSnYZOTKbOfvFO8I1R-2ngO_7YB70mLx-ME2jb-iPtkrbNoz46JhMPGiSEihpBnZwVu42fDJH3BqapvEcgVfM4pO7kk48s8p8coWFxCiB4JDPWTdKaxTLqnMUPyJpXEcLDN3Hq2sVJGauOkMABgfPfUZkUfcKnUuMw9JddrsujdsC_G8_GHk9y4bDk9ARLRMsrsncRTPrFx5gKKKFOpOL8t4hMbhivntOD6MxA_9tAx7NBq83CG4t8TH4RdsNk9qcP3efNzHgibxoV6vjf27x5EV0aZu8Iz_j5cV_4xYH8Mog0jNsk2H5CQa38GrzlKkF5CFLIhGOOeg-QzgnJORYT_GF003__mC0)

### c. Nhiệm vụ của từng lớp phân tích
- Controller :
  - ReportController: Lớp chính điều khiển toàn bộ luồng tạo báo cáo, xác thực thông tin đầu vào và quyết định các hành động tiếp theo.
- Entities :
  - Report: Lớp đại diện cho một báo cáo. Nó chứa thông tin về loại báo cáo, ngày bắt đầu và kết thúc, cùng với dữ liệu tính toán.
  - Employee: Lớp đại diện cho một nhân viên trong hệ thống, chứa các thông tin cần thiết để tạo báo cáo.
  - ReportData: Lớp chứa dữ liệu tính toán liên quan đến báo cáo, như tổng số giờ làm việc hoặc tổng lương.
- Boundary :
  - ReportUI: Giao diện người dùng (UI) cho phép Quản trị viên Bảng Lương nhập thông tin để tạo báo cáo, ví dụ như loại báo cáo, ngày bắt đầu và kết thúc, và tên nhân viên.
  - ErrorMessageDisplay: Lớp hiển thị thông báo lỗi khi có thông tin thiếu hoặc sai trong quá trình nhập liệu.
  - ReportDisplay: Lớp hiển thị báo cáo cho người dùng sau khi hệ thống đã tạo ra báo cáo.

### d. Một số thuộc tính và phương thức của các lớp phân tích
- ReportController:
    - Phương thức:
      - createReport(): Tạo báo cáo dựa trên yêu cầu của người dùng.
      - validateInput(): Kiểm tra tính hợp lệ của các thông tin đầu vào (loại báo cáo, ngày bắt đầu, ngày kết thúc, tên nhân viên).
      - saveReport(): Lưu báo cáo vào vị trí được chỉ định.
      - discardReport(): Hủy bỏ báo cáo nếu người dùng không muốn lưu.
- Report: 
    - Thuộc tính:
      - reportType (String): Loại báo cáo (ví dụ: "Total Hours Worked", "Pay Year-to-Date").
      - startDate (Date): Ngày bắt đầu của báo cáo.
      - endDate (Date): Ngày kết thúc của báo cáo.
      - employeeList (List<Employee>): Danh sách các nhân viên cần báo cáo.
      - reportData (ReportData): Dữ liệu tính toán báo cáo.
    - Phương thức:
      - generateReport(): Tạo báo cáo bằng cách lấy dữ liệu từ các nhân viên trong phạm vi thời gian đã chỉ định.
      - saveToFile(String filePath): Lưu báo cáo vào tệp.
      - discard(): Hủy bỏ báo cáo.
  
- Employee:
    - Thuộc tính:
      - employeeId (String): Mã nhân viên.
      - employeeName (String): Tên nhân viên.
      - hoursWorked (float): Tổng số giờ làm việc (chỉ áp dụng cho báo cáo "Total Hours Worked").
      - payYTD (float): Tổng lương đã trả (chỉ áp dụng cho báo cáo "Pay Year-to-Date").
    - Phương thức:
      - calculateTotalHoursWorked(): Tính tổng số giờ làm việc của nhân viên trong khoảng thời gian được chỉ định.
      - calculatePayYTD(): Tính tổng lương đã trả cho nhân viên trong năm tài chính.

- ReportData:
    - Thuộc tính:
      - totalHoursWorked (float): Tổng số giờ làm việc trong báo cáo.
      - totalPayYTD (float): Tổng lương đã trả trong báo cáo.
    - Phương thức:
      - calculateHoursWorked(): Tính tổng số giờ làm việc.
      - calculatePayYTD(): Tính tổng lương đã trả.

- ReportUI:
    - Phương thức:
      - requestReportCriteria(): Hiển thị giao diện yêu cầu người dùng nhập các tiêu chí cho báo cáo (loại báo cáo, ngày bắt đầu, ngày kết thúc, tên nhân viên).
      - showReport(Report report): Hiển thị báo cáo cho người dùng.
      - showErrorMessage(String message): Hiển thị thông báo lỗi nếu thông tin nhập vào không hợp lệ.

- ErrorMessageDisplay:
    - Phương thức:
      - showError(String message): Hiển thị một thông báo lỗi cho người dùng.

- ReportDisplay: 
    - Phương thức:
      - displayReportData(Report report): Hiển thị các dữ liệu tính toán báo cáo (số giờ làm việc hoặc tổng lương).

### e. Mối quan hệ giữa các lớp
- ReportController chịu trách nhiệm nhận yêu cầu từ ReportUI, lấy dữ liệu từ các lớp Report, Employee, ReportData, và chuyển đến các lớp giao diện (ReportDisplay, ErrorMessageDisplay).
- Report có mối quan hệ kết hợp với Employee (để xác định người tạo) và ReportData (để chứa dữ liệu chi tiết).
- ReportUI, ErrorMessageDisplay, và ReportDisplay là các giao diện hiển thị cho người dùng, nhận dữ liệu và thông báo từ ReportController.

### f. Biểu đồ lớp mô tả lớp phân tích
![BieuDoLopPhanTich](https://www.planttext.com/api/plantuml/png/V94n3e9044NxFSLqLjo1A1GMDYGUO911DbbsoCmGmzaiF99NC1hNe47Q_z-VLypzUilLK6piWtCRAAZraM3BOsnG9ZW5L2M5bWMi8pZkNPswYWOMcoUb2Ck1LF5CXTSXuFIBf_WfgoYWUOxQ-K6X9hiGnQHqwJnasNkxusZ28P20Mr0jWr_QDMIMVAZ5gko7m1FHsh10mzJ_JzCbvtAApUi53m000F__0m00)


## Phần 2 : Create Employee Report

### a. Các lớp phân tích
-  Lớp Controller: EmployeeReportController
-  Lớp Entities: Employee, Project, ReportCriteria, EmployeeReport
-  Lớp Boundary: EmployeeInterface, ProjectManagementDatabase, FileSystemService

### b. Biểu đồ sequence
![BieuDoSequence](https://www.planttext.com/api/plantuml/png/d5NBRjGm5DtxAwwwvmUoG1LJe4X3XMY5OEdnc4cGOmyU9rAM5GiM28akM26aAHMgLAbgsKuMB5prF_m5_08tcKdp8fcKBAmazZbpxpddPlwaltSNXceJXO9GPfI6n-5Sg8HpCb6Hd5ATtBrv9WtNRodZX2bfj19tEo_vN6apMhyLN1CkJM1APF7yGgjtd9dYSGFJ0V86j0bQxvPbRC3FgQGp7kBXFMheX2ugbJu913zC5eQ7Xrp70LPA2ZPuyB3TY0Tlx4K4pAtE8p1kTQfWOd5Xk93MwIf5isCF7hdLbO6Rarwk9gnAwS5hUyh0-2xznK3wzeU4EB0Nyfyzj0iuA15OnksrIyyOkFGyWVTHuj9ZIGQLqI5EaD_xzdAeGXxi1oxz8FE6Fe5GA4bGWY6sIvZx-3B4ca7Ex3BPPjO17h-StwEMUi0y6DzULriXzVr-UM--s3CG3G92XO5nipM1hUqSkVIhdC5J5E4xZEqoX5Tu-v71o5UmXnw3FPOx1F3giwKpzTYDM_rCO4gb3mjC3gukFS6wg9xndBSJsw5lpR0csHPlHWZwB3jHlRQCSbjbvgwfkXkxz5jGe-HoEYp5wpqFZde7SO3Z_pF9NPAMB7bkgWFBrlBb-IgFRGl7bfdDYBCnYxCVDneLpVY7k5bCsW26chEj3_1cvcfZhqgwdAa56Zg8fL1SOAYhUlhvX-_-IXQvsM_W1mUlwhsooynwNFrMZdQHCVlJpQw_0000__y30000)

### c. Nhiệm vụ của từng lớp phân tích
- Controller :
  - EmployeeReportController: Lớp này sẽ xử lý các tương tác và quản lý quy trình tạo báo cáo cho nhân viên. Nó sẽ điều khiển luồng của ca sử dụng và tương tác với các lớp khác để lấy dữ liệu và tạo báo cáo.
- Entities :
  - Employee: Lớp này đại diện cho nhân viên đang sử dụng hệ thống, bao gồm các thuộc tính và phương thức liên quan như mã nhân viên và xác thực quyền.
  - Project: Lớp này đại diện cho dự án và được sử dụng để lấy thông tin liên quan đến dự án (ví dụ: số charge).
  - ReportCriteria: Lớp này sẽ lưu trữ và xác thực các tiêu chí báo cáo mà nhân viên cung cấp, bao gồm loại báo cáo, phạm vi ngày và số charge nếu cần.
  - EmployeeReport: Lớp này đại diện cho đối tượng báo cáo thực tế, bao gồm các phương thức để tạo, lưu hoặc hủy báo cáo dựa trên tiêu chí.
- Boundary :
  - EmployeeInterface: Lớp này quản lý việc giao tiếp với nhân viên, bao gồm nhập thông tin báo cáo và hiển thị kết quả báo cáo, yêu cầu nhân viên lưu hoặc hủy báo cáo.
  - ProjectManagementDatabase: Lớp này làm giao diện với cơ sở dữ liệu quản lý dự án để lấy danh sách các số charge có sẵn nếu loại báo cáo là "Tổng Giờ Làm Việc Cho Dự Án".
  - FileSystemService: Lớp này chịu trách nhiệm lưu báo cáo vào vị trí và tên do nhân viên chỉ định.  

### d. Một số thuộc tính và phương thức của các lớp phân tích
- EmployeeReportController
  - Thuộc tính:
      - employee: Employee - đối tượng nhân viên hiện tại.
      - criteria: ReportCriteria - tiêu chí báo cáo được cung cấp bởi nhân viên.
      - report: EmployeeReport - báo cáo được tạo dựa trên tiêu chí.
  - Phương thức:
    - createReport(): Khởi tạo quá trình tạo báo cáo, bao gồm việc yêu cầu tiêu chí và xử lý báo cáo.
    - validateEmployee(): Xác thực quyền của nhân viên trước khi cho phép tạo báo cáo.
    - requestCriteria(): Yêu cầu và lấy tiêu chí báo cáo từ giao diện.
    - generateReport(): Dựa trên tiêu chí, tạo báo cáo thông qua lớp EmployeeReport.
    - saveReport(location: String): Lưu báo cáo vào vị trí chỉ định.
    - discardReport(): Hủy bỏ báo cáo nếu không lưu.
- Employee
  - Thuộc tính:
    - employeeId: String - mã định danh của nhân viên.
    - name: String - tên của nhân viên.
    - role: String - vai trò của nhân viên, dùng để xác thực quyền.
  - Phương thức:
    - isAuthorized(): Kiểm tra xem nhân viên có quyền tạo báo cáo hay không.
    - getEmployeeDetails(): Lấy các thông tin cần thiết của nhân viên.
- Project
  - Thuộc tính:
    - projectId: String - mã định danh của dự án.
    - chargeNumber: String - mã số charge của dự án, dùng để tính giờ làm việc cho dự án.
    - projectName: String - tên của dự án.
  - Phương thức:
    - getChargeNumbers(): Lấy danh sách các mã số charge của các dự án có sẵn từ cơ sở dữ liệu.
    - findProjectById(projectId: String): Tìm dự án theo mã dự án.
- ReportCriteria
  - Thuộc tính:
    - reportType: String - loại báo cáo (ví dụ: Tổng Giờ Làm Việc, Tổng Giờ Làm Việc Cho Dự Án, Nghỉ Phép/Ốm, Tổng Lương Tính Đến Hiện Tại).
    - startDate: Date - ngày bắt đầu của báo cáo.
    - endDate: Date - ngày kết thúc của báo cáo.
    - chargeNumber: String - mã số charge (nếu báo cáo là "Tổng Giờ Làm Việc Cho Dự Án").
  - Phương thức:
    - validateCriteria(): Xác thực các tiêu chí (kiểm tra loại báo cáo, ngày tháng, số charge nếu cần).
    - setCriteria(type: String, startDate: Date, endDate: Date, chargeNumber?: String): Thiết lập tiêu chí cho báo cáo.
    - isComplete(): Kiểm tra tính đầy đủ của thông tin cần thiết để tạo báo cáo.
- EmployeeReport
  - Thuộc tính:
    - reportData: Map<String, Object> - dữ liệu báo cáo chứa các giá trị và kết quả tính toán cho báo cáo.
    - criteria: ReportCriteria - tiêu chí để tạo báo cáo.
  - Phương thức:
    - generate(criteria: ReportCriteria): Tạo báo cáo dựa trên tiêu chí đã cung cấp.
    - display(): Hiển thị báo cáo cho nhân viên.
    - save(location: String): Lưu báo cáo vào vị trí chỉ định.
    - discard(): Hủy báo cáo nếu không cần lưu.
- EmployeeInterface
  - Thuộc tính:
    - controller: EmployeeReportController - điều khiển chính để quản lý luồng của báo cáo.
  - Phương thức:
    - promptReportCriteria(): Hiển thị yêu cầu và các tùy chọn cho tiêu chí báo cáo.
    - displayReport(report: EmployeeReport): Hiển thị báo cáo đã tạo cho nhân viên.
    - promptSaveLocation(): Hiển thị yêu cầu nhập vị trí và tên file để lưu báo cáo.
    - displayError(message: String): Hiển thị thông báo lỗi nếu có vấn đề trong quá trình tạo báo cáo.
- ProjectManagementDatabase
  - Phương thức:
    - getAvailableChargeNumbers(): Truy xuất danh sách các mã số charge có sẵn từ cơ sở dữ liệu.
    - findProjectChargeNumber(projectId: String): Lấy mã số charge cho một dự án cụ thể.
- FileSystemService
  - Phương thức:
    - saveFile(location: String, data: Map<String, Object>): Lưu báo cáo vào vị trí chỉ định.
    - deleteFile(location: String): Xóa tệp nếu không cần lưu.
    - getFile(location: String): Lấy tệp từ vị trí chỉ định (nếu cần phục hồi hoặc xem lại).
      
### e. Mối quan hệ giữa các lớp
- Controller và Entities:
  - EmployeeReportController tương tác với các lớp Employee, ReportCriteria, EmployeeReport để lấy dữ liệu nhân viên, tiêu chí báo cáo và tạo báo cáo thực tế.
- Controller và Boundary:
  - EmployeeReportController sử dụng EmployeeInterface để hiển thị thông tin và nhận đầu vào từ nhân viên.
  - ProjectManagementDatabase được sử dụng để truy xuất thông tin về dự án và các mã số charge.
  - FileSystemService được sử dụng để lưu hoặc xóa báo cáo.
- Entities và Boundary:
  - Lớp ProjectManagementDatabase cung cấp thông tin dự án để lớp Project xử lý.
  - FileSystemService lưu hoặc phục hồi báo cáo được tạo trong EmployeeReport.
 
### f. Biểu đồ lớp mô tả lớp phân tích
![BieuDoLopPhanTich](https://www.planttext.com/api/plantuml/png/N93B3S9034JlMyKsa1xoZpWW8LA1anYqQ3_8wo2bDWwKH0jaCH29qqWppsFBp_iZZmp4ixDg2BEVW1RTkAiD2-BECz89HjGGTR7b1meN77aF7ixeq7CD30F4DrTkN6iizajaT3tIpKXFfSRWcOBzhJdYDH1NubgaHDLghJMytPBCvcj-9iYiznb8KVlF2vAYJgb2PzbQMOfK8dMIHgGLwLIEVag_U0400F__0m00)

## Phần 3 : Login

### a. Các lớp phân tích
-  Lớp Controller: LoginController
-  Lớp Entities: User và AuthenticationService
-  Lớp Boundary: LoginScreen
 
### b. Biểu đồ sequence
![BieuDoSequence](https://www.planttext.com/api/plantuml/png/X90zQWGn38Lxdq9Lkhr0Yh0XFn18DoIzHXQx1eszIFA6ETiMUwHS8J930e50N1XBdwNtU9-NwzuSrViY2ScRmfkn0XhqDBTUC-eAh-rGwaJAN0UHHAswDjd0mrR8DaQ9gnTVuRxxSJm9lRGwiPuByVY1ANNOtO70BJnLZx6A2yCDdD3iesbECZ05dlgy50SPCf3PiOWb6XI3lgEKZCuGplAGmg0ele5VNOY3iFjPIyIsTUdRocEna-0A6UquDmmRBCRmKi__R7iELrtvxssi6fakeOO7ZcXosiSrqlu2003__mC0)

### c. Nhiệm vụ của từng lớp phân tích
- Controller :
  - LoginController: Điều phối luồng xử lý giữa giao diện (LoginScreen) và lớp logic xử lý.
- Entities :
  - User: Đại diện cho dữ liệu người dùng.
  - AuthenticationService: Xử lý logic xác thực người dùng.
- Boundary :
  - LoginScreen: Là giao diện để người dùng tương tác với hệ thống.

### d. Một số thuộc tính và phương thức của các lớp phân tích
-  Lớp Controller: LoginController
  - Thuộc tính:
    - username: String - Tên đăng nhập do người dùng nhập.
    - password: String - Mật khẩu do người dùng nhập.
  - Phương thức:
    - login(username: String, password: String): Boolean
      → Thực hiện kiểm tra đăng nhập bằng cách gọi lớp AuthenticationService.
    - displayMessage(message: String): void
      → Hiển thị thông báo đăng nhập thành công hoặc lỗi.
    - redirectToDashboard(): void
      → Điều hướng người dùng đến màn hình dashboard sau khi đăng nhập thành công.
- Lớp Entities
  - Lớp User:
    - Thuộc tính:
      - username: String - Tên đăng nhập của người dùng.
      - password: String - Mật khẩu của người dùng.
    - Phương thức:
      - getUsername(): String
      → Lấy tên đăng nhập của người dùng.
    - getPassword(): String
      → Lấy mật khẩu của người dùng.
- Lớp AuthenticationService:
  - Thuộc tính:
    - users: List<User> - Danh sách các tài khoản người dùng đã đăng ký.
  - Phương thức:
    - validateCredentials(username: String, password: String): Boolean
      → Kiểm tra thông tin đăng nhập từ cơ sở dữ liệu và trả về kết quả (hợp lệ hoặc không hợp lệ).
    - findUserByUsername(username: String): User?
      → Tìm kiếm thông tin người dùng dựa trên tên đăng nhập.
- Lớp Boundary: LoginScreen
  - Thuộc tính:
    - inputUsername: String - Dữ liệu nhập vào từ ô tên đăng nhập.
    - inputPassword: String - Dữ liệu nhập vào từ ô mật khẩu.
    - errorMessage: String - Thông báo lỗi hiển thị trên màn hình.
  - Phương thức:
    - captureInput(): void
      → Lấy thông tin từ các ô nhập liệu (username và password).
    - showErrorMessage(message: String): void
      → Hiển thị thông báo lỗi khi đăng nhập thất bại.
    - navigateToDashboard(): void
      → Chuyển người dùng sang giao diện chính nếu đăng nhập thành công.

### e. Mối quan hệ giữa các lớp
- LoginController là lớp điều phối trung tâm, giao tiếp với cả LoginScreen để nhận dữ liệu và AuthenticationService để xử lý xác thực.
- AuthenticationService chịu trách nhiệm xác thực thông tin người dùng thông qua việc kiểm tra với lớp User.
- LoginScreen chỉ hiển thị giao diện người dùng và thu thập dữ liệu, sau đó truyền cho LoginController để xử lý.
- SystemState được sử dụng để quản lý trạng thái hệ thống sau khi đăng nhập thành công.

### f. Biểu đồ lớp mô tả lớp phân tích
![BieuDoLopPhanTich](https://www.planttext.com/api/plantuml/png/HCyx3i8m303GtQUmklS2JFqEI6mLx2QrQ4IQeCG5zMmC78ahKBSWDiVFlxoVho89HPb61-Sm-PxYZ8TmiRupaTaZ9Ip112ynk0tgxU4uAbR0NgpCU4nReluboaa63Gs93RxZUBU6jQBvR-hc93nsGh9A2r1YdcE5EypsNZYI4NnO6JAe51g54pdRQyToOQyRoAMlj-h7swffdOr9XsVGADVAzS3cYfEUkzHH1WNxNlyF7m000F__0m00)

## Phần 4 : Maintain Employee Information

### a. Các lớp phân tích
-  Lớp Controller: MaintainEmployeeController
-  Lớp Entities: Employee
-  Lớp Boundary: EmployeeInterface

### b. Biểu đồ sequence
![BieuDoSequence](https://www.planttext.com/api/plantuml/png/b5EzJiCm4Dxz5ATCC5JT6L2h94WCbQfMVG0JNy1IR1Vx2lApCV18l09s6YUcq8eENkw-l_iaVtryBXnnImVLCTwGiR3ctfgkMmebjNHaUHWor2J9mufBJU7LQjyPZrWQJH6C5hY3Ci7IEWxhD1nqjzuHghXPfqrGQQLLdAJHbUITUOxhYh6_ei3i7aguWsAB7JO48NIWmSrIYFbkBpZXl0eRmjk2bH7yqpSGD_XwG4U0AMKWyUAiMHqvjQPmuyYGkZL3uEGIKI73X243hlSS45KV-iMyGvFT2w8_k60LpD9bEnUy1f3BzQTUXK1nFl9H9IzZZ9NBRP2in3UygecL4RBrfvH9z6YRLpNMS37kXPmFKcUzFdbuh7vrAY8zzfcN-xzMJvoXjKQDcHUeHVmRtm000F__0m00)

### c. Nhiệm vụ của từng lớp phân tích
- Controller :
  - MaintainEmployeeController: Chịu trách nhiệm điều khiển và xử lý các thao tác với thông tin nhân viên trong hệ thống.
- Entities :
  - Employee: Lớp này đại diện cho một nhân viên trong hệ thống, chứa tất cả các thông tin chi tiết của nhân viên.
- Boundary :
  - EmployeeInterface: Đây là lớp giao diện giữa người dùng (Payroll Administrator) và hệ thống. Giao diện này nhận thông tin từ người dùng và hiển thị thông báo hoặc kết quả sau khi thực hiện thao tác.
 
### d. Một số thuộc tính và phương thức của các lớp phân tích
- Lớp Controller: MaintainEmployeeController
  - Thuộc tính:
    - employeeData: List<Employee>: Danh sách nhân viên trong hệ thống.
  - Phương thức:
    - addEmployee(employee: Employee): void: Thêm nhân viên mới.
    - updateEmployee(employeeId: String, updatedInfo: Employee): void: Cập nhật thông tin nhân viên.
    - deleteEmployee(employeeId: String): void: Xóa thông tin nhân viên.
    - requestEmployeeInfo(): void: Yêu cầu thông tin nhân viên (cập nhật hoặc thêm).
    - displayConfirmationMessage(message: String): void: Hiển thị thông báo xác nhận.
- Entities: Employee
  - Thuộc tính:
    - employeeId: String: Mã nhân viên duy nhất.
    - name: String: Tên nhân viên.
    - employeeType: String: Loại nhân viên (hour, salaried, commissioned).
    - mailingAddress: String: Địa chỉ của nhân viên.
    - socialSecurityNumber: String: Số an sinh xã hội của nhân viên.
    - phoneNumber: String: Số điện thoại của nhân viên.
    - hourlyRate: Double: Mức lương theo giờ (nếu có).
    - salary: Double: Mức lương cơ bản (nếu có).
    - commissionRate: Double: Tỷ lệ hoa hồng (nếu có).
    - otherDeductions: Double: Các khoản khấu trừ khác (401k, bảo hiểm).
  - Phương thức:
    - getEmployeeId(): String: Trả về mã nhân viên.
    - getName(): String: Trả về tên nhân viên.
    - getEmployeeType(): String: Trả về loại nhân viên.
    - getMailingAddress(): String: Trả về địa chỉ của nhân viên.
Lớp Boundary: EmployeeInterface
  - Thuộc tính:
    - errorMessage: String: Thông báo lỗi khi thao tác thất bại.
  - Phương thức:
    - displayEmployeeInfo(employee: Employee): void: Hiển thị thông tin nhân viên.
    - requestEmployeeInfo(): void: Yêu cầu thông tin về nhân viên từ người dùng (cho thao tác thêm hoặc sửa).
    - showErrorMessage(message: String): void: Hiển thị thông báo lỗi.
    - showConfirmationMessage(message: String): void: Hiển thị thông báo xác nhận.

### e. Mối quan hệ giữa các lớp
- MaintainEmployeeController --> EmployeeInterface: Controller sử dụng Boundary để nhận thông tin và hiển thị thông báo.
- MaintainEmployeeController --> Employee: Controller sử dụng Entities để thao tác với dữ liệu nhân viên.

### f. Biểu đồ lớp mô tả lớp phân tích
![BieuDoLopPhanTich](https://www.planttext.com/api/plantuml/png/N8yz3i8m34PtdyBgpWKOK6aA4aC54YSmZO58-K6EAzIpCN0ahW0fGmM3f_S-V_RhyQopakWGF9pI42t9Y2Q5u79sARBTX9jF8_CkAikPUaRAk9xTmo3zbJBlnR9iauJ26-XJL4aUEt9HF_EZcI_qB4Ksm56T_gqgf0LOusAnGeDBhAOBg5UyExrMqCpaE9o2KqnJplAdp-SAp2IqHUWeqeN_2YmfLL1pjELvU0C00F__0m00)


## Phần 5 : Maintain Purchase Order

### a. Các lớp phân tích
-  Controller: PurchaseOrderController, OrderManagementController
-  Entities: PurchaseOrder, Customer, Product
-  Boundary: PurchaseOrderUI, SystemNotification, PurchaseOrderSearchUI

### b. Biểu đồ sequence
![BieuDoSequence](https://www.planttext.com/api/plantuml/png/t5KnRkCm4EprYeMRQ-8Ff0W2s2dSN8m4VW13hX82egYGomH-snLvqdtXrajBaHoRPwTC8q7KxEpkpCZ---VZDf8Ab5nJAKq-m6pXdRCnMj-YWJlNDNwBE0CLXuUgumghRQTQWjaw1VsY8ju7Ws6p4kJwVhCge1Q-fU2R1iCU_NbGgDfZfuZ7RIHqlptPscf5FBN0HiTLzGlcypai0Yf2w2b1E7TlgdulcD_8v70DZzYWPlfSDAlac5yFq6jumDU4aS0BZq5Ijed7kDR1lrc3e5CaxnXhszfVGHUyIPhY5QZMWE4sGvUn838C0wPj9WYfODn-mnRVOI8Seu-mFY2bq4wHi5f-eHv9oLLotq9CMcECTMf0xxgoxl1kwMKt27ECQwQgBMti6ZKGWEEBUiRUf4rdBZSf5nLDah60F2J1bcpA6vomOiHNj8B53HRVy43UfstcFjUEqprav5xCd8sQlruqbcpxNDelAs0aXS69TSNWzVWp0dZWNY5y_53Ru7exBitSlkpRCLjoSYwEMIuwBsP6i3yiPf_JIDPqzZ0dwCYclSUYHI5bh8X63fZyVep0H_OzyEsCW9ta-r_4Xi9lXEoMlvlTFsfL_GC00F__0m00)

### c. Nhiệm vụ của từng lớp phân tích
- Controller :
  - PurchaseOrderController: Chịu trách nhiệm quản lý các thao tác thêm, sửa, và xóa các đơn hàng. Lớp này sẽ nhận các yêu cầu từ Commissioned Employee (người dùng), sau đó gọi các phương thức trong lớp Entity để thực hiện các thay đổi liên quan đến đơn hàng.
  - OrderManagementController: Điều phối việc quản lý các đơn hàng, bao gồm việc xác định các yêu cầu người dùng (tạo mới, cập nhật hoặc xóa), cũng như xử lý các tình huống đặc biệt như không tìm thấy đơn hàng hoặc quyền truy cập không hợp lệ.
- Entities :
  - PurchaseOrder: Đại diện cho một đơn hàng, chứa các thông tin như mã đơn hàng, khách hàng, sản phẩm đã mua, địa chỉ thanh toán, và trạng thái đơn hàng (mở/đóng). Lớp này sẽ có các phương thức để thay đổi hoặc truy xuất thông tin của đơn hàng.
  - Customer: Đại diện cho khách hàng của một đơn hàng, có thể bao gồm thông tin như tên, địa chỉ thanh toán, và điểm liên lạc của khách hàng.
  - Product: Đại diện cho các sản phẩm trong đơn hàng, chứa thông tin về sản phẩm, số lượng và giá trị.
- Boundary :
  - PurchaseOrderUI: Giao diện người dùng để thêm, sửa và xóa đơn hàng. Đây là lớp mà Commissioned Employee tương tác trực tiếp, bao gồm các màn hình hoặc biểu mẫu để nhập thông tin đơn hàng, chọn hành động (thêm, sửa, xóa) và hiển thị kết quả.
  - SystemNotification: Lớp chịu trách nhiệm gửi thông báo lỗi hoặc thành công cho người dùng, ví dụ, khi không tìm thấy đơn hàng, khi có lỗi truy cập, hoặc khi thao tác thành công (ví dụ: "Đơn hàng đã được thêm thành công").
  - PurchaseOrderSearchUI: Cung cấp giao diện cho người dùng để tìm kiếm và truy cập đơn hàng theo ID, có thể là một biểu mẫu nhập ID đơn hàng hoặc bảng kết quả tìm kiếm.
### d. Một số thuộc tính và phương thức của các lớp phân tích
- Lớp Controller:
  - PurchaseOrderController
    - Thuộc tính:
      - purchaseOrderService (PurchaseOrderService) – Cung cấp các phương thức xử lý logic liên quan đến đơn hàng.
      - purchaseOrderRepository (PurchaseOrderRepository) – Lưu trữ và truy vấn dữ liệu đơn hàng từ cơ sở dữ liệu.
  - Phương thức:
    - createPurchaseOrder(customerDetails, productDetails, billingAddress) – Xử lý việc tạo đơn hàng mới.
    - updatePurchaseOrder(orderID, updatedDetails) – Cập nhật thông tin đơn hàng.
    - deletePurchaseOrder(orderID) – Xóa đơn hàng khỏi hệ thống.
    - getPurchaseOrder(orderID) – Truy xuất thông tin đơn hàng từ cơ sở dữ liệu.
- OrderManagementController
  - Thuộc tính:
    - purchaseOrderController (PurchaseOrderController) – Điều phối các tác vụ cụ thể về đơn hàng.
    - orderSearchService (OrderSearchService) – Cung cấp chức năng tìm kiếm đơn hàng.
  - Phương thức:
    - searchPurchaseOrders(searchCriteria) – Tìm kiếm các đơn hàng dựa trên tiêu chí (ví dụ: ID, khách hàng, trạng thái).
    - closePurchaseOrder(orderID) – Đóng đơn hàng khi đã hoàn thành.
    - cancelPurchaseOrder(orderID) – Hủy bỏ đơn hàng nếu có lỗi hoặc yêu cầu từ người dùng.
- Entities:
  - PurchaseOrder
    - Thuộc tính:
      - orderID (String) – Mã định danh duy nhất của đơn hàng.
      - customer (Customer) – Thông tin khách hàng liên quan đến đơn hàng.
      - products (List<Product>) – Danh sách các sản phẩm được mua trong đơn hàng.
      - billingAddress (String) – Địa chỉ thanh toán của khách hàng.
      - orderDate (Date) – Ngày tạo đơn hàng.
      - status (OrderStatus) – Trạng thái của đơn hàng (OPEN, CLOSED, CANCELLED).
      - commissionedEmployee (Employee) – Nhân viên chịu trách nhiệm cho đơn hàng.
    - Phương thức:
      - validateOrderDetails() – Kiểm tra tính hợp lệ của các chi tiết đơn hàng.
      - updateOrderDetails(newDetails) – Cập nhật thông tin đơn hàng.
      - deleteOrder() – Xóa đơn hàng khỏi hệ thống.
      - generateOrderID() – Tạo mã đơn hàng duy nhất.
  - Customer
    - Thuộc tính:
      -customerID (String) – Mã định danh khách hàng.
      - name (String) – Tên khách hàng.
      - contact (String) – Số điện thoại hoặc địa chỉ email của khách hàng.
      - billingAddress (String) – Địa chỉ thanh toán của khách hàng.
    - Phương thức:
      - updateContactDetails(newContact) – Cập nhật thông tin liên hệ của khách hàng.
      - updateBillingAddress(newAddress) – Cập nhật địa chỉ thanh toán của khách hàng.
   - Product
    - Thuộc tính:
      - productID (String) – Mã sản phẩm duy nhất.
      - productName (String) – Tên sản phẩm.
      - price (Decimal) – Giá của một đơn vị sản phẩm.
      - quantity (Integer) – Số lượng sản phẩm được mua.
    - Phương thức:
      - calculateTotalPrice() – Tính tổng giá trị của sản phẩm (số lượng * giá mỗi sản phẩm).
      - updatePrice(newPrice) – Cập nhật giá của sản phẩm.
Lớp Boundary: 
  - PurchaseOrderUI
    - Phương thức:
      - displayCreateOrderForm() – Hiển thị giao diện để nhân viên nhập thông tin tạo đơn hàng.
      - displayOrderDetails(orderID) – Hiển thị chi tiết đơn hàng cho nhân viên.
      - promptForUpdate(orderID) – Hiển thị giao diện cho phép nhân viên cập nhật đơn hàng.
      - confirmDeleteOrder() – Yêu cầu nhân viên xác nhận việc xóa đơn hàng.
  - SystemNotification
    - Phương thức:
      - displaySuccessMessage(message) – Hiển thị thông báo thành công.
      - displayErrorMessage(message) – Hiển thị thông báo lỗi.
      - displayWarningMessage(message) – Hiển thị cảnh báo.
  - PurchaseOrderSearchUI
    - Phương thức:
      - displaySearchForm() – Hiển thị giao diện để nhân viên nhập tiêu chí tìm kiếm.
      - displaySearchResults(results) – Hiển thị kết quả tìm kiếm đơn hàng.
### e. Mối quan hệ giữa các lớp
- Controller Classes:
  - PurchaseOrderController phụ thuộc vào PurchaseOrder, PurchaseOrderService, và PurchaseOrderRepository để thực hiện các thao tác quản lý đơn hàng.
  - OrderManagementController hợp tác với PurchaseOrderController và sử dụng OrderSearchService để thực hiện các thao tác tìm kiếm và quản lý đơn hàng nâng cao.
- Entities:
  - PurchaseOrder có mối quan hệ 1-n với Customer (một đơn hàng thuộc về một khách hàng) và Aggregation với Product (một đơn hàng có thể chứa nhiều sản phẩm).
  - PurchaseOrder có mối quan hệ 1-1 với CommissionedEmployee (một nhân viên chịu trách nhiệm cho một đơn hàng).
- Boundary Classes:
  - PurchaseOrderUI, SystemNotification, và PurchaseOrderSearchUI là các lớp giao diện người dùng và thông báo, chúng hợp tác với các lớp Controller (như   -        - PurchaseOrderController và OrderManagementController) để thực hiện các thao tác liên quan đến đơn hàng và hiển thị thông tin cho người dùng.

### f. Biểu đồ lớp mô tả lớp phân tích
![BieuDoLopPhanTich](https://www.planttext.com/api/plantuml/png/L50xhi903Enz2YiD5HUWWYmyYGA1a3Y0IVnULjeFiXqXpaR1aRW2MOBWKRYOyNWyzlrwcwkHM1y3m0JhtAUMv88ka2eh7Dz4Zj6h-fouNSLJo1VcTJAMNseOIN7nqUvwQJfItahByfCbbdvT_5rE9Za4bd43D2E16_B9XleQ_QSU35mnM2Npzee7F8AlcQ9S5kMU0zaGLpj_KbZWT8eEPrWzGrDZYcTlNGNrktCO3gx05RmiU4E9_We5SqxjyqC03m000F__0m00)

## 6.Run Payroll
### a. Các lớp phân tích
- Lớp Boundary:  PayrollInterface, BankSystemInterface
- Lớp Controller: RunPayrollController
- Lớp entities: Employee, Payroll
### b. Biểu đồ Sequence
![RunPayroll](https://www.planttext.com/api/plantuml/png/X9F1Jjmm48RlVefvWQht7YeskwlI6oezqAF9fciBxnWvOuJFFN3Wn1kGLbLLf1Kz9weukE8z_0HzXOx3Xi22IYwHnj_y_--Pv6ztirEJTEHNHWXPadMm9uEpnamMAusw9YUvACIXzRYGBWp7xv4gzrcM5SWQ9kDn8V5eFzHKhHuHXIWj4ZV21uyRYUbTnLGk4rDH8MaAC5yT6nkglcqs53SjkJONuhc8yEejJE0D5Acz9lXpaTeV7agLsYR0OMg_uHBCxQ_R1fTYajafiv_Y5JCzUPgwDPZuUvkTPdR6x4Vd0vpwr7udMAJk6enEtPa7LF4hmecELtW7ppFCjdPRQdul5TUeW6niS3ZafFQfLBxFBjjyGI2LkdCWny9CaugDtjONqX3igOrWRlXPyakENl6IVNpe1O-KpUq2-EdD2ZPxnrFGiDJIvZkUbmfmcJEfUCa66Is6sHt4fkJ4gLtZmmPHcRfwCSMnqgczyKFqrniTac7CCxkVunRDtyH2Z8lPjHmEg5_CSylB-pZuttQVJFan16eq46A7pVFFyWy00F__0m00)
### c. Nhiệm vụ của từng lớp phân tích:
- PayrollInterface: Cung cấp giao diện để hệ thống hiển thị trạng thái và kết quả khi chạy bảng lương. Đây là lớp mà người dùng (chẳng hạn như Payroll Administrator) tương tác để xem báo cáo, xác nhận thanh toán, và thực hiện các thao tác liên quan đến bảng lương.
- BankSystemInterface: Cung cấp giao diện để kết nối và truyền dữ liệu đến hệ thống ngân hàng để xử lý thanh toán qua chuyển khoản trực tiếp.
-  RunPayrollController: lớp điều khiển chính trong ca sử dụng Run Payroll, chịu trách nhiệm xử lý các bước như tính toán lương, in phiếu lương, gửi giao dịch ngân hàng, v.v.
- Employee: Đại diện cho một nhân viên trong hệ thống, bao gồm các thông tin cá nhân và thông tin thanh toán.
- Payroll: Lớp đại diện cho bảng lương, bao gồm thông tin liên quan đến việc tính toán lương của tất cả nhân viên trong mỗi chu kỳ bảng lương.
### d. Một số thuộc tính và phương thức của các lớp phân tích:
- PayrollInterface:
  + payrollStatus: Trạng thái của việc chạy bảng lương (hoàn thành, lỗi, đang chờ).
  + employeeList: Danh sách nhân viên đã nhận thanh toán.
  + displayPayrollStatus(): Hiển thị trạng thái bảng lương.
  + displayEmployeePaymentDetails(): Hiển thị chi tiết thanh toán của từng nhân viên.
-BankSystemInterface:
  + transactionStatus: Trạng thái giao dịch với hệ thống ngân hàng.
  + sendBankTransaction(): Gửi giao dịch ngân hàng.
  + retryBankTransaction(): Thử lại giao dịch nếu hệ thống ngân hàng không sẵn sàng.
- RunPayrollController:
  + payrollDate: Ngày bảng lương được chạy.
  + employeeList: Danh sách nhân viên cần được thanh toán.
  + calculatePay(): Tính toán lương cho từng nhân viên dựa trên thông tin từ thẻ chấm công, đơn hàng và thông tin nhân viên.
  + processPayment(): Xử lý thanh toán cho nhân viên, bao gồm in phiếu lương hoặc gửi giao dịch ngân hàng.
  + checkBankSystemStatus(): Kiểm tra trạng thái hệ thống ngân hàng và xử lý nếu hệ thống không khả dụng.
  + deleteEmployee(): Xóa nhân viên đã bị đánh dấu xóa sau khi bảng lương đã được xử lý.
- Employee:
  + employeeId: Mã số nhân viên.
  + name: Tên nhân viên.
  + salary: Lương cơ bản của nhân viên (nếu là nhân viên lương cố định).
  + hourlyRate: Mức lương theo giờ (nếu là nhân viên lương theo giờ).
  + benefits: Các phúc lợi (Bảo hiểm, nghỉ phép, v.v.).
  + paymentMethod: Phương thức thanh toán (chuyển khoản, lấy phiếu lương, v.v.).
  + status: Trạng thái của nhân viên (đang làm việc, đã nghỉ việc, v.v.).\
  + calculatePay(): Tính toán lương cho nhân viên.
  + generatePaycheck(): Tạo phiếu lương cho nhân viên.
  + sendPayment(): Gửi thanh toán cho nhân viên qua chuyển khoản ngân hàng.
- Payroll:
  + payrollDate: Ngày chạy bảng lương.
  + employeePayments: Danh sách các khoản thanh toán cho nhân viên.
  + runPayroll(): Chạy bảng lương cho tất cả nhân viên.
  + generateReports(): Tạo báo cáo về bảng lương.
  + processPayments(): Xử lý thanh toán cho nhân viên.
### e. Mối quan hệ giữa các lớp
- PayrollInterface (Giao diện với người dùng) giao tiếp với RunPayrollController để yêu cầu xử lý bảng lương.
- RunPayrollController truy xuất và tính toán dữ liệu từ Employee và tạo đối tượng Payroll.
- RunPayrollController gửi giao dịch đến BankSystemInterface nếu phương thức thanh toán là chuyển khoản.
- RunPayrollController tạo phiếu lương nếu phương thức thanh toán là phiếu lương/nhận tay.
- PayrollInterface hiển thị kết quả cho người dùng sau khi bảng lương hoàn tất.
### f. Biểu đồ lớp mô tả lớp phân tích
![RunPayroll](https://www.planttext.com/api/plantuml/png/L8x13S8m34Nldi8BT8SsQG_S44nWMYCX4WSbpY6pzS18h413Wn2d9xt_l-NN-koJKjJi7S0bP5ae5ZnIYS6vWoZ7AysCb73unORaVYv9sVyr3Cn1T1lYAKixONVZEDQ61HQzQS79Frme_9cDNzacrKq00tOTMWJJQ2l77LlSioprwJS0003__mC0)
