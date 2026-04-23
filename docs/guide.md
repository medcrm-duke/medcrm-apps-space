# Hướng dẫn chạy dự án

Dự án này sử dụng Monorepo với Turborepo, bao gồm ứng dụng di động (Expo React Native) và ứng dụng web (Next.js). Dưới đây là các câu lệnh cơ bản để quản lý và phát triển dự án.

## 1. Cài đặt Dependencies

Trước khi bắt đầu, hãy đảm bảo bạn đã cài đặt toàn bộ dependencies ở thư mục gốc (root) của dự án.

```bash
# Cài đặt các gói phụ thuộc
npm install
```

## 2. Turborepo (Quản lý Monorepo)

Turborepo giúp tối ưu hóa việc chạy các script (dev, build, lint, v.v.) trên nhiều packages và ứng dụng cùng lúc.

- **Chạy tất cả các dự án (web & native) ở chế độ development:**
  ```bash
  npx turbo run dev
  ```
- **Build tất cả các dự án:**
  ```bash
  npx turbo run build
  ```
- **Chạy kiểm tra mã nguồn (Lint) cho tất cả:**
  ```bash
  npx turbo run lint
  ```
- **Xóa cache của turbo (rất hữu ích khi có lỗi lạ):**
  ```bash
  npx turbo run clean
  # hoặc xóa thư mục .turbo thủ công
  ```
- **Chỉ chạy script cho một ứng dụng cụ thể (VD: ứng dụng web):**
  ```bash
  npx turbo run dev --filter=web
  ```
  *(Thay `web` bằng tên name trong file `package.json` của ứng dụng bạn muốn chạy, ví dụ `native`, `docs`...)*

## 3. Expo React Native (Ứng dụng Di động)

Ứng dụng di động thường nằm trong thư mục `apps/native` (theo file bạn đang mở). Bạn có thể dùng `turbo` để chạy hoặc vào trực tiếp thư mục để chạy lệnh Expo.

- **Khởi chạy Metro bundler của Expo:**
  ```bash
  npx turbo run dev --filter=native
  # Hoặc nếu bạn đang ở trong thư mục apps/native/:
  npx expo start
  ```
- **Chạy trên máy ảo / thiết bị Android:**
  Nhấn phím `a` trong terminal sau khi Metro bundler đã chạy, hoặc:
  ```bash
  npx expo start --android
  ```
- **Chạy trên máy ảo / thiết bị iOS (Yêu cầu macOS):**
  Nhấn phím `i` trong terminal sau khi Metro bundler đã chạy, hoặc:
  ```bash
  npx expo start --ios
  ```
- **Khởi chạy lại Expo và xóa cache:**
  ```bash
  npx expo start -c
  ```

## 4. Next.js & Vercel (Ứng dụng Web)

Ứng dụng web Next.js thường được đặt trong thư mục `apps/web`.

- **Chạy chế độ phát triển (Development):**
  ```bash
  npx turbo run dev --filter=web
  # Hoặc nếu ở trong apps/web/:
  npm run dev
  ```
- **Build production cho ứng dụng Web:**
  ```bash
  npx turbo run build --filter=web
  ```
- **Khởi chạy server production (sau khi đã build):**
  ```bash
  npx turbo run start --filter=web
  ```
- **Deploy với Vercel:**
  Vercel hỗ trợ Turborepo và Next.js một cách tự động (First-class support).
  1. Nếu liên kết qua GitHub: Đẩy code lên nhánh chính, Vercel sẽ tự động nhận diện Monorepo và build.
  2. Deploy thủ công bằng Vercel CLI ở thư mục gốc:
     ```bash
     npm i -g vercel
     vercel
     ```
     Làm theo hướng dẫn trên terminal để liên kết project.
