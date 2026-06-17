Postman API Testing
1. Giới thiệu về Postman
Postman là một nền tảng toàn diện cho việc phát triển, sử dụng và quản lý API. Công cụ này cho phép người dùng tạo, gửi, kiểm tra và chia sẻ các yêu cầu API một cách dễ dàng. Postman hiện là một trong những công cụ phổ biến được sử dụng trong lĩnh vực kiểm thử API.
Một số tính năng chính của Postman:
•	Tạo yêu cầu HTTP: Postman cho phép tạo các yêu cầu HTTP với nhiều phương thức khác nhau như GET, POST, PUT, DELETE. Người dùng có thể nhập URL API, thêm header, body và các tham số yêu cầu.
•	Gửi yêu cầu và xem phản hồi: Postman cho phép gửi request đến API và xem response trả về, bao gồm status code, header, body và thời gian phản hồi.
•	Kiểm tra API: Postman hỗ trợ viết test script để kiểm tra status code, dữ liệu trả về, thời gian phản hồi và định dạng JSON.
•	Quản lý Collection: Postman cho phép gom nhiều request vào một collection để dễ quản lý và chạy kiểm thử theo nhóm.
•	Quản lý môi trường: Postman hỗ trợ tạo environment để lưu các biến như base URL, token, API key.
•	Tự động hóa kiểm thử: Postman có Collection Runner giúp chạy nhiều request liên tiếp và xem kết quả pass/fail.
•	Chia sẻ API: Postman cho phép chia sẻ collection, environment và tài liệu API với các thành viên khác.
2. Công cụ sử dụng
Công cụ	Mục đích
Postman	Tạo request, gửi request và kiểm thử API
GitHub	Lưu trữ sản phẩm và viết báo cáo trong README.md
ReqRes API	API demo dùng để thực hành kiểm thử
Postman Collection Runner	Chạy tự động nhiều request trong collection
API demo được sử dụng:
https://reqres.in
Header sử dụng cho các request:
x-api-key: YOUR_API_KEY
Content-Type: application/json
3. Nội dung thực hiện
Trong bài thực hành, em đã tạo một collection trên Postman để kiểm thử các API cơ bản của ReqRes. Collection bao gồm các request với các phương thức GET, POST, PUT và DELETE.
STT	Method	API	Mục đích
1	GET	/api/users/2	Lấy thông tin một người dùng
2	POST	/api/users	Tạo người dùng mới
3	PUT	/api/users/2	Cập nhật thông tin người dùng
4	DELETE	/api/users/2	Xóa người dùng
4. Kịch bản kiểm thử
4.1. Request GET - Lấy thông tin người dùng
Method: GET
https://reqres.in/api/users/2
Mục đích: Kiểm tra API lấy thông tin người dùng theo ID.
Kết quả mong đợi:
•	Status code trả về là 200 OK.
•	Response có dữ liệu người dùng.
•	Dữ liệu trả về ở định dạng JSON.
Test script:
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response is JSON", function () {
    pm.response.to.be.json;
});

pm.test("Response time is less than 1000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
4.2. Request POST - Tạo người dùng mới
Method: POST
https://reqres.in/api/users
Body:
{
    "name": "Dang Minh Quang",
    "job": "Student"
}
Mục đích: Kiểm tra API tạo mới người dùng.
Kết quả mong đợi:
•	Status code trả về là 201 Created.
•	Response có thông tin người dùng vừa tạo.
•	Response có trường id và createdAt.
Test script:
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

pm.test("Response has id", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("id");
});

pm.test("Response has createdAt", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("createdAt");
});
4.3. Request PUT - Cập nhật người dùng
Method: PUT
https://reqres.in/api/users/2
Body:
{
    "name": "Dang Minh Quang",
    "job": "Tester"
}
Mục đích: Kiểm tra API cập nhật thông tin người dùng.
Kết quả mong đợi:
•	Status code trả về là 200 OK.
•	Response có thông tin đã cập nhật.
•	Response có trường updatedAt.
Test script:
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response has updatedAt", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("updatedAt");
});
4.4. Request DELETE - Xóa người dùng
Method: DELETE
https://reqres.in/api/users/2
Mục đích: Kiểm tra API xóa người dùng.
Kết quả mong đợi:
•	Status code trả về là 204 No Content.
•	Request được xử lý thành công.
Test script:
pm.test("Status code is 204", function () {
    pm.response.to.have.status(204);
});
5. Kết quả thực hiện
5.1. Tạo Collection trên Postman

  <img width="510" height="359" alt="image" src="https://github.com/user-attachments/assets/18eb5a5a-9c20-4d69-bbf0-570d28a233be" />

5.2. Kiểm thử request GET
<img width="975" height="621" alt="image" src="https://github.com/user-attachments/assets/297e643d-3893-44c0-8731-c7e0a5932f81" />

  
5.3. Kiểm thử request POST
<img width="979" height="629" alt="image" src="https://github.com/user-attachments/assets/a9e7f88f-a95f-49d0-a9f0-01811ec1e043" />

  
5.4. Kiểm thử request PUT
<img width="966" height="605" alt="image" src="https://github.com/user-attachments/assets/f7f2348d-13bc-4d94-b95b-2cbc38d38b78" />

  
5.5. Kiểm thử request DELETE
<img width="968" height="604" alt="image" src="https://github.com/user-attachments/assets/590647d0-d262-4c45-89a5-c575ac804409" />

  
5.6. Chạy Collection Runner
<img width="973" height="595" alt="image" src="https://github.com/user-attachments/assets/9403c868-7e30-4e62-a372-cb2f323328a7" />

  
6. Phân tích kết quả kiểm thử
Sau khi thực hiện các request bằng Postman, các API cơ bản đã được kiểm thử thành công.
Method	API	Status mong đợi	Kết quả
GET	/api/users/2	200	Pass
POST	/api/users	201	Pass
PUT	/api/users/2	200	Pass
DELETE	/api/users/2	204	Pass
Thông qua kết quả kiểm thử, có thể thấy các request gửi đến API đều trả về status code đúng như mong đợi. Các response trả về đúng định dạng JSON đối với các request GET, POST và PUT. Request DELETE trả về status code 204, thể hiện thao tác xóa được xử lý thành công.
Ngoài ra, việc sử dụng test script trong Postman giúp tự động kiểm tra status code, thời gian phản hồi và dữ liệu trả về. Điều này giúp giảm thao tác kiểm tra thủ công và tăng độ tin cậy trong quá trình kiểm thử API.
7. Nhận xét
Thông qua bài thực hành, em đã hiểu cách sử dụng Postman để gửi các request HTTP như GET, POST, PUT và DELETE. Em cũng biết cách thêm header, nhập body dạng JSON, xem response, kiểm tra status code và viết test script cơ bản.
Bên cạnh đó, em đã biết cách tạo collection, lưu các request vào collection và chạy tự động nhiều request bằng Collection Runner. Đây là bước quan trọng trong quá trình kiểm thử API vì giúp kiểm tra nhiều chức năng trong cùng một lần chạy.
8. Kết luận
Postman là công cụ hữu ích trong kiểm thử API, giúp kiểm tra nhanh chức năng của backend, xác minh dữ liệu phản hồi và hỗ trợ tự động hóa kiểm thử ở mức cơ bản.
Qua bài thực hành với ReqRes API, các request GET, POST, PUT và DELETE đều được kiểm thử. Kết quả cho thấy API phản hồi đúng status code mong đợi và dữ liệu trả về phù hợp với từng phương thức. Vì vậy, Postman là công cụ phù hợp để sinh viên làm quen với kiểm thử API và quy trình kiểm thử tự động ở mức cơ bản.
9. Tài liệu tham khảo
•	Video hướng dẫn Postman do giảng viên cung cấp.
•	Tài liệu Postman.
•	Tài liệu ReqRes API.

