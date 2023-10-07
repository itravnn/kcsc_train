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

Ở file _xuly.php_ ban đầu có giá trị **`$password = $_POST['txtPassword']`** bây giờ ta thêm hàm **md5()** để mã hóa passwd, giá trị lúc này thành **`$password   = md5($_POST['txtPassword'])`**. Khi đó, nếu ta nhập **passwd=1** thì giá trị passwd được lưu tại bảng CSDL sẽ được mã hóa thành **c4ca4238a0b923820dcc509a6f75849b**.  

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
### 3. Sử dụng tường lửa










