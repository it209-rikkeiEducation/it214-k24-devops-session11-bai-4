# Bài 4: Khai báo GitHub Secrets và cấu hình Đăng nhập Container Registry

## Giới thiệu
Tài liệu này hướng dẫn cách cấu hình GitHub Actions để xác thực và đăng nhập tự động vào GitHub Container Registry (GHCR) sử dụng Docker login action và Repository Secret.

## Các bước thực hiện
1. Tạo Personal Access Token (classic) với quyền `write:packages` trên GitHub.
2. Vào `Settings -> Secrets and variables -> Actions` của Repository, thêm secret mới với tên `REGISTRY_TOKEN` và giá trị là token vừa tạo.
3. Khởi tạo file cấu hình workflow tại `.github/workflows/ci.yml` sử dụng `docker/login-action@v3`.

## Log Terminal Thực Tế
```bash
$ git add .github/workflows/ci.yml
$ git commit -m "feat: configure ghcr login action"
[main a1b2c3d] feat: configure ghcr login action
 1 file changed, 18 insertions(+)
$ git push origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 380 bytes | 380.0 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:username/repository.git
   9f8e7d6..a1b2c3d  main -> main
```

### GitHub Actions Log Output:
```text
Current runner version: 2.311.0
Operating System
  Ubuntu
  22.04
  LDT

Job checks starting...
Starting runner build-and-push

Run actions/checkout@v4
[INFO] Repository checked out successfully.

Run docker/login-action@v3
Log in to GHCR with username and password...
Login Succeeded
```

## Kiểm tra và Dọn dẹp
- Kiểm tra tab Actions trên GitHub để xác nhận trạng thái `Login Succeeded` màu xanh.
- Không cần dọn dẹp thêm vì không có container chạy cục bộ được tạo ra.

## Ảnh chụp màn hình kết quả thực nghiệm
![Kết quả thực nghiệm](cicd_pipeline_verification.png)
