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


## Phần 2 : Create Administrative Report

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
![BieuDoLopPhanTich]([https://www.planttext.com/api/plantuml/png/V94n3e9044NxFSLqLjo1A1GMDYGUO911DbbsoCmGmzaiF99NC1hNe47Q_z-VLypzUilLK6piWtCRAAZraM3BOsnG9ZW5L2M5bWMi8pZkNPswYWOMcoUb2Ck1LF5CXTSXuFIBf_WfgoYWUOxQ-K6X9hiGnQHqwJnasNkxusZ28P20Mr0jWr_QDMIMVAZ5gko7m1FHsh10mzJ_JzCbvtAApUi53m000F__0m00](https://www.planttext.com/api/plantuml/png/N93B3S9034JlMyKsa1xoZpWW8LA1anYqQ3_8wo2bDWwKH0jaCH29qqWppsFBp_iZZmp4ixDg2BEVW1RTkAiD2-BECz89HjGGTR7b1meN77aF7ixeq7CD30F4DrTkN6iizajaT3tIpKXFfSRWcOBzhJdYDH1NubgaHDLghJMytPBCvcj-9iYiznb8KVlF2vAYJgb2PzbQMOfK8dMIHgGLwLIEVag_U0400F__0m00))
