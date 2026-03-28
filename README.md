# App Store Docker Templates

Kho template triển khai ứng dụng bằng Docker Compose cho hệ sinh thái `hitechcloud`.

> Metadata version hiện tại: `1.6.0`

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [English Summary](#english-summary)
- [Mục tiêu của repository](#mục-tiêu-của-repository)
- [Cấu trúc dữ liệu](#cấu-trúc-dữ-liệu)
- [Danh mục ứng dụng](#danh-mục-ứng-dụng)
- [Quy ước chung của template](#quy-ước-chung-của-template)
- [Yêu cầu trước khi sử dụng](#yêu-cầu-trước-khi-sử-dụng)
- [Quy trình triển khai nhanh](#quy-trình-triển-khai-nhanh)
- [Ví dụ sử dụng](#ví-dụ-sử-dụng)
- [Biến môi trường thường gặp](#biến-môi-trường-thường-gặp)
- [Cách thêm ứng dụng mới](#cách-thêm-ứng-dụng-mới)
- [Quy chuẩn đóng góp](#quy-chuẩn-đóng-góp)
- [Định hướng mở rộng](#định-hướng-mở-rộng)
- [License](#license)

## Giới thiệu

Repository này lưu trữ:

- metadata danh sách ứng dụng trong `hitechcloud.json`
- phiên bản metadata trong `hitechcloud.json.version.txt`
- các mẫu `docker-compose.yml` theo từng ứng dụng và từng phiên bản trong `stable/hitechcloud`

Mục đích chính là chuẩn hóa việc đóng gói, lưu trữ và triển khai nhanh các dịch vụ phổ biến như:

- website / CMS
- database
- runtime
- proxy
- storage
- monitoring
- công cụ DevOps

## English Summary

This repository contains Docker Compose templates and application metadata for the `hitechcloud` ecosystem.

It is designed to:

- maintain a centralized app catalog
- map each app to one or more supported versions
- store ready-to-use `docker-compose.yml` templates
- keep deployment structure consistent across services

Core files:

- `hitechcloud.json`: app metadata catalog
- `hitechcloud.json.version.txt`: metadata version
- `stable/hitechcloud/<app-key>/<version>/docker-compose.yml`: deployment template

## Mục tiêu của repository

Repository này hướng tới các mục tiêu sau:

1. **Chuẩn hóa cấu trúc template** giữa nhiều ứng dụng khác nhau.
2. **Tách metadata và template triển khai** để dễ bảo trì.
3. **Hỗ trợ nhiều phiên bản ứng dụng** trong cùng một repo.
4. **Dễ tích hợp vào hệ thống App Store / Control Panel** hoặc quy trình tự động hóa nội bộ.
5. **Giảm thời gian triển khai** nhờ các mẫu có sẵn và biến môi trường mặc định.

## Cấu trúc dữ liệu

### 1. File metadata

File `hitechcloud.json` chứa danh sách ứng dụng, phiên bản và thuộc tính đi kèm, ví dụ:

- tên hiển thị
- loại ứng dụng
- tag
- mô tả ngắn
- website / GitHub / tài liệu
- kiến trúc hỗ trợ
- mức khuyến nghị
- dung lượng RAM tối thiểu
- khả năng cập nhật chéo phiên bản

### 2. File version metadata

File `hitechcloud.json.version.txt` chứa version của bộ metadata. Hiện tại:

- `1.0.0`

### 3. Thư mục template

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

## Danh mục ứng dụng

Hiện tại repository đang có các ứng dụng sau:

| Ứng dụng | Key | Nhóm | Phiên bản | Ghi chú |
|---|---|---|---|---|
| WordPress | `wordpress` | Website / CMS | `6.7` | CMS phổ biến |
| MySQL | `mysql` | Database | `5.7`, `8.0` | CSDL quan hệ |
| MariaDB | `mariadb` | Database | `11.4` | Nhánh cộng đồng của MySQL |
| Redis | `redis` | Database / Cache | `7.4` | In-memory store |
| phpMyAdmin | `phpmyadmin` | Tool / Database | `5.2` | Quản trị MySQL qua web |
| Adminer | `adminer` | Tool / Database | `5.2` | Quản trị database nhẹ |
| pgAdmin | `pgadmin` | Tool / Database | `8.14` | Quản trị PostgreSQL qua web |
| Drupal | `drupal` | Website / CMS | `11` | CMS doanh nghiệp |
| Ghost | `ghost` | Website / CMS | `5` | Nền tảng blog hiện đại |
| Nginx Proxy Manager | `nginx-proxy-manager` | Tool / Proxy | `2.12` | Reverse proxy + SSL |
| PostgreSQL | `postgresql` | Database | `17` | CSDL quan hệ mạnh mẽ |
| MongoDB | `mongodb` | Database | `8.0` | NoSQL document database |
| Memcached | `memcached` | Database / Cache | `1.6` | Cache phân tán |
| Node.js | `node` | Runtime | `22` | JavaScript runtime |
| Python | `python` | Runtime | `3.12` | Runtime cho ứng dụng Python |
| Deno | `deno` | Runtime | `2` | Runtime JavaScript/TypeScript hiện đại |
| Gitea | `gitea` | DevOps / Git | `1.22` | Git self-hosted |
| MinIO | `minio` | Tool / Storage | `latest` | Object storage tương thích S3 |
| Portainer | `portainer` | DevOps / Docker | `2.24` | Quản trị Docker |
| Uptime Kuma | `uptime-kuma` | Tool / Monitoring | `1.23` | Giám sát dịch vụ |
| Grafana | `grafana` | Tool / Monitoring | `11.5` | Dashboard quan sát hệ thống |
| Prometheus | `prometheus` | Tool / Monitoring | `2.54` | Thu thập metrics và alerting |
| Jenkins | `jenkins` | DevOps | `2.479` | CI/CD phổ biến |
| SonarQube | `sonarqube` | DevOps / Tool | `10.8` | Phân tích chất lượng mã nguồn |
| Nextcloud | `nextcloud` | Tool / Storage | `30` | Lưu trữ và cộng tác self-hosted |
| RabbitMQ | `rabbitmq` | Database / Tool | `4.0` | Message broker phổ biến |
| Elasticsearch | `elasticsearch` | Database / Tool | `8.17` | Search engine phân tán |
| Kibana | `kibana` | Tool / Monitoring | `8.17` | Giao diện quan sát Elastic |
| Meilisearch | `meilisearch` | Database / Tool | `1.12` | Search engine nhẹ và nhanh |
| n8n | `n8n` | Tool / DevOps | `1.82` | Workflow automation |
| Mailpit | `mailpit` | Tool | `1.21` | Mail testing cho dev |
| Directus | `directus` | Tool / Website | `11.4` | Headless CMS và data platform |
| Bun | `bun` | Runtime | `1.2` | JavaScript runtime hiệu năng cao |
| Strapi | `strapi` | Website / CMS | `5` | Headless CMS phổ biến |
| NocoDB | `nocodb` | Tool / Database | `0.262` | Airtable mã nguồn mở |
| PrestaShop | `prestashop` | Website / Ecommerce | `8.2` | Nền tảng ecommerce mã nguồn mở |
| Appsmith | `appsmith` | Tool / AppHub | `1.60` | Low-code platform cho internal tools |
| File Browser | `filebrowser` | Tool / Storage / NAS | `2.31` | Quản lý file qua web |
| Syncthing | `syncthing` | Storage / NAS | `1.29` | Đồng bộ file P2P |
| Duplicati | `duplicati` | Storage / NAS | `2.0` | Backup automation |
| ClickHouse | `clickhouse` | Database / Analytics | `25.1` | Columnar analytics database |
| Typesense | `typesense` | Database / Search | `28.0` | Search engine cho ứng dụng |
| Qdrant | `qdrant` | Database / AI / Search | `1.13` | Vector database |
| Weaviate | `weaviate` | Database / AI / Search | `1.28` | AI-native vector database |
| Ollama | `ollama` | AI / LLM | `0.6` | Chạy mô hình AI cục bộ |
| Open WebUI | `open-webui` | AI / LLM / Tool | `0.6` | Web UI cho Ollama và LLM |
| Flowise | `flowise` | AI / LLM / Tool | `2.2` | Orchestration workflow cho LLM |
| AnythingLLM | `anythingllm` | AI / LLM / Tool | `1.7` | Chat với knowledge base riêng |
| Langfuse | `langfuse` | AI / LLM / Monitoring | `2.95` | Observability cho ứng dụng LLM |
| LiteLLM | `litellm` | AI / LLM / Middleware | `1.61` | Gateway thống nhất cho model provider |
| OpenHands | `openhands` | AI / LLM / DevOps | `0.28` | AI coding agent platform |
| MCP Gateway | `mcp-gateway` | MCP / Middleware | `0.1` | Gateway cho Model Context Protocol |
| Supabase Studio | `supabase` | AppHub / Database | `2025.03` | Console cho backend platform |
| Baserow | `baserow` | AppHub / Database | `1.31` | No-code database platform |
| Windmill | `windmill` | Tool / DevOps | `1.417` | Automation và internal workflows |
| Airbyte | `airbyte` | CI/CD / DevOps / Data | `1.5` | Data sync và ELT |
| Metabase | `metabase` | Analytics / Monitoring | `0.53` | BI dashboard và analytics |
| Plausible | `plausible` | Analytics / Monitoring | `3.0` | Website analytics nhẹ |
| Matomo | `matomo` | Analytics / Monitoring | `5.1` | Web analytics self-hosted |
| Listmonk | `listmonk` | Email / Tool | `4.1` | Newsletter và mailing list |
| Stalwart Mail | `stalwart-mail` | Email / System | `0.11` | Mail server self-hosted |
| Immich | `immich` | Storage / Media | `1.129` | Backup và quản lý ảnh/video self-hosted |
| PhotoPrism | `photoprism` | Storage / Media / AI | `240915` | Quản lý thư viện ảnh bằng AI |
| Jellyfin | `jellyfin` | Media / Streaming | `10.10` | Media server mã nguồn mở |
| Audiobookshelf | `audiobookshelf` | Media / Library | `2.17` | Quản lý audiobook và podcast |
| Calibre-Web | `calibre-web` | Media / Library | `0.6` | Giao diện web cho thư viện ebook |
| Vaultwarden | `vaultwarden` | Security / Tool | `1.32` | Password manager tương thích Bitwarden |
| Paperless-ngx | `paperless-ngx` | Tool / Document | `2.14` | Lưu trữ tài liệu và OCR |
| Seafile | `seafile` | Storage / Collaboration | `11.0` | Đồng bộ và chia sẻ tệp doanh nghiệp |
| Homebox | `homebox` | Tool / Home | `0.15` | Quản lý tài sản và vật dụng gia đình |
| Docmost | `docmost` | Tool / Wiki | `0.19` | Nền tảng tài liệu và knowledge base |
| Glance | `glance` | Tool / Dashboard | `0.6` | Dashboard tối giản cho self-hosting |
| Homepage | `homepage` | Tool / Dashboard | `0.10` | Cổng điều hướng dịch vụ self-hosted |
| Traefik | `traefik` | Proxy / Middleware | `3.3` | Reverse proxy cloud-native |
| Caddy | `caddy` | Proxy / Web Server | `2.9` | Web server tự động HTTPS |
| Kong | `kong` | Proxy / API Gateway | `3.9` | API gateway và traffic management |
| Keycloak | `keycloak` | Security / IAM | `26.1` | Identity và single sign-on |
| Zitadel | `zitadel` | Security / IAM | `2.66` | Quản lý danh tính và truy cập hiện đại |
| Harbor | `harbor` | DevOps / Registry | `2.12` | Private container registry doanh nghiệp |
| GitLab | `gitlab` | Git / DevOps | `17.10` | Nền tảng Git và CI/CD all-in-one |
| Appwrite | `appwrite` | AppHub / Backend | `1.8` | Backend-as-a-service mã nguồn mở |
| PocketBase | `pocketbase` | Database / Backend | `0.28` | Backend nhẹ với embedded database |
| RedisInsight | `redisinsight` | Database / Tool | `2.60` | Giao diện quản trị Redis |
| Mongo Express | `mongo-express` | Database / Tool | `1.0` | Giao diện web cho MongoDB |
| OpenSearch | `opensearch` | Database / Search | `2.19` | Search và analytics engine mã nguồn mở |
| OpenSearch Dashboards | `opensearch-dashboards` | Monitoring / Search | `2.19` | Dashboard phân tích cho OpenSearch |
| Milvus | `milvus` | Database / AI / Search | `2.5` | Vector database hiệu năng cao |
| Activepieces | `activepieces` | Tool / Automation | `0.52` | Workflow automation mã nguồn mở |
| Chatwoot | `chatwoot` | Tool / Support | `4.3` | Nền tảng customer support và live chat |
| Outline | `outline` | Tool / Wiki | `0.78` | Knowledge base cho team |
| Wiki.js | `wikijs` | Website / CMS / Wiki | `2.5` | Hệ thống wiki hiện đại |
| Invoice Ninja | `invoice-ninja` | Website / Business | `5.10` | Quản lý hóa đơn và báo giá |
| Mattermost | `mattermost` | Collaboration / Chat | `10.5` | Nền tảng chat và cộng tác cho team |
| Rocket.Chat | `rocketchat` | Collaboration / Chat | `7.5` | Team chat mã nguồn mở |
| Zulip | `zulip` | Collaboration / Chat | `10.0` | Team messaging theo luồng hội thoại |
| Jitsi | `jitsi` | Collaboration / Video | `stable` | Họp video self-hosted |
| Gitea Actions Runner | `gitea-actions-runner` | DevOps / CI | `0.2` | Runner cho Gitea Actions |
| Uptime Kuma Agent | `uptime-kuma-agent` | Monitoring / Tool | `1.0` | Node mẫu cho giám sát Kuma |
| GlitchTip | `glitchtip` | Monitoring / Error Tracking | `4.0` | Theo dõi lỗi và exception |
| SigNoz | `signoz` | Monitoring / Observability | `0.71` | Observability platform mã nguồn mở |
| PostHog | `posthog` | Analytics / Monitoring | `1.149` | Product analytics và event tracking |
| Cal.com | `calcom` | Tool / Scheduling | `5.4` | Nền tảng đặt lịch và booking |

## Quy ước chung của template

Qua các template hiện có, cấu trúc chung thường bao gồm:

- `version: "3"`
- một service chính cho ứng dụng
- `container_name` có thể override bằng biến môi trường
- `restart: unless-stopped`
- `ports` có giá trị mặc định nhưng cho phép tùy biến
- `environment` để cấu hình nhanh khi deploy
- `volumes` để lưu dữ liệu bền vững
- `healthcheck` để hỗ trợ theo dõi trạng thái container
- `networks` sử dụng external network `tinohost-network`

Điều này giúp các template có tính nhất quán cao và dễ được xử lý bởi công cụ tự động.

## Yêu cầu trước khi sử dụng

Trước khi dùng các template, nên bảo đảm:

- đã cài Docker
- đã cài Docker Compose hoặc hỗ trợ `docker compose`
- máy chủ có đủ tài nguyên theo khuyến nghị của từng ứng dụng
- đã tạo external Docker network `tinohost-network`
- đã chuẩn bị file `.env` nếu cần thay đổi thông số mặc định

Ví dụ tạo network:

```bash
docker network create tinohost-network
```

## Quy trình triển khai nhanh

Quy trình khuyến nghị:

1. Chọn ứng dụng và phiên bản cần triển khai.
2. Vào đúng thư mục template.
3. Đọc nhanh các biến môi trường trong `docker-compose.yml`.
4. Tạo file `.env` nếu cần override giá trị mặc định.
5. Chạy `docker compose up -d`.
6. Kiểm tra log và `healthcheck` sau khi container khởi động.

## Ví dụ sử dụng

### Ví dụ 1: Chạy WordPress

```bash
cd stable/hitechcloud/wordpress/6.7
docker compose up -d
```

Mẫu WordPress hiện dùng các biến quan trọng như:

- `HOST_PORT`
- `DB_HOST`
- `DB_USER`
- `DB_PASSWORD`
- `DB_NAME`

### Ví dụ 2: Chạy MySQL 8.0

```bash
cd stable/hitechcloud/mysql/8.0
docker compose up -d
```

Mẫu MySQL hỗ trợ các biến như:

- `MYSQL_ROOT_PASSWORD`
- `MYSQL_DATABASE`
- `MYSQL_USER`
- `MYSQL_PASSWORD`
- `HOST_PORT`

### Ví dụ 3: Chạy Nginx Proxy Manager

```bash
cd stable/hitechcloud/nginx-proxy-manager/2.12
docker compose up -d
```

Mẫu này cho phép cấu hình:

- `HTTP_PORT`
- `HTTPS_PORT`
- `ADMIN_PORT`
- `DISABLE_IPV6`

## Biến môi trường thường gặp

Tùy ứng dụng, một số biến phổ biến gồm:

| Biến | Ý nghĩa |
|---|---|
| `CONTAINER_NAME` | Tên container |
| `HOST_PORT` | Cổng public mặc định của service |
| `HTTP_PORT` | Cổng HTTP |
| `HTTPS_PORT` | Cổng HTTPS |
| `ADMIN_PORT` | Cổng trang quản trị |
| `DB_HOST` | Host database |
| `DB_USER` | User database |
| `DB_PASSWORD` | Mật khẩu database |
| `DB_NAME` | Tên database |
| `MYSQL_ROOT_PASSWORD` | Mật khẩu root MySQL |
| `MYSQL_DATABASE` | Database khởi tạo ban đầu |
| `MYSQL_USER` | User MySQL khởi tạo ban đầu |
| `MYSQL_PASSWORD` | Mật khẩu cho user MySQL |

Ví dụ `.env` cho WordPress:

```env
CONTAINER_NAME=wordpress-app
HOST_PORT=8080
DB_HOST=mysql
DB_USER=wordpress
DB_PASSWORD=strong-password
DB_NAME=wordpress
```

## Cách thêm ứng dụng mới

Khi bổ sung app mới vào repository, nên cập nhật đồng thời cả metadata lẫn template.

### Bước 1: Tạo thư mục template

Tạo đúng cấu trúc:

```text
stable/hitechcloud/<app-key>/<version>/docker-compose.yml
```

### Bước 2: Thêm metadata vào `hitechcloud.json`

Cần khai báo đầy đủ các trường cần thiết như:

- `name`
- `key`
- `type`
- `tags`
- `shortDescEn` / `shortDescZh`
- `Required`
- `architectures`
- `memoryRequired`
- `versions`

### Bước 3: Tăng version metadata

Cập nhật file `hitechcloud.json.version.txt` khi danh sách ứng dụng hoặc metadata thay đổi.

### Bước 4: Kiểm tra template

Nên xác nhận:

- file compose hợp lệ
- port mặc định không mâu thuẫn với ứng dụng tương tự
- volume được mount rõ ràng
- biến môi trường có default value hợp lý
- network ngoài `tinohost-network` được khai báo đúng
- `healthcheck` hoạt động nếu image hỗ trợ

## Quy chuẩn đóng góp

Để repository dễ bảo trì, nên tuân thủ các quy ước sau:

- dùng `app-key` nhất quán giữa metadata và tên thư mục
- mỗi version có thư mục riêng, không ghi đè chéo phiên bản
- ưu tiên đặt giá trị mặc định an toàn, dễ hiểu
- hạn chế hard-code thông tin nhạy cảm
- dùng tên biến môi trường rõ nghĩa
- giữ cấu trúc file đơn giản, dễ đọc
- bổ sung `healthcheck` khi khả thi
- giữ cùng external network để dễ liên kết giữa các stack

## Định hướng mở rộng

Repository có thể được hoàn thiện thêm theo các hướng sau:

- thêm `README.md` riêng cho từng app
- thêm `.env.example` cho mỗi template
- bổ sung ảnh icon cho app trong metadata
- thêm script kiểm tra tính hợp lệ của `hitechcloud.json`
- thêm bước CI để validate `docker-compose.yml`
- thêm changelog cho metadata và template
- sinh tài liệu catalog tự động từ metadata

## Tác vụ nhanh

| Nhu cầu | Vị trí |
|---|---|
| Xem metadata app | `hitechcloud.json` |
| Xem version metadata | `hitechcloud.json.version.txt` |
| Xem template compose | `stable/hitechcloud/<app-key>/<version>/docker-compose.yml` |
| Xem giấy phép | `LICENSE` |

## License

Repository đi kèm file `LICENSE` ở thư mục gốc. Hãy tham khảo nội dung file này trước khi phân phối lại hoặc tích hợp vào hệ thống khác.

---

Nếu cần bước tiếp theo, tôi có thể bổ sung thêm:

- `README` riêng cho từng ứng dụng
- `CONTRIBUTING.md`
- `.env.example` mẫu cho các app chính
- tài liệu chuẩn metadata cho `hitechcloud.json`
