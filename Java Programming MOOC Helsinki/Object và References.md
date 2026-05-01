# Object và References

Việc gọi một hàm khởi tạo với lệnh `new` sẽ dẫn đến vài sự kiện xảy ra. Đầu tiên, một khoảng không gian trong bộ nhớ máy tính sẽ được dự phòng để lưu trữ các biến đối tượng. Sau đó, các giá trị mặc định hoặc giá trị khởi tạo sẽ được thiết lập cho các biến đối tượng đó. 

Một lời gọi hàm khởi tạo sẽ trả về một tham chiếu đến đối tượng. Tham chiếu là thông tin về vị trí nơi mà dữ liệu đối tượng được lưu trữ

Về cơ bản, nó có 3 bước tường minh sau khi ta gọi từ khóa `new`:

B1: Tìm chỗ trống trên heap và cấp phát vùng nhớ cho Object
B2: Gán default value đưa mọi thứ về 0, `fasle` hoặc `null` tùy theo loại tham số.
B3: đổ dữ liệu, các câu lệnh như `this.age = age` mới chạy để ghi đè dữ liệu thật lên các ô nhớ dọn sẵn.

Vì vậy, giá trị của biến được thiết lập là một tham chiếu, nói cách khác, nó là kiến thức về vị trí các dữ liệu liên quan đến đối tượng đó.

> [!info]- Hình ảnh minh họa
> ![[Object and References.png]] 

Trong hình ảnh minh họa trên, object `john = alex` không phải là copy, chỉ là nó thêm một cái tên trỏ tới một object, điều này dẫn đến việc mọi thay đổi của `john` thực chất là thay đổi chính object mà `alex` đang tham chiếu.

```java
john.setName("Michael Jackson");
System.out.println("alex object: " + alex.getName());
System.out.println("john object: " + john.getName());
```

Muốn độc lập thì phải tạo Object mới bằng `new` để cung cấp vùng nhớ riêng cho Object đó.