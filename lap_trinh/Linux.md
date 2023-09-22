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

![image](https://github.com/itravnn/kcsc_train/assets/127108265/c93a9e65-1050-4300-b4c1-8f3e8ad814e7)

**cd** Thay đổi vị trí thư mục hiện tại - di chuyển đến vị trí thư mục khác

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b8752414-eeda-48c0-9e2d-4dbeb9b662a6)

các options:

- `cd ..` : di chuyển lên 1 cấp thư mục trên
- `cd`    : di chuyển đến thư mục home
- `cd /`  : di chuyển đến thư mục root
- `cd -`  : di chuyển đến thư mục bạn ở trước đó
- `cd <tên thư mục con>` : di chuyển đến thư mục con bên trong thư mục hiện tại
- `cd <đường dẫn đến thư mục>` : di chuyển đến thư mục với đường dẫn cụ thể. Ví dụ **/home/itra/Documents**
  
**ls** xem nội dung của thư mục

![image](https://github.com/itravnn/kcsc_train/assets/127108265/12fe283c-f930-4ee9-94a4-f5ffde8c5063)

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

![image](https://github.com/itravnn/kcsc_train/assets/127108265/43f18a9a-14c7-4d4a-a5f8-29f7c8d0db23)

Đầu ra  ![image](https://github.com/itravnn/kcsc_train/assets/127108265/f9a09b02-7eff-4244-bedf-e1d4c1982329) cho biết bạn đang sử dụng kiến trúc 64bit. Đầu ra `i686` sẽ là hệ thống 32bit

**uname -o** cho biết tên hệ hiều hành đang sử dụng

![image](https://github.com/itravnn/kcsc_train/assets/127108265/e713d9f5-69dd-49bd-b4c9-d992feebce0d)

**lshw** để xem thông tin phần cứng quan trọng như bộ nhớ, CPU, ổ cứng ....

_LƯU Ý_ là lệnh trên chạy được với tư cách là _root_, ta sử dụng lệnh **sudo** để cho biết là máy chủ, sau đó hệ thống sẽ hỏi passwd để xác minh

![image](https://github.com/itravnn/kcsc_train/assets/127108265/179ee4d9-9ee4-4c6f-a9d7-fb8dd06aa1e2)

Có thể dùng lệnh `lswh -short` để tóm ngắn gọn thông tin CPU, bộ nhớ, các ổ dĩa, các cổng USB, card mạng…

![image](https://github.com/itravnn/kcsc_train/assets/127108265/a93e09ff-6057-4b0d-b928-68d7bc06236d)

Để xem thông tin chi tiết CPU như số core, tốc độ, dung lượng bộ nhớ cache…, dùng lệnh **lscpu**

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0bc4249a-42ed-4c83-b9af-9e73f1357977)

**free** để kiểm tra dung lượng RAM đang sử dụng và còn trống trên hệ thống

![image](https://github.com/itravnn/kcsc_train/assets/127108265/8308fb2e-dd24-4df0-b4ff-9cbbbdc10884)

các options:
- `-h`: (human-readable) hiển thị cách dễ đọc với con người
- `-g`: hiển thị đơn vị dạng GB
- `-m`: hiển thị đơn vị dạng MB

**du** hiển thị mức chiếm dụng không gian đĩa cứng ở thư mục hiện tại và các thư mục con. 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/c0bf481b-9674-4d7a-a7a6-9477bfa8d88b)

**df** hoặc **df -h** để hiện thị địa chỉ của tệp tin và dung lượng của ổ cứng

![image](https://github.com/itravnn/kcsc_train/assets/127108265/61588592-2e3e-43f7-9a35-100525b8c29d)

**top** hiển thị thông tin về hệ thống Linux của bạn, các tiến trình đang chạy và tài nguyên hệ thống, bao gồm: CPU, RAM, phân vùng Swap, và tổng số các tác vụ đang chạy.

![image](https://github.com/itravnn/kcsc_train/assets/127108265/1b1e10cd-93cd-4868-9d9b-fe6a8b7432a8)

Để liệt kê các gói đã cài đặt trên Ubuntu, có thể sử dụng lệnh `apt list --installed`. 

_Advanced Packaging Tool (apt) cung cấp tất cả các tiện ích quan trọng mà bạn cần để quản lý các gói trên hệ thống. Bạn có thể cài đặt, gỡ, xóa và dọn dẹp các gói bằng các gói công cụ này_

![image](https://github.com/itravnn/kcsc_train/assets/127108265/8c8a9d15-bc20-401a-967b-131e7ac3bcd3)

Để đếm số gói đã cài đặt của apt trong ubuntu, sử dụng lệnh `apt list --installed | wc -l`

![image](https://github.com/itravnn/kcsc_train/assets/127108265/f9d06d2e-d548-4801-9d05-a3f738689022)

Có thể sử dụng tiện ích _dpkg_ để liệt kê các gói đã cài đặt: `dpkg -l` hoặc `dpkg -list`

![image](https://github.com/itravnn/kcsc_train/assets/127108265/9e13a403-c80d-4349-897f-366bca8093c5)

_Sự khác biệt giữa `apt` và `dpkg` là: dpkg sẽ không cài dặt gói phụ thuộc, apt thì sẽ tự động kiểm tra và tải xuống các phần phụ thuộc_

**ifconfig** Hiển thị danh sách các thiết bị mạng trên máy tính. Qua đó, bạn có thể biết được địa chỉ IP hiện tại của máy

![image](https://github.com/itravnn/kcsc_train/assets/127108265/87f0472e-1f86-4eab-a3fc-aed833f4dd74)

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
  
![image](https://github.com/itravnn/kcsc_train/assets/127108265/6faed4bd-d0e8-4a89-80c1-439f485fcb6c)

Thông tin về file **/etc/passwd**

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0f56040b-7fcb-482c-80a8-96f7fee8e392)

- Các lệnh thực thi:
   - Tạo User: `useradd [option] <username>`
     các option:
     - `-c "thông tin người dùng"`
     - `-d <thư mục cá nhân>`
     - `-m` tạo thư mục cá nhân nếu chưa tồn tại
     - `-g <nhóm của người dùng>`

   Ví dụ: để tạo 1 user thì ta sử dụng quyền root là **sudo**
  
![image](https://github.com/itravnn/kcsc_train/assets/127108265/bfde0c08-5541-4734-8da1-d518c7db7cc2)

   Nhớ đặt pass cho user sau khi add

   ![image](https://github.com/itravnn/kcsc_train/assets/127108265/f880149c-3382-4f23-a6cb-73986174c573)

   Sau đó dùng lệnh đọc file **/etc/passwd** để ktra xem user đã được tạo chưa

   ![image](https://github.com/itravnn/kcsc_train/assets/127108265/8320ed4a-576d-482a-a5de-fa226dd6d90e)

   
   - Thay đổi thông tin cá nhân: `usermod [option] <username>`
     các option tương tự **useradd**

   - Xóa người dùng: `userdel [option] <username>`

   - Khóa/Mở khóa người dùng
      - `passwd -l <username>` / `passwd -u <username>`
      - `usermod -L <username>` / `usermod -U <username>`

### Group
- Về file **/etc/group**

![image](https://github.com/itravnn/kcsc_train/assets/127108265/bc4efc6b-811b-4cdd-b461-a29c87e79c5e)

_Các user có thể đọc được file này, tuy nhiên chỉ root mới thay đổi được_

Thông tin file **/etc/group**

![Screenshot from 2023-09-21 02-04-08](https://github.com/itravnn/kcsc_train/assets/127108265/a3c64cee-8089-4af1-b8f3-e68815623cdf)

- Các lệnh thực thi: cơ bản giống với user
  - tạo nhóm : ` groupadd <tên nhóm>`
  - xóa nhóm : `groupdel <tên nhóm>`
  - đổi tên nhóm : `groupmod -n <tên mới> <tên cũ>`
  - sửa gid nhóm : `groupmod -g <gid mới> <tên nhóm>`

## Lệnh find, grep, phân quyền trong Ubuntu
### Find
- **find [path] [expression]**. Ví dụ
   - Để tìm kiếm file có kiểu "txt" trong thư mục /home: `find /home -name "*.txt"`

![image](https://github.com/itravnn/kcsc_train/assets/127108265/9310926d-dccf-409e-a432-526e1d1d5584)

_`-iname` thêm i (tức là ignore) vào là bạn có thể tìm theo tên mà không phân biệt hoa thường_

  - Tìm kiếm các thư mục (-type d) có tên là src : `find / -type d -name src`

![image](https://github.com/itravnn/kcsc_train/assets/127108265/96df4d1f-4e11-42d3-b629-a0061de1dd12)

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

![image](https://github.com/itravnn/kcsc_train/assets/127108265/437c3ee0-ed0b-41d8-90f3-51fecf8f0f39)

  - Tìm file khi nhớ tên file và địa chỉ ở đâu, ta có thể sử dụng option _-r_. Giả sử tìm từ "chào" mà ta không nhớ tên file hay gì hết, ta dùng lệnh `grep -r "chào" *`

![image](https://github.com/itravnn/kcsc_train/assets/127108265/2e86196e-bea5-4fc5-90fe-c36e5ac6da87)

### Phân quyền trong Ubuntu
- Trong linux có 3 dạng đối tượng:
   - Owner : người sở hữu
   - Group owner : nhóm sở hữu
   - Other users : người khác
- Quyền hạn:
  - **Read - r - 4** : cho phép đọc nội dung
  - **Write - w - 2** : dùng để tạo, thay đổi hay xóa
  - **Execute - x - 1*** : thực thi chương trình

![image](https://github.com/itravnn/kcsc_train/assets/127108265/e6aeb53b-e76d-4a09-9674-f3cf8286300a)

_Có thể dùng lệnh **ls -l** để xem chi tiết các file, thư mục_

![image](https://github.com/itravnn/kcsc_train/assets/127108265/2df04320-b6eb-4d67-af6a-a8eaf1855b91)

   | File type | User | Group | Other | Name |
   | :-------- | :--- | :---- | :---- | :--- |
   | d (dir)   | rwx  | rwx   | r-x   | bao  |
   | - (file)  | rw-  | rw-   | r--   | chao |

- Thay đổi quyền với `chmod`
   - Phân quyền bằng số

![image](https://github.com/itravnn/kcsc_train/assets/127108265/7dc64ab6-f32d-4232-a488-9e704bf0df89)

Ví dụ: để phân quyền cho một file có tên _chao_ với quyền _rwxrw-r--_. Nó có nghĩa là user có tất cả quyền đọc, ghi, thực thi. Group có quyền đọc và ghi và other thì chỉ có quyền đọc.

user: r + w +x = 4 + 2 + 1 = 7

group: r + w = 4 + 2 = 6

other: r = 4 = 4

Vậy quyền của cả file sẽ là **764**, sau đó sử dụng lệnh sau để phân quyền: `chmod 764 chao`

![image](https://github.com/itravnn/kcsc_train/assets/127108265/d7969bcf-2b2e-4720-bc48-035ec02b3f5f)

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

![image](https://github.com/itravnn/kcsc_train/assets/127108265/089acac9-000d-41ff-b4c4-cc7f542f55f2)

Sau đó nếu ta thử chạy file trên terminal thì sẽ baó lỗi chưa được cấp quyền thực thi

![image](https://github.com/itravnn/kcsc_train/assets/127108265/5f6f403e-bc8a-47d1-b687-e0a61d907e08)

Sử dụng lệnh `chmod u+x test1.sh` để thêm quyền thực thi cho user trong file test1.sh

Sau đó ta sẽ chạy được file 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0247f5ed-35b1-448b-9bbd-c341f69cd93c)

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

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0529184a-637f-424b-a54d-d4bc7c7010d1)

![image](https://github.com/itravnn/kcsc_train/assets/127108265/74ebbb24-8cb4-43ab-ae62-0386d5047f5d)

- Lệnh read: đọc dữ liệu từ bàn phím và gắn giá trị cho biến: **read n**

![image](https://github.com/itravnn/kcsc_train/assets/127108265/1f8c539f-6ed6-48cf-acae-48de4ef07689)

![image](https://github.com/itravnn/kcsc_train/assets/127108265/e1cebb7f-714b-4407-9398-c586943be333)

### Các phép toán số học:
   - Sử dụng **expr**:

     vd ** a=`expr 23 + 3` **

     _cặp dấu nháy ngược sẽ yêu cầu thực thi lệnh ( khác với dấu nháy kép sẽ được kiểu là chuỗi )_

   - Sử dụng **let**:
   
     vd `let "a=$a+3"` || `let "a+=3"`
   
   - Sử dụng **$((...))**:

      vd `a=$((a+4))` 

Ví dụ:

![image](https://github.com/itravnn/kcsc_train/assets/127108265/6af5fca6-3213-46c5-b97b-d65a9e75ecaf)

Kết quả

![image](https://github.com/itravnn/kcsc_train/assets/127108265/bf9d8dc2-4599-439a-bc61-44b2fc5af3e9)

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
  
![image](https://github.com/itravnn/kcsc_train/assets/127108265/2ce798b3-041f-4026-9319-7bc0ca848fd4)

### Các loại vòng lặp trong Shell
#### Vòng lặp while 

Vòng lặp while cho bạn khả năng thực thi một tập hợp các lệnh lặp đi lặp lại cho tới khi một số điều kiện xảy ra. Nó thường được sử dụng khi bạn cần thao tác giá trị biến lặp đi lặp lại.

![image](https://github.com/itravnn/kcsc_train/assets/127108265/7ee8cc59-3894-4779-9e48-96cbff220161)

Ví dụ sử dụng vòng lặp while để hiển thị các số từ 0 đến 9

![image](https://github.com/itravnn/kcsc_train/assets/127108265/fcd65eb8-d1ca-4f2c-b0fe-ffa2dfa147c5)

Kết quả được in ra như sau

![image](https://github.com/itravnn/kcsc_train/assets/127108265/766d1c28-99d5-41d8-affd-1451f37b1a22)

#### Vòng lặp for

Vòng lặp for hoạt động trên các danh sách của các mục. Nó lặp đi lặp lại một tập hợp các lệnh cho mỗi mục trong một danh sách.

![image](https://github.com/itravnn/kcsc_train/assets/127108265/2b30c484-b3b6-4631-99bc-33b6cdbac1d5)

Ví dụ đơn giản mà sử dụng vòng lặp for để duyệt qua danh sách các số

![image](https://github.com/itravnn/kcsc_train/assets/127108265/681994b5-219b-4d1a-873c-37664aa31286)

Kết quả ra được là

![image](https://github.com/itravnn/kcsc_train/assets/127108265/e12392c9-78f7-4f2a-b630-78326faad3be)

#### Vòng lặp until

Vòng lặp while là hoàn hảo cho tình huống mà bạn muốn thực thi một tập hợp lệnh trong khi một số điều kiện là true.

![image](https://github.com/itravnn/kcsc_train/assets/127108265/72adc3f1-b44c-4568-953a-a277f30692e6)

Ở đây command được ước lượng. Nếu giá trị kết quả là false, thì lệnh được thực thi. Nếu command là true, thì khi đó các lệnh sẽ không được thực hiện và chương trình sẽ nhảy tới dòng lệnh sau lệnh done.

VÍ dụ sử dụng vòng lặp until để hiển thị các số từ 0 đến 9

![image](https://github.com/itravnn/kcsc_train/assets/127108265/35bb6b1b-b48a-45c6-bafc-504580c3e6f1)

Kết quả

![image](https://github.com/itravnn/kcsc_train/assets/127108265/fbb132be-def0-4567-a6b7-dbe7559326ae)

#### Vòng lặp select

Vòng lặp select cung cấp một cách dễ dàng để tạo một menu được đánh số từ đó người sử dụng có thể chọn lựa

![image](https://github.com/itravnn/kcsc_train/assets/127108265/48154a4c-d5fb-41b7-8d96-c7de267e386f)

Vòng lặp select thường được kết hợp cùng lệnh **case**

![image](https://github.com/itravnn/kcsc_train/assets/127108265/8c7a14f0-ad46-4a43-b5d6-69ad2a7f7bd2)

Ví dụ cho 1 người chọn 1 loại quả trong danh sách

![image](https://github.com/itravnn/kcsc_train/assets/127108265/a50ff8da-1a09-45ba-8bd7-b866c38f9c5c)

Kết quả hiển thị

![image](https://github.com/itravnn/kcsc_train/assets/127108265/81a11e5e-47da-4ab9-9850-4945793515b1)

### Câu điều kiện 
![image](https://github.com/itravnn/kcsc_train/assets/127108265/3001cfa8-9b28-42a3-9014-562587c87db3)

Ví dụ so sánh 2 số nhập từ bàn phím

![image](https://github.com/itravnn/kcsc_train/assets/127108265/e91b8c4c-b72f-456e-8432-1d1a32205add)

Kết quả cho ra

![image](https://github.com/itravnn/kcsc_train/assets/127108265/c295902d-2cb2-40ef-a4fd-82bd96763a42)

Ví dụ tiếp theo ta sẽ kiểm tra 1 thư mục xem có tồn tại không sau nếu có thì in ra dường dẫn nếu không thì báo lỗi

![image](https://github.com/itravnn/kcsc_train/assets/127108265/f2c0999f-9bc5-4f83-b21a-3946420dd170)

