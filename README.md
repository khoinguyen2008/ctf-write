# ctf-write
Challenge: Bandit Level 14 -> 33
Category: Linux
Difficulty: Easy
Source: Overthewire
xin chào các bạn, đây là write up của mình đầu tiên về ctf, các thử thách về bandit chủ yếu xoay quanh về các lệnh linux cơ bản sau đây là cách mình giải quyết từ lv 14- lv 33, đây là write up đầu tiên của mình mong các bạn góp ý
## LV 13 -> 14

ở lv này mình dùng máy ảo kali để chạy các bạn có thể tham khảo máy ảo ở đây : https://viblo.asia/p/free-kali-ssh-server-hack-moi-luc-moi-noi-5pPLkjBZJRZ 
đề bài yêu cầu đăng nhập bằng ssh từ máy chủ của lv13 sang lv 14 và mật khẩu được lưu trong file  /etc/bandit_pass/bandit14 và chỉ xem được khi đăng nhập bằng private key, 
<img width="1489" height="579" alt="image" src="https://github.com/user-attachments/assets/fa82da72-ae7a-422e-a6df-4ee1206e659c" />

## solution
* `nano` : tạo một file trên sever ảo
* `ssh` : dùng để kết nối bảo mật
* `chmod` : dùng để cấp quyền cho file

để giải quyết bài này mình sẽ xem nội dung của file sshkey.private và copy nội dung đó, sau đó mình thoát ra ngoài sv chính
dùng lệnh `nano sshkey.private` và dán nội dung đó vào , tiếp theo mình sẽ cấp quyền cho file bằng lệnh `chmod 700 sshkey.private` và mình dùng lệnh `ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220` để kết nối vào bandit14

<img width="1093" height="524" alt="image" src="https://github.com/user-attachments/assets/ae2425eb-8638-4b7d-81f0-1684a3f13a29" />
<img width="1082" height="757" alt="image" src="https://github.com/user-attachments/assets/27f8fa81-7b6a-4018-8ee1-2597e1ad2a9a" />
pass của màn này là: aaWecNkG4FhxJQxz07uiwzVP6bJiYS65

## LV 14 -> 15
Ở lv này đề bài yêu cầu mình gửi mật khẩu ở lv hiện tại tới localhost 3000
<img width="1301" height="720" alt="image" src="https://github.com/user-attachments/assets/286fe719-6963-4a08-9dfc-e278cab2bba5" />

## solution
*`nc` : dùng để tạo máy chủ, gửi/nhận thông điệp qua TCP/UDP

để giải quyết bài này mình dùng lệnh `nc localhost 30000` và nhập mật khẩu của vl hiện tại
<img width="701" height="189" alt="image" src="https://github.com/user-attachments/assets/e79be07b-6b8c-40a9-b5a0-b4e68b934a6e" />
pass của màn này là : pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

## LV 15 - 16
ở lv này đề bài yêu cầu kết nối với sever localhost ở port 30001 bằng giao thức SSL/TLS và nhập mật khẩu ở lv hiện tại
<img width="1413" height="643" alt="image" src="https://github.com/user-attachments/assets/4581d759-a665-4c08-8af4-f4ce3fc31f5c" />
## solution
*`openssl` : dùng để mã hóa dữ liệu , giải mã dữ liệu , tạo và kiểm tra SSL/TLS kết nối

*`s_client`: con command openssl dùng để thiết lập kết nối sever SSL/TLS
ở lv này mình dùng câu lệnh `openssl s_client` để kết nối với localost ở port:30001
cụ thể : `openssl s_client -connect localhost:30001` sau đó nhập mật khẩu của lv hiện tại vào
<img width="1339" height="745" alt="image" src="https://github.com/user-attachments/assets/34fad7a0-b87b-47b7-8963-21c16c67f825" />
<img width="516" height="214" alt="image" src="https://github.com/user-attachments/assets/2ffe9872-eb69-4b0a-a741-ca803559a605" />

pass của màn này là : kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V

## LV 16 - 17
Level này yêu cầu ta kết nối vào localhost và 1 port nào đó nằm trong phạm vi từ 31000 đến 32000 và có SSL/TLS. Trong số các port đó, có duy nhất 1 port là cung cấp cho chúng ta thông tin về level tiếp theo, còn các port còn lại khi ta nhập password của level này thì nó sẽ in lại password đấy.
<img width="1519" height="652" alt="image" src="https://github.com/user-attachments/assets/2d4805dd-8cb1-4a4c-b751-fd91171cc032" />

## solution
*`nmap`: dùng để scan như tìm host,tìm port,..
*`ncat`: dùng để gửi dữ liệu qua TCP/UDP (hỗ trợ SSL/TLS)

mình dùng lệnh `nmap` để scan các cổng đang hoạt động , dùng option `-p 31000-32000` để scan port trong phạm vi 31000-32000 , dùng thêm option `sV` để hiển thị chi tiết hơn
<img width="1561" height="742" alt="image" src="https://github.com/user-attachments/assets/8c5d6a35-9162-4936-be48-872bb0208437" />

sau khi dùng lệnh `nmap` thì có xuất hiện 2 cổng 31518 , 31790 có SSL thì mình lần lượt thử 2 cổng bằng lệnh `ncat --ssl localhost 31790` và thấy cổng 31790 cho ra khóa RSA
<img width="1086" height="847" alt="image" src="https://github.com/user-attachments/assets/729c5b37-5307-4ac7-9688-5ba46fb86aa0" />
sau đó copy lại khóa RSA và thoát ra khỏi màn hình chính bằng lệnh `exit` sau đó dùng lệnh `nano sshkey.private` dán khóa rsa 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9f5e4312-ff65-42d9-92fb-c4e5a32764b4" />
sau đó cấp quyền bằng lệnh `chmod 700 sshkey.private` 
<img width="990" height="331" alt="image" src="https://github.com/user-attachments/assets/c5896687-0630-4188-80a4-12c0004ebbe3" />
sau đó dùng lệnh `ssh -i sshkey.private bandit17@bandit.labs.overthewire.org -p 2220` 
và cuối cùng dùng lệnh `cat /etc/bandit_pass/bandit17` để lấy pass
<img width="1818" height="957" alt="image" src="https://github.com/user-attachments/assets/f5364c74-14b9-44fa-bf30-633b8cd01e88" />

pass của màn này là : pWXMAZoxGC8JmDMfmT5MGEsobMM3vnj2
## LV 17 - 18
trong LV này cho ta hai file đó là `passwords.new` và `passwords.old` và pass của lv tiếp theo nằm ở dòng khác biệt của hai file này
<img width="1561" height="559" alt="image" src="https://github.com/user-attachments/assets/916f9f9f-7198-42da-94e9-b25255625a75" />
## solution
bài này mình dùng lệnh `diff` ( viết tắt của different trong tiếng anh) 
cụ thể `diff passwords.new passwords.old`
<img width="1389" height="222" alt="image" src="https://github.com/user-attachments/assets/d38e64b6-d7f7-4304-a383-9aa23eb2b148" />

pass của màn này là :OQxXZjELndr90zuhOTDYBEomI0SZITXI











