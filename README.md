# Bước 1:Xác định Input&Output(I/O)
- Input:Phản hồi thô của khách hàng.
- Output:
1. File Json để lưu vào hệ thống
2. Bảng Markdow để nhân viên xem
3. Cơ chế xử lý lỗi (nếu khách gửi tin nhắn trống hay tin nhắn vô nghĩa)sẽ báo lỗi.
# Bước 2:lệnh Prompt
```
[CONTEXT] Bạn là chuyên gia tự động hóa dữ liệu thương mại điện tử.
[REQUEST] Trích xuất thông tin từ phản hồi của khách hàng thành JSON và Markdown Table gồm các trường: customer_name, product_name, rating, sentiment, key_issue.
[EXPLANATION] 
- Ví dụ 1 (Có dữ liệu): Input: "Mình tên Lan, mua máy xay sinh tố dùng tốt, 4 sao." -> Output JSON: {"status": "success", "data": {"customer_name": "Lan", "product_name": "Máy xay sinh tố", "rating": 4, "sentiment": "Positive", "key_issue": "Dùng tốt"}}
- Ví dụ 2 (Dữ liệu rỗng/vô nghĩa): Input: "..." -> Output JSON: {"status": "error", "message": "Dữ liệu không hợp lệ."}
[ACTION] Xử lý dữ liệu tại phần [EXTRAS]. Bắt buộc trả về đúng định dạng JSON và Bảng Markdown. Nếu dữ liệu rỗng, phải trả về lỗi, tuyệt đối không tự bịa thông tin.
[TONE] khách quan.
[EXTRAS] "Mình tên Lan, vừa mua máy xay sinh tố bên mình hôm qua, máy dùng tốt nhưng hộp đựng bị móp một góc nhỏ, hy vọng shop rút kinh nghiệm. Đánh giá 4/5 sao."
```
# Phần 3 Kết quả:
```json
{
  "status": "success",
  "data": {
    "customer_name": "Lan",
    "product_name": "Máy xay sinh tố",
    "rating": 4,
    "sentiment": "Positive",
    "key_issue": "Máy tốt nhưng hộp móp nhẹ"
  }
}

| Khách hàng | Sản phẩm | Đánh giá | Cảm xúc | Vấn đề chính |
| :--- | :--- | :--- | :--- | :--- |
| Lan | Máy xay sinh tố | 4/5 | Positive | Máy tốt nhưng hộp móp nhẹ |
```
