# App Store Docker Templates

Kho mẫu ứng dụng Docker cho hệ sinh thái `hitechcloud`.

## Tổng quan

Dự án này lưu trữ danh sách ứng dụng và các mẫu `docker-compose.yml` dùng để triển khai nhanh nhiều dịch vụ phổ biến như CMS, cơ sở dữ liệu, công cụ DevOps, proxy, runtime và monitoring.

Nguồn dữ liệu chính nằm ở:

- `hitechcloud.json`: metadata của toàn bộ ứng dụng và phiên bản
- `stable/hitechcloud/<app>/<version>/docker-compose.yml`: mẫu triển khai theo từng ứng dụng
- `hitechcloud.json.version.txt`: phiên bản dữ liệu metadata

## Cấu trúc thư mục

```text
stable/
  hitechcloud/
    <app-key>/
      <version>/
        docker-compose.yml
```

Ví dụ:

- `stable/hitechcloud/wordpress/6.7/docker-compose.yml`
- `stable/hitechcloud/mysql/8.0/docker-compose.yml`
- `stable/hitechcloud/nginx-proxy-manager/2.12/docker-compose.yml`

## Danh sách ứng dụng hiện có

| Ứng dụng | Key | Nhóm | Phiên bản |
|---|---|---|---|
| WordPress | `wordpress` | Website / CMS | `6.7` |
| MySQL | `mysql` | Database | `5.7`, `8.0` |
| MariaDB | `mariadb` | Database | `11.4` |
| Redis | `redis` | Database | `7.4` |
| phpMyAdmin | `phpmyadmin` | Tool / Database | `5.2` |
| Nginx Proxy Manager | `nginx-proxy-manager` | Tool / Proxy | `2.12` |
| PostgreSQL | `postgresql` | Database | `17` |
| MongoDB | `mongodb` | Database | `8.0` |
| Memcached | `memcached` | Database / Cache | `1.6` |
| Node.js | `node` | Runtime | `22` |
| Gitea | `gitea` | DevOps / Git | `1.22` |
| MinIO | `minio` | Tool / Storage | `latest` |
| Portainer | `portainer` | DevOps / Docker | `2.24` |
| Uptime Kuma | `uptime-kuma` | Tool / Monitoring | `1.23` |

## Đặc điểm chung của template

Phần lớn template trong thư mục `stable/hitechcloud` có các đặc điểm sau:

- dùng Docker Compose định dạng version `3`
- hỗ trợ cấu hình qua biến môi trường
- dùng volume để lưu dữ liệu bền vững
- có `healthcheck` cho container
- kết nối vào network ngoài `tinohost-network`
- đặt `restart: unless-stopped`

## Yêu cầu trước khi sử dụng

- Đã cài Docker và Docker Compose
- Đã tạo external network `tinohost-network`
- Có sẵn file `.env` nếu muốn tùy biến port, tên container, tài khoản hoặc mật khẩu

Ví dụ tạo network:

```bash
docker network create tinohost-network
```

## Cách sử dụng một template

1. Chọn ứng dụng và phiên bản cần triển khai.
2. Mở file `docker-compose.yml` tương ứng.
3. Tạo file `.env` cùng thư mục nếu cần override biến môi trường.
4. Chạy Docker Compose để khởi động dịch vụ.

Ví dụ với WordPress:

```bash
cd stable/hitechcloud/wordpress/6.7
docker compose up -d
```

## Ví dụ cấu hình môi trường

Một số template hỗ trợ các biến như:

- `CONTAINER_NAME`
- `HOST_PORT`
- `HTTP_PORT`
- `HTTPS_PORT`
- `ADMIN_PORT`
- `MYSQL_ROOT_PASSWORD`
- `MYSQL_DATABASE`
- `MYSQL_USER`
- `MYSQL_PASSWORD`
- `DB_HOST`
- `DB_USER`
- `DB_PASSWORD`
- `DB_NAME`

Ví dụ file `.env`:

```env
CONTAINER_NAME=wordpress-app
HOST_PORT=8080
DB_HOST=mysql
DB_USER=wordpress
DB_PASSWORD=strong-password
DB_NAME=wordpress
```

## Cập nhật metadata ứng dụng

Khi thêm ứng dụng mới, nên cập nhật đồng thời:

1. `hitechcloud.json`
2. `hitechcloud.json.version.txt`
3. thư mục template tương ứng trong `stable/hitechcloud`

## Lưu ý khi đóng góp

- đặt key ứng dụng nhất quán với metadata trong `hitechcloud.json`
- mỗi phiên bản nên có thư mục riêng
- ưu tiên khai báo biến môi trường với giá trị mặc định hợp lý
- bổ sung `healthcheck` khi image hỗ trợ
- giữ cấu trúc thư mục đồng nhất để dễ tự động hóa

## Giấy phép

Dự án phân phối kèm file `LICENSE` ở thư mục gốc.

## Gợi ý mở rộng

Có thể bổ sung thêm trong tương lai:

- `README.md` riêng cho từng ứng dụng
- file `.env.example` cho từng template
- quy ước kiểm tra tính hợp lệ của `docker-compose.yml`
- changelog cho metadata và template

## Tác vụ nhanh

- Xem metadata: `hitechcloud.json`
- Xem phiên bản metadata: `hitechcloud.json.version.txt`
- Xem template ứng dụng: `stable/hitechcloud/.../docker-compose.yml`

---

Nếu cần, tôi có thể viết tiếp bản `README` song ngữ Việt - Anh hoặc README chi tiết hơn cho từng app.
