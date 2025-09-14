# PPAPIKey Server - Flutter App Rebuild

Dự án Flutter được tạo lại từ file IPA gốc của ứng dụng PPAPIKey Server.

## Thông tin ứng dụng

- **Tên**: PPAPIKey Server
- **Bundle ID**: com.pp.ppapikeyflutter
- **Phiên bản**: 1.0.0
- **Platform**: iOS (Flutter)

## Tính năng

- Quản lý loại người dùng (Normal, VIP, Admin)
- Lưu trữ API Key với SharedPreferences
- Giao diện người dùng thân thiện

## Cài đặt

```bash
flutter pub get
flutter run
```

## Build IPA với GitHub Actions

Xem file `BUILD_GUIDE.md` để biết hướng dẫn chi tiết về cách build IPA tự động thông qua GitHub Actions.

## Cấu trúc dự án

```
├── lib/main.dart              # Mã nguồn Flutter
├── assets/images/             # Hình ảnh ứng dụng
├── ios/                       # Cấu hình iOS
├── .github/workflows/         # GitHub Actions
└── pubspec.yaml              # Dependencies
```

## Liên hệ

Tạo issue trên GitHub nếu có vấn đề hoặc câu hỏi.