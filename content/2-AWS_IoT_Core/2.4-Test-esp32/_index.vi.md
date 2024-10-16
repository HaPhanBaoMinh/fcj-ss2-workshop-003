---
title: "MQTT test ESP32"
weight: 4
chapter: false
pre: " <b> 2.4. </b> "
---

Chúng ta sẽ sử dụng ESP32 để test kết nối giữa thiết bị và AWS IoT Core.


### 1. Đầu tiên chúng ta cần lấy thông tin về endpoint của MQTT broker.

Chúng ta vào aws shell và chạy lệnh sau:

    aws iot describe-endpoint

Ta sẽ nhận được thông tin như sau:

![Overview](/fcj-ss2-workshop-003/images/28.png)

Đây là thông tin endpoint của MQTT broker mà chúng ta sẽ sử dụng để kết nối với AWS IoT Core.

### 2. Ở file main.py chúng ta điền thông tin cert như sau:

```python
import network
import time
from machine import Pin, I2C
import dht
import ujson
from umqtt.simple import MQTTClient
from i2c_lcd import I2cLcd  # Import the custom I2C_LCD class
import ussl as ssl

# MQTT Server Parameters
MQTT_CLIENT_ID = "ESP32-001"
MQTT_BROKER    = "a23sutvtpz6muq-ats.iot.ap-southeast-1.amazonaws.com"
MQTT_TOPIC     = "test"

# DHT22 sensor setup
sensor = dht.DHT22(Pin(15))

# I2C and LCD setup (adjust the I2C address if necessary)
i2c = I2C(0, sda=Pin(21), scl=Pin(22), freq=400000)  # SDA to pin 27, SCL to pin 26
I2C_ADDR = 0x27  # Default I2C address for the LCD
lcd = I2cLcd(i2c, I2C_ADDR, 2, 16)  # Assuming a 16x2 LCD

# Private key and certificate (paste the contents here as strings)
key_data = """
-----BEGIN RSA PRIVATE KEY-----

-----END RSA PRIVATE KEY-----
"""

cert_data = """
-----BEGIN CERTIFICATE-----

-----END CERTIFICATE-----
"""

ca_data = """
-----BEGIN CERTIFICATE-----

-----END CERTIFICATE-----
"""

# WiFi connection
print("Connecting to WiFi", end="")
sta_if = network.WLAN(network.STA_IF)
sta_if.active(True)
sta_if.connect('Wokwi-GUEST', '')
while not sta_if.isconnected():
    print(".", end="")
    time.sleep(0.1)
print(" Connected!")

# MQTT setup
print("Connecting to MQTT server... ", end="")

ssl_params = {
    'key': key_data,
    'cert': cert_data,
    'cadata':ca_data
}
client = MQTTClient(
    MQTT_CLIENT_ID, 
    MQTT_BROKER, 
    ssl=True,
    ssl_params=ssl_params,
    port=8883
)

client.connect()

print("Connected!")

# Display welcome message on LCD
lcd.clear()
lcd.putstr("Weather Station")
time.sleep(2)

prev_weather = ""
while True:
    print("Measuring weather conditions... ", end="")
    sensor.measure() 
    temp = sensor.temperature()
    humidity = sensor.humidity()

    timestamp = time.time()
    
    # Format the message for MQTT
    message = ujson.dumps({
        "temp": temp,
        "humidity": humidity,
        "device_id": device_id,
        "timestamp": timestamp
    })
    
    # Display temperature and humidity on the LCD
    lcd.clear()
    lcd.putstr("Temp: {:.1f} C".format(temp))
    lcd.move_to(0, 1)
    lcd.putstr("Humidity: {:.1f}%".format(humidity))
    
    # Publish to MQTT if there is a change in the readings
    print("Updated!")
    print("Reporting to MQTT topic {}: {}".format(MQTT_TOPIC, message))
    client.publish(MQTT_TOPIC, message)
    prev_weather = message
        
    time.sleep(30) # Wait for 5 seconds before taking the next reading
```
Khi chúng ta chạy file main.py trên ESP32 thì chúng ta sẽ thấy thông tin về nhiệt độ và độ ẩm được hiển thị trên LCD và cũng được publish lên topic **test** trên AWS IoT Core.

![Overview](/fcj-ss2-workshop-003/images/29.png)

Chúng ta kiểm tra trên MQTT test client thì chúng ta sẽ thấy message được publish lên topic **test**.

![Overview](/fcj-ss2-workshop-003/images/30.png)

Good job!

Bây giờ bạn có thể đổi thông tin topic và publish message khác lên topic đó.