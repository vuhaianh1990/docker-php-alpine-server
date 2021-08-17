# docker-php-alpine-server
1. Các loại console docker:
- docker : Lệnh console chính. Pull, push các images và tạo các containers
- docker-compose: Lệnh console tạo các image và containers như là các service liên kết với nhau
- docker-machine: Lệnh console gồm các lệnh mục đích control máy ảo virtualbox (Dành cho windows)

2. Các thao tác cơ bản setup và chạy cornet framework thông qua docker:

- IP mạc định của container docker là 192.168.99.100 (Dành cho windows)
    docker-machine ip

- Xem danh sách các images trong máy ảo mình
    docker images

- Xem danh sách các containers trong máy ảo mình đang chạy (started)
    docker ps

- Xem danh sách các containers trong máy ảo mình đã được tạo từ images nhưng ngừng hoạt động (stop)
    docker ps -a

- Setup cornet framework thông qua docker-compose (P/s: "cd" tới thư mục chứ docker-compose.yml)
    docker-compose up

    P/s: Lưu ý khi setup để ý đường dẫn nơi chứa project đã map với máy ảo chưa? Nó đã được mount với VirtualBox và tên đường dẫn mount đã chính xác chưa? Mặc đinh:
    + /D_Drive: Tên mount với ổ D
    + /path: Đường dẫn với thư mục: WWW, vhost, certs, logs

- Start các service (container) đã được setup: (P/s: "cd" tới thư mục chứ docker-compose.yml)
    docker-compose start

- Stop các service (container) đã được setup: (P/s: "cd" tới thư mục chứ docker-compose.yml)
    docker-compose stop

- Xoá container không sử dụng
    docker rm -f <docker-id>|<docker-name>

- Xoá tất cả các containers không sử dụng
    docker rm -f $(docker ps -aq)

- Xoá image không sử dụng:
    docker rmi <image-name>

- Truy cập vào container thông qua docker
    docker exec -it (<docker-id>|<docker-name>) (bash|sh)

- Truy cập vào cotainer thông qua SSH
    ssh root@192.168.99.100 -p 22 (Dành cho windows)
    ssh root@localhost -p 22 (Dành cho MacOs)
    P/s:
        + Tuỳ trường hợp người dùng có thể thay đổi port: 2222
        + Password: root


3. Tài khoản mạc định cornet được setup thông qua docker-compose

App service (container):
- Root:
    username: root
    password: root

Database service (container):
- Root:
    username: root
    password: rootpw
- User (Thay đổi trong file docker-compose.yml):
    username: anhvu
    password: keykey90