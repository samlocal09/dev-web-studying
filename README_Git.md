# Ops: GIT

Tổng hợp các lệnh, trường hợp phổ biến, được sử dụng và xử lý trong quá trình phát triển mã nguồn.

/assets/git/intro.png
##### Source: https://www.getdbt.com/ui/img/guides/analytics-engineering/git-workflow-1.png

## Ghi chú

- @{name}: Dùng để chỉ một biến/giá trị cần nhập vào

## Local/Remote repository (repo)

Remote repo là nơi chia sẽ công khai hoặc trong nhóm người dùng nhất định được quản lý trên server.
Local repo là nơi làm việc của mỗi thiết bị cụ thể, ví dụ là máy của bạn.

Bạn có thể publish (push) những thay đổi, chức năng mới được triển khai từ local lên remote repo để mọi người đều có thể sử dụng. Và ngược lại bạn cũng có thể kéo về (pull/fetch) những thay đổi mới về máy local của bạn.

## clone

Để tham gia vào phát triển repo, bạn cần phải sao chép repo về máy local. Cách clone phổ biến là qua url HTTPS.

```
git clone @{url_https}
``` 

Ví dụ:
```
git clone https://github.com/samlocal09/1-Ops-Git-Basic-Day-Life.git
```

Khi clone thành công, bạn sẽ thấy các dữ liệu trong repo ở local giống với remote repo lúc bấy giờ, lúc này bạn đã có thể bắt đầu triển khai phát triển repo.

## branch, checkout

Để copy hay còn gọi là rẻ nhánh tự một nhánh nào đó, bạn có thể dùng lệnh branch. Mặc định, lệnh này để tạo ra một nhánh mới giống với nhánh hiện tại bạn đang làm việc.

Việc rẻ nhánh giúp bạn có một nơi workspace) để thể triển khai công việc riêng biệt và lưu trữ những thay đổi mà không làm ảnh hưởng đến phiên bản hiện tại.

```
git branch @{new_branch_name}
```

Để chuyển (switch) sang nhánh khác, bạn có thể dùng lệnh checkout. 

```
git checkout @{branch_name}
```

## fetch, pull

Trong quá trình phát triển, repo sẽ được cập nhật thường xuyên từ các user cùng tham gia vào dự án. Để làm mới local repo, bạn có thể sử dụng lệnh pull/fetch tuỳ trường hợp. Cả 2 lệnh đều dùng để kéo những thay đổi từ remote repo về local của bạn, nhưng có điểm khác biệt sau:

- Lệnh fetch không hợp nhất chúng với local repository, sẽ không bị ảnh hưởng gì nếu bạn làm việc trên một nhánh và đang có những chỉnh sửa, lệnh fecth không làm thay đổi trạng thái bạn đang làm việc. Nhờ vào lệnh này, bạn có thể xem những thay đổi trên nhánh bạn đang làm việc chung.

```
git fetch
```

- Lệnh pull cũng tương tự như fetch, nhưng nó sẽ làm thêm hành động là merge thay đổi vào workspace bạn đang làm việc. Nó giúp đảm bảo cho workspace bạn làm việc luôn ở trạng thái mới nhất. Có thể sẽ xảy ra xung đột (conflict) trong cùng một tệp nếu có nhiều sữa đổi từ nhiều commit tại một hoặc nhiều vị trí.

```
git pull
```

## add, commit

Để lưu những nội dung thay đổi cần bạn sử dụng lệnh commit, commit nôm na giúp lưu các nội dụng được dánh dấu lại, nhưng chưa đưa lên remote repo. Nó chỉ ở dưới local repo máy bạn.

Thế nên bạn cần phải cho biết nhưng thay đổi nào (file) nào cần được lưu trong commit đó qua lệnh add. 

```
git add .
```

Khi commit bạn cần ghi chú lại thông tin cho commit đó, là cách để biết mục đích của lần thay đổi này là gì.

```
git commit -m "@{message}"
```

## push

Lệnh push dùng để public những commit dưới local ở nhánh hiện tại lên remote repo. Lúc này, mọi người có thể kéo về và thấy nhựng thay đổi của bạn tại nhánh đó.

```
git push
```

## merge

Lệnh merge giúp gộp thay đổi từ một nhánh khác. Các commit sẽ được gộp vào trong nhánh và sắp xếp theo thứ tự thời gian tăng dần. Đây là hành động có thể gây ra xung đột (conflict).

```
git merge @{merge_branch_name_to}
```

## Quản lý task của bạn
Mỗi người sẽ có cách quản lý task mình riêng, đây là một cách đơn giản để dễ dàng quản lý task của bạn trong quá trình phát triển dự án.

1. Clean/Reset repo, giúp tránh những lỗi tạo nhánh mới
```
git reset --hard
git clean -f
```

2. Fetch/Pull thay đổi về.
3. Rẻ nhánh từ nhánh bạn muốn tiếp tuc phát triển. Lấy vị dụ, thông thường ta có nhánh develop là nhánh làm việc giữa các developer, và là nhánh chứa hầu hết các tính năng. Bạn cần triển khai tính năng mới, thì bạn có thể rẻ nhánh từ nhánh develop.
4. Checkout qua nhanh bạn vừa tạo và thực hiện triển khai tính năng. Để đảm bảo không mất công sức, bạn luôn có thể commit và push lên remote repo để trong tình huống xấu, code vẫn luôn được lưu trữ nhé.
5. Khi task hoàn thành, bạn cần merge thay đổi vào lại nhánh chính, lấy ví dụ trên là nhánh develop. Các portal quản lý repo có hỗ trợ bạn tạo pull request (PR) để làm việc đó, PR còn có nhiều mục đích khác như để review code, tag những item bạn đang làm việc,...
6. Xử lý conflict nếu có. Thường thì người PR sẽ cần phải xử lý conflict nếu có và push lên conflict code đã được resolve

## TortoiseGit Windows Shell Interface

Việc commit/push/merge,... code diễn ra thường xuyên. Có những lệnh giúp bạn thao tác nhanh hơn, nhưng cũng có những việc khuyến khích nên sử dụng công cụ để tạo sự dễ dàng hơn.

TortoiseGit là một trong những cộng cụ như vậy. Hình dung thay vì gõ lệnh, bạn có thể dùng những chức năng của nó qua giao diện. Commit code luôn cần bạn là người tự review đầu tiên, bạn có thể dễ dàng thay được thay đổi trước và sau, cũng như loại bỏ những mã code dùng để test mà quên xoá chẳng hạn... Và cũng tạo thuận tiên trong việc xử lý conflict.

## Tips

Trong lúc làm việc không hẳn là bạn chỉ làm việc trong một workspace duy nhất, đôi lúc bạn cũng phải fixbug. Chuyển môi trường dev, staging, uat qua lại nhiều lần. Để giúp tăng chút ít thời gian cho việc này, bạn có thể tạo file lệnh chạy tự động cho các môi trường. Ví dụ trên windows là file .batch

File batch chuyển môi trường tham khảo
```
set SourcePath=D:\Project\A

REM #####Setting Environment - develop: Start#####
cd /d %SourcePath%

git rm -f .git/index.lock
git reset --hard
git clean -f
git fetch

git checkout develop
git pull 

git reset --hard origin/develop

REM #####Setting  Env: Done#####

IF %ERRORLEVEL% == 1 goto error_msg
pause
exit /b 1

:error_msg
echo build error
pause
exit /b 1

pause
```



