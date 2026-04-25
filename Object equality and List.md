# So sánh đối tượng trong ArrayList

Để kiểm tra đối tượng có tồn tại trong `ArrayList`, ta sẽ sử dụng method `contains`.

Thay vì ta viết một vòng lặp và dùng `equals` tìm xem có thấy đối tượng này không, nếu có trả về `true` không thì trả về `false` thì hàm contains sẽ thay ta làm việc đó. Cách viết thủ công và cách sử dụng hàm `contains` sẽ được thông qua ví dụ dưới đây

```java
// Giả sử ta có đối tượng Bird có thuộc tính name
// Ta có một danh sách `Bird` như sau

ArrayList<Bird> birds = new ArrayList<>();
Bird red = new Bird("Red");
birds.add(red); // Đây là Object trong List 
```

Cách viết thông thường - điều này chỉ đúng với ArrayList

```java
red = new Bird("Red"); // Object khác nhưng gán lại cho red - cùng state
boolean isFound = false;
for (Bird i : birds) {
	if (i.equals(red))
		isFound = true;
		break;
	}
}
```

Dùng contains
```java
System.out.println(birds.contains(red));
```

Tuy nhiên, cả hai đều trả về false vì `contains` không hề biết thế nào là hai `Bird` giống nhau, nó phụ thuộc hoàn toàn vào `equals` mà object cung cấp.

Mặc định, hàm `contains` hoạt động như cách ta viết tường minh vòng for ra để chạy, nó duyệt qua từng phần tử trong danh sách, nếu như tìm thấy nó sẽ dừng lại và return true, tuy nhiên, mỗi khi duyệt nó lại gọi hàm `equals` ra điểm kiểm tra xem mà mặc định ,`Object.equals()` so sánh tham chiếu (giống với `==`). Điều này dẫn đến nó so sánh tham chiếu chứ không so sánh Object như ta muốn, vậy nên ta phải định nghĩa lại hàm `equals`.

Ta sẽ định nghĩa lại hàm `equals` như sau để so sánh trạng thái (state) của object thay vì chỉ so sánh identity/reference. 

```java
@Override
public boolean equals(Object compared)  {
	if (this == compared) { // cùng một object
		return true;
	}
	if (!(compared instanceof Bird)) { // Nếu không phải đối tượng kiểu Bird
		return false;}
	Bird comparedBird = (Bird) compared; // Ép kiểu về Bird 
	return Objects.equals(this.name, comparedBird.name);
}
```

Hai bird có cùng name được coi là bằng nhau và đây thuộc về quy định thiết kế không phải mặc định cho mọi class

%% TODO: override hashCode() khi học đến hashmap/hastSet %%
%% Contract: nếu equals() true thì hashCode() phải bằng nhau %%