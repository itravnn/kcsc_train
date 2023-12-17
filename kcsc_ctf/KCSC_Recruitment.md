## Web - Pokemon Hof Panel Level 1

Vào link thì web có giao diện như dưới, có phần để nhập tên và chọn nhân vật 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/4fcbf529-53df-4359-9ec8-1aac2def8a31)

Em nhập thử linh tinh vô coi, umm thì không được gì cả. Rồi em hint thì ommmm em cũng hiểu cho lắm :<

![image](https://github.com/itravnn/kcsc_train/assets/127108265/bc6dabdd-4264-4e9d-90e5-57891fe52609)

Xong em vào phần khai khác lỗ hổng để xem thì có đoạn ni em thấy có hiểu chút 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/72446398-3ce6-419e-8331-4a8b799059f2)

```
O:4:"User":2:{s:4:"name":s:6:"carlos"; s:10:"isLoggedIn":b:1;}
```

Như ở ví dụ trên thì đối tượng user có 2 thuộc tính là name là thuộc tính isLoggedIn, thuộc tính name có giá trị là carlos , còn thuộc tính isLoggedIn thì có giá trị true ( nếu sai thì  là số 0)

Như vậy được rùi em đẩy lên burp xem thử

![image](https://github.com/itravnn/kcsc_train/assets/127108265/c6888fda-c411-465e-a04a-72ea8e219530)

Giá trị của trainer đã được encode, xem phần đã decode thì nhận thấy giá trị isChampion là 0, sửa 0 thành 1 để đăng nhập được chấp nhận thì sẽ ra flag

`KCSC{n0w_y0u_kn0w_s3r1al1z3_f0m4rt}`

## Web - Mi Tom Thanh Long

Sau khi vô trang thì em có test thử các danh mục nhưng không có gì, rồi để ý ở thanh url giá trị có thay đổi khi vào các mục khác nhau đồ. Rồi em thử thêm dấu ' vô coi có gì khong thì hiện báo lỗi

![image](https://github.com/itravnn/kcsc_train/assets/127108265/813abcd0-b3e3-4fdb-a7ac-14cdf88c5cc9)

Sau khi tìm hiểu trên mạng thì em tìm thấy bài writeup của clb mình, em có bấm vô coi thì thấy được cách giải quyết bằng [cơ chế URI](https://aithietke.com/directory-traversal-vulnerabilities-phan-4/) , dễ hiểu thì cơ chế này giúp mình đọc được nội dung file

payload 

```
?page=php://filter/convert.base64-encode/resource=pages/flag.php
```

![image](https://github.com/itravnn/kcsc_train/assets/127108265/2311e08d-0f97-4f6b-bb4e-4924ee1695f4)

payload sẽ trả về nội dung ở dạng base64_encode, chỉ cần decode sẽ thu được nội dung:

` KCSC{Lan_Dau_Tien_Trai_Thanh_Long_Co_Trong_KCSC:))}`

## Pwn - A gift for pwners

Bài ni thì đơn giản rùi chỉ cần tải file về, mỏi mắt nhìn chút là được 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/d004a080-4a27-4de8-a8f4-b4c754022850)

`KCSC{A_gift_for_the_pwners_0xdeadbeef}`

hết ạ




