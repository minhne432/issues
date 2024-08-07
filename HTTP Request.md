HTTP request (yêu cầu HTTP) có cấu trúc bao gồm các phần chính sau đây: Request Line, Headers, và Body. Dưới đây là mô tả chi tiết cho từng phần.

### 1. Request Line

Dòng yêu cầu bao gồm ba phần: phương thức HTTP, URL (hoặc URI), và phiên bản giao thức HTTP.

```
METHOD /path/to/resource HTTP/version
```

Ví dụ:

```
GET /index.html HTTP/1.1
```

### 2. Headers

Các header cung cấp thông tin bổ sung về yêu cầu hoặc về client. Mỗi header là một cặp khóa-giá trị, được phân tách bởi dấu hai chấm.

```
Header-Name: Header-Value
```

Một số headers phổ biến:

- `Host`: Tên miền của server (bắt buộc trong HTTP/1.1)
- `User-Agent`: Thông tin về client (trình duyệt, ứng dụng,...)
- `Accept`: Các loại MIME mà client có thể xử lý
- `Content-Type`: Loại nội dung của body yêu cầu (thường dùng trong các yêu cầu POST, PUT,...)
- `Authorization`: Thông tin xác thực

Ví dụ:

```
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Content-Type: application/json
Authorization: Bearer <token>
```

### 3. Body

Phần body chứa dữ liệu được gửi từ client tới server. Body thường chỉ có trong các yêu cầu sử dụng phương thức POST, PUT, PATCH.

Ví dụ:

```json
{
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

### Cấu trúc hoàn chỉnh của một HTTP request

Dưới đây là ví dụ về một yêu cầu HTTP hoàn chỉnh sử dụng phương thức POST:

```
POST /api/v1/users HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>

{
    "name": "John Doe",
    "email": "john.doe@example.com"
}
```

### Các phương thức HTTP phổ biến

- **GET**: Yêu cầu lấy dữ liệu từ server (không có body).
- **POST**: Gửi dữ liệu tới server để xử lý (có body).
- **PUT**: Cập nhật tài nguyên hiện có hoặc tạo tài nguyên mới nếu không tồn tại (có body).
- **DELETE**: Xóa tài nguyên trên server (không có body).
- **PATCH**: Cập nhật một phần tài nguyên hiện có (có body).

### Tổng kết

Cấu trúc của một yêu cầu HTTP bao gồm:

1. **Request Line**: METHOD, URL, HTTP version.
2. **Headers**: Các thông tin bổ sung.
3. **Body**: Dữ liệu (nếu có).

Nếu bạn cần thêm thông tin chi tiết hoặc có câu hỏi cụ thể, hãy cho tôi biết!
