# Khái niệm
Kỹ thuật **Cross-Site Scripting (XSS)** được thực hiện dựa trên việc chèn các đoạn script nguy hiểm vào trong source code ứng dụng web. Nhằm thực thi các đoạn mã độc Javascript để chiếm phiên đăng nhập của người dùng.

Phân loại: **3** loại

- **Reflected XSS :** loại kịch bản khai thác này hacker sẽ gửi cho victim một URL có chứa đoạn mã nguy hiểm (thường là javascript). Khi victim request đến URL đó thì hacker sẽ nhận được respond mong muốn.
- **Stored XSS :** Lỗi này xảy ra khi ứng dụng web không kiểm tra kỹ lưỡng dữ liệu đầu vào *trước khi lưu vào CSDL*. Với kỹ thuật Stored XSS , hacker *không khai thác trực tiếp* mà phải thực hiện tối thiểu qua 2 bước.
  - Đầu tiên hacker thông qua các điểm đầu vào(form, input, textarea...) không lọc kỹ để chèn vào CSDL các đoạn mã nguy hiểm.
  - Tiếp theo, khi người dùng truy cập vào ứng dụng web và thực hiện các thao tác liên quan đến dữ liệu được lưu này,đoạn mã của hacker sẽ được thực thi trên trình duyệt người dùng. Đến đây hacker coi như đã thành công

>Khác với **Reflected XSS** là hacker phải *lừa* được nạn nhân truy cập vào URL của mình, thì **Stored XSS** không cần phải thực hiện việc này, sau khi chèn được mã nguy hiểm vào CSDL của ứng dụng, hacker chỉ việc ngồi chờ nạn nhân tự động truy cập vào.

>**Reflected XSS** và **Stored XSS** đều có đặc điểm chung là các đoạn mã nguy hiểm sau khi được chèn vào sẽ *được thực thi sau respond của server, có nghĩa là lỗi nằm về phía server.* Có một kiểu khai thác XSS khác đi ngược lại với đặc điểm này, mã độc được *thực thi ngay khi xử lý phía client mà không thông qua server*, được biết đến với cái tên **DOM Based XSS**.

- **DOM Based XSS :** là kỹ thuật khai thác XSS dựa trên việc thay đổi cấu trúc DOM của tài liệu, cụ thể là HTML. DOM Based có phần giống với Reflected hơn là Stored XSS khi phải lừa người dùng truy cập vào một URL đã nhúng mã độc. 

# Xây dựng lab
## Reflected XSS
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

<form>
  Enter your name: <input type="text" name="name"><br>
  <input type="submit" value="Submit">
</form>

<?php
if (isset($_GET['name'])) {
  echo "Xin chào, " . $_GET['name'] ;
}
?>

</body>
</html>
```

Tham số **name** được nhận từ input người dùng và sẽ trực tiếp hiển thị ra giao diện

![image](https://github.com/itravnn/kcsc_train/assets/127108265/41ae2311-7576-4ee5-8750-199a3f5960c7)

thay vì nhập tên thông thường , ta nhập input là một chuỗi javascript **`<script>alert('XSS')</script>`**

![image](https://github.com/itravnn/kcsc_train/assets/127108265/435ed591-7d3c-406e-a5d1-0da95e70c9f0)

hàm **alert()** đưa ra thông báo. Chứng tỏ web có chứa lỗ hổng XSS

## Stored XSS
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
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <form action="" method="POST">
                    Tên người: <td> <input type="text" class="input" placeholder= "" name="username"></td><br/>
                    Bình luận: <td> <input type="text" class="input" placeholder= "" name="comment"></td><br/>
                  
    <input type="submit" name="submit" value="Submit" ></br>
    </form>

    <?php
    if (isset($_POST['submit'])){
        $username   = $_POST['username'];
        $comment    = $_POST['comment'];

        if(!empty($username) && !empty($comment) ) {
        
           $sql = "INSERT INTO `xss_user` (`username`, `comment`) VALUES('$username', '$comment')";

           if($conn->query($sql)==TRUE){
            
              echo "xin chao ".$_POST['username'].". BẠn đã bình luận: ".$_POST['comment'] ;

            }else{
            echo "Lỗi {$sql}".$conn->error;
            }
         }
    else {
        echo "Bạn cần đăng nhập đầy đủ thông tin.";
    }
    }
    ?>
</body>
</html>
```
Sau khi nhập tên và phần bình luận. Dữ liệu sẽ được lưu lại trong bảng CSDL.

![image](https://github.com/itravnn/kcsc_train/assets/127108265/983d234c-62bb-4210-91c0-ce5bd84fa000)

![image](https://github.com/itravnn/kcsc_train/assets/127108265/009f0164-ef18-4940-ae41-41d56c1fdb0f)

tiếp theo, nếu ta nhập input vào là **`<script> alert("hacked") </script>`** 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/eb9f8b45-db34-4cff-9011-c3b326a11485)

có lỗ hổng xss và ở trường hợp này đoạn mã sẽ được lưu vào CSDL

![image](https://github.com/itravnn/kcsc_train/assets/127108265/9b9e7847-02a3-435c-a0ee-ff2f337c4140)








