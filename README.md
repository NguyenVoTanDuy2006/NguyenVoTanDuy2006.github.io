# Đồ án cá nhân — Tiền xử lý dữ liệu

Đồ án môn Khai phá dữ liệu, tập trung vào phân tích thống kê, thiết kế pipeline
tiền xử lý và đánh giá tác động trên hai loại dữ liệu: **chuỗi thời gian** và
**văn bản**.

- **Sinh viên:** Nguyễn Võ Tấn Duy
- **MSSV:** Chưa bổ sung
- **Website:** <https://nguyenvotanduy2006.github.io/>
- **Repository:** <https://github.com/NguyenVoTanDuy2006/NguyenVoTanDuy2006.github.io>

## Trạng thái

Đang chuẩn bị cấu trúc trình bày cho đồ án. Chưa chọn bộ dữ liệu, chưa có kết quả
thực nghiệm và chưa thiết lập Jupyter Book.

Sản phẩm cuối cùng sẽ là **một Jupyter Book** chứa các notebook phân tích, được
build và xuất bản trên GitHub Pages từ repository này.

## Phạm vi thực hiện

| Phần | Dữ liệu | Nội dung dự kiến |
| --- | --- | --- |
| (a) | Chuỗi thời gian | EDA, điền khuyết, kiểm định tính dừng, phân rã chuỗi, trích xuất đặc trưng, phát hiện dị thường và dự báo |
| (b) | Văn bản | EDA, chuẩn hóa, tokenization, stop words, stemming/lemmatization, vector hóa và đánh giá phân loại |

Mỗi kỹ thuật sẽ được trình bày theo thứ tự: mục tiêu và lý thuyết, thiết lập thí
nghiệm, code và kết quả, phân tích và hạn chế.

## Dữ liệu

- **Chuỗi thời gian:** chưa chọn; cần trải dài ít nhất 2 năm, tần suất ngày hoặc giờ.
- **Văn bản:** chưa chọn; cần ít nhất 10.000 mẫu và ít nhất 2 nhãn phân loại.

Sau khi chọn dữ liệu, bổ sung mô tả, nguồn công khai trên Hugging Face hoặc Kaggle
và cách tải dữ liệu. Dữ liệu thô dung lượng lớn không được đưa vào Git.

## Cấu trúc hiện tại

```text
.
├── README.md              # Giới thiệu và hướng dẫn cập nhật website
├── index.md               # Trang chủ, lấy nội dung từ README
├── _config.yml            # Cấu hình Jekyll và theme Primer
├── Gemfile                # Thư viện Ruby cho website
├── Gemfile.lock           # Các phiên bản thư viện đã khóa
├── .github/workflows/
│   └── pages.yml          # Build và deploy website bằng GitHub Actions
├── preprocessing.md       # Đề bài và tiêu chí chấm điểm
├── pyproject.toml         # Cấu hình dự án Python
├── .python-version        # Phiên bản Python dùng khi phát triển
└── src/
    └── individualproject/ # Package Python ban đầu
```

## Môi trường Python

Dự án yêu cầu **Python >= 3.12** theo `pyproject.toml`.
Nếu đã cài [uv](https://docs.astral.sh/uv/), chạy tại thư mục repository:

```bash
uv sync
```

Lệnh này chuẩn bị môi trường Python. Các thư viện phân tích và công cụ dựng book
sẽ được bổ sung khi triển khai; hiện chưa có lệnh build hoặc preview Jupyter Book.

## Xem trước website ở local

Website hiện dùng Jekyll 4.4 và theme Primer. Cần Ruby 3.4 và Bundler; Python
không thực hiện bước build website này.

Sau khi cài Bundler, chạy tại thư mục repository:

```bash
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve --livereload
```

Mở <http://localhost:4000/> để xem trước. Sau khi sửa `_config.yml`, dừng server
bằng **Ctrl + C** và chạy lại. Có thể build riêng bằng `bundle exec jekyll build`;
HTML/CSS được tạo trong `_site/`. Các thư mục `_site/`, `vendor/` và `.bundle/`
đã được Git bỏ qua.

## Xuất bản lên GitHub Pages

Repository dùng workflow `.github/workflows/pages.yml` để cài Ruby 3.4, cài các
thư viện theo `Gemfile.lock`, build Jekyll rồi deploy `_site/` lên Pages.

Thiết lập một lần trên GitHub:

1. Mở repository, vào **Settings → Pages**.
2. Trong **Build and deployment → Source**, chọn **GitHub Actions**.
3. Sau khi workflow có trên nhánh `main`, mở tab **Actions**, chọn
   **Deploy Jekyll site to Pages** để theo dõi. Có thể chọn **Run workflow** trên
   nhánh `main` nếu cần chạy thủ công.

Chế độ **Deploy from a branch** dùng bộ thư viện mặc định của GitHub Pages,
không đáp ứng yêu cầu Jekyll 4.4 trong `Gemfile` hiện tại. Khi thấy thông báo
`The github-pages gem can't satisfy your Gemfile's dependencies`, kiểm tra lại
rằng Source đã là **GitHub Actions** và workflow tự build ở trên đang được dùng.

## Cập nhật website từ máy cá nhân

Sau khi chỉnh sửa README, chạy các lệnh sau tại thư mục repository:

```bash
git add README.md
git commit -m "docs: update project introduction and Pages guide"
git push origin main
```

Workflow tự build và deploy sau mỗi lần push vào `main`. Mở tab **Actions** trong
repository để xem tiến trình và lỗi nếu có.
Khi workflow thành công, mở website và tải lại trang. Thay đổi có thể mất tới
10 phút để xuất hiện; nếu còn thấy nội dung cũ, thử **Ctrl + Shift + R**.

Bạn cũng có thể sửa trực tiếp trên GitHub: mở `README.md`, chọn **Edit this file**,
chỉnh nội dung rồi **Commit changes** vào `main`. Sau đó, tại máy cá nhân, chạy
`git pull --ff-only origin main` khi thư mục làm việc sạch để lấy thay đổi về.

## Chuyển sang Jupyter Book

Khi khung book được triển khai, repository sẽ có nguồn notebook, cấu hình book và
hướng dẫn build. Workflow sẽ được cập nhật để build book và deploy HTML của book;
Source của Pages tiếp tục là **GitHub Actions**. Nội dung website lúc đó được cập
nhật bằng cách sửa nguồn book và push lên GitHub.

## Tài liệu tham khảo

- [Cấu hình nguồn xuất bản GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [Tạo site, chọn trang đầu và thời gian xuất bản](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
- [Build Jekyll bằng GitHub Actions với phiên bản và thư viện tùy chọn](https://jekyllrb.com/docs/continuous-integration/github-actions/)
