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
  -v mongodb_data:colink-mongodb \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=123456 \
  mongo:8.0
```