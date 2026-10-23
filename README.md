# Đồ án cá nhân — Tiền xử lý dữ liệu

Đồ án môn Khai phá dữ liệu, tập trung vào phân tích thống kê, thiết kế pipeline
tiền xử lý và đánh giá tác động trên hai loại dữ liệu: **chuỗi thời gian** và
**văn bản**.

- **Sinh viên:** Nguyễn Võ Tấn Duy
- **MSSV:** Chưa bổ sung
- **Website:** <https://nguyenvotanduy2006.github.io/>
- **Repository:** <https://github.com/NguyenVoTanDuy2006/NguyenVoTanDuy2006.github.io>

## Trạng thái

Đã thiết lập Jupyter Book, workflow deploy GitHub Pages và các thư mục cho code,
dữ liệu, kết quả. Đã chọn hai bộ dữ liệu và tạo khung nội dung cho từng phần; notebook
thực nghiệm chưa hoàn chỉnh.

Sản phẩm cuối cùng là **một Jupyter Book** chứa các notebook phân tích, được build
và xuất bản trên GitHub Pages từ repository này.

## Phạm vi thực hiện

| Phần | Dữ liệu | Nội dung dự kiến |
| --- | --- | --- |
| (a) | Chuỗi thời gian | EDA, điền khuyết, kiểm định tính dừng, phân rã chuỗi, trích xuất đặc trưng, phát hiện dị thường và dự báo |
| (b) | Văn bản | EDA, chuẩn hóa, tokenization, stop words, stemming/lemmatization, vector hóa và đánh giá phân loại |

Mỗi kỹ thuật sẽ được trình bày theo thứ tự: mục tiêu và lý thuyết, thiết lập thí
nghiệm, code và kết quả, phân tích và hạn chế.

## Dữ liệu

- **Chuỗi thời gian:** [2022 Ukraine Russian War](https://www.kaggle.com/datasets/piterfm/2022-ukraine-russian-war), dữ liệu tổn thất được báo cáo theo ngày. Các file personnel và equipment có 1.696 ngày từ 2022-02-25 đến 2026-10-17; có thêm file hiệu chỉnh riêng. Dataset được ghi giấy phép CC BY-NC-SA 4.0.
- **Văn bản:** [60k Stack Overflow Questions with Quality Rating](https://www.kaggle.com/datasets/imoore/60k-stack-overflow-questions-with-quality-rate), 60.000 câu hỏi có nhãn `HQ`, `LQ_EDIT`, `LQ_CLOSE`, chia thành 45.000 mẫu train và 15.000 mẫu validation.

Dữ liệu đã tải về nhưng được Git bỏ qua, không commit dữ liệu thô. Có thể tải lại bằng
Kaggle CLI sau khi cấu hình tài khoản Kaggle:

```bash
kaggle datasets download -d piterfm/2022-ukraine-russian-war -p data/raw/ukraine_war --unzip
kaggle datasets download -d imoore/60k-stack-overflow-questions-with-quality-rate -p data/raw/stack_overflow_60k --unzip
```

Khi chia sẻ kết quả dùng dữ liệu Ukraine, ghi công nguồn và tuân thủ giấy phép CC
BY-NC-SA 4.0.

## Cấu trúc repository

```text
.
├── README.md                         # Thông tin đồ án và hướng dẫn build/deploy
├── myst.yml                          # Cấu hình Jupyter Book và mục lục
├── .github/workflows/pages.yml       # Build và deploy book lên GitHub Pages
├── preprocessing.md                  # Đề bài và tiêu chí chấm điểm
├── .python-version                   # Phiên bản Python cho local và CI
├── pyproject.toml, uv.lock           # Cấu hình và khóa phụ thuộc Python
├── book/
│   ├── index.md                      # Trang mở đầu
│   ├── time_series/                  # Nội dung và notebook chuỗi thời gian
│   └── text/                         # Nội dung và notebook văn bản
├── src/
│   ├── time_series/                  # Hàm Python tái sử dụng cho chuỗi thời gian
│   └── text/                         # Hàm Python tái sử dụng cho văn bản
├── data/
│   ├── raw/                          # Dữ liệu gốc, không commit
│   ├── interim/                      # Dữ liệu trung gian, không commit
│   └── processed/                    # Dữ liệu đã xử lý, không commit
└── outputs/
    ├── figures/                      # Biểu đồ sinh ra, không commit
    └── tables/                       # Bảng kết quả sinh ra, không commit
```

## Cài đặt và build local

Dự án yêu cầu **Python >= 3.12**. Cài [uv](https://docs.astral.sh/uv/) nếu máy bạn
chưa có, sau đó chạy tại thư mục repository:

```bash
uv sync
uv run jupyter book build --html
```

Các file HTML được tạo trong `_build/html/`. Để mở preview tự động cập nhật khi
chỉnh nội dung, chạy:

```bash
uv run jupyter book start
```

Mở địa chỉ mà terminal in ra, thường là <http://localhost:3000/>. Có thể dừng server
bằng **Ctrl + C**.

## Xuất bản lên GitHub Pages

Workflow `.github/workflows/pages.yml` cài Python và các dependency từ `uv.lock`,
build Jupyter Book thành HTML, rồi deploy artifact lên GitHub Pages sau mỗi lần push
vào nhánh `main`.

Thiết lập một lần trên GitHub:

1. Mở repository, vào **Settings → Pages**.
2. Trong **Build and deployment → Source**, chọn **GitHub Actions**.
3. Push thay đổi lên `main`, rồi theo dõi workflow **Deploy Jupyter Book to Pages**
   trong tab **Actions**.

Sau khi workflow thành công, website được cập nhật tại
<https://nguyenvotanduy2006.github.io/>. Dữ liệu trong `data/` và kết quả trong
`outputs/` được Git bỏ qua; chỉ commit nguồn notebook, code và tài liệu cần thiết.

## Cập nhật đồ án

Sau khi sửa notebook, code hoặc tài liệu, commit và push các thay đổi:

```bash
git add -A
git commit -m "ci: deploy Jupyter Book to Pages"
git push origin main
```

Workflow sẽ tự build và deploy lại book. Nếu build lỗi, mở tab **Actions** để xem
log của lần chạy tương ứng.

## Tài liệu tham khảo

- [Jupyter Book: build và xuất bản](https://jupyterbook.org/stable/build-and-publish/)
- [Jupyter Book: deploy lên GitHub Pages](https://jupyterbook.org/stable/get-started/publish/)
- [GitHub Pages: custom workflow với GitHub Actions](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)
