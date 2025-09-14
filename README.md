# PPAPIKey Flutter App

Ứng dụng Flutter PPAPIKey Server được rebuild từ IPA gốc.

## Tính năng

- Giao diện người dùng với Material Design
- Quản lý loại người dùng (Normal, VIP, Admin)
- Lưu trữ API Key với SharedPreferences
- Avatar động theo loại người dùng
- Giao diện tiếng Việt

## Cấu trúc Project

```
ppapikey_flutter_rebuild/
├── lib/
│   └── main.dart          # File chính của ứng dụng
├── assets/
│   └── images/            # Hình ảnh (logo, avatar)
├── ios/                   # Cấu hình iOS
├── pubspec.yaml          # Dependencies Flutter
└── .github/
    └── workflows/
        └── build-ios.yml  # GitHub Actions để build IPA
```

## Build IPA với GitHub Actions

### Tự động Build
1. Push code lên branch `main`
2. GitHub Actions sẽ tự động build IPA
3. Download IPA từ tab "Actions" → "Artifacts"

### Manual Build
1. Vào tab "Actions" trên GitHub
2. Chọn workflow "Build iOS IPA"
3. Click "Run workflow"
4. Chọn branch `main`
5. Click "Run workflow"

## Build Local

### Yêu cầu
- Flutter SDK 3.16.0+
- Xcode (cho iOS)
- macOS (cho iOS build)

### Các bước
```bash
# Clone repository
git clone https://github.com/Nidios1/appsever.git
cd appsever

# Install dependencies
flutter pub get

# Build iOS (cần macOS + Xcode)
flutter build ios --release

# Build IPA (cần Apple Developer account)
cd ios
xcodebuild -workspace Runner.xcworkspace \
           -scheme Runner \
           -configuration Release \
           -destination generic/platform=iOS \
           -archivePath Runner.xcarchive \
           archive

xcodebuild -exportArchive \
           -archivePath Runner.xcarchive \
           -exportPath . \
           -exportOptionsPlist ExportOptions.plist
```

## Dependencies

- `flutter`: SDK Flutter
- `shared_preferences`: Lưu trữ dữ liệu local
- `cupertino_icons`: Icons cho iOS

## Cấu hình iOS

- Bundle ID: `com.example.ppapikey_flutter_rebuild`
- Version: 1.0.0+1
- Export Options: Đã cấu hình trong `ExportOptions.plist`

## Lưu ý

- Để build IPA thành công, cần có Apple Developer account
- GitHub Actions sẽ build trên macOS runner
- IPA sẽ được upload dưới dạng artifact
- Build logs sẽ được lưu nếu có lỗi

## Liên hệ

Repository: https://github.com/Nidios1/appsever.git