---
title: "Cài đặt ESP32"
weight: 1
chapter: false
pre: "<b> 1.1. </b>"
---

![Overview](/fcj-ss2-workshop-003/images/02.png)

## WOKWI 

Trong bài lab này, chúng ta sẽ sử dụng Wokwi để mô phỏng việc thu thập dữ liệu từ cảm biến nhiệt độ và độ ẩm DHT11 và gửi dữ liệu lên AWS IoT Core thông qua giao thức MQTT.

## Setup thiết bị

Sau khi đã ta đã có tài khoản trên Wokwi, chúng ta tiến hành tạo một project mới.

1. Truy cập vào trang chủ của Wokwi: [https://wokwi.com/](https://wokwi.com/)
2. Đăng nhập vào tài khoản của bạn.
3. Tạo một project mới bằng cách chọn `New Project`.

![Overview](/fcj-ss2-workshop-003/images/03.png)

4. Chọn `ESP32` từ danh sách các linh kiện.

![Overview](/fcj-ss2-workshop-003/images/04.png)

5. Chọn `MicroPython`.

![Overview](/fcj-ss2-workshop-003/images/05.png)

6. Chọn `diagram.json` và paste nội dung sau vào:

![Overview](/fcj-ss2-workshop-003/images/06.png)

```json
{
  "version": 1,
  "author": "Anonymous maker",
  "editor": "wokwi",
  "parts": [
    {
      "type": "wokwi-esp32-devkit-v1",
      "id": "esp",
      "top": 137.33,
      "left": -18.01,
      "rotate": 270,
      "attrs": {}
    },
    {
      "type": "wokwi-lcd1602",
      "id": "lcd1",
      "top": 18.67,
      "left": 76,
      "attrs": { "pins": "i2c" }
    },
    { "type": "wokwi-resistor", "id": "r1", "top": 113.34, "left": -106.01, "attrs": {} },
    { "type": "wokwi-resistor", "id": "r2", "top": 130.67, "left": -106.68, "attrs": {} },
    { "type": "wokwi-dht22", "id": "dht1", "top": 182.7, "left": 205.8, "attrs": {} }
  ],
  "connections": [
    [ "esp:TX0", "$serialMonitor:RX", "", [] ],
    [ "esp:RX0", "$serialMonitor:TX", "", [] ],
    [ "lcd1:SCL", "esp:D22", "green", [ "h0" ] ],
    [ "lcd1:SDA", "esp:D21", "green", [ "h0" ] ],
    [ "lcd1:VCC", "esp:3V3", "red", [ "h-30", "v103", "h41" ] ],
    [ "lcd1:GND", "esp:GND.1", "black", [ "h-39", "v123", "h31" ] ],
    [ "r2:2", "esp:D22", "green", [ "v1", "h9" ] ],
    [ "r1:2", "esp:D21", "green", [ "v0", "h37" ] ],
    [ "r2:1", "r1:1", "green", [ "v0" ] ],
    [ "r1:1", "lcd1:VCC", "green", [ "v0" ] ],
    [ "dht1:VCC", "esp:3V3", "red", [ "v0", "h-19.2", "v-134.4", "h-105.6" ] ],
    [ "dht1:SDA", "esp:D15", "green", [ "v9.6", "h-38.3", "v-134.4", "h-119.01" ] ],
    [ "dht1:GND", "esp:GND.2", "black", [ "v19.2", "h-172.8" ] ]
  ],
  "dependencies": {}
}
```

1. Kết quả:

![Overview](/fcj-ss2-workshop-003/images/07.png)