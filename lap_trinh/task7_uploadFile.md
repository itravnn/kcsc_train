## Code chức năng upload file bằng php

Phần client-side
```
       <form method="post" enctype="multipart/form-data">
                
            <h3>Upload file : </h3>
                
            <input type="file" id="txtFile" name="txtFile" /> <br>

            <input type="submit" value="Upload now" name="btnSubmit" />

        </form>
```

Phần xử lý upload 

```
<?php
              
    if(isset($_POST["btnSubmit"])) {
    $target_dir = './uploads/';                // lưu file vào thư mục uploads
    $file_name = $_FILES["txtFile"]["name"];   //lấy tên của file
    $target_file   = $target_dir . $file_name; // vị trí lưu file trong server

    // kiểm tra file đã tồn tại hay chưa
    if(file_exists($target_file)){
        echo "File đã tồn tại !!!";
        exit();
    } 
    //kiểm tra lỗi                 
    if($_FILES["txtFile"]["error"] != 0) { 
        echo 'Có lỗi khi upload !!!';
    } elseif($_FILES["txtFile"]["size"] > 1000000){
        echo "Lỗi kích thước quá lớn !!!";
      } else {
            //tải file lên server
            move_uploaded_file($_FILES["txtFile"]["tmp_name"], $target_file);
            echo "<br>"."File " . $file_name . " đã được upload lên server!"."<br>";
            echo "<a href = 'http://localhost/task4/upload_file/uploads/" . $file_name . "'>here</a>";    
          }
    }
?>
```

![image](https://github.com/itravnn/kcsc_train/assets/127108265/bc853e69-ea22-4f34-b3fb-0e74c4fbd82e)

## Debug phân tích thành phần request gửi lên

![image](https://github.com/itravnn/kcsc_train/assets/127108265/d8073745-650e-4ce1-aa06-ee4422efec0a)

>Màu đỏ là phần biến cục bộ (Locals): là biến được khai báo bên trong hàm và chỉ được truy cập bên trong hàm đó

>Màu xanh là biến siêu toàn cầu (Superglobals): là biến mà chũng ta có thể truy cập bất kể phạm vi, và có thể truy cập chúng từ bất kỳ hàm, lớp hoặc tệp nào

>Màu vàng là dòng chương trình đang dừng sau khi đặt **breakpoint** và gửi request lên server

Khi breakpoint dừng tại dòng 15, tại phần biến global :

- **$_POST** được sử dụng để thu thập dữ liệu HTML Form có method = "post"
  
![image](https://github.com/itravnn/kcsc_train/assets/127108265/a6ded67e-ecf8-4e7a-8878-b7b3e864eb87)

- **$_FILE** để nhận dữ liệu từ file gửi lên

![image](https://github.com/itravnn/kcsc_train/assets/127108265/6c8057f1-9ae5-4a15-92b8-4579099fb476)

>**name**: Tên của file khi upload lên; 
**type**: Kiểu file khi upload (VD: file ảnh loại .gif, .png, .jpg,…v…v…); 
**tmp_name**: Đường dẫn tạm của file khi upload; 
**error**: Trạng thái lỗi khi upload. 0 là không có lỗi; 
**size**: Dung lượng file khi upload lên được tính bằng đơn vị bytes

- **$_REQUEST** được sử dụng để thu thập dữ liệu sau khi gửi HTML FORM

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b14a628a-2022-48fe-b13a-070c57685706)

- **$_SERVER** chứa thông tin về các tiêu đề, đường dẫn và vị trí tập lệnh.

![image](https://github.com/itravnn/kcsc_train/assets/127108265/1c682c56-640a-454f-8684-238319e2f85d)

Khi cho breakpoint chạy đến dòng 17, thì các biến bắt đầu nhận giá trị, đàu tiên là biến $target_dir được nhận giá trị 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/a8aa406b-c5d8-42b5-a130-d7d17ea36269)

Cứ vậy cho breakpoint chạy đến hết dòng 18 thì các biến được nhận hết giá trị

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b65023a0-3731-4217-89c9-468debbe2f6f)

## Filter và bypass filter file upload

### Một số filter để ngăn chặn khả năng tải lên mã độc khi upload file như:

- Client side filters
- Content/type Vertification
- The extension Black listing
- The extension White listing

### Khai thác lỗ hổng

### 1. Client side filters

Client Side Filters là một kiểu xác thực các request khi được gửi lên server. Dưới đây là một cách để bypass qua filter này, đó là giả mạo yêu cầu gửi lên

Ví dụ có một trang web *chỉ* đăng tải ảnh, khi muốn tải file **hack.php** : 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b6e5c599-5146-4465-8608-9d1d660f7e7a)

Trước tiên cần đổi lại extension của file thành **hack.php.jpg** để đánh lừa rằng ta đang để đúng định dạng là một file ảnh

![image](https://github.com/itravnn/kcsc_train/assets/127108265/abaf2ad7-4acf-4d84-9b00-89bc185b060d)

Sau đó sử dụng burp suite để chặn lại request gửi đến server, sau đó lại đổi tên file thành **hack.php** rồi send

![image](https://github.com/itravnn/kcsc_train/assets/127108265/ced41500-03ed-4f96-880e-385fbe0b9e45)

Kết quả thu được rằng đã upload thành công file

![image](https://github.com/itravnn/kcsc_train/assets/127108265/3d0feaa5-46cd-4866-8a27-cc2a3317315e)

### 2. Content/type Vertification

Đây là kiểu xác thực mà nhà phát triển yêu cầu file upload trong trường hợp này **bắt buộc** phải là kiểu image thì mới được chấp thuận. Tuy nhiên, Content/type lại có thể thay đổi trước khi đến server cho nên chúng ta chỉ cần đổi từ type ***application/octet-stream** sang image/(kiểu định dang ảnh của bạn) ví dụ như là image/png

![image](https://github.com/itravnn/kcsc_train/assets/127108265/4fa74d22-9411-4b40-b1bb-8a8bdf99a422)

### 3. The extension Black listing

Black list tức là 1 danh sách đen các shell bị các nhà phát triển web chặn nhằm chống việc tải shell lên trang web.

Ví dụ một trang web lọc các file php không cho tải lên server

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b1331331-6645-48c0-a158-63d1b5dac04b)

Một số cách để bypass trường hợp này như: đổi đuôi extension thành `shell.php1` ,`shell.php2` ,`shell.php3`, ... hoặc là thay đổi ký tự hoa thường:  `shell.Php1`, `shell.PHP2` , ... hoặc là sủ dụng file **.htaccess** 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b4c955a5-201f-4887-85de-5bace6df19df)


### 4. The extension White listing

Trái với black list, một số trang web lại yêu cầu bạn bắt buộc phải sử dụng những extension được liệt kê trong white list như là: .jpg ,jpeg , .gif ,...

![image](https://github.com/itravnn/kcsc_train/assets/127108265/95a0e9f2-f46f-4a9f-95ca-ea4ff903f058)

trường hợp này, chúng ta cũng bypass tương tự như ở phần bypass Content/type Vertification , bằng cách sửa đổi Content/type

### Khác

Ngoài ra còn 1 số các bypass khác như

- Null Byte Injection là một kỹ thuật khai thác trong đó sử dụng các ký tự null byte URL-encoded (ví dụ: 00%, hoặc 0x00 trong hex). Phần phía sau %00 sẽ được hiểu là giá trị null , là giá trị kết thúc của chuỗi nên tệp được tải lên với tên là shell.php thay vì shell.php%00.png

- Sử dụng Double Extension : shell.php.jpg,shell.php;.jpg,shell.php:jpg


















