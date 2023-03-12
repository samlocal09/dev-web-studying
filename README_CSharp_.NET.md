# Dev: .NET

Tổng hợp các kiến thức học tập, làm việc tích luỹ theo thời gian.

<img src="./assets/.net/intro.png" width="100%"/>

###### Source: https://www.koskila.net/wp-content/uploads/2020/03/OdysGhkgFv1.png

## Common - List Add vs List Append

Dùng .Add để thêm một phần tử mới vào list, phần tử mới sẽ nối tiếp list trước đó. Đây là hành động có thể chỉnh sửa (modify) list.

>> Vd: List1 = [2, 3, 4], List1.Add(5) => List1 = [2,3,4,5].

Dùng Append khi muốn sao chép list và thêm phần tử mới. Method Append là behavior của IEnumerable, List gọi được là ILIST implement IEnumerable. Enumerable.Append() trả về collection mới, chứ không chỉnh sửa list đang dùng.

>> vd List1 = [2, 3, 4], List1.Append(5) => List1 = [2,3,4], không thay đổi.