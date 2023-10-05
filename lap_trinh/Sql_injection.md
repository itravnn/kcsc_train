## Cách khắc phục SQLi
### 1. Sử dụng các hàm trong PHP để ngăn chặn lỗ hổng SQLi
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

- Sử dụng **PDO Prepared statements**

PDO prepared statements sử dụng các câu lệnh SQL được thực thi trước đó để tránh các lỗ hổng bảo mật như SQL injection. Đồng thời nó cũng giúp tối ưu hóa các truy vấn và tăng tốc độ truy vấn. Làm việc với PDO bạn sẽ không cần phải viết các câu lệnh SQL cụ thể mà chỉ sử dụng các phương thức mà PDO cung cấp.
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
### 2. Sử dụng tường lửa










