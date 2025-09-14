# Hướng dẫn Build IPA với GitHub Actions

## Bước 1: Chuẩn bị Repository

1. **Tạo GitHub Repository mới**
   - Đăng nhập vào GitHub
   - Tạo repository mới với tên `ppapikey-flutter-rebuild`
   - Clone repository về máy local

2. **Upload code lên GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: PPAPIKey Flutter rebuild"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/ppapikey-flutter-rebuild.git
   git push -u origin main
   ```

## Bước 2: Cấu hình iOS Certificate và Provisioning Profile

### Tạo Certificate (nếu chưa có)

1. **Mở Keychain Access**
   - Applications → Utilities → Keychain Access

2. **Tạo Certificate Request**
   - Keychain Access → Certificate Assistant → Request a Certificate From a Certificate Authority
   - Điền thông tin và lưu file .certSigningRequest

3. **Tạo Certificate trên Apple Developer**
   - Đăng nhập vào [Apple Developer Portal](https://developer.apple.com)
   - Certificates, Identifiers & Profiles → Certificates
   - Tạo certificate mới (iOS Distribution)

4. **Download và cài đặt Certificate**
   - Download certificate và double-click để cài vào Keychain

5. **Export Certificate**
   - Mở Keychain Access
   - Tìm certificate vừa tạo
   - Right-click → Export
   - Chọn định dạng .p12 và đặt mật khẩu

### Tạo Provisioning Profile

1. **Tạo App ID**
   - Apple Developer Portal → Identifiers
   - Tạo App ID với Bundle ID: `com.pp.ppapikeyflutter`

2. **Tạo Provisioning Profile**
   - Profiles → Tạo profile mới
   - Chọn App ID và Certificate
   - Download profile

## Bước 3: Cấu hình GitHub Secrets

1. **Vào Repository Settings**
   - GitHub repository → Settings → Secrets and variables → Actions

2. **Thêm các Secrets sau:**

   ```
   BUILD_CERTIFICATE_BASE64: [Base64 encoded của file .p12]
   P12_PASSWORD: [Mật khẩu của file .p12]
   KEYCHAIN_PASSWORD: [Mật khẩu keychain (có thể đặt bất kỳ)]
   PROVISIONING_PROFILE_BASE64: [Base64 encoded của file .mobileprovision]
   EXPORT_METHOD: app-store (hoặc ad-hoc, enterprise)
   ```

3. **Cách encode file thành Base64:**
   ```bash
   # Trên macOS/Linux
   base64 -i certificate.p12 -o certificate_base64.txt
   
   # Trên Windows (PowerShell)
   [Convert]::ToBase64String([IO.File]::ReadAllBytes("certificate.p12"))
   ```

## Bước 4: Trigger Build

### Cách 1: Push code (Tự động)
```bash
git add .
git commit -m "Update app configuration"
git push origin main
```

### Cách 2: Manual trigger
1. Vào GitHub repository
2. Actions tab
3. Chọn workflow "Build iOS IPA"
4. Click "Run workflow"

## Bước 5: Download IPA

1. **Sau khi build thành công:**
   - Vào Actions tab
   - Click vào workflow run vừa hoàn thành
   - Scroll xuống phần "Artifacts"
   - Download file `ppapikey-app-ipa`

2. **File IPA sẽ có tên:**
   - `Runner.ipa` hoặc tương tự

## Troubleshooting

### Lỗi thường gặp:

1. **"No matching provisioning profiles found"**
   - Kiểm tra Bundle ID trong Xcode project
   - Đảm bảo App ID và Provisioning Profile khớp nhau

2. **"Certificate not found"**
   - Kiểm tra certificate đã được encode đúng Base64
   - Đảm bảo mật khẩu P12_PASSWORD đúng

3. **"Flutter not found"**
   - GitHub Actions sẽ tự động cài Flutter
   - Kiểm tra version Flutter trong workflow file

4. **"Xcode build failed"**
   - Kiểm tra iOS deployment target
   - Đảm bảo tất cả dependencies đã được cài đặt

### Debug Steps:

1. **Kiểm tra logs trong GitHub Actions**
   - Vào Actions tab
   - Click vào workflow run
   - Xem chi tiết logs từng step

2. **Test local build:**
   ```bash
   flutter clean
   flutter pub get
   flutter build ios --release --no-codesign
   ```

3. **Kiểm tra Flutter doctor:**
   ```bash
   flutter doctor
   ```

## Lưu ý quan trọng

1. **Bundle ID**: Phải khớp với App ID trên Apple Developer Portal
2. **Certificate**: Phải còn hiệu lực và được Apple approve
3. **Provisioning Profile**: Phải match với App ID và Certificate
4. **Team ID**: Cần có trong ExportOptions.plist
5. **Flutter Version**: Đảm bảo tương thích với iOS version

## Kết quả

Sau khi hoàn thành, bạn sẽ có:
- ✅ Dự án Flutter hoàn chỉnh
- ✅ GitHub Actions workflow để build IPA tự động
- ✅ IPA file có thể cài đặt trên thiết bị iOS
- ✅ Quy trình CI/CD hoàn chỉnh

Chúc bạn thành công! 🎉
