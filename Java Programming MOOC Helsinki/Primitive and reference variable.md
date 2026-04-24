# Biến nguyên thủy và biến tham chiếu

Java có hai loại biến, trong đó 

- **Biến nguyên thủy** là biến lưu trực tiếp giá trị.
- **Biến tham chiếu** là biến lưu một reference do JVM quản lý, dùng để truy cập Object trên heap.

## Biến nguyên thủy

Java có 8 kiểu nguyên thủy: 

| Kiểu      | Kích thước             | Miền giá trị     | Chú thích                                     |
| --------- | ---------------------- | ---------------- | --------------------------------------------- |
| `boolean` | không xác định (logic) | `true` / `false` | JVM không quy định size cụ thể                |
| `byte`    | 8-bit                  | -128 → 127       | số nguyên có dấu                              |
| `short`   | 16-bit                 | -32,768 → 32,767 | ít dùng                                       |
| `char`    | 16-bit                 | 0 → 65,535       | ký tự Unicode, không dấu                      |
| `int`     | 32-bit                 | -2³¹ → 2³¹ - 1   | kiểu số nguyên mặc định                       |
| `long`    | 64-bit                 | -2⁶³ → 2⁶³ - 1   | cần suffix `L` khi khai báo literal           |
| `float`   | 32-bit                 | ~±3.4E38         | ~6–7 chữ số thập phân, cần suffix `f`         |
| `double`  | 64-bit                 | ~±1.8E308        | ~15–16 chữ số thập phân, mặc định cho số thực |

Các biến nguyên thủy không phải lúc nào cũng ở trong stack, nhưng theo mô hình khái niệm chúng được lưu trong stack frame.

## Biến tham chiếu

Biến tham chiếu lưu một reference value do JVM quản lý, dùng để truy cập object trên heap.

```java
Person alex = new Person("Alex", 10);

// Khi print object mà chưa override `toString()`, output là `ClassName@hashCode`
System.out.println(alex); // Person@4aa298b7
// tương đương: alex.getClass().getName() + "@" + Integer.toHexString(alex.hashCode())
```

> `hashCode()` mặc định không phải memory address thật — từ Java 7 trở đi JVM có thể di chuyển object trong heap (GC compaction), giá trị này là implementation-dependent

## Cơ chế truyền tham số

Java **chỉ có một cơ chế duy nhất**: pass by value. Khi gọi method, giá trị của biến được **sao chép** vào stack frame mới.  Đối với:

- Primitive thì copy giá trị
- Object thì copy reference

```java
void foo(Person p) {
    p.setName("Vader");       
	// mutate object gốc — p và alex cùng reference
	p = new Person("Solo");   
	// chỉ thay đổi bản copy reference trong method
}

Person alex = new Person("Alex", 10);
foo(alex);
System.out.println(alex.getName()); // "Vader", không phải "Solo"
```

### Không thể thay đổi reference bên ngoài method
  
```java  
void foo(Person p) {  
	p = null;  
}  
  
Person alex = new Person("Alex", 10);  
foo(alex);  
System.out.println(alex); // vẫn còn
```

### Hai reference, một object

Gán `b = a` với reference type không tạo object mới . Thay vào đó, giá trị reference của `a` được copy sang `b`, nên cả hai cùng trỏ tới cùng một object trên heap.

```java
Person alex = new Person("Alex", 10);
Person john = alex; // john nhận bản copy của reference (trỏ cùng object với alex)

alex.setName("Bob");
System.out.println(john.getName()); // "Bob" — cùng object

john.setName("Hihi");
System.out.println(alex.getName()); // "Hihi" — cùng object
```

### Làm thế nào mà Java sao chép được giá trị của biến

Tên gọi của nó là **Operand Stack** (ngăn xếp toán hạng). Cơ chế hoạt động có thể tóm tắt như sau:

```java
int a = 10;
foo(a);
```

Bước 1: Load giá trị của `a` từ local variable đẩy lên operand stack 
Bước 2: Gọi method invokestatic foo 
- Tạo stack frame mới 
- Pop giá trị từ operand stack 
- Gán vào tham số `x` 

Bên trong method

```txt
foo frame:
x = 10
```

Tương tự như Object, nhưng thay vì lấy giá trị, nó lấy reference value.

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
         0: iinc          0, 1 # Local variable slot 0 (x) = x + 1 
         3: return

  public static void main(java.lang.String[]);
    Code:
         0: bipush        10 # push 10 từ operand stack rồi lưu vào local var slot 1 (a)
         2: istore_1            # pop từ stack, lưu vào local variable a
         3: iload_1             # đẩy giá trị của `a` từ local variable slot 1 lên operand stack, chuẩn bị cho lời gọi `invokestatic`"
         4: invokestatic  #7                  // Method foo:(I)V
         7: return
}
```

