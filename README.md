# HƯỚNG DẪN TRUY CẬP SOURCE CODE (Dành cho GV: Thầy Nguyễn Tuấn Đăng)

**Kính gửi Thầy,**

Em là **Phạm Tấn Khương** (MSSV: 3122410191).

Repository này là **Public** để nộp báo cáo. Tuy nhiên, để đảm bảo tính liêm chính học thuật, phần mã nguồn cốt lõi (Source code) được em lưu trữ dưới dạng **Git Submodule (Private)**.

⚠️ **LƯU Ý QUAN TRỌNG:**
Để xem được code bên trong thư mục con, Thầy cần có quyền truy cập vào Repository Private. Em đã gửi lời mời (Invite Collaborator) đến email **`ntdsgvn@gmail.com`**.

👉 **Thầy vui lòng kiểm tra Email và Chấp nhận lời mời trước khi bấm vào thư mục bên dưới.**

---

### 📂 Folder truy cập Source Code
Sau khi đã chấp nhận quyền truy cập, Thầy vui lòng click vào thư mục có ở trong hình dưới đây:

*(Thư mục này liên kết trực tiếp đến Private Repository chứa code)*

<div align="center">
  <img width="100%" alt="Hướng dẫn truy cập" src="https://github.com/user-attachments/assets/5345d1db-4f05-49c4-bc9f-05c60cc220f4" />
</div>

# Trợ lý Quản lý Lịch trình Cá nhân

## Giới Thiệu

Trợ lý quản lý lịch trinh cá nhân là một ứng dụng tích hợp AI giúp người dùng quản lý thời gian hiệu quả thông qua việc nhập liệu bằng ngôn ngữ tự nhiên (Tiếng Việt). Hệ thống tự động trích xuất thông tin, phát hiện trùng lịch, nhắc nhở bằng âm thanh và hỗ trợ chuẩn hóa lỗi chính tả.

## Video demo sản phẩm
[Demo_doacn.7z](Demo_doacn.7z)

## Tính Năng Chính

### 🗣️ Xử Lý Ngôn Ngữ Tự Nhiên (NLP)

  - Nhập lịch trình bằng câu văn thông thường (ví dụ: "Họp nhóm lúc 9h sáng mai tại thư viện").
  - Tự động trích xuất: Tên sự kiện, Thời gian (Bắt đầu/Kết thúc), Địa điểm.
  - Hỗ trợ các từ viết tắt thông dụng (t2, cn, vp, ks...) và tự động sửa lỗi chính tả tiếng Việt.

### 📅 Quản Lý Sự Kiện

  - Xem danh sách lịch trình dưới dạng bảng trực quan.
  - Thêm, Sửa, Xóa sự kiện nhanh chóng.
  - **Phát hiện trùng lịch**: Cảnh báo ngay lập tức nếu khung giờ mới bị chồng chéo với sự kiện đã có.

### ⏰ Hệ Thống Nhắc Nhở

  - Cơ chế chạy ngầm kiểm tra lịch hẹn mỗi giây.
  - Phát âm thanh cảnh báo tùy chọn (Tiếng nước rơi, Piano, Đồng hồ báo thức).
  - Hiển thị thông báo (Toast notification) chi tiết khi đến giờ.

### ⚙️ Tùy Chỉnh Cá Nhân

  - Cài đặt âm lượng và nhạc chuông thông báo.
  - Tìm kiếm sự kiện theo từ khóa.
  - Xuất dữ liệu lịch trình ra file JSON.

### 🤖 Kiểm Thử Tự Động

  - Hệ thống sinh Test Case tự động với các cấp độ từ cơ bản đến phức tạp (Stress Test) để kiểm tra độ chính xác của AI.

## Công Nghệ Sử Dụng

### Backend (API & Logic)

  - **Framework**: FastAPI
  - **Language**: Python 3.10+
  - **Database**: SQLite (Tích hợp sẵn, không cần cài đặt server riêng)
  - **NLP Libraries**: Underthesea (POS Tagging), Transformers (Hugging Face - Text Correction)
  - **Server**: Uvicorn

### Frontend (User Interface)

  - **Framework**: Streamlit
  - **Components**: AgGrid (Bảng dữ liệu), Streamlit Extras
  - **Audio**: Pygame, Winsound
  - **Data Handling**: Pandas, Requests

## Cài Đặt

### Yêu Cầu Hệ Thống

  - Python 3.10 trở lên
  - Pip (Python Package Installer)
  - Các thư viện phụ thuộc (được liệt kê bên dưới)

### Bước 1: Cài đặt thư viện

Mở terminal tại thư mục gốc dự án và chạy lệnh sau để cài các gói cần thiết:

```bash
pip install -r requirements.txt
```

### Bước 2: Khởi chạy Backend (API)

Backend sẽ chạy server AI để xử lý ngôn ngữ và quản lý Database.

```bash
cd backend
python api.py
```


### Bước 3: Khởi chạy Frontend

Mở một terminal mới (giữ terminal Backend đang chạy) và thực hiện:

```bash
streamlit run frontend.py
```

## Cấu Trúc Dự Án

Dựa trên cấu trúc thư mục thực tế:

```
Personal_Schedule_Assistant/
├── .streamlit/             # Cấu hình giao diện Streamlit
├── backend/                # Xử lý Logic & API
│   ├── api.py              # FastAPI App (AI Processing & Endpoints)
│   ├── function.py         # Database CRUD & Utility functions
│   └── personal_schedule.db # SQLite Database (Tự tạo khi chạy)
├── dynamic_test_case/      # Module sinh Test Case tự động
│   └── create_testcase.py  # Script tạo file test markdown
├── models/                 # Chứa Model AI (Vietnamese Correction)
├── songs/                  # File âm thanh thông báo (.mp3)
├── frontend.py             # Giao diện chính (Streamlit)
├── README.md
└── requirements.txt
```

## API Documentation

Hệ thống sử dụng FastAPI, bạn có thể xem tài liệu chi tiết tại `http://127.0.0.1:8000/docs` sau khi chạy backend. Các endpoint chính:

### NLP & Schedule Processing

  - `POST /predict` - Phân tích câu lệnh tiếng Việt, trích xuất thông tin và kiểm tra trùng lịch.
  - `POST /update` - Phân tích lại câu lệnh khi chỉnh sửa sự kiện.

## Chạy Tests

Để kiểm tra độ chính xác của mô hình AI với các trường hợp khó (viết tắt, không dấu, thời gian phức tạp):

```bash

cd dynamic_test_case
python create_testcase.py
```

Kết quả sẽ được xuất ra file `dynamic_test_case.md` chứa bảng so sánh Input và Expected Output.

## Sinh viên thực hiện

  - Sinh viên thực hiện: Phạm Tấn Khương
  - MSSV: 3122410191

## Lưu ý
  Vì không muốn bị sao chép code, nên mã nguồn của dự án trong link github này không thể tải về được.
  Thây cô hoặc bạn nào có nhu cầu muốn tải và xem code của em. Vui lòng liên hệ email sau: tankhuongpham35@gmail.com.
