# Camera QC — Việt Phú

Trang chụp ảnh hiện trường cho hệ thống QA/QC. Chạy trên GitHub Pages để có
HTTPS thật — `getUserMedia()` bị chặn trong iframe của Apps Script HtmlService,
nên camera trực tiếp phải nằm ở một trang độc lập.

## Trang này làm gì

- Mở camera sau của thiết bị, toàn màn hình. **Không có đường chọn tệp** từ
  thư viện ảnh hay Files.
- Sau khi chụp, đóng năm thông tin **vào pixel** của ảnh: mã phiếu, thời gian
  ghi hình, họ tên người chụp, vai trò (QLX/QC), địa điểm GPS.
- Gửi ảnh lên Camera Upload API bằng vé có chữ ký, kèm toạ độ và trạng thái
  định vị.

## Cách mở

Trang **không mở trực tiếp được**. Nó cần một vé do máy chủ phát:

```
https://nghiahoangvietphu.github.io/camera-qc/#ve=<vé>&api=<URL API>
```

Tham số đi qua **hash fragment** (`#`), không qua query string: hash không bao
giờ được gửi tới máy chủ, nên vé — có chứa họ tên người chụp — không lọt vào
log của GitHub Pages.

Vé có hiệu lực ngắn. Hết hạn thì trang yêu cầu quay lại ứng dụng QA/QC.

## Trạng thái định vị

Thiếu GPS **không chặn** việc chụp hay lưu. Bốn trạng thái:

| Trạng thái | Đóng vào ảnh |
|---|---|
| `CO_DIA_DANH` | tên địa danh + toạ độ |
| `CHUA_RO_DIA_DANH` | `Chưa xác định địa danh` + toạ độ |
| `KHONG_CO_GPS` | `Không rõ địa điểm ghi hình` |
| `TU_CHOI_QUYEN` | `Người dùng từ chối cấp quyền ghi vị trí` |

## Không có gì bí mật trong repo này

Trang là HTML tĩnh, không chứa khoá ký, ID bảng tính, địa chỉ API hay dữ liệu
QC. Mọi thứ đó đến từ tham số lúc chạy. Trang **không tự ký vé** — nó chỉ mang
vé do máy chủ phát.

## Hỗ trợ

iOS Safari 14.3+, Chrome/Edge bản mới. Bắt buộc HTTPS.
