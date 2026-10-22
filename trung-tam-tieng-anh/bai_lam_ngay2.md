# BÀI LÀM – ÔN TẬP NGÀY 2

- **Họ tên: Tran Xuan Nhat**
- **Lớp: HN-KS26-CNTT3**
- **Link repository:**
- **Hệ điều hành (Windows/macOS): Windows**

## Bài 1. Lọc log thủ công

### Lệnh đã chạy

```shell
Get-Content logs/access.log | Select-String "ERROR" > logs/error_report.txt

```

### 2 dòng lỗi đầu tiên trong error_report.txt

```text
2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)

```

## Bài 2. Đếm bằng pipeline

### Lệnh

```shell
Get-Content logs/access.log | Select-String "WARNING" | Measure-Object -Line
Get-Content logs/payment.log | Select-String "ERROR" | Measure-Object -Line

```

### Kết quả đếm (Windows: giá trị Count; macOS: con số in ra)

```text
WARNING trong access.log: 4
ERROR trong payment.log: 3
```

## Bài 3. Chạy script auto_warning (.ps1 hoặc .sh)

### Lệnh chạy (Windows: nếu dùng Phụ lục 2 thì ghi cả 2 lệnh)

```shell
# Script: auto_warning.ps1
# Tac gia: TRAN XUAN NHAT
# Ngay tao: 21/10/2026

Write-Host "Dang loc canh bao thanh toan..."
"=== CANH BAO THANH TOAN ===" > logs/warning_report.txt
Get-Content HOAN_THIEN | Select-String "WARNING" >> logs/warning_report.txt

Write-Host "Hoan thanh!"

```

### Nội dung file logs/warning_report.txt

```text
=== CANH BAO THANH TOAN ===

2025-10-18 09:19:13 [WARNING] Cong thanh toan phan hoi cham
2025-10-18 09:28:16 [WARNING] Nhieu lan nhap sai ma OTP
2025-10-18 09:43:01 [WARNING] So du vi gan bang hoc phi
2025-10-18 09:46:22 [WARNING] So du vi gan bang hoc phi
2025-10-18 09:49:43 [WARNING] So du vi gan bang hoc phi

```

## Bài 4. Báo cáo tổng hợp

### Các lệnh đã chạy

```shell
"=== TONG HOP ACCESS LOG ===" > logs/tong_hop_ngay2.txt
Get-Content logs/access.log | Select-String "ERROR" >> logs/tong_hop_ngay2.txt
Get-Content logs/payment.log | Select-String "WARNING" | Measure-Object -Line | Select-Object -ExpandProperty Lines >> logs/tong_hop_ngay2.txt

```

### Nội dung file logs/tong_hop_ngay2.txt

```text
=== TONG HOP ACCESS LOG ===

2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:33:51 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:37:19 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:49:43 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:53:11 [ERROR] Het thoi gian cho (timeout)

```

## Bài 5. Câu hỏi ngắn

- **a)Lệnh >file dùng để ghi đè nội dung nếu file đã có dữ liệu thì dữ liệu cũ sẽ bị thay bằng dữ liệu mới. Lệnh >>file dùng để ghi nối tiếp dữ liệu mới vào cuối file mà không làm mất đi nội dung cũ.**
- **b)Nếu câu lệnh thứ hai dùng >, tệp tong_hop_ngay2.txt sẽ bị xóa mất dòng === TONG HOP ACCESS LOG === vừa tạo ở lệnh trước, file lúc này chỉ còn lại các dòng log chứa ERROR.**
- **c)Dùng đường dẫn tương đối giúp script linh hoạt. Khi chia sẻ thư mục dự án sang máy tính của người khác hoặc đẩy lên máy chủ, hoạt động chính xác mà không bị lỗi "sai đường dẫn tuyệt đối"**

## Tự chấm (điền sau khi có đáp án)

- **Điểm tự chấm:** ..../100
- **Lỗi mình đã mắc và cách sửa:**
