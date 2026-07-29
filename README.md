# VHKD — Trung Tâm Vận Hành Karofi

Dashboard nội bộ cho Phòng Vận hành Kinh doanh (Karofi): liệt kê các nhóm công việc, kỹ năng Cowork và công cụ tự xây bằng Claude Code. Mỗi thẻ có nút "Sử dụng" để nhập tham số và copy câu lệnh tiếng Việt, sẵn sàng dán vào Cowork.

File chính là [`index.html`](./index.html) — trang dashboard, tự chứa (không gọi API/CDN ngoài), chạy được bằng cách mở trực tiếp trong trình duyệt hoặc host qua GitHub Pages.

Đi kèm là [`shipment-tracking.html`](./shipment-tracking.html) — công cụ Shipment Tracking (bản đã có Google OAuth để đọc/ghi trực tiếp Google Sheet, lấy từ `CLAUDE-OUTPUTS/Shipment Tracking/github-pages/index.html`). Thẻ **"Update data lịch trình"** trong `index.html` link tới file này bằng đường dẫn tương đối — cả hai file phải nằm cùng thư mục để link hoạt động.

## ⚠️ Trước khi push lên GitHub

- `index.html` có nhắc tới **đường dẫn nội bộ** (VD: `D:\Operation\Claude\Projects\Cong-cu-Gia-thanh-BOM\...`) cho công cụ tra giá thành BOM (công cụ này chạy cục bộ, không đưa vào repo).
- `shipment-tracking.html` chứa sẵn **ID Google Sheet**, **Google API key** và **OAuth Client ID** (để đăng nhập ghi dữ liệu). Nếu đẩy lên **repo public**, các giá trị này sẽ hiển thị công khai.

Khuyến nghị:

- Đặt repo ở chế độ **Private** trên GitHub (Settings → repo → Danger Zone, hoặc chọn Private lúc tạo repo), **hoặc**
- Rà lại 2 file trên, thay các đường dẫn/ID/key nhạy cảm bằng placeholder trước khi để repo public.

Ngoài ra, OAuth Client ID trong `shipment-tracking.html` chỉ hoạt động với các "Authorized JavaScript origins" đã khai báo trong Google Cloud Console — sau khi có URL GitHub Pages thật (`https://<user>.github.io`), cần vào Google Cloud Console thêm origin đó vào OAuth Client, nếu không nút đăng nhập Google trên trang sẽ báo lỗi.

## Cách đưa lên GitHub Pages

```bash
cd "D:\Operation\Claude\Projects\VHKD"
git branch -M main
git remote add origin https://github.com/<tên-tổ-chức-hoặc-user>/VHKD.git
git push -u origin main
```

Sau đó vào GitHub → repo **VHKD** → **Settings → Pages** → chọn nguồn **Deploy from a branch**, branch `main`, thư mục `/ (root)`. Trang sẽ chạy tại `https://<user>.github.io/VHKD/`.

## Cập nhật dashboard sau này

Toàn bộ cấu trúc nhóm/tab/kỹ năng/công cụ nằm trong biến `GROUPS` ở đầu thẻ `<script>` trong `index.html` (có comment đánh dấu). Sửa trực tiếp mảng này rồi commit + push lại là cập nhật xong cho tất cả mọi người xem — không cần sửa gì khác.

Người dùng cũng có thể tự thêm nhanh một mục (kỹ năng/công cụ) ngay trên trang bằng nút **"+ Thêm kỹ năng / công cụ"** — nhưng mục đó chỉ lưu trong `localStorage` của trình duyệt đang dùng, không xuất hiện cho người khác cho tới khi được thêm thủ công vào `GROUPS` và push lại.
