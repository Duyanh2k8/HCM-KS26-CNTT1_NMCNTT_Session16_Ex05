# Bài 5 : Tối ưu tiện ích mở rộng cho hệ thống điều phối vận tải
## Phần 1: Phân tích
### 1. JSON Viewer là gì?
JSON Viewer là tiện ích mở rộng giúp hiển thị dữ liệu JSON từ API theo cấu trúc phân cấp, thay vì hiển thị một chuỗi văn bản dài khó đọc.

Ví dụ, máy chủ GreenLogistics trả về dữ liệu GPS:
```JSON
{
  "vehicle_id": "GL001",
  "driver": "Nguyen Van A",
  "location": {
    "latitude": 10.762622,
    "longitude": 106.660172
  },
  "status": "delivering"
}
```
Khi không có JSON Viewer, dữ liệu có thể hiển thị thành một chuỗi văn bản dài. Khi sử dụng JSON Viewer, dữ liệu được trình bày theo dạng cây phân cấp, có tô màu cú pháp và khả năng thu gọn, mở rộng.

**Vai trò trong quá trình Debug API:**
- Quan sát cấu trúc dữ liệu API.
- Kiểm tra các trường `vehicle_id`, `latitude`, `longitude`.
- Phát hiện trường dữ liệu bị thiếu hoặc sai kiểu.
- Kiểm tra dữ liệu lồng nhau.
- Hỗ trợ xác định lỗi trong quá trình trao đổi dữ liệu giữa Client và Server.
## Phần 2: Triển khai
### 1. Danh sách 5 Extensions cần thiết
Chia thành 3 nhóm chức năng:
1. JSON Viewer `Dev Suite`
- Định dạng và hiển thị JSON theo dạng cây.
- Kiểm tra dữ liệu GPS trả về từ API.
- Hỗ trợ phát hiện lỗi cấu trúc JSON.

Cài đặt: [JSON Viewer](https://chromewebstore.google.com/detail/jsonvue/chklaanhfefbnpoihckbnefhakgolnmc).

2. ModHeader `Dev Suite`
- Kiểm tra và tùy chỉnh HTTP Request Headers.
- Hỗ trợ thử nghiệm API.
- Kiểm tra các Header như Authorization, Content-Type.

Cài đặt: [ModHeader](https://chromewebstore.google.com/detail/modheader/pfmipeldmapjkkkdbbfobganlgjcbdcj?utm_source=chatgpt.com).

3. ColorZilla `Productivity`
- Lấy mã màu HEX, RGB từ giao diện website.
- Sử dụng công cụ Eyedropper để chọn màu.
- Hỗ trợ kiểm tra màu sắc trong thiết kế giao diện.

Cài đặt: [ColorZilla](https://chromewebstore.google.com/detail/colorzilla/bhlhnicpbhignbdhedgjhgdocnmhomnp).

4. WhatFont `Productivity`
- Nhận diện font chữ trên website.
- Kiểm tra tên font và kiểu chữ.
- Hỗ trợ kiểm tra và chuẩn hóa giao diện UI.

Cài đặt: [WhatFont](https://chromewebstore.google.com/detail/what-font-font-finder/opogloaldjiplhogobhmghlgnlciebin).

5. uBlock Origin Lite `Security`
- Chặn quảng cáo không mong muốn.
- Hạn chế trình theo dõi (Trackers).
- Hỗ trợ giảm tài nguyên tải từ các nội dung quảng cáo.

Cài đặt: [uBlock Origin Lite](https://chromewebstore.google.com/detail/ublock-origin-lite/ddkjiahejlhfcafbddmgiahcphecmpfh).
### 2. Bảng tổng hợp 5 tiện ích
|Nhóm|	Extension|	Chức năng chính|
|-|-|-|
|Dev Suite	|JSON Viewer|	Đọc dữ liệu JSON|
|Dev Suite	|ModHeader|	Kiểm tra HTTP Headers|
|Productivity|	ColorZilla|	Lấy mã màu HEX/RGB|
|Productivity	|WhatFont|	Nhận diện font chữ|
|Security|	uBlock Origin Lite	|Chặn quảng cáo và tracker|
### 3. Cách cài đặt Extensions
1. Mở Google Chrome.
2. Truy cập Chrome Web Store.
3. Tìm tên tiện ích cần cài đặt.
4. Kiểm tra tên nhà phát triển và quyền truy cập.
5. Nhấn Add to Chrome.
6. Chọn Add extension để xác nhận.
7. Lặp lại với các tiện ích còn lại.
### 4. Cách ghim Extensions lên Toolbar
Các bước thực hiện:
1. Nhấn biểu tượng hình mảnh ghép (Extensions) ở góc trên bên phải Chrome.
2. Tìm tiện ích muốn ghim.
3. Nhấn biểu tượng chiếc ghim (Pin) bên cạnh tiện ích.
4. Lặp lại cho những tiện ích thường xuyên sử dụng.
5. Kiểm tra các biểu tượng xuất hiện trên Toolbar.
### 5. Thiết lập Site Access – On click
Site Access cho phép kiểm soát phạm vi website mà Extension được phép đọc hoặc thay đổi dữ liệu.

**Các bước thiết lập:**
1. Nhập `chrome://extensions` vào thanh địa chỉ.
2. Chọn Details tại tiện ích cần cấu hình.
3. Tìm mục Site access.
4. Chọn On click.
5. Thực hiện tương tự với các tiện ích phù hợp.
## Phần 3: Kiểm thử
### 1. Kiểm tra tài nguyên của Extensions
Khi trình duyệt bị lag trong lúc tải biểu đồ Waterfall hoặc kiểm tra API, cần xác định tiện ích nào đang tiêu thụ nhiều RAM và CPU.

**Bước 1: Mở trang quản lý Extensions**

Nhập địa chỉ:
```text
chrome://extensions
```
Tại đây có thể:
- Xem danh sách tiện ích đã cài đặt.
- Bật hoặc tắt tiện ích.
- Kiểm tra quyền truy cập.
- Gỡ bỏ tiện ích không cần thiết.

**Bước 2: Kiểm tra mức sử dụng RAM**

Nhấn tổ hợp phím:
```text
Shift + Esc
```
Trình duyệt sẽ mở Chrome Task Manager.

Quan sát các cột:
|Thông số|	Ý nghĩa|
|---|---|
|Task	|Tên tiến trình|
|Memory footprint	|Lượng RAM đang sử dụng|
|CPU	|Mức sử dụng CPU|
|Network|	Lưu lượng mạng|
|Process ID|	Mã tiến trình|

**Bước 3: Xác định Extension gây lag**
1. Tìm các tiến trình có tên Extension.
2. Quan sát cột Memory footprint.
3. Kiểm tra tiến trình có mức sử dụng CPU cao.
4. Xác định tiện ích không cần thiết.
5. Thử tắt tiện ích và kiểm tra lại tốc độ trình duyệt.

**Bước 4: Tối ưu tài nguyên**
- Tắt tiện ích không sử dụng.
- Gỡ bỏ tiện ích trùng chức năng.
- Không mở nhiều công cụ kiểm thử cùng lúc nếu không cần thiết.
- Chỉ giữ những Extension thực sự phục vụ công việc.
### 2. Tiêu chí kiểm thử
|STT|	Nội dung kiểm thử	|Kết quả mong đợi|
|-|-|-|
|1|	Mở API GPS bằng JSON Viewer	|JSON hiển thị rõ ràng|
|2|	Kiểm tra HTTP Headers	|Đọc được thông tin Request Headers|
|3|	Sử dụng ColorZilla	|Lấy được mã màu HEX/RGB|
|4|	Sử dụng WhatFont	|Nhận diện được font chữ|
|5|	Truy cập website bằng uBlock Origin Lite|	Quảng cáo và tracker được lọc theo cấu hình|
|6|	Kiểm tra Site Access|	Extension chỉ có quyền trong phạm vi cho phép|
|7|	Kiểm tra RAM và CPU|	Xác định được tiến trình gây tiêu tốn tài nguyên|
