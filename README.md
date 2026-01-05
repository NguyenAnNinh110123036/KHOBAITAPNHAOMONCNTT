# Thiết kế và Cài đặt CSDL NoSQL cho Hệ thống Quản lý Dự án và Cộng tác Nhóm

Dự án này thực hiện việc thiết kế, cài đặt và khai thác cơ sở dữ liệu NoSQL (MongoDB) để quản lý quy trình làm việc của các nhóm dự án. Toàn bộ quá trình từ kết nối, nạp dữ liệu từ Excel đến truy vấn thống kê được thực hiện trên **Google Colab** bằng ngôn ngữ **Python**.

## 📌 Tổng quan đề tài
Hệ thống cho phép quản lý đa dự án (Ký túc xá, Nhà trọ, Nhà xe...), theo dõi các nhiệm vụ (Tasks), thành viên trong nhóm, và lưu trữ lịch sử tương tác (Comments, Activity History).

## 🛠 Công nghệ & Thư viện sử dụng
* **Database:** MongoDB Atlas (Cloud NoSQL).
* **Ngôn ngữ:** Python 3.
* **Thư viện chính:**
    * `pymongo`: Kết nối và thao tác với MongoDB.
    * `pandas` & `openpyxl`: Xử lý và chuyển đổi dữ liệu từ file Excel (.xlsx).
    * `urllib.parse`: Mã hóa thông tin xác thực cho chuỗi kết nối URI.
    * `datetime`: Quản lý mốc thời gian hoạt động.

## 🗄 Cấu trúc Cơ sở dữ liệu (Collections)
Dữ liệu được tổ chức thành các tập hợp linh hoạt (Documents) bao gồm:
1.  **Thanh_vien:** Lưu trữ ID, Họ tên, Email và vai trò của người dùng.
2.  **groups:** Quản lý thông tin nhóm và danh sách thành viên chi tiết trong nhóm.
3.  **projects:** Thông tin về các dự án (Tên, mô tả, ngày bắt đầu/kết thúc).
4.  **Tasks:** Danh sách công việc, trạng thái (`done`, `doing`), ngày thực hiện và người phụ trách.
5.  **Files:** Lưu trữ đường dẫn tài liệu liên kết với từng nhiệm vụ.
6.  **Comments:** Lưu các trao đổi của thành viên trong từng đầu việc.
7.  **ActivityHistory:** Nhật ký hoạt động chi tiết của hệ thống.


## 🚀 Các chức năng chính trong Code

### 1. Kết nối & Bảo mật
Sử dụng `quote_plus` để mã hóa thông tin tài khoản, đảm bảo kết nối an toàn đến Cluster MongoDB Atlas.

### 2. Import dữ liệu tự động
* Đọc dữ liệu từ các file Excel chuyên biệt (`Thanh_vien.xlsx`, `Group.xlsx`, `taks.xlsx`).
* Tự động làm sạch dữ liệu (Xử lý giá trị Null/NaN bằng `pandas`).
* Đồng bộ hóa dữ liệu vào MongoDB với chức năng xóa tài liệu cũ để tránh trùng lặp.

### 3. Truy vấn & Thống kê nâng cao (Aggregation)
* **Truy vấn chi tiết thành viên:** Xem một thành viên thuộc nhóm nào, đang làm dự án gì và các nhiệm vụ cụ thể được giao.
* **Truy vấn dự án:** Liệt kê toàn bộ thành viên và trạng thái công việc của một dự án cụ thể.
* **Thống kê hiệu suất:**
    * Tìm dự án/nhóm có số lượng nhiệm vụ nhiều nhất/ít nhất.
    * Xác định thành viên năng nổ nhất (được giao nhiều việc nhất) trong từng nhóm.
    * Phân tích mức độ tương tác thông qua số lượng bình luận trên mỗi nhiệm vụ.

## 📈 Kết quả thực hiện (Ví dụ)
* **Dự án nhiều nhiệm vụ nhất:** Hệ thống quản lý ký túc xá (19 nhiệm vụ).
* **Nhóm hoạt động mạnh nhất:** Nhóm 1 (19 nhiệm vụ).
* **Thời gian thực thi:** Các truy vấn phức tạp (Lookup & Unwind) đạt tốc độ ~0.7s.

---
**Thực hiện bởi:** Nguyễn An Ninh  
**Lớp:** DA23TTA  
**Môi trường:** Google Colab & MongoDB Atlas
