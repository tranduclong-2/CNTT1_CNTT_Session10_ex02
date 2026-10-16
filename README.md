# CNTT1_CNTT_Session10_ex02
## Phần 1: Báo cáo phân tích (I/O)
- Input (Văn bản thô): Yêu cầu kỹ thuật, mã nguồn điều khiển thiết bị, thông số cấu hình cảm biến và các bước kiểm tra phần cứng.
- Output (Giao diện render chuyên nghiệp): Giao diện tài liệu trên GitHub hiển thị trực quan các khối mã Python có màu sắc, bảng biểu so sánh thiết bị rõ ràng và danh sách kiểm tra (Task List) tương tác.
## Phần 2: Source code
1. Mã nguồn python                                                                                                                                                            
```python
import time
import Adafruit_DHT
import RPi.GPIO as GPIO

CAM_BIEN = Adafruit_DHT.DHT22
CHAN_DATA = 4        # chân nối dây DATA của cảm biến
CHAN_BOM = 17        # chân nối relay máy bơm
NGUONG_THAP = 60     # độ ẩm dưới 60% thì bật bơm

GPIO.setmode(GPIO.BCM)
GPIO.setup(CHAN_BOM, GPIO.OUT)

try:
    while True:
        do_am, nhiet_do = Adafruit_DHT.read_retry(CAM_BIEN, CHAN_DATA)

        if do_am is None:
            print("Không đọc được cảm biến")
        elif do_am < NGUONG_THAP:
            GPIO.output(CHAN_BOM, GPIO.HIGH)
            print(f"Độ ẩm {do_am:.1f}% -> BẬT máy bơm")
        else:
            GPIO.output(CHAN_BOM, GPIO.LOW)
            print(f"Độ ẩm {do_am:.1f}% -> TẮT máy bơm")

        time.sleep(10)   # chờ 10 giây rồi đo lại
except KeyboardInterrupt:
    print("Dừng chương trình")
finally:
    GPIO.cleanup()
```
2. Bảng so sánh

| Tiêu chí | Cảm biến cũ DHT11 | Cảm biến mới DHT22 |
|---|---|---|
| Đo nhiệt độ | 0–50°C | -40–80°C |
| Đo độ ẩm | 20–80% RH | 0–100% RH |
| Độ chính xác độ ẩm | Khoảng ±5% RH | Khoảng ±2–5% RH |
| Độ chính xác nhiệt độ | Khoảng ±2°C | Khoảng ±0,5°C |
| Giá thành | Rẻ hơn | Đắt hơn |
| Ứng dụng | Theo dõi cơ bản | Theo dõi trang trại cần độ chính xác cao hơn |


## 6. Task List kiểm tra thiết bị

- [x] Chuẩn bị cảm biến DHT22 và Raspberry Pi
- [x] Kiểm tra dây nối và nguồn điện
- [ ] Cài đặt thư viện `Adafruit_DHT`
- [ ] Kết nối cảm biến với Raspberry Pi
- [ ] Chạy thử chương trình Python
- [ ] Kiểm tra dữ liệu nhiệt độ và độ ẩm
- [ ] Kiểm tra hoạt động của máy bơm
- [ ] Hoàn tất kiểm tra hệ thống



