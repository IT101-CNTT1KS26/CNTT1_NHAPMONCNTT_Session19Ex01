# PHÂN TÍCH VÀ QUY TRÌNH PHÒNG CHỐNG TẤN CÔNG HOMOGRAPH (PHISHING)


## PHẦN 1: PHÂN TÍCH KÝ TỰ LẠ VÀ TẤN CÔNG HOMOGRAPH

1. **Xác định ký tự lạ trong URL:**
* Trong chuỗi `[https://githúb.com/login](https://githúb.com/login)`, ký tự bất thường nằm ở chữ **`ú`** (có dấu sắc, mã Unicode U+00FA) thay vì chữ **`u`** chuẩn (mã ASCII U+0075) của tên miền chính thống `github.com`.


2. **Tại sao nó có thể đánh lừa người dùng?**
* **Tấn công IDN Homograph Attack (Giả mạo đồng hình):** Kẻ tấn công sử dụng các ký tự quốc tế (Internationalized Domain Names - IDN) có hình dáng gần như trùng khớp hoàn toàn với các ký tự Latinh tiêu chuẩn để đăng ký tên miền lừa đảo.
* **Đánh lừa thị giác:** Với tốc độ nhìn lướt nhanh của con người, bộ não thường tự động "bù đắp" và xem chữ `ú` giống hệt chữ `u`. Người dùng lầm tưởng đây là trang GitHub thật, dẫn đến việc nhập thông tin đăng nhập và bị đánh cắp tài khoản.



---

## PHẦN 2: QUY TRÌNH KIỂM TRA NHANH TRƯỚC KHI NHẬP MASTER PASSWORD

Để vô hiệu hóa hoàn toàn các bẫy Homograph và Phishing trước khi gõ mật khẩu, hãy áp dụng quy trình kiểm tra 2 bước sau:

### Bước 1: Kiểm tra nhanh bằng mắt thường và Trình duyệt

* **Soi kỹ từng ký tự:** Rà soát kỹ phần tên miền chính (Domain Name) ngay trước dấu `/` đầu tiên. Kiểm tra xem có dấu phụ (dấu sắc, huyền, mũ...), ký tự lạ hoặc lỗi chính tả cố ý hay không (ví dụ: `github` thành `githúb`, `rn` thay cho `m`).
* **Quan sát cơ chế Punycode của trình duyệt:** Các trình duyệt hiện đại (Chrome, Edge, Firefox) được tích hợp cơ chế bảo vệ chống Homograph. Nếu bạn copy hoặc rê chuột vào đường dẫn đáng nghi, trình duyệt có thể hiển thị dạng mã hóa gốc bắt đầu bằng tiền tố **`xn--`** (ví dụ: `xn--githb-exa.com`), lập tức vạch trần bản chất giả mạo của tên miền.

### Bước 2: Sử dụng "Tấm khiên" Password Manager (Quy tắc tự động điền)

* **Nguyên lý bảo mật:** Các ứng dụng quản lý mật khẩu uy tín (như Bitwarden, 1Password) nhận diện website dựa trên **Domain chính xác tuyệt đối**.
* **Hành động kiểm tra:**
* Hãy để Trình quản lý mật khẩu tự động điền (Autofill) thông tin tài khoản.
* **Nếu Password Manager từ chối điền hoặc không hiện gợi ý:** Đây là **cảnh báo đỏ** cho thấy bạn đang đứng trên một trang web giả mạo (vì tên miền `githúb.com` hoàn toàn khác với `github.com` đã lưu trong hệ thống quản lý mật khẩu). Tuyệt đối không tự tay gõ lại Master Password hay OTP lên trang đó.