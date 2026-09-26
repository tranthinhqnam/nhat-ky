# 🌾 Nhật Ký Đồng Quê: hướng dẫn đưa lên mạng miễn phí

Sau khi làm xong, blog của bạn có địa chỉ dạng **https://tên-github-của-bạn.github.io**.
Ai có link cũng đọc được, nhưng chỉ bạn viết được.

## Cách trang hoạt động
- Toàn bộ bài viết nằm trong file `entries.json` trong repo GitHub của bạn.
- Khách vào trang sẽ đọc file đó.
- Khi bạn bấm **Lưu nhật ký**, trang dùng GitHub token của bạn để ghi thẳng vào `entries.json`.
  GitHub Pages tự cập nhật, khoảng 1 phút sau khách sẽ thấy bài mới.
- Không cần server hay database, và hoàn toàn miễn phí.

---

## Bước 1: Tạo tài khoản GitHub
Vào https://github.com/signup và đăng ký. Tên đăng nhập (username) chính là phần đầu của domain.
Ví dụ username `thinhtran` thì domain là `thinhtran.github.io`.

## Bước 2: Tạo repo
1. Bấm **+** ở góc phải trên, chọn **New repository**.
2. **Repository name**: gõ đúng `USERNAME.github.io`, thay USERNAME bằng username của bạn.
   Đặt đúng tên này thì blog nằm ngay ở domain gốc, không có đuôi phía sau.
3. Chọn **Public**. GitHub Pages miễn phí chỉ hỗ trợ repo công khai.
4. Bấm **Create repository**.

## Bước 3: Upload file
**Cách dễ nhất, không cần gõ lệnh:**
1. Trong repo vừa tạo, bấm **uploading an existing file**.
2. Kéo 2 file `index.html` và `entries.json` từ thư mục `~/nhat-ky` vào.
3. Bấm **Commit changes**.

**Hoặc dùng lệnh trong Terminal:**
```bash
cd ~/nhat-ky
git init -b main
git add index.html entries.json .nojekyll
git commit -m "Nhật ký đầu tiên"
git remote add origin https://github.com/USERNAME/USERNAME.github.io.git
git push -u origin main
```
Khi được hỏi mật khẩu, bạn phải dán một token có quyền ghi repo (xem Bước 5), vì GitHub không nhận mật khẩu thường.

## Bước 4: Bật GitHub Pages
1. Trong repo, vào **Settings**, rồi chọn **Pages** ở menu trái.
2. Mục **Source** chọn **Deploy from a branch**. Branch chọn `main`, thư mục `/ (root)`, rồi bấm **Save**.
3. Đợi 1–2 phút rồi mở `https://USERNAME.github.io`. Blog đã lên mạng 🎉

## Bước 5: Tạo "chìa khóa" để viết bài (token)
1. Mở https://github.com/settings/personal-access-tokens/new
   (hoặc vào Settings, chọn Developer settings, rồi Personal access tokens, chọn **Fine-grained tokens**, bấm **Generate new token**).
2. **Token name**: `nhat-ky`
3. **Expiration**: chọn thời hạn, ví dụ 1 năm. Hết hạn thì tạo token mới.
4. **Repository access**: chọn **Only select repositories**, rồi chọn repo `USERNAME.github.io`.
5. **Permissions** → **Repository permissions** → **Contents**: chọn **Read and write**.
6. Bấm **Generate token** và copy token (bắt đầu bằng `github_pat_...`).
   GitHub chỉ hiện token **một lần**, nên lưu nó vào chỗ an toàn.

## Bước 6: Viết nhật ký mỗi ngày
1. Mở blog, kéo xuống cuối trang, bấm **Chủ nhà**.
2. Dán token, bấm **Vào**.
3. Nút **✍️ Viết hôm nay** sẽ hiện ra. Viết xong bấm **Lưu nhật ký**.
4. Muốn sửa hoặc xóa bài, bấm **✏️ Sửa** ở bài đó.
5. Trang có sẵn một bài mẫu, bạn có thể sửa lại hoặc xóa đi.

Token được nhớ trong trình duyệt, nên mỗi thiết bị (laptop, điện thoại) chỉ cần đăng nhập một lần.

---

## ⚠️ Lưu ý
- **Repo là công khai**: ai cũng xem được file `entries.json`. Đừng viết thông tin nhạy cảm.
- **Không đưa token cho người khác.** Nếu dùng máy người khác, nhớ bấm **Chủ nhà → Đăng xuất**.
  Lỡ lộ token thì vào trang token trên GitHub, bấm **Revoke**, rồi tạo token mới.
- Khách thấy bài mới sau khoảng 1 phút. Nếu chưa thấy, nhấn tải lại trang.

## Muốn domain đẹp hơn?
- **Miễn phí**: xin subdomain `ten-ban.is-a.dev` tại https://is-a.dev (gửi yêu cầu qua GitHub, được duyệt thì dùng được).
- **Tốn phí**: mua domain `.com`, `.vn`, `.io.vn`,... (domain `.io.vn` khá rẻ), rồi vào **Settings → Pages → Custom domain** để gắn.
- Khi dùng domain riêng, mở `index.html`, tìm `const CONFIG` và điền tay:
  ```js
  owner: 'USERNAME',
  repo: 'USERNAME.github.io',
  ```

## Chạy thử trên máy
```bash
cd ~/nhat-ky
python3 -m http.server 8000
```
Rồi mở http://localhost:8000. Trên máy, trang chạy ở **chế độ thử**: bài viết chỉ lưu trong trình duyệt, không lên GitHub.
