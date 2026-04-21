# ArrayList

ArrayList là một mảng động thuộc gói `java.util`, nó có khả năng thay đổi kích cỡ, thêm xóa phần tử một cách linh hoạt.

## Đặc điểm

- **Kích thước linh hoạt:** tăng 1.5x khi đầy

- **Lưu trữ đối tượng:** Sử dụng generics (`E`), thực chất là lưu reference (Object), kiểu dữ liệu nguyên thủy phải dùng Wrapper (Integer, Double, ...).

- **Thứ tự:** Duy trì đúng thứ tự các phần tử được thêm vào - giống như mảng, phần tử đầu tiên bắt đầu từ 0

- **Đồng bộ:** Không an toàn trong môi trường đa luồng

## Các phương thức phổ biến (API Level)

| Kiểu trả về | Tên phương thức     | Độ phức tạp | Mô tả                                           |
| ----------- | ------------------- | ----------- | ----------------------------------------------- |
| boolean     | add(E e)            | O(1)*       | Thêm phần tử vào cuối danh sách (có thể resize) |
| void        | add(int index, E e) | O(n)        | Chèn phần tử vào vị trí chỉ định                |
| E           | get(int index)      | O(1)        | Lấy phần tử tại index                           |
| E           | set(int index, E e) | O(1)        | Ghi đè phần tử tại index                        |
| E           | remove(int index)   | O(n)        | Xóa phần tử tại index (phải shift)              |
| boolean     | remove(Object o)    | O(n)        | Xóa phần tử đầu tiên khớp                       |
| int         | size()              | O(1)        | Số lượng phần tử                                |
| boolean     | contains(Object o)  | O(n)        | Kiểm tra tồn tại                                |
| void        | clear()             | O(n)        | Xóa toàn bộ phần tử                             |
> [!note] Khấu hao
> Đôi khi add sẽ là O(n) khi resize (copy mảng).
## Đánh đổi 

**Dùng khi**

- Truy xuât phần tử ngẫu nhiên thông qua chỉ số.
- Dữ liệu ít bị thay đổi, chủ yếu là đọc
- Tốn ít bộ nhớ.

**Không nên dùng khi** 

- Thao tác thêm xóa ở giữa hoặc đầu thường xuyên
- Cần thread-safe
- Dữ liệu quá lớn và resize nhiều

> Đánh đổi tốc độ ghi để lấy tốc độ đọc

**So sánh với cấu trúc liên quan**

| Thao tác            | ArrayList | LinkedList | Giải thích                                                                                                     |
| ------------------- | --------- | ---------- | -------------------------------------------------------------------------------------------------------------- |
| Truy xuất (get/set) | O(1)      | O(n)       | ArrayList truy cập thông qua chỉ số, LinkedList phải duyệt từ đầu.                                             |
| Thêm/xóa cuối       | O(1)      | O(1)       | Cả hai đều nhanh, nhưng ArrayList đôi khi mất thời gian hơn do phải tăng dung lượng.                           |
| Thêm/xóa đầu        | O(n)      | O(1)       | ArrayList phải dồn lại toàn bộ phần tử để lấp lại vj trí vừa xóa đi, còn LinkedList chỉ cần thay đổi con trỏ.  |
| Thêm xóa giữa       | O(n)      | O(n)       | Cả hai đều tốn thời gian để tìm, ArrayList do shift, còn LinkedList do tìm vị trí, còn việc chèn/xóa thì O(1). |
| Bộ nhớ              | ít hơn    | Nhiều hơn  | LinkedList tốn bộ nhớ nhiều hơn do phải lưu con trỏ, địa chỉ trước/sau.                                        |
> [!note] Khấu hao
>  - Linked List add-giữa = O(n) tổng: (n) tìm vị trí + O(1) mỗi pointer
>  - Lined List chỉ nhanh khi có reference

## Ghi chú

- **Resize họat động thế nào:** Arrays.copyOf sang mảng mới x 1.5