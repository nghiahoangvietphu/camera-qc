# Camera QC — trang HTTPS độc lập

Nguyên mẫu Gate C0-B. **Một tệp tĩnh duy nhất** (`index.html`), không cần
build, không phụ thuộc gói nào, không có khóa bí mật.

## Vì sao phải tách khỏi Apps Script

Web app Apps Script phục vụ giao diện bên trong **iframe của Google**. Trong
iframe đó, `getUserMedia()` bị chặn — đã kiểm trên iPhone Safari tại DEV @40
và nhận `NotAllowedError`. Camera trực tiếp vì thế bắt buộc phải chạy ở
**top-level browsing context**, tức một trang HTTPS riêng.

## Triển khai

Tệp này chạy trên **bất kỳ hosting tĩnh HTTPS nào**. Yêu cầu duy nhất:

- HTTPS (bắt buộc cho `getUserMedia`)
- phục vụ ở top-level, **không** nhúng trong iframe

Không cần máy chủ ứng dụng, không cần cơ sở dữ liệu.

## Kiểm nhanh tại chỗ

```bash
npm run camera-qc
```

Mở `http://localhost:8787`. `localhost` được coi là ngữ cảnh an toàn nên
camera chạy được ngay trên máy tính — đủ để kiểm giao diện, **nhưng không
thay thế được UAT trên điện thoại thật**.

## Phạm vi

Gate C0-B chỉ chứng minh camera. Chưa đăng nhập, chưa watermark, chưa gửi ảnh
về máy chủ. Những phần đó thuộc Gate C1.
