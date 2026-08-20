# Export Ops Hub — front-end tĩnh

Các trang tĩnh của hệ xuất khẩu Karofi, host qua GitHub Pages tại `https://karofisale.github.io/export/`.

| File | Là gì |
|---|---|
| [`pi-app.html`](./pi-app.html) | **App báo giá PI (Export Ops Hub)** — bản tĩnh của web app Apps Script. Sale đăng nhập tên + PIN, xem khách của mình, lập/sửa đơn, tính %LN + CBM + container, xuất PI Excel/PDF, quản lý Shipment/chứng từ. |
| [`hdsd.html`](./hdsd.html) · [`hdsd.pdf`](./hdsd.pdf) | **Hướng dẫn sử dụng** chia theo vai trò. App link tới `hdsd.html` từ topbar và màn hình đăng nhập (URL tuyệt đối). |
| [`shipment-tracking.html`](./shipment-tracking.html) | Công cụ Shipment Tracking bản đứng riêng (**đã ngừng dùng** — chức năng này giờ nằm trong chính app, tab "Quản lý Shipment"). Giữ lại để tra cứu. |
| `index.html` | Chỉ là **trang chuyển hướng** sang dashboard ở repo `karofisale/VHKD`. Repo này không chứa dashboard nữa. |

## Repo này KHÔNG chứa dashboard

Dashboard "Trung Tâm Vận Hành Karofi" nằm ở repo riêng **[`karofisale/VHKD`](https://github.com/karofisale/VHKD)** → https://karofisale.github.io/VHKD/. Trước đây có 1 bản copy trong repo này (từ đợt cutover 29/07/2026) nhưng đã lạc hậu và gây nhầm lẫn, nên thay bằng trang chuyển hướng.

## `pi-app.html` được BUILD, đừng sửa tay

File này sinh ra từ mã nguồn Apps Script, **sửa trực tiếp ở đây sẽ bị ghi đè lần build sau**. Nguồn:

- `D:\Operation\Claude\Projects\ExportOps-App\gas\Index.html` + `Style.html` + `App.html`

Build bằng script trong `ExportOps-App` (ghép 3 file trên, chèn `window.EXPORTOPS_API` = URL `/exec` của deployment đang chạy, xuất ra `pi-app.html` ở repo này). Các file `.gs` **không** nằm trong bản build — thay đổi backend phải dán vào Apps Script Editor và tạo deployment mới, không phải rebuild file này.

## Lưu ý bảo mật

`shipment-tracking.html` chứa sẵn **ID Google Sheet**, **Google API key** và **OAuth Client ID** — repo public thì các giá trị này hiện công khai. Đây là lý do nên bỏ hẳn file này khi không còn cần tra cứu. `pi-app.html` không chứa key (mọi truy cập dữ liệu đi qua backend Apps Script).
