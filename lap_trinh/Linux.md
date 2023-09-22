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

- `ls -a` : liệt kê các file ẩn

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

## Lệnh find, grep, phân quyền tròng Ubuntu
### Find
- **find [path] [expression]**. Ví dụ
   - Để tìm kiếm file có kiểu "txt" trong thư mục /home: `find /home -name "*.txt"`

![image](https://github.com/itravnn/kcsc_train/assets/127108265/9310926d-dccf-409e-a432-526e1d1d5584)

_`-iname` thêm i (tức là ignore) vào là bạn có thể tìm theo tên mà không phân biệt hoa thường_

  - Tìm kiếm các thư mục (-type d) có tên là src : `find / -type d -name src`

![image](https://github.com/itravnn/kcsc_train/assets/127108265/96df4d1f-4e11-42d3-b629-a0061de1dd12)

   - find / -type f : chỉ tìm file
    
- Dùng các ký tự thay thế cho một phần hoăcj toàn bộ tên cần tìm kiếm:
   - * : mọi chuỗi kể cả rỗng
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
















