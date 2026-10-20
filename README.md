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

## Xuất bản trang README lên GitHub Pages

Trong giai đoạn đầu, có thể dùng README làm trang giới thiệu. Trên GitHub:

1. Mở repository, vào **Settings → Pages**.
2. Trong **Build and deployment → Source**, chọn **Deploy from a branch**.
3. Chọn nhánh **main**, thư mục **/(root)** rồi nhấn **Save**.

GitHub Pages có thể dùng `README.md` làm trang đầu khi thư mục xuất bản chưa có
`index.html` hoặc `index.md`. Nếu đã có một trong hai file index, hãy chỉnh trang
đó để thay đổi nội dung trang chủ.

## Cập nhật website từ máy cá nhân

Sau khi chỉnh sửa README, chạy các lệnh sau tại thư mục repository:

```bash
git add README.md
git commit -m "docs: update project introduction and Pages guide"
git push origin main
```

Với cấu hình xuất bản từ `main` và `/(root)` ở trên, GitHub sẽ tự build và deploy
sau khi push. Mở tab **Actions** trong repository để xem tiến trình và lỗi nếu có.
Khi workflow thành công, mở website và tải lại trang. Thay đổi có thể mất tới
10 phút để xuất hiện; nếu còn thấy nội dung cũ, thử **Ctrl + Shift + R**.

Bạn cũng có thể sửa trực tiếp trên GitHub: mở `README.md`, chọn **Edit this file**,
chỉnh nội dung rồi **Commit changes** vào `main`. Sau đó, tại máy cá nhân, chạy
`git pull --ff-only origin main` khi thư mục làm việc sạch để lấy thay đổi về.

## Chuyển sang Jupyter Book

Khi khung book được triển khai, repository sẽ có nguồn notebook, cấu hình book,
hướng dẫn build và workflow xuất bản. Khi đó sẽ chuyển **Settings → Pages →
Source** sang **GitHub Actions** để workflow build và deploy HTML của book.
Nội dung website lúc đó được cập nhật bằng cách sửa nguồn book và push lên GitHub.

## Tài liệu tham khảo

- [Cấu hình nguồn xuất bản GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [Tạo site, chọn trang đầu và thời gian xuất bản](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)
