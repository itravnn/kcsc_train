### 1. Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data

![image](https://github.com/itravnn/kcsc_train/assets/127108265/d7b15679-86c6-4ebb-b9f4-cc5258becae9)

Truy cập vào lab, giao diện như hình dưới

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0e8b9513-e131-40e7-a3ba-755eacee049c)

Sau đó thử nhấp vào từng option thì để ý thấy trên thanh URL, giá trị sau tham số `category` thay đổi

![image](https://github.com/itravnn/kcsc_train/assets/127108265/8e490a00-1c0b-4c0b-8ecc-900fdeedb636)

![image](https://github.com/itravnn/kcsc_train/assets/127108265/91f4f6fa-b35c-4399-8fbe-227dbb697c27)

thêm dấu **`'`** vào sau thì thấy trang web trả về thông báo lỗi, so có thể thực hiện tấn công sql

![image](https://github.com/itravnn/kcsc_train/assets/127108265/ab6a9c3c-06b0-4727-9d42-0fcc60bea1dc)

thêm **`' or 1=1--`** vào sau tham số `category` thì câu truy vấn sql lúc này thành `SELECT * FROM products WHERE category = 'Accessories' or 1=1 --`, do 1=1 luôn đúng nên web trả về lúc này sẽ bao gồm tất cả sản phẩm kể cả sản phẩm bị ẩn

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b28f0001-5997-4a40-a07e-374a073f00e2)

### 2. Lab: SQL injection vulnerability allowing login bypass

![image](https://github.com/itravnn/kcsc_train/assets/127108265/61dfcbd7-8bba-413a-8197-2464eadd6f40)

Truy cập vào lab, để ý thấy tên lab _lỗ hổng sqli cho phép vượt qua đăng nhập_ nên vào phần **my account** 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/ba2b4449-348b-4051-8754-b42e5b539a6c)

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b8312a92-4e0a-4964-88d9-99c8574925b2)

tại phần login, đề chỉ cho username=administrator mà không biết passwd, để bypass thì ở phần nhập username ta nhập giá trị **`administrator' --`**, còn passwd thì tùy ý. do là sau dấu **`--`** mọi thứ đều bỏ qua nên câu truy vấn lúc này luôn đúng

![image](https://github.com/itravnn/kcsc_train/assets/127108265/9cb486a9-0ad3-4369-b649-e23468450d22)

![image](https://github.com/itravnn/kcsc_train/assets/127108265/74517782-2daa-4b56-9751-f034bddb744f)

Đăng nhập thành công, hoặc nếu không biết cả username thì có thể nhập **`' or 1=1--`**, cũng sẽ đăng nhập được vô

### 3. Lab: SQL injection UNION attack, determining the number of columns returned by the query

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


















