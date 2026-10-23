# BOSCH — BEA CAN Communication & Diagnostic

Project thực hành hệ thống nhúng với **STM32F405RGT6**, giao tiếp **CAN/UART** và công cụ chẩn đoán **Python/Tkinter**.

## Thành phần

| Đường dẫn | Nội dung |
| --- | --- |
| `03_BEA_BasicConfiguredSourceCode/` | Firmware STM32, cấu hình STM32CubeIDE, HAL/CMSIS và linker scripts. |
| `01_Diagnostic/BEA2026_Diag_Checker/` | Ứng dụng desktop gửi/nhận dữ liệu qua cổng serial và thực hiện các dịch vụ chẩn đoán. |
| `01_Diagnostic/` | Tài liệu bài thực hành chẩn đoán và sơ đồ hệ thống. |
| `02_Communication/` | Tài liệu bài thực hành giao tiếp CAN. |
| `BEA_pratical_tool_Installation_guide.docx` | Tài liệu hướng dẫn cài đặt công cụ. |
| `BEA_CAN2CAN_DEMO_TEN1HC_HUST.hex` | Firmware HEX có sẵn trong tài liệu gốc. |

## Chức năng trong mã nguồn

- Giao tiếp CAN1/CAN2 và xử lý dữ liệu qua UART.
- Kiểm tra dữ liệu CAN bằng counter/checksum.
- Các dịch vụ chẩn đoán `0x22` (Read Data By Identifier), `0x27` (Security Access) và `0x2E` (Write Data By Identifier).
- Đọc nhiệt độ, đọc CAN ID và xử lý yêu cầu thay đổi CAN ID.
- Công cụ Python có giao diện chọn cổng COM, baud rate, dữ liệu dạng String/Hex và nhật ký TX/RX.

Đây là mô tả dựa trên mã nguồn; hoạt động thực tế cần kiểm tra với bo mạch và thiết bị CAN/serial tương ứng.

## Chạy công cụ chẩn đoán trên Windows

Yêu cầu: **Python 3.12**, có Tcl/Tk, và driver cho thiết bị USB-to-serial.

Mở PowerShell tại thư mục gốc project:

```powershell
cd 01_Diagnostic/BEA2026_Diag_Checker
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe BEA_DiagChecker.py
```

Kết nối thiết bị, chọn cổng COM và baud rate phù hợp. Firmware hiện cấu hình UART **115200 baud, 8N1**. Xem thêm [README của công cụ](01_Diagnostic/BEA2026_Diag_Checker/README.md); các đường dẫn ổ đĩa tuyệt đối trong tài liệu đó là ví dụ của môi trường ban đầu.

### Chạy kiểm thử Python

Tại `01_Diagnostic/BEA2026_Diag_Checker/`:

```powershell
.\.venv\Scripts\python.exe -m pip install pytest
.\.venv\Scripts\python.exe -m pytest
```

Các kiểm thử có sẵn dùng kết nối serial giả lập, không cần bo mạch.

## Mở và build firmware

1. Cài STM32CubeIDE và công cụ/driver cần thiết theo tài liệu đi kèm.
2. Import project có sẵn từ thư mục `03_BEA_BasicConfiguredSourceCode/`.
3. Kiểm tra target **STM32F405RGT6**, cấu hình build và kết nối phần cứng.
4. Build project, sau đó nạp firmware bằng công cụ phù hợp với bo mạch.

File `.ioc` được giữ nguyên từ project gốc. Kiểm tra cấu hình so với mã nguồn hiện tại trước khi dùng tính năng sinh lại mã. File HEX đi kèm chưa được xác minh là kết quả build của phiên bản mã nguồn hiện tại.

## Tệp và giấy phép

- `.gitignore` loại trừ build output, môi trường Python, cache, log và tệp tạm Office.
- Tài liệu, firmware HEX và các tệp cấu hình STM32CubeIDE được giữ lại.
- Các thông báo bản quyền và giấy phép của STMicroelectronics/Arm trong `Drivers/` được giữ nguyên. Kho này không bổ sung giấy phép chung cho toàn bộ nội dung.
