## Web - Pokemon Hof Panel Level 1

Vào link thì web có giao diện như dưới, có phần để nhập tên và chọn nhân vật 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/4fcbf529-53df-4359-9ec8-1aac2def8a31)

Em nhập thử linh tinh vô coi, umm thì không được gì cả. Rồi em xem hint thì ommmm em cũng hiểu cho lắm :<

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

## Web - Apply To KCSC

hmm bài ni hôm sau khi mà đọc wu giải thì mình mới làm ra (làm rồi mới thấy nó giống với bài rootme đã từng làm :<)

vào trang thì là dạng upload file, thử up 1 file php, hmm 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/1ada8bd7-4f05-483e-9bbb-521f400277b1)

rồi đó, mình ngồi suốt chỉ để loay hoay với mấy cách như kiểu thêm đuôi, null byte mà up lên thành công nhưng không xem được file, sầu thiệt

rồi sai khi đọc wu thì mình mới nghĩ sao lúc đấy không nghĩ đến đẩy lên burp để thây đổi tên file, aaaaaaaaaaaa

vậy rồi sau khi dùng burp bwats request gửi lên, mình sẽ thay đổi duôi file thành **.php**, vì có vể như web chỉ cần xác nhận đúng định dạng file gửi là ok

![Screenshot 2023-12-18 213601](https://github.com/itravnn/kcsc_train/assets/127108265/eb1112cd-3d36-499f-a9ea-5deb4c6a2556)

sau khi đã upload thành công, ta chỉ việc ls để xem thư mục hiện có, đến `ls ../../../../` thì thấy có thư mục flag

![Screenshot 2023-12-18 214645](https://github.com/itravnn/kcsc_train/assets/127108265/3d2fd474-7a96-4268-b5cc-f200b42ba961)

dùng lệnh cat để đọc nội dung `cat ../../../../flag`

`KCSC{W3lc0m3_T0_KCSC_2023____}`



## Pwn - A gift for pwners

Bài ni thì đơn giản rùi chỉ cần tải file về, mỏi mắt nhìn chút là được 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/d004a080-4a27-4de8-a8f4-b4c754022850)

`KCSC{A_gift_for_the_pwners_0xdeadbeef}`

hết ạ




