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

### Cách ngăn chặn XSS
- Kiểm tra và lọc dữ liệu đầu vào, sử dụng các hàm như `htmlentities()`, `htmlspecialchars()` để mã hoá các ký tự đặc biệt.
- Mã hóa các dữ liệu đầu ra như password, ... bằng hàm như `base_encode()`
- CSP (Content Security Policy) : là một tính năng bảo mật web cho phép người quản trị trang web cấu hình các nguồn tài nguyên cho phép tải và sử dụng trên trang web đó. Điều này có thể giúp ngăn chặn các cuộc tấn công XSS bằng cách không cho phép tài nguyên không đáng tin cậy được tải và sử dụng trên trang web.
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

có lỗ hổng xss và ở trường hợp này đoạn mã sẽ được lưu vào CSDL, nhiều trường hợp khác, hacker sẽ gửi đoạn script độc hại hơn với nhiều mục đích như chiếm lấy cookie người dùng,... sau đó đoạn script lưu lại tịa CSDL và chỉ cần người dùng đăng nhập thì dữ liệu sẽ được gửi tới hacker mà người dùng không hề hay biết

![image](https://github.com/itravnn/kcsc_train/assets/127108265/9b9e7847-02a3-435c-a0ee-ff2f337c4140)

## DOM-based XSS
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
		Enter your search: <input type="text" name="search" id="search"><br/>
		<input type="submit" value="Submit" onclick="check_xss()">
	</form>

	<script type="text/javascript">
		function check_xss() {
		var valueSearch = document.getElementById("search").value;
        document.write("you searched :"+valueSearch);
		}
	</script> 

</body>
</html>
```
ở đây, biến `valueSearch` lấy giá trị input của `search` thông qua hàm `getElementById()`, sau đó sử dụng hàm `document.write()` để ghi nội dung. Ví dụ nhập vào 1 đoạn search bất kì, sẽ hiển thị như dưới

![image](https://github.com/itravnn/kcsc_train/assets/127108265/7f97cf86-d0ee-47e9-800e-bfe18ce7aeec)

thử nhập `<script> alert("so pretty :>") </script>` thì thấy hiện thông báo, đoạn script đã được thực hiện

![image](https://github.com/itravnn/kcsc_train/assets/127108265/89e9b71a-98ed-44c4-92cf-2c09cda9cd7b)

![image](https://github.com/itravnn/kcsc_train/assets/127108265/2aafdb17-5119-4cd2-af43-df8f23082058)





