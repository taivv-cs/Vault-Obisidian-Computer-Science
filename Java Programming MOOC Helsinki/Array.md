# Array

Array có trong Java từ rất sớm, trước cả Collections Framework (Java 1.2) và trước cả Generics. Điều này cho thấy Array giữ vai trò là Low-level container, không giống như ArrayList - được triển khai dựa trên Array.

Array hay còn gọi là mảng, nó chứa một số lượng giới hạn các phần tử được đánh dấu bằng chỉ số.

Các giá trị của mảng còn được gọi là phần tử.

Array là object, có thuộc tính `length` nhưng không có method (ngoài những gì kế thừa từ Object) như và không override.

## Đặc điểm

- Kích thước cố định khi được khởi tạo, tăng hay giảm kích thước mảng phải tạo mảng mới.
- Truy cập ngẫu nhiên thông qua vị trí rất nhanh vì dữ liệu nằm liên tiếp trong ô nhớ, đổi lại chèn xóa ở giữa và đầu rất tốn kém.
- Lưu trữ cùng kiểu dữ liệu
- Không có thread-safe.
## Độ phức tạp

| Tính năng          | Độ phức tạp |
| ------------------ | ----------- |
| Truy cập           | O(1)        |
| Thêm/xóa giữa cuối | O(n)        |
| Tìm kiếm           | O(n)        |

## Đánh đổi

**Dùng khi**

- Biết trước kích thước
- Cần hiệu năng tối đa
- Truy xuất dữ liệu thông qua chỉ số

**Không nên dùng khi**

- Cần resize linh hoạt
- Thêm/xóa thường xuyên
- Cần API tiện lợi

## Thao tác mảng

### Khởi tạo mảng

**Có hai cách để khởi tạo mảng**

Một mảng được khai báo bằng cách thêm dấu ngoặc vuông sau loại phần tử mà nó chứa.

Một mảng mời được khởi tạo bằng cách gọi `new` theo sau là loại phần tử, dấu ngoặc vuông.

- Cách đầu tiên, ta phải xác định rõ kích thước của mảng khi tạo.

```java
int[] numbers = new int[3];

// Tuy nhiên, khi khởi tạo theo các này thì mọi phần tử sẽ được Java gán bằng 0, đối với Object thì null
```

- Cách thứ hai là gán phần tử ngay khi vừa khởi tạo

```java
int [] numbers = {1, 2, 3};
// Khai báo và khởi tạo kích thước mảng cùng lúc -> Java tự biết kích thước mảng là 3

// Hoặc viết đầy đủ expression
int [] numbers = new int[]{1, 2, 3};

```

> [!note] Hint
> Cách viết đầy đủ biểu thức có thể được dùng ở mọi nơi. Ví dụ:
> ```java
>System.out.println(Arrays.toString(new int[] {1, 2, 3}));
> ```

### Gán và truy cập phần tử

Mỗi phần tử của mảng được tham chiếu bằng vị trí của nó. Ví dụ dưới đây sẽ tạo ra một mảng chứa 3 số nguyên, sau đó gán giá trị cho chỉ số 0 và 2.

```java
int[] numbers = new int[3];
numbers[0] = 2;
numbers[2] = 5;

numbers[3]; // ArrayIndexOutOfBoundsException
```

