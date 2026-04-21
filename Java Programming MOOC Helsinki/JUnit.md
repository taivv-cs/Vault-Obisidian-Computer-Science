# JUnit

**JUnit** là thư viện phổ biến thư viện phổ biến nhất thế giới về kiểm thử. Khi viết code, để kiểm tra code mình có lỗi trong thực tế hay không người ta phải triển khai thứ gọi là _Unit Test_. Thư viện này sẽ đảm nhận vai trò đó trong việc kiểm thử bởi chính lập trình viên.

JUnit đảm bảo rằng các method của chính ta viết chạy tự động thay vì phải chạy thủ công `sout`.

JUnit sẽ tự động hóa khi đẩy lên github, nếu như code không pass test, ngay lập tức nó sẽ bị reject và không đẩy lên máy chủ thật.

JUnit có thể chay riêng từng test, và có thể chạy lại bất cứ lúc nào.

## Anotation

**Anotation** được dùng để đánh dấu để được khiển các luồng test

- `@Test`: Đánh dấu đây là một phương thức kiểm thử.

- `@BeforeEach`: Chạy hàm này trước mỗi bài test (thường dùng để khởi tạo dữ liệu mới).

- `@AfterEach`: Chạy sau mỗi bài test (thường dùng để xóa dữ liệu rác)

- `ParameterizedTest`: Cho phép chạy 1 bài test với 100 danh sách 100 mã vạch khác nhau cùng lúc
