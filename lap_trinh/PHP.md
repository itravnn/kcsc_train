# Giới thiệu chung
## PHP
- PHP là một ngôn ngữ lập trình dùng để xây dựng các ứng dụng web, hay là  ngôn ngữ kịch bản vận hành mã nguồn mở, phục vụ cho các công việc ở phía server

- Một số câu lệnh trong php :

  - Câu lệnh **if else** :
```
if ($bieuthuc){
    // Những Câu Lệnh 1;
}
else{
    // Những câu lệnh 2;
}
```
- Có 2 cách gửi dữ liệu từ Client lên Server đó là dùng phương thức **GET** hoặc phương thức **POST**:

  - Phương thức **GET** là phương thức gửi dữ liệu thông qua đường dẫn URL . Server sẽ nhận đường dẫn đó và phân tích trả về kết quả. Tất cả các dữ liệu mà Client gửi lên bằng phương thức GET đều được lưu trong một biến toàn cục mà PHP tự tạo ra đó là biến $_GET

  - Phương thức **POST** sẽ gửi dữ liệu qua một cái form HTML và các giá trị sẽ được định nghĩa trong các input gồm các kiểu (textbox, password, ...) và được nhận dang thông qua tên (name) của các input đó. Tất cả các dữ liệu gửi bằng phương thức POST đều được lưu trong một biến toàn cục $_POST do PHP tự tạo ra

## MySQL
- MySQL là một hệ quản trị CSDL dùng để lưu trữ dữ liệu và nó thường được dùng kèm theo với PHP.  CSDL SQL là ngôn ngữ dùng để truy vấn dữ liệu, là cầu nối giữa lập trình viên và hệ quản trị CSDL. Cách vận hành trong MySQL :

  - B1: MySQL tạo ra bảng để lưu trữ dữ liệu, định nghĩa sự liên quan giữa các bảng đó.

  - B2: Client sẽ gửi yêu cầu 

  - B3: Ứng dụng trên server sẽ phản hồi thông tin và trả về kết quả trên máy client.

- Một số lệnh của SQL là :

  - **SELECT** <tên các thuộc tính> FROM <tên các quan hệ>
  - Lệnh **INSERT** trong MySQL được sử dụng để chèn một bản ghi đơn hoặc nhiều bản ghi vào một bảng. Cú pháp cho câu lệnh INSERT trong MySQL : 
```
INSERT INTO table
(column1, column2, ... )
VALUES
(expression1, expression2, ... ),
(expression1, expression2, ... ),
...;
```
  - lệnh thực hiện truy vấn: **mysqli_query( $connect,' các câu lệnh truy vấn ')**

- Một số hàm trong MySQL :

  - **isset()**: là hàm kiểm tra một biến có tồn tại hay không.
  - **include()** : là hàm triệu gọi file
  - **empty()** : trong php dùng để kiểm tra một biến nào đó có giá trị rỗng hoặc chưa được khởi tạo hay không
  - **mysqli_query( $connect,' các câu lệnh truy vấn ')** : hàm thực hiện truy vấn
  - **mysqli_fetch_array()** : Hàm này trả về hàng (row) ở dạng như một mảng liên hợp, một mảng số, hoặc cả hai. Hàm này trả về FALSE nếu không có hàng nào.

- Các ràng buộc SQL được sử dụng để chỉ định các quy tắc cho _dữ liệu trong bảng_. Các ràng buộc thường được sử dụng trong SQL:

  - **NOT NULL** – Đảm bảo rằng một cột không thể có giá trị NULL

  - **UNIQUE** – Đảm bảo rằng tất cả các giá trị trong một cột là khác nhau

  - **PRIMARY KEY** – Xác định duy nhất từng hàng trong bảng

  - **CHECK** – Đảm bảo rằng tất cả các giá trị trong một cột thỏa mãn một điều kiện cụ thể

  - **INDEX** – Được sử dụng để tạo và truy xuất dữ liệu từ cơ sở dữ liệu rất nhanh chóng

## Tạo một trang web có chức năng đăng ký, đăng nhập
Trước khi thực hiện cần đảm bảo rằng đã khởi động XAMPP khởi động Apache và MySQL đã nhé!

Cần tạo một thư mục trong _htdocs_ để chứa 4 file tên là dangky.php, dangnhap.php, xuly.php, connect.php
## Bước 1: tạo ra một bảng là “_tbl_user_” để chứa data gồm các cột “id, username, password, email, address, sex, sđt" 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/8624c343-5ff1-4e2f-b8b0-b5c0da24a0fb)

## Bước 2:  Tạo Form đăng ký _dangky.php_

```
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <title>Trang đăng ký</title>
    </head>
    <body>
        <h1>Trang đăng ký</h1>
        <form action="xuly.php" method="POST">      
            Tên đăng nhập : <td> <input type="text" name="txtUsername" size="50" /> </td> <br/>
            Mật khẩu      : <td> <input type="password" name="txtPassword" size="50" /> </td> <br/>
            Email         : <td><input type="text" name="txtEmail" size="50" /> </td> <br/>
            Số điện thoại : <td><input type="text" name="txtSđt" size="50" /> </td> <br/>
            Địa chi       :<td> <input type="text" name="txtAdd" size="50" /></td> <br/>
            Giới tính     :
                    <td>
                        <select name="txtSex">
                            <option value=""></option>
                            <option value="Nam">Nam</option>
                            <option value="Nu">Nữ</option>
                        </select>
                    </td><br/>
            <input type="submit" value="Đăng ký" />
            <input type="reset" value="Nhập lại" />
        </form>
    </body>
</html>
```

## Bước 3: Tạo file xử lý _xuly.php_ để ghi dữ liệu vào Database MySQL
```
<?php
include('connect.php');
$username   = ($_POST['txtUsername']);
$password   = ($_POST['txtPassword']);
$email      = ($_POST['txtEmail']);
$sex        = ($_POST['txtSex']);
$address    = $_POST['txtAdd'];
$sđt        = $_POST['txtSđt'];
if(!empty($username) && !empty($password) && !empty($email) && !empty($sex) && !empty($address) && !empty($sđt)) {
    $sql = "INSERT INTO `tbl_user` (`username`, `password`, `email`, `sex`, `address`, `sđt`) VALUES('$username', '$password', '$email', '$sex', '$address', '$sđt')";
    
    if($conn->query($sql)==TRUE){
        echo "Lưu dữ liệu thành công.";
    }else{
        echo "Lỗi {$sql}".$conn->error;
    }
}
else {
    echo "Bạn cần đăng nhập đầy đủ thông tin.";
}
?>
```
## Bước 4: Tạo file _dangnhap.php_ để xử lý đăng nhập
Phần giao diện đưuọc code 1 đoạn bằng html
```
File này sẽ có 2 phần: 1 phần để code giao diện trang đăng nhập và 1 phần là kiểm tra thông tin đăng nhập
<!DOCTYPE html>
<html>
    <head>
        <title></title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    </head>
    <body>
        <form action='' method='POST'>
            Tên đăng nhập :<td><input type='text' id="user" name='txtUsername' /></td><br/>
            Mật khẩu :<td><input type='password' id="pass" name='txtPassword' /></td><br/>
            <input type='submit' name="dangnhap" value='Đăng nhập' />
            <a href='dangky.php' title='Đăng ký'>Đăng ký</a>
        </form>
    </body>
</html>
```
Phần xử lý đăng nhập được code bằng php
```
<?php
// Khai báo sử dụng session
session_start();

// Xử lý đăng nhập
if (isset($_POST['dangnhap'])) 
{
    // kết nối với database
    include('connect.php');
    
    // lấy dữ liệu nhập vào
    $username = $_POST['txtUsername'];
    $password = $_POST['txtPassword'];

    // kiểm tra tên đăng nhập và mật khẩu đã nhập đủ chưa
    if (!$username || !$password) {
        echo "Vui lòng nhập đầy đủ tên đăng nhập và mật khẩu. <a href='javascript: history.go(-1)'>Trở lại</a>";
        exit;
        } 
    if (isset($_POST['dangnhap'])) {
        // Kiểm tra username hoặc password trong CSDL có trùng không
        $sql = "select * from tbl_user where username = '$username' and password = '$password'";  
        // Thực thi câu truy vấn
        $result = mysqli_query($conn,$sql);  
        // Nội dung của các row được gán cho biến $row
        $row = mysqli_fetch_array($result, MYSQLI_ASSOC);  
    
    // Sử dụng hàm `mysqli_num_rows()` để đếm số dòng SELECT được
    // Nếu có bất kỳ dòng dữ liệu nào SELECT được <-> Người dùng có tồn tại và đã đúng thông tin USERNAME, PASSWORD    
    if (mysqli_num_rows($result) > 0){
        echo "Xin chào " .$username. ". Bạn đã đăng nhập thành công. <br/> " ;
        echo "Thông tin tài khoản <br/>";
        echo "Giới tính :{$row['sex']}  <br/> ";
        echo "Email :{$row['email']}  <br/> ";
        echo "Địa chỉ :{$row['address']}  <br/> ";
        echo "Sđt :{$row['Sđt']}  <br/> ";
        }
    die();
        }  
        else{  
            echo "Mật khẩu không đúng. Vui lòng nhập lại. <a href='javascript: history.go(-1)'>Trở lại</a>";
        exit;
        }     
}   
?>
```
## Bước 5:Tạo file _connect.php_ để kết nối tới cơ sở dữ liệu Database
```
<?php 
$host = "localhost";
$username = "root";
$password ="";
$dbname = "user";

$conn = new mysqli($host, $username, $password, $dbname);

if($conn->connect_error){
    die("Kết nối không thành công : ". $conn->connect_error);
}
?>
```
## Kết quả
Ta có trang đăng kí

![image](https://github.com/itravnn/kcsc_train/assets/127108265/db25dfd1-764c-4a83-84e7-df86d6528294)

Trang đăng nhập

![image](https://github.com/itravnn/kcsc_train/assets/127108265/7c0ef1ba-a1ae-4b1d-be5d-c8142f56bf0e)

Sau khi đăng nhập thành công

![image](https://github.com/itravnn/kcsc_train/assets/127108265/d8439d85-95ff-499d-ba4f-8580da089d53)


