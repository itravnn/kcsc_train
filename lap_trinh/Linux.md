# Giới thiệu chung
- Linux là một hệ điều hành máy tính được phát triển từ năm 1991 dựa trên hệ điều hành Unix và bằng viết bằng ngôn ngữ C.
- Cấu trúc hệ điều hành:
  - Kernel: là phần quan trọng nhất, bởi chứa đựng các module hay các thư viện để quản lý, giao tiếp giữa phần cứng máy tính và các ứng dụng.

  - Shell: là phần thực thi các lệnh (command) từ người dùng hoặc từ các ứng dụng yêu cầu, chuyển đến cho Kernel xử lý. Shell chính là cầu nối để kết nối Kernel và Application, phiên dịch các lệnh từ Application gửi đến Kernel để thực thi.

     Có các loại Shell như sau: sh (the Bourne Shell), bash(Bourne-again shell), csh (C shell), ash (Almquist shell), tsh (TENEX C shell), zsh (Z shell).
  - Application: là ứng dụng người dùng, phần để người dùng cài ứng dụng, chạy ứng dụng phục vụ yêu cầu của mình.
- Trong linux, hệ thống file được tổ chức theo dạng cây
- **Ubuntu** là một trong những phiên bản Linux phổ biến nhất. Vì vậy, hiện tại mình đang sử dụng hệ điều hành này. Ubuntu cung cấp rất nhiều các câu lệnh sử dụng trên Terminal. Để mở Terminal, sử dụng phím tắt: **Ctrl Alt T**
# Các thao tác cơ bản
## Các câu lệnh về thư mục và tập tin
**pwd** sẽ in ra đường dẫn thư mục hiện tại đang ở

![image](https://github.com/itravnn/kcsc_train/assets/127108265/1e50faa0-b96e-4c79-a60d-e0b34864aae7)


**cd** Thay đổi vị trí thư mục hiện tại - di chuyển đến vị trí thư mục khác

![Screenshot from 2023-08-30 23-39-31](https://github.com/itravnn/kcsc_train/assets/127108265/c581e86c-7092-4f0a-a790-bd5230b544f0)


các options:

- `cd ..` : di chuyển lên 1 cấp thư mục trên
- `cd`    : di chuyển đến thư mục home
- `cd /`  : di chuyển đến thư mục root
- `cd -`  : di chuyển đến thư mục bạn ở trước đó
- `cd <tên thư mục con>` : di chuyển đến thư mục con bên trong thư mục hiện tại
- `cd <đường dẫn đến thư mục>` : di chuyển đến thư mục với đường dẫn cụ thể. Ví dụ **/home/itra/Documents**
  
**ls** xem nội dung của thư mục

![Screenshot from 2023-08-30 23-50-26](https://github.com/itravnn/kcsc_train/assets/127108265/ede8c427-3ca1-4444-bcd4-e2a53e8375a4)


các options:
    
- `ls -R` : liệt kê các file và thư mục con bên trong
- `ls -a` : liệt kê các file ẩ
- `ls -l` : hiển thị thông tin chi tiết của các file

**cp** dùng để sao chép các tệp tin hay thư mục đến 1 thư mục khác
- `cp <tên tập tin> <tên thư mục>` : dùng để copy một tập tin vào một thư mục
- `cp -r <tên thư mục nguồn> <tên thư mục đích>` : dùng để copy thư mục nguồn vào thư mục đích

**mv** Dùng để di chuyển tập tin đến một thư mục mới đồng thời đổi tên tập tin đó
- `mv <tên tập tin cũ> <tên thư mục đích / tên tập tin mới>` : di chuyển một tập tin đến thư mục mới đồng thời đổi tên tập tin.
- `mv <tên tập tin cũ> <tên thư mục đích>` : di chuyển tập tin đến thư mục đích và không đổi tên.

**rm** dùng để xóa tệp tin hay thư mục
- `rm <tên tập tin>` : dùng để xoá tập tin
- `rmdỉr <tên thư mục>` : dùng để xoá một thư mục rỗng
- `rm -r <tên thư mục>` : xoá bất kỳ thư mục nào

**mkdir** để tạo thư mục mới `mkdir <tên thư mục>`

**touch** để tạo file mới `touch <tên tập tin>`

**man** hiển thị hướng dẫn các câu lệnh `man <tên câu lệnh>`

## Các câu lệnh về thông tin hệ thống
Để xem thông tin về hệ thống, ta có thể sử dụng các lệnh sau:

**uname -m** để xem kiến trúc phần cứng của hệ thống 

![Screenshot from 2023-08-31 00-09-32](https://github.com/itravnn/kcsc_train/assets/127108265/48bc8201-2c46-4d31-b578-e84cf186a507)


Đầu ra ![Screenshot from 2023-08-31 00-10-21](https://github.com/itravnn/kcsc_train/assets/127108265/3b6006ea-3b86-48fc-868c-fbbe9819f7f4)
 cho biết bạn đang sử dụng kiến trúc 64bit. Đầu ra `i686` sẽ là hệ thống 32bit

**uname -o** cho biết tên hệ hiều hành đang sử dụng

![Screenshot from 2023-08-31 00-13-21](https://github.com/itravnn/kcsc_train/assets/127108265/6b98bb19-56ff-46ac-ab51-f5d7c7a8672d)


**lshw** để xem thông tin phần cứng quan trọng như bộ nhớ, CPU, ổ cứng ....

_LƯU Ý_ là lệnh trên chạy được với tư cách là _root_, ta sử dụng lệnh **sudo** để cho biết là máy chủ, sau đó hệ thống sẽ hỏi passwd để xác minh

![Screenshot from 2023-08-31 00-22-03](https://github.com/itravnn/kcsc_train/assets/127108265/2fb6d4e4-7867-4be4-877c-fc9b867424c7)


Có thể dùng lệnh `lswh -short` để tóm ngắn gọn thông tin CPU, bộ nhớ, các ổ dĩa, các cổng USB, card mạng…

![Screenshot from 2023-08-31 00-23-40](https://github.com/itravnn/kcsc_train/assets/127108265/397ee4b4-afb3-4be8-babd-6036dd2445d7)


Để xem thông tin chi tiết CPU như số core, tốc độ, dung lượng bộ nhớ cache…, dùng lệnh **lscpu**

![Screenshot from 2023-08-31 00-26-49](https://github.com/itravnn/kcsc_train/assets/127108265/25bdf984-c11b-42cf-9d67-a787364893d1)


**free** để kiểm tra dung lượng RAM đang sử dụng và còn trống trên hệ thống

![Screenshot from 2023-09-19 21-48-12](https://github.com/itravnn/kcsc_train/assets/127108265/7764da6c-656a-43b5-97ca-2a859ca002bb)


các options:
- `-h`: (human-readable) hiển thị cách dễ đọc với con người
- `-g`: hiển thị đơn vị dạng GB
- `-m`: hiển thị đơn vị dạng MB

**du** hiển thị mức chiếm dụng không gian đĩa cứng ở thư mục hiện tại và các thư mục con. 

![Screenshot from 2023-09-20 17-05-15](https://github.com/itravnn/kcsc_train/assets/127108265/ea0a1220-c2e6-472c-a909-f1f625cc6589)


**df** hoặc **df -h** để hiện thị địa chỉ của tệp tin và dung lượng của ổ cứng

![Screenshot from 2023-09-19 21-46-43](https://github.com/itravnn/kcsc_train/assets/127108265/7110f518-247e-42a4-85fd-85df66c49f3d)


**top** hiển thị thông tin về hệ thống Linux của bạn, các tiến trình đang chạy và tài nguyên hệ thống, bao gồm: CPU, RAM, phân vùng Swap, và tổng số các tác vụ đang chạy.

![Screenshot from 2023-09-20 16-54-52](https://github.com/itravnn/kcsc_train/assets/127108265/799f2d3b-9f86-49d5-a09c-c5d8acd2bea2)


Để liệt kê các gói đã cài đặt trên Ubuntu, có thể sử dụng lệnh `apt list --installed`. 

_Advanced Packaging Tool (apt) cung cấp tất cả các tiện ích quan trọng mà bạn cần để quản lý các gói trên hệ thống. Bạn có thể cài đặt, gỡ, xóa và dọn dẹp các gói bằng các gói công cụ này_

![Screenshot from 2023-09-19 22-37-53](https://github.com/itravnn/kcsc_train/assets/127108265/b0e940c4-7bff-4729-83e8-b2c3556f4667)


Để đếm số gói đã cài đặt của apt trong ubuntu, sử dụng lệnh `apt list --installed | wc -l`

![Screenshot from 2023-09-19 22-42-40](https://github.com/itravnn/kcsc_train/assets/127108265/19a667e9-da1b-4ec4-b4ad-cca49de20951)


Có thể sử dụng tiện ích _dpkg_ để liệt kê các gói đã cài đặt: `dpkg -l` hoặc `dpkg -list`

![Screenshot from 2023-09-19 22-59-44](https://github.com/itravnn/kcsc_train/assets/127108265/ad9bf44a-2dea-492f-874a-a3e9993e0fc7)


_Sự khác biệt giữa `apt` và `dpkg` là: dpkg sẽ không cài dặt gói phụ thuộc, apt thì sẽ tự động kiểm tra và tải xuống các phần phụ thuộc_

**ifconfig** Hiển thị danh sách các thiết bị mạng trên máy tính. Qua đó, bạn có thể biết được địa chỉ IP hiện tại của máy

![Screenshot from 2023-09-20 17-09-07](https://github.com/itravnn/kcsc_train/assets/127108265/bb5243f6-be66-4166-8210-4500a1baa36e)

**adduser** Dùng để thêm một user mới cho máy: `adduser <tên user mới>`

**passwd** Dùng để thêm password cho người dùng mới: `passwd <tên user mới>`

**sudo** Nhiều câu lệnh trong Terminal cần phải có sudo phía trước. Khi dùng sudo, máy tính hiểu rằng bạn đang thực thi câu lệnh với quyền cao nhất, đó là quyền root.

Để thực thi được câu lệnh này, bạn bắt buộc phải nhập mật khẩu. Một số lệnh bắt buộc phải dùng sudo như:
- `sudo shutdown -h now`: tắt máy tính ngay lập tức
- `sudo reboot`: khởi động lại máy tính
## Tìm hiểu trình soạn thảo văn bản vi
- `vi <File_name>` tạo một file văn bản mới, mở nếu nó tồn tại
- Chia làm 2 chế độ :
   - chế độ soạn thảo văn bản (Insert Mode) : nhấn **i**
   - chế độ lệnh (Command Mode) : nhấn **ESC**
- Để thoát:
   - thoát + không lưu : **:q!**
   - thoát + lưu : **:wq!**
- Để di chuyển: ở chế độ lệnh: dùng phím mũi tên. Một số lệnh
   - **a** chèn văn bản ở sau vị trí con trỏ hiện tại
   - **o** tạo một dòng mới để nhập vb tại vị trí con trỏ hiện tại
   - **x** xóa một ký tự dưới vị trí con trỏ hiện tại
   - **dd** xóa dòng mà con trỏ hiện tại đang ở
   - **dS** xóa vị trí con trỏ tới phần cuối cùng của dòng
   - **yy** sao chép dòng hiện tại
   - **p** dán vb sau vị trí con trỏ
Một số lệnh đọc file:
  - **cat** đọc file, hiển thị văn bản ở terminal. Ngoài ra thì **cat >** còn có thể tạo và soạn thảo văn bản ngay trên cửa sổ terminal( sau khi soạn thảo xong thì nhấn _ctrl d_ )
  - **view** xem văn bản ở chế độ chỉ đọc

## User và Group trong Ubuntu
### User
- Có 2 loại User:
   - User hệ thống: thực thi các module, script cần thiết phục vụ cho HĐH
   - User người dùng: login để sử dụng HĐH, gồm có _super user_ và _regular user_

- Về file **/etc/passwd**
  
![Screenshot from 2023-09-21 01-51-22](https://github.com/itravnn/kcsc_train/assets/127108265/744fe08d-3c46-44d3-963d-700a2573003b)


Thông tin về file **/etc/passwd**

![Screenshot from 2023-09-21 01-53-30](https://github.com/itravnn/kcsc_train/assets/127108265/83a50e5e-79f5-48d4-b378-58e62851893e)


- Các lệnh thực thi:
   - Tạo User: `useradd [option] <username>`
     các option:
     - `-c "thông tin người dùng"`
     - `-d <thư mục cá nhân>`
     - `-m` tạo thư mục cá nhân nếu chưa tồn tại
     - `-g <nhóm của người dùng>`

   Ví dụ: để tạo 1 user thì ta sử dụng quyền root là **sudo**
  
![Screenshot from 2023-09-21 02-25-21](https://github.com/itravnn/kcsc_train/assets/127108265/39bbe0c2-ef55-4f62-a122-ebbcf7faa9c9)


   Nhớ đặt pass cho user sau khi add

 ![Screenshot from 2023-09-21 02-33-26](https://github.com/itravnn/kcsc_train/assets/127108265/c9bcd5eb-1e77-44e9-98d6-b814c36c7341)

   Sau đó dùng lệnh đọc file **/etc/passwd** để ktra xem user đã được tạo chưa

 ![Screenshot from 2023-09-21 02-30-42](https://github.com/itravnn/kcsc_train/assets/127108265/bf6627ad-9844-433e-959a-e5ff39bd0aee)


   
   - Thay đổi thông tin cá nhân: `usermod [option] <username>`
     các option tương tự **useradd**

   - Xóa người dùng: `userdel [option] <username>`

   - Khóa/Mở khóa người dùng
      - `passwd -l <username>` / `passwd -u <username>`
      - `usermod -L <username>` / `usermod -U <username>`

### Group
- Về file **/etc/group**

![Screenshot from 2023-09-21 02-03-06](https://github.com/itravnn/kcsc_train/assets/127108265/dac4fe40-23e2-408d-a2d1-368e5ad4697a)


_Các user có thể đọc được file này, tuy nhiên chỉ root mới thay đổi được_

Thông tin file **/etc/group**

![Screenshot from 2023-09-21 02-04-08](https://github.com/itravnn/kcsc_train/assets/127108265/5a71a268-1413-40c3-bd3a-2fc7be8c0852)

- Các lệnh thực thi: cơ bản giống với user
  - tạo nhóm : ` groupadd <tên nhóm>`
  - xóa nhóm : `groupdel <tên nhóm>`
  - đổi tên nhóm : `groupmod -n <tên mới> <tên cũ>`
  - sửa gid nhóm : `groupmod -g <gid mới> <tên nhóm>`

## Lệnh find, grep, phân quyền trong Ubuntu
### Find
- **find [path] [expression]**. Ví dụ
   - Để tìm kiếm file có kiểu "txt" trong thư mục /home: `find /home -name "*.txt"`

![Screenshot from 2023-09-21 23-42-56](https://github.com/itravnn/kcsc_train/assets/127108265/714e2856-efaa-4593-81ae-859960b6eba4)


_`-iname` thêm i (tức là ignore) vào là bạn có thể tìm theo tên mà không phân biệt hoa thường_

  - Tìm kiếm các thư mục (-type d) có tên là src : `find / -type d -name src`

![Screenshot from 2023-09-21 23-46-26](https://github.com/itravnn/kcsc_train/assets/127108265/f4086336-911d-4960-984c-01c7a648d8fe)


   - **find / -type f** : chỉ tìm file
    
- Dùng các ký tự thay thế cho một phần hoăcj toàn bộ tên cần tìm kiếm:
   - *: mọi chuỗi kể cả rỗng
   - ? : một ký tự bất kỳ
   - \ : loại bỏ ý nghĩa đặc biệt của các ký tự *, ?, vv
### Grep
- Tìm kiếm nội dung. Cú pháp: `grep [option] "nội dung" ten_file`. Các option:
   - -i : không phân biệt chữ hoa thường
   - -n : kèm theo số thứ tự dòng khi xuất
   - -r : tìm lặp trong thư mục con
   - -w : tìm nguyên từ
- Ví dụ:
  - Tìm những dòng có từ "chào" trong file xin.txt
![Screenshot from 2023-09-22 00-19-22](https://github.com/itravnn/kcsc_train/assets/127108265/02f2f7de-8717-43ed-aa88-04b085d8e34d)

  - Tìm file khi nhớ tên file và địa chỉ ở đâu, ta có thể sử dụng option _-r_. Giả sử tìm từ "chào" mà ta không nhớ tên file hay gì hết, ta dùng lệnh `grep -r "chào" *`

![Screenshot from 2023-09-22 00-25-15](https://github.com/itravnn/kcsc_train/assets/127108265/ceeb1510-eedb-4762-996d-a8d38b46ebe2)

### Phân quyền trong Ubuntu
- Trong linux có 3 dạng đối tượng:
   - Owner : người sở hữu
   - Group owner : nhóm sở hữu
   - Other users : người khác
- Quyền hạn:
  - **Read - r - 4** : cho phép đọc nội dung
  - **Write - w - 2** : dùng để tạo, thay đổi hay xóa
  - **Execute - x - 1*** : thực thi chương trình

![Screenshot from 2023-09-22 00-37-23](https://github.com/itravnn/kcsc_train/assets/127108265/219e059d-a518-4e41-8b9c-8d6cc9e9ab57)

_Có thể dùng lệnh **ls -l** để xem chi tiết các file, thư mục_

![Screenshot from 2023-09-22 00-43-18](https://github.com/itravnn/kcsc_train/assets/127108265/00bb1bce-498f-4b95-9e27-a7397cc90c2d)

   | File type | User | Group | Other | Name |
   | :-------- | :--- | :---- | :---- | :--- |
   | d (dir)   | rwx  | rwx   | r-x   | bao  |
   | - (file)  | rw-  | rw-   | r--   | chao |

- Thay đổi quyền với `chmod`
   - Phân quyền bằng số

![Screenshot from 2023-09-22 00-39-15](https://github.com/itravnn/kcsc_train/assets/127108265/52d2b3ba-4934-4091-8870-ae216df967db)

Ví dụ: để phân quyền cho một file có tên _chao_ với quyền _rwxrw-r--_. Nó có nghĩa là user có tất cả quyền đọc, ghi, thực thi. Group có quyền đọc và ghi và other thì chỉ có quyền đọc.

user: r + w +x = 4 + 2 + 1 = 7

group: r + w = 4 + 2 = 6

other: r = 4 = 4

Vậy quyền của cả file sẽ là **764**, sau đó sử dụng lệnh sau để phân quyền: `chmod 764 chao`

![Screenshot from 2023-09-22 00-59-00](https://github.com/itravnn/kcsc_train/assets/127108265/6f66facf-c328-46f3-9ced-b7c3f9a75da3)


  - Ngoài ra cũng có thể tham khảo thêm câu lệnh `chmod u=rwx,g=rw,o=r <filename>`

  | Ký hiệu | Ý nghĩa |
  | :------ | :------ |
  | u       | user    |
  | g       | group   |
  | o       | other   |
  | a       | tất cả  |

## Lập trình Shell script trong Ubuntu
### Thực thi file
- Cấp quyền thực thi: `chmod u+x ten_file`
- Chạy chương trình: **./ten_file** hoặc **/bin/sh ten_file.sh**
Ví dụ: Soạn 1 chương trình trên text editor, cho ra 1 đoạn echo. Lưu chương trình trong thư mục text với tên test1.sh

![Screenshot from 2023-09-22 22-59-36](https://github.com/itravnn/kcsc_train/assets/127108265/8fe79315-f348-4978-9199-1dbe3019636c)

Sau đó nếu ta thử chạy file trên terminal thì sẽ baó lỗi chưa được cấp quyền thực thi

![Screenshot from 2023-09-22 23-00-54](https://github.com/itravnn/kcsc_train/assets/127108265/39a40645-ac13-41dc-a0d3-ff48fb1ac8ca)

Sử dụng lệnh `chmod u+x test1.sh` để thêm quyền thực thi cho user trong file test1.sh

Sau đó ta sẽ chạy được file 

![Screenshot from 2023-09-22 23-04-34](https://github.com/itravnn/kcsc_train/assets/127108265/eaaa9311-b6f4-41a3-9af7-a29c46c3ddab)

### Biến
- Gồm 2 loại:
   - Biến hệ thống: được tạo ra và quản lí bởi linux, được viết bằng chữ in hoa (BASH, HOME, PATH...)
   - Biến do người dùng định nghĩa: được tạo và quản lý bởi người dùng
- Khai báo biến: **ten_bien=gia_tri**
- Lệnh **echo**: xuất nội dung ra màn hình `echo [opion] [chuỗi/biến]`. Các opion:
   - -n: không in ký tự xuống dòng
   - -e: cho phép hiểu những ký tự theo sau dấu \ trong chuỗi
   - \a: alert(tiếng chuông)
   - \b: backspace
   - \c: không xuống dòng
   - \n: xuống dòng
   - \r: về đầu dòng
   - \t: tab
   - \\: dấu \
- Để xuất giá trị của biến( $ten_bien): **echo $ten_bien**

![Screenshot from 2023-09-22 23-24-54](https://github.com/itravnn/kcsc_train/assets/127108265/1f71f5d5-d1ca-4714-a740-1062e2ffa8d9)

Đầu ra

![Screenshot from 2023-09-22 23-25-24](https://github.com/itravnn/kcsc_train/assets/127108265/d94ee3a5-08e7-46b1-8ff0-62e00f62e1d0)

- Lệnh read: đọc dữ liệu từ bàn phím và gắn giá trị cho biến: **read n**

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b0e15082-f87b-41a4-9564-f58ff33106c5)


![Screenshot from 2023-09-22 23-28-20](https://github.com/itravnn/kcsc_train/assets/127108265/d9a28f3f-9809-4f84-a22a-8b2a8dedab53)

### Các phép toán số học:
   - Sử dụng **expr**:

     vd ** a=`expr 23 + 3` **

     _cặp dấu nháy ngược sẽ yêu cầu thực thi lệnh ( khác với dấu nháy kép sẽ được kiểu là chuỗi )_

   - Sử dụng **let**:
   
     vd `let "a=$a+3"` || `let "a+=3"`
   
   - Sử dụng **$((...))**:

      vd `a=$((a+4))` 

Ví dụ:

![Screenshot from 2023-09-22 23-51-06](https://github.com/itravnn/kcsc_train/assets/127108265/d1efc20f-ab37-4e6c-9b15-9503b218d36f)


Kết quả

![Screenshot from 2023-09-22 23-51-40](https://github.com/itravnn/kcsc_train/assets/127108265/b72393a2-192f-4bdd-a272-a478b90f9f0d)


### So sánh chuỗi:

| So sánh    | Kết quả      |
| :----------| :------------|
| str1 = str2| True nếu 2 chuỗi bằng nhau ( chính xác từng ký tự) |
| str1 != str2 | True nếu 2 chuỗi không bằng nhau |
| -n str1 | True nếu str1 không rỗng |
| -z str1 | True nếu str1 rỗng ( chuỗi NULL ) |

### Các phép toán tử so sánh số học:
   - **-eq** : bằng
   - **-ge** : lớn hơn hoặc bằng
   - **-gt** : lớn hơn
   - **-le** : nhỏ hơn hoặc bằng
   - **-lt** : nhỏ hơn
   - **-ne** : khác
### Kiểm tra điều kiện tập tin:
  
![Screenshot from 2023-09-23 00-09-16](https://github.com/itravnn/kcsc_train/assets/127108265/d7d8d756-27b3-44b2-89b9-00a4dc7f3754)


### Các loại vòng lặp trong Shell
#### Vòng lặp while 

Vòng lặp while cho bạn khả năng thực thi một tập hợp các lệnh lặp đi lặp lại cho tới khi một số điều kiện xảy ra. Nó thường được sử dụng khi bạn cần thao tác giá trị biến lặp đi lặp lại.

![Screenshot from 2023-09-23 00-19-57](https://github.com/itravnn/kcsc_train/assets/127108265/d76bd08a-421f-4bd5-b621-647c0d42e87b)


Ví dụ sử dụng vòng lặp while để hiển thị các số từ 0 đến 9

![Screenshot from 2023-09-23 00-27-36](https://github.com/itravnn/kcsc_train/assets/127108265/d45092fd-fe60-4922-be84-b491776302e8)


Kết quả được in ra như sau

!![Screenshot from 2023-09-23 00-28-34](https://github.com/itravnn/kcsc_train/assets/127108265/278e3a02-d535-49cf-802a-dab8475383f7)

#### Vòng lặp for

Vòng lặp for hoạt động trên các danh sách của các mục. Nó lặp đi lặp lại một tập hợp các lệnh cho mỗi mục trong một danh sách.

![Screenshot from 2023-09-23 00-33-32](https://github.com/itravnn/kcsc_train/assets/127108265/935bd9db-4211-41e7-b332-74c4bbfbc293)


Ví dụ đơn giản mà sử dụng vòng lặp for để duyệt qua danh sách các số

![Screenshot from 2023-09-23 00-49-43](https://github.com/itravnn/kcsc_train/assets/127108265/551e7141-8751-4b18-93f5-173dbcf15e58)



Kết quả ra được là

![Screenshot from 2023-09-23 00-48-57](https://github.com/itravnn/kcsc_train/assets/127108265/91c259e3-8bf9-4445-b2cb-95c3f1272c30)


#### Vòng lặp until

Vòng lặp while là hoàn hảo cho tình huống mà bạn muốn thực thi một tập hợp lệnh trong khi một số điều kiện là true.

![Screenshot from 2023-09-23 00-51-26](https://github.com/itravnn/kcsc_train/assets/127108265/47f7b2a4-3e81-4597-8720-da0772b76547)


Ở đây command được ước lượng. Nếu giá trị kết quả là false, thì lệnh được thực thi. Nếu command là true, thì khi đó các lệnh sẽ không được thực hiện và chương trình sẽ nhảy tới dòng lệnh sau lệnh done.

VÍ dụ sử dụng vòng lặp until để hiển thị các số từ 0 đến 9

![Screenshot from 2023-09-23 00-56-58](https://github.com/itravnn/kcsc_train/assets/127108265/b667012b-dc0f-41f4-963f-299eb2443aa2)


Kết quả

![Screenshot from 2023-09-23 00-57-34](https://github.com/itravnn/kcsc_train/assets/127108265/62cbfa77-6fcc-45ab-99f2-b721f1770c93)

#### Vòng lặp select

Vòng lặp select cung cấp một cách dễ dàng để tạo một menu được đánh số từ đó người sử dụng có thể chọn lựa

![Screenshot from 2023-09-23 00-59-14](https://github.com/itravnn/kcsc_train/assets/127108265/7546a704-de73-43b3-9635-a31befa33040)


Vòng lặp select thường được kết hợp cùng lệnh **case**

![Screenshot from 2023-09-23 01-12-40](https://github.com/itravnn/kcsc_train/assets/127108265/84ee59f6-6871-4c63-bddf-c01a92cb2293)

Ví dụ cho 1 người chọn 1 loại quả trong danh sách

![Screenshot from 2023-09-23 01-18-56](https://github.com/itravnn/kcsc_train/assets/127108265/86b672c8-1523-4260-8331-bb2394d5b207)

Kết quả hiển thị

![Screenshot from 2023-09-23 01-19-59](https://github.com/itravnn/kcsc_train/assets/127108265/70b65b29-e01a-40f4-8a72-928c08e86307)

### Câu điều kiện 

![Screenshot from 2023-09-23 01-31-17](https://github.com/itravnn/kcsc_train/assets/127108265/5a491f7b-97a1-4e97-a76f-8ca86bcdbd18)

Ví dụ so sánh 2 số nhập từ bàn phím

![Screenshot from 2023-09-23 01-37-16](https://github.com/itravnn/kcsc_train/assets/127108265/87b41867-775f-4cdc-83f7-f9bca5c50d4f)

Kết quả cho ra

![Screenshot from 2023-09-23 01-36-52](https://github.com/itravnn/kcsc_train/assets/127108265/56c87e52-ac21-444b-9f30-370a80dfbabd)

Ví dụ tiếp theo ta sẽ kiểm tra 1 thư mục xem có tồn tại không sau nếu có thì in ra dường dẫn nếu không thì báo lỗi

![Screenshot from 2023-09-23 01-57-32](https://github.com/itravnn/kcsc_train/assets/127108265/3a6c660d-997d-4069-9ae5-32c24c1ad982)

