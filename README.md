# PHƯƠNG PHÁP NỘI SUY HỖ TRỢ GIẢM ĐỘ TRỄ TRONG GAME TRỰC TUYẾN
## Mô tả

Dead Reckoning là kỹ thuật dự đoán và nội suy trạng thái dựa trên dữ kiện từ quá khứ trong game trực tuyến. Mục tiêu của kỹ thuật này là đảm bảo trong môi trường mạng có độ trễ cao, vật thể vẫn có thể di chuyển chính xác và mượt mà cho dù thiếu thông tin từ Server.

Khóa luận nghiên cứu và cài đặt hệ thống phương pháp đề xuất nhằm cải tiến và khắc phục những vấn đề còn tồn động trong kỹ thuật Dead Reckoning.

## Vấn đề của Dead Reckoning
Dead Reckoning cơ bản còn tồn đọng một số vấn đề sau:

- Hạ tầng thời gian và lưu trữ trạng thái:
  - Kỹ thuật dự đoán giả định rằng thời điểm nhận trạng thái từ Server là thời điểm diễn ra trạng thái đấy mà không xét tới độ trễ mạng
  - Chưa có đồng bộ thời gian giữa Client và Server, dẫn tới thiếu đồng bộ trạng thái trên hệ thống
  - Chưa có cơ chế lưu trữ trạng thái để có thể hỗ trợ các kỹ thuật tua ngược để đồng bộ trạng thái giữa Client và Server
- Cơ chế dự đoán và nội suy:
  - Kỹ thuật cơ bản vẫn đang dùng mô hình dự đoán dựa trên chuyển động thẳng đều, dự đoán sẽ thiếu chính xác nếu vật thể di chuyển với vận tốc thay đổi liên tục
  - Kỹ thuật chưa có cơ chế thích ứng với độ trễ mạng không ổn định, ngưỡng sai số cố định có thể dẫn tới vấn đề mất cân bằng giữa độ chính xác và độ mượt chuyển động
  - Nội suy tuyến tính không đem lại sự mượt mà trong chuyển động do kỹ thuật này không dữ được quán tính chuyển động
- Input từ người chơi và các tương tác quan trọng:
  - Dead Reckoning không phù hợp với dự đoán và nội suy chuyển động cho vật thể do người chơi điều khiển, lí do là vì người chơi rất khó đoán
  - Các tương tác quan trọng đôi khi cũng có thể bị bỏ qua do độ lệch giữa trạng thái hiển thị trên Client và trạng thái thực sự trên Server

## Phương pháp đề xuất
Khóa luận đề xuất và cài đặt hệ thống cải tiến Dead Reckoning:

- Hạ tầng thời gian và lưu trữ trạng thái:
  - Mỗi gói tin từ Server sẽ có thêm timestamp, Client từ đó sẽ có thể dự đoán trạng thái thực chính xác hơn
  - Client và Server sẽ có tần suất cập nhật khung hình cố định giống nhau, từ đó đảm bảo đồng bộ khi lưu trữ trạng thái trên hệ thống
  - Bộ đệm xoay vòng để lưu trữ trạng thái, đảm bảo không tốn nhiều dung lượng cho các thông tin đã cũ
- Cơ chế dự đoán và nội suy:
  - Mô hình dự đoán dựa trên chuyển động thẳng biến đổi đều giúp dự đoán chính xác hơn
  - Cơ chế thích ứng ngưỡng sai số với độ trễ biến thiên, đảm bảo cân bằng giữa độ chính xác và độ mượt chuyển động
  - Nội suy SmoothDamp dựa trên hệ lò xo giảm chấn tới hạn, đảm bảo quán tính trong quá trình chuyển động giúp vật di chuyển mượt mà
- Input từ người chơi và các tương tác quan trọng:
  - Kỹ thuật Client-side Prediction áp dụng ngay lập tức input từ người chơi mà không cần phải đợi phản hồi từ Server, từ đó giúp người chơi có thể nhận được phản hồi hiển thị ngay lập tức
  - Kỹ thuật Server Reconciliation đảm bảo Client vẫn bám sát theo trạng thái thực từ Server, đảm bảo độ chính xác hiển thị
  - Lag Compensation giúp quay ngược và mô phỏng lại input trong quá khứ để đảm bảo không có tương tác nào bị bỏ qua
 
## 
