🧾 Giới thiệu
Repo tempPrinttAppSheet là một công cụ hỗ trợ người dùng AppSheet tạo các mẫu in (phiếu chi, phiếu thu...) dưới dạng trang HTML. Dữ liệu từ AppSheet sẽ được truyền vào mẫu thông qua URL chứa tham số, sau đó hiển thị lên trình duyệt để người dùng có thể in trực tiếp.

📦 Cấu trúc repo
Repo chứa các file HTML như:

phieuchi.html: Mẫu HTML để in phiếu chi

(Có thể mở rộng thêm: phieuthu.html, phieubc.html…)

Mỗi file HTML được thiết kế sẵn để nhận dữ liệu từ tham số URL (query string), sau đó hiển thị nội dung đầy đủ như: đơn vị, địa chỉ, người nhận, số tiền, lý do, ngày tháng,...

⚙️ Cách sử dụng trong AppSheet
Bước 1: Tạo Action trong AppSheet
Tạo một Action kiểu:
"External: open a website"
Nhập URL theo định dạng sau:

appsheet
Sao chép
Chỉnh sửa
CONCATENATE(
  "https://dohuuduy.github.io/tempPrinttAppSheet/phieuchi.html?",
  "donvi=", ENCODEURL(ANY(Info[Đơn vị])), "&",
  "diachi=", ENCODEURL(ANY(Info[Đại chỉ])), "&",
  "quyenso=", ENCODEURL([Quyển số]), "&",
  "so=", ENCODEURL([Số]), "&",
  "no=", ENCODEURL([Nợ]), "&",
  "co=", ENCODEURL([Có]), "&",
  "nguoinhan=", ENCODEURL([Người Nhận/Nộp]), "&",
  "diachinhan=", ENCODEURL([Địa chỉ Nhận/Nộp]), "&",
  "lydo=", ENCODEURL([Lý do]), "&",
  "sotien=", ENCODEURL([Số tiền]), "&",
  "kemtheo=", ENCODEURL([Kèo theo]), "&",
  "ngay=", DAY([Thời gian]), "&",
  "thang=", MONTH([Thời gian]), "&",
  "nam=", YEAR([Thời gian])
)
📌 Lưu ý:

Sử dụng hàm ENCODEURL() để đảm bảo dữ liệu không bị lỗi khi có dấu tiếng Việt hoặc ký tự đặc biệt.

Info là tên bảng chứa thông tin chung như đơn vị, địa chỉ (có thể thay bằng bảng khác nếu bạn cấu trúc khác).

Bước 2: Gắn Action vào nút hoặc hành động trong ứng dụng
Bạn có thể gán Action này vào:

Một nút trong giao diện chi tiết

Một hành động tự động sau khi ghi dữ liệu

Workflow/Automation nếu cần

📄 Kết quả hiển thị
Khi người dùng nhấn vào Action, hệ thống sẽ mở trình duyệt với một URL có dạng như sau:

perl
Sao chép
Chỉnh sửa
https://dohuuduy.github.io/tempPrinttAppSheet/phieuchi.html?donvi=Công%20ty%20ABC&diachi=Hà%20Nội&quyenso=01&so=123&no=0&co=1000000&nguoinhan=Nguyễn%20Văn%20A&diachinhan=Đà%20Nẵng&lydo=Thanh%20toán%20hợp%20đồng&sotien=1.000.000đ&kemtheo=Hóa%20đơn%20số%20123&ngay=23&thang=6&nam=2025
Trang HTML phieuchi.html sẽ nhận các biến trong URL, hiển thị đúng thông tin và tự động gợi ý in nếu bạn thiết lập.

🛠️ Tuỳ chỉnh mẫu in
Bạn có thể:

Tùy chỉnh giao diện HTML trong phieuchi.html

Thêm CSS để định dạng đẹp hơn

Thêm nút in (<button onclick="window.print()">In</button>) nếu cần

📁 Mở rộng thêm
Bạn có thể tạo thêm mẫu khác bằng cách:

Tạo file mới như phieuthu.html, phieubc.html,...

Copy nội dung mẫu, thay đổi các biến cần hiển thị

Gọi đúng tên file trong URL khi tạo Action

❓ Ví dụ thực tế
Giả sử bạn có phiếu chi với dữ liệu như sau:

Trường	Giá trị
Đơn vị	Công ty ABC
Địa chỉ	Hà Nội
Quyển số	01
Số	123
Nợ	0
Có	1.000.000
Người nhận/nộp	Nguyễn Văn A
Địa chỉ nhận/nộp	Đà Nẵng
Lý do	Thanh toán hợp đồng
Số tiền	1.000.000đ
Kèm theo	Hóa đơn số 123
Thời gian	23/06/2025

Khi bấm nút in, AppSheet sẽ mở:

r
Sao chép
Chỉnh sửa
https://dohuuduy.github.io/tempPrinttAppSheet/phieuchi.html?...[các biến được điền]...
Và hiển thị một phiếu chi hoàn chỉnh sẵn sàng để in.
