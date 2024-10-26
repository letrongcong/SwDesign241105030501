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
