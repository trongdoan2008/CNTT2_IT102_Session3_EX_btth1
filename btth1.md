# [Bài thực hành 1] Trích xuất và định dạng thông tin tuyển dụng
##  **Yêu cầu**

Xây dựng một Prompt duy nhất có khả năng xử lý một đoạn email ứng tuyển thô và trả về đồng thời:

- C - Context: Đóng vai trò là Chuyên viên xử lý dữ liệu nhân sự cấp cao.

- R - Request: Trích xuất các trường thông tin: Họ tên, Số điện thoại, Email, Vị trí ứng tuyển, Năm kinh nghiệm, Kỹ năng chính
```
(Họ tên: Chuyển về dạng viết hoa chữ cái đầu (Ví dụ: Nguyễn Văn A))

Số điện thoại: Chuẩn hóa về định dạng đầu số quốc gia hoặc loại bỏ dấu cách dư thừa.

Kỹ năng chính: Gom nhóm thành một danh sách không trùng lặp (ví dụ: ['Python', 'SQL', 'FastAPI']).

Trả về định dạng JSON thuần túy theo cấu trúc:

  { "name": "...", "phone": "...", "email": "...", "position": "...", "experience_years": , "skills": [...] }
```

- E - Explanation: Dữ liệu này sẽ dùng để import trực tiếp vào database tuyển dụng nên cần độ chính xác 100%.
```
Không được tự ý thêm thắt hoặc ảo giác các thông tin không có trong email của ứng viên.

Nếu thông tin nào bị thiếu (ví dụ không ghi số điện thoại), phải để giá trị là null trong JSON, không được tự điền bừa.

Chỉ trả về dữ liệu kết quả, nghiêm cấm viết thêm các đoạn văn giải thích ở đầu hoặc cuối câu trả lời.

Kiểm tra tính đúng đắn của cấu trúc JSON bằng các công cụ Validate JSON.
```
- A - Action: Quét qua email thô, xác định đúng các trường thông tin, phân loại kỹ năng thành một danh sách.

- T - Tone: Chính xác, khách quan, không thêm thắt văn phong cảm xúc.

- E - Extras: Cung cấp ít nhất 2 ví dụ Few-shot mẫu (cặp dữ liệu Input email thô -&gt; Output mong muốn) để định hình kết quả của AI.

few-shot 

1.

```json
input: tôi là nguyễn văn a có sdt là 0912345678  có email là a@gmail.com và em muốn ứng tuyển là python developer có 2 năm kinh nghiệm có những kĩ năng về mảng python sql fastAPI

{
"name": "Nguyễn Văn A",
    
    "phone": "+8412345678",
    
    "email": "a@gmail.com",
    
    "position": "Python Developer",
    
    "experience_years": 2,
    
    "skills": ["Python", "SQL", "FastAPI"]
}
  ```

2.
```json

input: tôi là lê thị meo có sdt là 0987654321  có email là Meo@gmail.com và em muốn ứng tuyển là tester có 1 năm kinh nghiệm có những kĩ năng về mảng Selenium", "Jira", "SQL
{
  "name": "Lê Thị Meo",
  
  "phone": "+8487654321",
  
  "email": "Meo@gmail.com",
  
  "position": "Tester",
  
  "experience_years": 1,
  
  "skills": ["Selenium", "Jira", "SQL"]
}
```