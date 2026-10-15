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
*`nc` : dùng để gửi thông điệp tới địa chỉ nào đó

để giải quyết bài này mình dùng lệnh `nc localhost 30000` và nhập mật khẩu của vl hiện tại
<img width="701" height="189" alt="image" src="https://github.com/user-attachments/assets/e79be07b-6b8c-40a9-b5a0-b4e68b934a6e" />
pass của màn này là : pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7



