# HỆ THỐNG TRỰC QUAN HÓA HIỆU SUẤT TÀI CHÍNH CÁC DOANH NGHIỆP TRONG NHÓM VN30 (2020 - 2024)

## 1. Tổng Quan Dự Án (Project Overview)
Dự án được xây dựng nhằm mục đích **Số hóa, Lưu trữ và Trực quan hóa tự động** dữ liệu báo cáo tài chính (BCTC) của các 20 doanh nghiệp thuộc nhóm chỉ số VN30 trong giai đoạn 5 năm (2020 - 2024). Hệ thống giải quyết bài toán xử lý dữ liệu tài chính thô từ các nguồn phân tán, đưa vào mô hình cơ sở dữ liệu tập trung (MySQL) và chuyển hóa thành các chỉ số phân tích động (DAX Power BI) nhằm hỗ trợ đưa ra quyết định đầu tư nhanh chóng.

* **Đối tượng nghiên cứu:** 3 nhóm ngành chính trong VN30 bao gồm: **Ngân hàng (Bank), Khối doanh nghiệp sản xuất/thương mại (Corporate), và Chứng khoán (Securities)**.
* **Mục tiêu cốt lõi:** Theo dõi xu hướng thị trường (Market Trend), So sánh cặp doanh nghiệp (Peer Comparison) và Đánh giá chi tiết sức khỏe tài chính của từng cổ phiếu (Company Profile).

---

## 2. Công Nghệ Sử Dụng (Tech Stack)
* **Database Management System:** MySQL Server (Local Instance).
* **Data Visualization & Analytics:** Power BI Desktop (Power Query, DAX, Data Modeling).
* **UI/UX Theme:** Thiết kế tối ưu hóa trải nghiệm người dùng dựa trên bản mẫu được lấy từ Metricalist.

---

## 3. Kiến Trúc Dữ Liệu & Mô Hình Hóa (Data Modeling)
Dự án áp dụng chặt chẽ mô hình **Star Schema** để tối ưu hóa hiệu năng tính toán và tốc độ tải biểu đồ trên Power BI.

### Các bảng Danh mục (Dimension Tables):
* `dim_companies`: Lưu trữ thông tin định danh doanh nghiệp (Ticker, Company Name, Sector, Exchange, Logo URL).
* `dim_calendar`: Quản lý chiều thời gian chuẩn hóa theo Quý và Năm (TimeKey, Year, Quarter, YearQuarter).
* `dim_items`: Chuẩn hóa danh mục tài khoản kế toán giữa 3 khối Ngành (Cân đối kế toán - Balance Sheet, Kết quả kinh doanh - Income Statement, Lưu chuyển tiền tệ - Cash Flow).

### Bảng Dữ kiện & Chỉ số (Fact Tables):
* `fact_financials`: Lưu trữ toàn bộ các con số tài chính thô được trích xuất (Giá trị hiện tại, giá trị quý liền kề).
* `financial_ratios`: Lưu trữ các chỉ số tài chính nâng cao được tính toán tự động thông qua **Stored Procedure** trực tiếp từ tầng Database để giảm tải cho tầng hiển thị.

---

## 4. Các Chỉ Số Phân Tích Cốt Lõi (Key Analytics Metrics)
Hệ thống sử dụng các công thức DAX nâng cao kết hợp xử lý MySQL để tính toán động theo thời gian:
* **Nhóm chỉ số hiệu quả (Profitability):** Biên lợi nhuận gộp (Gross Margin), Biên lợi nhuận thuần (Net Margin), Tỷ suất sinh lời trên tài sản (ROA), Tỷ suất sinh lời trên vốn chủ sở hữu (ROE).
* **Nhóm chỉ số tăng trưởng (Growth QoQ):** Tốc độ tăng trưởng Doanh thu, Tăng trưởng Lợi nhuận sau thuế (NPAT Growth QoQ), Tăng trưởng tổng tài sản (Asset Growth QoQ).
* **Cấu trúc vốn (Capital Structure):** Tỷ lệ Nợ/Vốn chủ sở hữu (Debt vs Equity Ratio) biến động theo từng quý.

---

## 5. Cấu Trúc Báo Cáo Trên Power BI Dashboard (Demo)

Báo cáo được phân tách mạch lạc thành **3 phân hệ chức năng chính** (tương ứng với các Tab điều hướng):

### Tab 1: Market Overview (Tổng quan thị trường)
* Khái quát quy mô toàn thị trường: Tổng doanh thu (Total Revenue), Tổng lợi nhuận ròng (Net Profit) của rổ VN30.
* Biểu đồ **Financial Performance Trend** kết hợp giữa cột Doanh thu và đường xu hướng Market ROE theo thời gian.
* Biểu đồ tròn **Net Profit Contribution by Sector** phân tích tỷ trọng đóng góp lợi nhuận của 3 khối Bank, Corporate và Securities.

### Tab 2: Peer Comparison (So sánh cặp doanh nghiệp)
* Cho phép người dùng tùy chọn linh hoạt 2 mã cổ phiếu bất kỳ (Ví dụ: `CTG` vs `FPT`) để đối chiếu trực tiếp.
* So sánh trực quan các đường xu hướng: **ROE Trend**, **Net Profit Growth (QoQ)**, **Net Margin** và cấu trúc đòn bẩy vốn **Capital Structure** qua các năm.

### Tab 3: Company Profile (Hồ sơ chi tiết doanh nghiệp)
* Đi sâu vào cấu trúc nội tại của một doanh nghiệp được chọn (Ví dụ: `FPT`).
* Tích hợp thanh đo trạng thái (KPI Status) tự động đánh giá (Ví dụ: *Status: Healthy Revenue*).
* Bảng ma trận tài chính chi tiết (**Detailed Financial Matrix**) phân rã động các dòng tiền và cấu trúc tài sản theo dạng bảng báo cáo kế toán tiêu chuẩn.

---

## 6. Hướng Dẫn Xem Dự Án (Instructions for Reviewers)

> **LƯU Ý QUAN TRỌNG:** Để thuận tiện nhất cho quá trình triển khai, toàn bộ dữ liệu từ MySQL local đã được cấu hình ở chế độ **Import Mode** và lưu trữ nén trực tiếp vào file báo cáo. **Chỉ cần tải thư mục này về và kích đúp mở file `PowerBI_demo.pbip` (hoặc `PowerBI_demo.pbix`) là có thể tương tác, click chọn bộ lọc và xem toàn bộ biểu đồ chạy mượt mà ngay lập tức** mà không cần phải cài đặt hay cấu hình lại kết nối server database.

Nếu cần cấu hình chạy lại hệ thống từ đầu với Database:
1. **Bước 1:** Khởi tạo Database bằng cách mở MySQL Workbench, tạo một schema tên là `vn30_data` và import file mã nguồn `database.sql` (nằm trong thư mục `database/` của kho lưu trữ này).
2. **Bước 2:** Mở file Power BI, chọn `Transform Data` -> `Data source settings` -> Đổi đường dẫn kết nối cục bộ (Server Local) về đúng cấu hình MySQL trên máy của bạn và bấm `Refresh` để cập nhật dữ liệu.