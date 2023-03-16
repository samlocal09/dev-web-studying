# Dev: .NET

Tổng hợp các kiến thức học tập, làm việc tích luỹ theo thời gian.

<img src="./assets/.net/intro.png" width="100%"/>

###### Source: https://www.koskila.net/wp-content/uploads/2020/03/OdysGhkgFv1.png

## List Add vs List Append

Dùng .Add để thêm một phần tử mới vào list, phần tử mới sẽ nối tiếp list trước đó. Đây là hành động có thể chỉnh sửa (modify) list.

> Vd: List1 = [2, 3, 4], List1.Add(5) => List1 = [2,3,4,5].

Dùng Append khi muốn sao chép list và thêm phần tử mới. Method Append là behavior của IEnumerable, List gọi được là ILIST implement IEnumerable. Enumerable.Append() trả về collection mới, chứ không chỉnh sửa list đang dùng.

> vd List1 = [2, 3, 4], List1.Append(5) => List1 = [2,3,4], không thay đổi.

## Concat 2 List - anonymous type

Có thể nối 2 list với nhau bằng method "concat". Với trường hợp 2 list cùng loại với nhau (cùng model) sẽ hoạt động tốt, chỉ cần chú ý ở trường hợp nếu 2 list là dạng anonymous.

Vd anonymous list
```csharp
    var data = new List<DataModel>
    {
        new DataModel { Name = "A", Value = 1 },
        new DataModel { Name = "B", Value = 2 },
    };
    var listA = data.Where(w => w.Value == 1).Select(s => new { PropA = s.Name , PropB = s.Value });
    var listB = data.Where(w => w.Value == 2).Select(s => new { PropA = s.Name , PropB = null });
	var listC = listA.Concat(listB);
	
	foreach(var i in listC) {
	    Console.WriteLine ($"item-{i}:"); 
	}
```
Có vấn đề khi giá trị của PropB bì null, dẫn đến 2 list trên sẽ đang được hiểu là:
```csharp
	listA: f__AnonymousTypee<string, int>
	listB: f__AnonymousTypee<string, int?>
```
Thế nên, TH vẫn phải nối 2 chuỗi này, thì các property trong list cần parse về cùng kiểu:
```csharp
    var listA = data.Where(w => w.Value == 1).Select(s => new { PropA = (string)s.Name , PropB = (int?)s.Value });
    var listB = data.Where(w => w.Value == 2).Select(s => new { PropA = (string)s.Name , PropB = (int?)null });
```

