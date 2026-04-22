# Biến nguyên thủy và biến tham chiếu

Trong Java có hai loại biến:

- Biến nguyên thủy: lưu trực tiếp giá trị
- Biến tham chiếu: lưu tham chiếu làm một reference trỏ tới .

**Biến nguyên thủy**

```java
int value = 10;
System.out.println(value); // 10
```

**Biến tham chiếu**

```java
public class Name {
	private String name;
	
	public name(String name) {
		this.name = name
	}
}

// === main function

Name luke = new Name("Luke");
	System.out.println(luke); // Name@4aa298b7 - Memory Addredsss
```
## Biến nguyên thủy

Java có tám biến nguyên thủy khác nhau. Trong đó: 

| Kiểu dữ liệu | Kích thước | Miền giá trị | Chú thích |
| ------------ | ---------- | ------------ | --------- |
| `boolean`    |            |              |           |
| `byte`       |            |              |           |
| `char`       |            |              |           |
| `int`        |            |              |           |
| `long`       |            |              |           |
| `float`      |            |              |           |
| `double`     |            |              |           |


Giá trị của một biến được truyền dưới dạng tham số sẽ không bị biến đổi ở phương thức gốc sau khi phương thức thực thi xong. Điều này có nghĩa là giá trị của các biến được sao chép bất cứ khi nào chúng được sử dụng trong các lời gọi phương thức - Pass by value, đây là cơ chế duy nhất của Java theo đặc tả của ngôn ngữ.

## Biến nguyên thủy và biến tham chiếu làm tham số phương thức

Khi gọi một phương thức, dù là biến nguyên thủy hay biến Object, giá trị được truyền vào sẽ được sao chép thay vì trỏ thẳng vào địa chỉ ô nhớ nắm giữ giá trị đó - đây còn gọi là remote control/address. Điều này giúp hạn chế side effect theo triết lý thiết kế của Java.

Trong Java có hai loại biến:

- Biến nguyên thủy: lưu trực tiếp giá trị
- Biến tham chiếu: lưu tham chiếu làm một reference trỏ tới .

**Biến nguyên thủy**

```java
int value = 10;
System.out.println(value); // 10
```

**Biến tham chiếu**

```java
public class Name {
	private String name;
	
	public name(String name) {
		this.name = name
	}
}

// === main function

Name luke = new Name("Luke");
System.out.println(luke); // Name@4aa298b7 tường minh ra là luke.hashCode()
```

**Vậy có cách nào thay đổi được không**

Câu trả lời là có, nếu ta tạo ra hàm `setter` cung cấp API cho bên ngoài được phép thay đổi giá trị, còn không thì không có cách nào.

```java
void foo(Name n) {
    n.setName("Vader"); // ảnh hưởng object gốc — vì cùng địa chỉ
    n = new Name("Solo"); // KHÔNG ảnh hưởng luke bên ngoài — vì gán lại reference copy
}
```
## Biến nguyên thủy

Java có tám biến nguyên thủy khác nhau. Trong đó: 

| Kiểu dữ liệu | Kích thước | Miền giá trị | Chú thích |
| ------------ | ---------- | ------------ | --------- |
| `boolean`    |            |              |           |
| `byte`       |            |              |           |
| `char`       |            |              |           |
| `int`        |            |              |           |
| `long`       |            |              |           |
| `float`      |            |              |           |
| `double`     |            |              |           |


Giá trị của một biến được truyền dưới dạng tham số sẽ không bị biến đổi ở phương thức gốc sau khi phương thức thực thi xong. Điều này có nghĩa là giá trị của các biến được sao chép bất cứ khi nào chúng được sử dụng trong các lời gọi phương thức - Pass by value, đây là cơ chế duy nhất của Java theo đặc tả của ngôn ngữ.

## Biến nguyên thủy và biến tham chiếu làm tham số phương thức

Khi gọi một phương thức, dù là biến nguyên thủy hay biến Object, giá trị được truyền vào sẽ được sao chép thay vì trỏ thẳng vào địa chỉ ô nhớ nắm giữ giá trị đó - đây còn gọi là remote control/address. Điều này giúp hạn chế side effect theo triết lý thiết kế của Java.

**Làm thế nào mà Java sao chép được giá trị của biến**

Tên gọi của nó là **Operand stack** hay còn gọi là ngăn xếp toán hạng 

Tôi sẽ tóm tắt nó như sau

```java
int a = 10;
foo(a);
```

Bước 1: Load giá trị của `a` từ local variable đẩy lên operand stack
Bước 2: Gọi method invokestatic foo
	- Tạo stack frame mới
	- pop giá trị từ operand stack
	- gán vào tham số `x`

Bên trong method

```txt
foo frame:
x = 10
```

Tương tự như Object, nhưng thay vì lấy giá trị, nó lấy địa chỉ ô nhớ.

Ví dụ thực tế, tôi sẽ annotation bằng dấu `//` tương tự như comment trong Java 
```bash 
❯ javap -c Main 
Compiled from "Main.java"
	public class Main {
  public Main();
    Code:
         0: aload_0 // push `this` -> call constructor của Object 
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return

  public static void foo(int);
    Code:
         0: iinc          0, 1 // Local variable slot 0 (x) = x + 1 
         3: return

  public static void main(java.lang.String[]);
    Code:
         0: bipush        10 // push 10 từ operand stack rồi lưu vào local var slot 1 (a)
         2: istore_1  // đẩy giá trị của `a` từ local variable slot 1 lên operand stack, chuẩn bị cho lời gọi `invokestatic`"
         3: iload_1
         4: invokestatic  #7                  // Method foo:(I)V
         7: return
}
```
