## Các kiểu tấn công SQLi

![image](https://github.com/itravnn/kcsc_train/assets/127108265/c940dec0-6b84-432c-8ace-04d1df4a3b9e)

- **In-band SQLi**
  - **Error-based SQLi** : một kỹ thuật tấn công SQL Injection dựa vào thông báo lỗi Được trả về từ Database Server có chứa thông tin về cấu trúc của cơ sở dữ liệu.
  - **Union-based SQLi** : Là một kỹ thuật tấn công SQL Injection dựa vào sức mạnh của toán tử UNION trong ngôn ngữ SQL cho phép tổng hợp kết quả của 2 hay nhiều câu truy vấn SELECTION trong cùng 1 kết quả và được trả về như một phần của HTTP response
- **Inferential SQLi (Blind SQLi)** : kẻ tấn công sẽ cố gắng xây dựng lại cấu trúc cơ sở dữ liệu bằng việc gửi đi các payloads, dựa vào kết quả phản hồi của web application và kết quả hành vi của database server.
  - **Blind-boolean-based SQLi** : Là kĩ thuật tấn công SQL Injection dựa vào việc gửi các truy vấn tới cơ sở dữ liệu bắt buộc ứng dụng trả về các kết quả khác nhau phụ thuộc vào câu truy vấn là True hay False.
  - **Time-based-blind SQLi** : là kĩ thuật tấn công dựa vào việc gửi những câu truy vấn tới cơ sở dữ liệu và buộc cơ sở dữ liệu phải chờ một khoảng thời gian (thường tính bằng giây) trước khi phản hồi.
- **Out-of-band SQLi** : không phải dạng tấn công phổ biến, chủ yếu bởi vì nó phụ thuộc vào các tính năng được bật trên Database Server được sở dụng bởi Web Application.

## Cách khắc phục SQLi
### 1. Xử lý, kiểm tra và mã hóa dữ liệu đầu vào
_Các dữ liệu đăng nhập và mật khẩu cần được xử lý để loại bỏ các ký tự đặc biệt và mã độc._
- **`mysql_real_escape_string()`**

Hàm sẽ chuyển các ký tự  đặc biệt trong chuỗi như **`'`**, **`"`** ,**`;`**, ... thành các ký tự hợp lệ để truy vấn cơ sở dữ liệu. Hàm sẽ tự động thêm dấu **`\`** vào trước kí tự đặc biệt. Ví dụ khi đầu vào input là **`' OR 1=1 --`** , sau khi sử dụng hàm sẽ trở thành **`\' OR 1=1 --`**. Câu truy vấn lúc này sẽ trở thành **`SELECT * FROM users WHERE username = '\' OR 1=1 --`**

Cách gọi hàm: 
```
$username = mysqli_real_escape_string($conn, $_POST['username']);
$password = mysqli_real_escape_string($conn, $_POST['password']);
```
- **`addslashes()`**

Công dụng và cách hoạt động cũng tương tự như hàm **mysql_real_escape_string()**. Cách gọi hàm:
```
$username = addslashes($_POST['username']);
$password = addslashes($_POST['password']);
```
- **`htmlspecialchars()`**

Hàm ni chỉ chuyển đổi các ký tự **`&`**, **`“`**, **`‘`**, **`<`** và **`>`** thành ký tự giả, hàm cũng chỉ chuyển đổi chuỗi, nếu truyền vào một biến kiểu số hoặc mảng sẽ không hoạt động. Cách gọi hàm như sau:
```
$username = htmlspecialchars($_POST['username']);
$password = htmlspecialchars($_POST['password']);
```
OR có thể truyền thêm 2 tham số khác vào hàm 
```
$username = htmlspecialchars($_POST['username'], ENT_QUOTES, 'UTF-8');
$password = htmlspecialchars($_POST['password'], ENT_QUOTES, 'UTF-8');
```
`ENT_QUOTES` sẽ tách ra cả dấu nháy kép và đơn, và `‘UTF-8’` là mã hóa ký tự, nó sẽ giúp bảo vệ các ký tự đặc biệt trong UTF-8

>Tuy nhiên, nếu dữ liệu được lấy từ cơ sở dữ liệu, chúng ta cần sử dụng hàm **mysqli_real_escape_string()** hoặc **PDO::quote()** để loại bỏ các ký tự đặc biệt trước khi sử dụng htmlspecialchars().

_Dữ liệu đăng nhập cần được kiểm tra để đảm bảo tính hợp lệ và an toàn. Các quy tắc kiểm tra người dùng, chẳng hạn như độ dài tối thiểu và tối đa, cũng nên được áp dụng._

Ví dụ 1 email nhập vào có dạng: 'trang123@gmail.com' sẽ được lọc input đầu vào với dòng lệnh **`/ ^[\w] + @([\w]+\.) + [\w]{2,4}$ /`** để attacker không sử dụng được các ký tự đặc biệt

_Mã hóa dữ liệu đăng nhập và mật khẩu, Mã hóa có thể được thực hiện bằng cách sử dụng các thuật toán mã hóa mạnh như MD5 hoặc SHA._

Ví dụ: 

Ban đầu ta gán cho passwd có giá trị **`$password = $_POST['txtPassword']`** bây giờ ta thêm hàm **md5()** để mã hóa passwd, giá trị lúc này thành **`$password   = md5($_POST['txtPassword'])`**. Khi đó, nếu ta nhập **passwd=1** thì giá trị passwd được lưu tại bảng CSDL sẽ được mã hóa thành **c4ca4238a0b923820dcc509a6f75849b**.  

### 2. Sử dụng Prepared Statements trong PHP
Ví dụ :Sử dụng **PDO Prepared statements**

Đối với mỗi biến trong truy vấn SQL, Prepared Statements sẽ mã hóa giá trị của biến này và chèn tự động vào truy vấn SQL. Điều này đảm bảo rằng người dùng không thể chèn mã độc vào truy vấn SQL.

PDO prepared statements sử dụng các câu lệnh SQL được thực thi trước đó để tránh các lỗ hổng bảo mật như SQL injection. Đồng thời nó cũng giúp tối ưu hóa các truy vấn và tăng tốc độ truy vấn.
```
$sql = "select * from tbl_user where username = ? and password = ? ";
        
// tạo prepared statement
$stmt = mysqli_stmt_init($conn);

// hàm `mysqli_stmt_prepare($stmt,$sql)` sẽ chuyển `sql` sang lệnh `stmt`. SAu đó cho vào hàm if để kiểm tra xem có success chưa để sẵn sàng cho việc execute
if (mysqli_stmt_prepare($stmt,$sql)){

// dùng để liên kết các tham số đầu vào với câu lệnh SQL đã được biên dịch. Nó được sử dụng để tránh các lỗi bảo mật và để tránh việc phải thực hiện các chuỗi để truy vấn cơ sở dữ liệu.
mysqli_stmt_bind_param($stmt,"ss", $username, $password );

// dùng để thực thi câu lệnh SQL đã được biên dịch trước bởi hàm `mysqli_stmt_prepare()`
mysqli_stmt_execute($stmt);

$result = mysqli_stmt_get_result($stmt);
```
### 3. Tối thiểu hóa đặc quyền người dùng
Để giảm thiểu tác dộng trong 1 cuộc tấn công Sqli thì người dùng chỉ nên có 1 số đặc quyền nhất định, các đặc quyền bổ dung sẽ được cấp khi cần thiết. Một số quyền nên cấp cho người dùng :

  | Privilege | Access  |
  | :------   | :------ |
  | Read      | Yes     |
  | Write     | Yes     |
  | Update    | Yes     |
  | Delete    | Yes     |
  | DROP Table| None    |
  | Alter Table | None  |

#### Ví dụ để tạo 1 user mới và gán quyền cho user trên Ubuntu linux

- B1: tạo 1 user mới với tên **thanh** và **passwd=111**

```
mysql> CREATE USER 'thanh'@'localhost' IDENTIFIED BY '111';
```

Lúc này thanh chưa có quyền làm gì với CSDL. Do vậy ta sẽ cấp cho thanh quyền truy cập vào các thông tin cần thiết

- B2: Gán quyền

```
mysql> GRANT ALL PRIVILEGES ON * . * TO 'thanh'@'localhost';
```
Dấu **`*`** ở trên tương ứng với _cơ sở dữ liệu_ và _bảng_ mà user có thể truy cập - cụ thể là lệnh này cho phép người dùng thêm, sửa, xóa thực thi các công việc trên tất cả các bảng trong cơ sở dữ liệu

Các lệnh thường dùng để gán quyền cho user:
  | Privilege | Access  |
  | :------   | :------ |
  | ALL PRIVILEGES | Cho phép MySQL user thực hiện toàn quyền trên databases (hoặc 1 vài db được thiết lập)|
  | CREATE | Cho phép user tạo mới tables hoặc databases|
  | DROP | Cho phép xóa tables hoặc databases|
  | DELETE | Cho phép xóa bản ghi dữ liệu trong bảng tables|
  | INSERT | Cho phép thêm bản ghi mới vào bảng csdl|
  | SELECT | Cho phép sử dụng lệnh Select để tìm kiếm dữ liệu|
  | UPDATE | Cho phép cập nhật csdl|
  | GRANT OPTION | Cho phép gán hoặc xóa quyền của người dùng khác|

- B3: Cập nhật thay đổi người dùng

Để thay đổi được thực hiện thì cần run câu lệnh
```
FLUSH PRIVILEGES;
```
Để hiện thị quyền hạn của user ta có thể sử dụng lệnh:
```
SHOW GRANTS FOR 'username'@'localhost';
```
ví dụ show quyền đang có của thanh

![image](https://github.com/itravnn/kcsc_train/assets/127108265/a0bbe323-c357-4821-9b28-932469f9ded0)

Nếu cần thu hồi lại quyền của user, **hãy dùng lệnh REVOKE**:
```
REVOKE type_of_permission ON database_name.table_name FROM 'username'@'localhost';
```
Hoặc bạn cũng có thể xóa user:

```
DROP USER 'username'@'localhost';
```
#### Hoặc bạn cũng có thể thực hiện tạo, gán quyền với phpMyAdmin trên XAMPP 

tạo tài khoản

![Screenshot from 2023-10-08 22-15-09](https://github.com/itravnn/kcsc_train/assets/127108265/15b008fc-cc78-41de-a044-3a82b3e7eb60)

gắn quyền

![image](https://github.com/itravnn/kcsc_train/assets/127108265/1bb84b96-8995-47fa-af0e-0065b1b38aee)

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0c5ebf36-3808-47d0-9efb-ea3d1290a5a5)


## Áp dụng vào bài code trước

Ở file _dangky.php_ và _connect.php_ vẫn sẽ để nguyên

Tại file _xyly.php_ ta thêm hàm **mp5()** vào giá trị passwd nhập vào

![image](https://github.com/itravnn/kcsc_train/assets/127108265/99adea16-d6e3-44ca-9f3d-55374bb7c2cd)

Ở phần xử lý đăng nhập của file _dangnhap.php_ ta sẽ sử dụng Prepared Statements thay vì dùng các câu truy vấn sql

```
if (isset($_POST['dangnhap'])) {
        // Kiểm tra username hoặc password trong CSDL có trùng không
        $sql = "select * from tbl_user where username = ? and password = ? ";
        
        // tạo prepared statement
        $stmt = mysqli_stmt_init($conn);

        if (mysqli_stmt_prepare($stmt,$sql)){

            // dùng để liên kết các tham số đầu vào với câu lệnh SQL đã được biên dịch. Nó được sử dụng để tránh các lỗi bảo mật và để tránh việc phải thực hiện các chuỗi để truy vấn cơ sở dữ liệu.
            mysqli_stmt_bind_param($stmt,"ss", $username, $password );

            //  dùng để thực thi câu lệnh SQL đã được biên dịch trước bởi hàm `mysqli_stmt_prepare()`. Nó trả về TRUE nếu câu lệnh được thực thi thành công và FALSE nếu thất bại.
            mysqli_stmt_execute($stmt);

            $result = mysqli_stmt_get_result($stmt);
            $row = mysqli_fetch_array($result, MYSQLI_ASSOC); 

            if (mysqli_num_rows($result) >0){
                echo "Xin chào " .$username. ". Bạn đã đăng nhập thành công. <br/> " ;
                echo "Thông tin tài khoản <br/>";
                echo "Giới tính :{$row['sex']}  <br/> ";
                echo "Email :{$row['email']}  <br/> ";
                echo "Địa chỉ :{$row['address']}  <br/> ";
                echo "Sđt :{$row['Sđt']}  <br/> ";
                die();
                }
                else{  
                    echo "Tên đăng nhập or Mật khẩu không đúng. Vui lòng nhập lại. <a href='javascript: history.go(-1)'>Trở lại</a>";
                exit;
                }     
        } else {
            echo "SQL statement failed";
        }
```

hết roài!!!
