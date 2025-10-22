# Hướng dẫn cài MongoDB bằng Podman

Tạo Volumn trên podman để lưu dữ liệu:

```bash
podman volume create colink-mongodb
```

Tạo network nếu chưa có:

```bash
podman network create colink
```

Chạy MongoDB

```bash
podman run -d --network colink \
  --name mongo8 \
  -p 27017:27017 \
  -v colink-mongodb:/data/db \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=123456 \
  mongo:8.0
```

### Huóng dẫn cấu hình network trên Window để kết nối MongoDB sau khi cài đặt thông qua mạng LAN

Chạy lệnh cấu hình (Ví dụ IP LAN của máy bạn là 10.82.119.168)

```bash
netsh interface portproxy add v4tov4 listenport=27017 listenaddress=10.82.119.168 connectport=27017 connectaddress=127.0.0.1
```

Kiểm tra cấu hình sau khi tạo

```bash
netsh interface portproxy show all
```

Xoá bỏ cấu hình

```bash
netsh interface portproxy delete v4tov4 listenport=27017 listenaddress=10.82.119.168
```
