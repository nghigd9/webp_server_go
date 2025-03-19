# WebP Server Go

<p align="center">
	<img src="./pics/webp_server.png"/>
</p>

[![CI](https://github.com/webp-sh/webp_server_go/actions/workflows/CI.yaml/badge.svg)](https://github.com/webp-sh/webp_server_go/actions/workflows/CI.yaml)
[![build docker image](https://github.com/webp-sh/webp_server_go/actions/workflows/release_binary.yaml/badge.svg)](https://github.com/webp-sh/webp_server_go/actions/workflows/release_binary.yaml)
[![Release WebP Server Go Binaries](https://github.com/webp-sh/webp_server_go/actions/workflows/release_docker_image.yaml/badge.svg)](https://github.com/webp-sh/webp_server_go/actions/workflows/release_docker_image.yaml)
[![codecov](https://codecov.io/gh/webp-sh/webp_server_go/branch/master/graph/badge.svg?token=VR3BMZME65)](https://codecov.io/gh/webp-sh/webp_server_go)

[📖 Tài liệu](https://docs.webp.sh/) | [🌍 Trang web](https://webp.sh/)

**WebP Server Go** là một máy chủ dựa trên Golang, giúp bạn phân phối hình ảnh ở định dạng **WebP** một cách tự động.  
Máy chủ sẽ tự động chuyển đổi các tệp **JPG, JPEG, PNG** theo mặc định. Bạn có thể tùy chỉnh định dạng đầu vào bằng cách chỉnh sửa tệp `config.json`.

✅ **Hỗ trợ các định dạng ảnh**: **JPEG, PNG, BMP, GIF** *(chỉ hỗ trợ ảnh tĩnh cho GIF)*

> **Ví dụ**: Khi bạn truy cập `https://your.website/pics/tsuki.jpg`, máy chủ sẽ tự động cung cấp hình ảnh ở định dạng **WebP** mà không thay đổi URL.  
> ~~Đối với trình duyệt Safari và Opera, hình ảnh gốc sẽ được sử dụng.~~  
> Giờ đây, WebP Server đã hỗ trợ Safari, Chrome và Firefox trên iOS 14/iPadOS 14. 🎉

---

## 🛠 Hướng dẫn sử dụng đơn giản (với Binary)

### 1️⃣ Chuẩn bị môi trường

Nếu bạn muốn chạy **WebP Server Go** trực tiếp trên máy của mình, cần cài đặt một số thư viện phụ thuộc (cần thiết để hỗ trợ AVIF):

#### 🔹 Đối với Ubuntu:
```bash
apt install libaom-dev -y
ln -s /usr/lib/x86_64-linux-gnu/libaom.so /usr/lib/x86_64-linux-gnu/libaom.so.3
```

#### 🔹 Đối với CentOS 7:
```bash
yum install libaom-devel -y
```

> ❗ Nếu bạn không muốn cài đặt trực tiếp trên hệ thống, hãy thử chạy bằng **Docker** để dễ dàng hơn.  
👉 [Hướng dẫn sử dụng Docker](https://docs.webp.sh/usage/docker/)

---

### 2️⃣ Tải về WebP Server Go
Tải **binary** mới nhất từ trang **[releases](https://github.com/webp-sh/webp_server_go/releases)**.

---

### 3️⃣ Tạo tệp cấu hình (`config.json`)

```bash
./webp-server -dump-config > config.json
```

Mặc định, tệp `config.json` sẽ có nội dung như sau:
```json
{
  "HOST": "127.0.0.1",
  "PORT": "3333",
  "QUALITY": "80",
  "IMG_PATH": "/path/to/pics",
  "EXHAUST_PATH": "/path/to/exhaust",
  "ALLOWED_TYPES": ["jpg", "png", "jpeg", "bmp"],
  "ENABLE_AVIF": false
}
```
> 🔴 **Lưu ý:** Hỗ trợ **AVIF** bị tắt theo mặc định vì chuyển đổi sang AVIF tiêu tốn nhiều tài nguyên CPU.

#### 📝 Ví dụ cấu hình:

Giả sử bạn có ảnh được lưu tại **`/var/www/img.webp.sh/path/tsuki.jpg`**,  
và ảnh này được cung cấp trên trang web tại **`https://img.webp.sh/path/tsuki.jpg`**.

| Đường dẫn ảnh trên máy chủ | Đường dẫn ảnh trên website |
| ------------------------- | ------------------------- |
| `/var/www/img.webp.sh/path/tsuki.jpg` | `https://img.webp.sh/path/tsuki.jpg` |

Khi đó, trong `config.json`, thiết lập:

```json
"IMG_PATH": "/var/www/img.webp.sh"
```

`EXHAUST_PATH` là thư mục lưu ảnh **WebP** đã được chuyển đổi. Ví dụ, nếu bạn đặt:
```json
"EXHAUST_PATH": "/var/cache/webp"
```
Thì ảnh WebP của **tsuki.jpg** sẽ được lưu tại:
```
/var/cache/webp/pics/tsuki.jpg.1582558990.webp
```

---

### 4️⃣ Chạy WebP Server Go
```bash
./webp-server --config=/path/to/config.json
```

---

### 5️⃣ Cấu hình **Nginx proxy_pass**
Thêm vào cấu hình Nginx:
```
proxy_pass http://localhost:3333/;
```
Sau đó, WebP Server sẽ bắt đầu hoạt động tự động. 🚀

---

## ⚡ Sử dụng nâng cao
WebP Server Go hỗ trợ chạy bằng **Supervisor**, **Docker** và nhiều tùy chọn khác.  
🔗 Xem hướng dẫn chi tiết tại: [https://docs.webp.sh/](https://docs.webp.sh/)

---

## 📜 Giấy phép
**WebP Server Go** được phát hành theo giấy phép **GPLv3**.  
Xem chi tiết tại tệp [`LICENSE`](./LICENSE).

---

🚀 **Chúc bạn sử dụng WebP Server Go hiệu quả!** 🚀