# Giới thiệu chung
- Linux là một hệ điều hành máy tính được phát triển từ năm 1991 dựa trên hệ điều hành Unix và bằng viết bằng ngôn ngữ C.
- Cấu trúc hệ điều hành:
  - Kernel: là phần quan trọng nhất, bởi chứa đựng các module hay các thư viện để quản lý, giao tiếp giữa phần cứng máy tính và các ứng dụng.

  - Shell: là phần thực thi các lệnh (command) từ người dùng hoặc từ các ứng dụng yêu cầu, chuyển đến cho Kernel xử lý. Shell chính là cầu nối để kết nối Kernel và Application, phiên dịch các lệnh từ Application gửi đến Kernel để thực thi.

     Có các loại Shell như sau: sh (the Bourne Shell), bash(Bourne-again shell), csh (C shell), ash (Almquist shell), tsh (TENEX C shell), zsh (Z shell).
  - Application: là ứng dụng người dùng, phần để người dùng cài ứng dụng, chạy ứng dụng phục vụ yêu cầu của mình.
- Trong linux, hệ thống file được tổ chức theo dạng cây
# Các thao tác cơ bản
## Tìm hiểu về các lệnh thường dùng
`pwd` sẽ in ra đường dẫn thư mục hiện tại đang ở

![image](https://github.com/itravnn/kcsc_train/assets/127108265/c93a9e65-1050-4300-b4c1-8f3e8ad814e7)

`cd` chuyển hướng trong hệ thống tập tin

![image](https://github.com/itravnn/kcsc_train/assets/127108265/b8752414-eeda-48c0-9e2d-4dbeb9b662a6)

các options:

    `cd ..` : di chuyển lên 1 cấp thư mục trên

    `cd`    : di chuyển đến thư mục home

    `cd /`  : di chuyển đến thư mục root

    `cd -`  : di chuyển đến thư mục bạn ở trước đó

`ls` xem nội dung của thư mục

![image](https://github.com/itravnn/kcsc_train/assets/127108265/12fe283c-f930-4ee9-94a4-f5ffde8c5063)

các options:
    
    `ls -R` : liệt kê các file và thư mục con bên trong

    `ls -a` : liệt kê các file ẩn

    `ls -l` : hiển thị thông tin chi tiết của các file

Để xem thông tin về hệ thống, ta có thể sử dụng các lệnh sau:

`uname -m` để xem kiến trúc phần cứng của hệ thống 

![image](https://github.com/itravnn/kcsc_train/assets/127108265/43f18a9a-14c7-4d4a-a5f8-29f7c8d0db23)

Đầu ra  ![image](https://github.com/itravnn/kcsc_train/assets/127108265/f9a09b02-7eff-4244-bedf-e1d4c1982329) cho biết bạn đang sử dụng kiến trúc 64bit. Đầu ra `i686` sẽ là hệ thống 32bit

`uname -o` cho biết tên hệ hiều hành đang sử dụng

![image](https://github.com/itravnn/kcsc_train/assets/127108265/e713d9f5-69dd-49bd-b4c9-d992feebce0d)

`lshw` để xem thông tin phần cứng quan trọng như bộ nhớ, CPU, ổ cứng ....

LƯU Ý là lệnh trên chạy được với tư cách là superuser, ta sử dụng lệnh `sudo` để cho biết là máy chủ, sau đó hệ thống sẽ hỏi passwd để xác minh

![image](https://github.com/itravnn/kcsc_train/assets/127108265/179ee4d9-9ee4-4c6f-a9d7-fb8dd06aa1e2)

Có thể dùng lệnh `lswh -short` để tóm ngắn gọn thông tin

![image](https://github.com/itravnn/kcsc_train/assets/127108265/a93e09ff-6057-4b0d-b928-68d7bc06236d)

Để xem thông tin chi tiết CPU, dùng lệnh `lscpu`

![image](https://github.com/itravnn/kcsc_train/assets/127108265/0bc4249a-42ed-4c83-b9af-9e73f1357977)




