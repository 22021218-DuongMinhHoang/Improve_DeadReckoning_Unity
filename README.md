# PHƯƠNG PHÁP NỘI SUY HỖ TRỢ GIẢM ĐỘ TRỄ TRONG GAME TRỰC TUYẾN
## Mô tả

Dead Reckoning là kỹ thuật dự đoán và nội suy trạng thái dựa trên dữ kiện từ quá khứ trong game trực tuyến. Mục tiêu của kỹ thuật này là đảm bảo trong môi trường mạng có độ trễ cao, vật thể vẫn có thể di chuyển chính xác và mượt mà cho dù thiếu thông tin từ Server.

Khóa luận nghiên cứu và cài đặt hệ thống phương pháp đề xuất nhằm cải tiến và khắc phục những vấn đề còn tồn động trong kỹ thuật Dead Reckoning.

Khóa luận sử dụng game MissileRally để cài đặt phương pháp đề xuất.
Ban đầu game MissileRally chỉ có Dead Reckoning cơ bản.

## Chức năng cài đặt

Các chức năng được cài đặt bao gồm:
- Dead Reckoning cơ bản:
  - Dự đoán bằng mô hình dự đoán bậc một
  - Nội suy tuyến tính
- Dead Reckoning cải tiến:
  - Server gửi thêm thông tin timestamp để Client dự đoán
  - NetworkTimer hỗ trợ đồng bộ tần suất cập nhật khung hình giữa Client và Server
  - CircularBuffer là bộ đệm xoay vòng giúp lưu trữ input và trạng thái theo tick
  - Dự đoán bằng mô hình bậc hai
  - Thay đổi ngưỡng sai số tối đa để thích ứng với độ trễ mạng biến thiên
  - Nội suy làm mượt chuyển động bằng SmoothDamp
- Kỹ thuật bổ trợ:
  - Client-side Prediction và Server Reconciliation hỗ trợ Client phản ứng ngay lập tức với input của người chơi thay vì phải đợi phản hồi từ Server
  - Lag Compensation hỗ trợ Server xác nhận input tương tác từ quá khứ để đảm bảo không bị bỏ qua tương tác quan trọng
- Giao diện hỗ trợ kiểm chứng độ hiệu quả của phương pháp đề xuất.

## Cách chạy code

Môi trường: Unity 2022.3 LTS

Quy trình chạy code:
- Tải mã nguồn về, giải nén và mở bằng Unity
- Cài đặt package ParrelSync
- Sử dụng ParrelSync để tạo bản sao của Editor hiện tại
- Mở bản sao vừa tạo
- Chạy game trên cả hai Editor
- Một Editor đóng vai trò là người chơi Host sẽ nhấn nút Host trên màn hình chính
- Một Editor đóng vai trò là người chơi Guest sẽ nhấn nút Join trên màn hình chính
- Khi cả hai người chơi đã vào phòng chờ thì cả hai nhấn Ready
- Cuộc đua bắt đầu, cả hai xe cố đi hết một vòng quanh đường đua trong thời gian ngắn nhất

## Cách chạy bản build demo

Quy trình chạy bản build demo:
- Tải bản release MissileRally từ github
- Giải nén và chạy từ 2 đến 4 chương trình game bằng MissileRally.exe
- Một người chơi đóng vai trò Host sẽ nhấn nút Host trên màn hình chính
- Các người chơi còn lại là Guest sẽ nhấn nút Join trên màn hình chính
- Khi các người choi đã vào phòng chờ thì nhấn Ready
- Cuộc đua bắt đầu, các xe cố đi hết một vòng quanh đường đua trong thời gian ngắn nhất

