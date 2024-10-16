---
title: "MQTT Test ESP32"
weight: 4
chapter: false
pre: " <b> 2.4. </b> "
---

We will use the ESP32 to test the connection between the device and AWS IoT Core.

### 1. First, we need to obtain the endpoint information of the MQTT broker.

We go to the AWS shell and run the following command:

    aws iot describe-endpoint

We will receive information as follows:

![Overview](/fcj-ss2-workshop-003/images/28.png)

This is the endpoint information of the MQTT broker that we will use to connect to AWS IoT Core.

### 2. In the `main.py` file, we will fill in the cert information as follows:

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
        
    time.sleep(30) # Wait for 30 seconds before taking the next reading
```

When we run the main.py file on the ESP32, we will see the temperature and humidity information displayed on the LCD and also published to the test topic on AWS IoT Core.

![Overview](/fcj-ss2-workshop-003/images/29.png)

We check on the MQTT test client, and we will see the message published to the **test** topic.
![Overview](/fcj-ss2-workshop-003/images/30.png)

Good job!

Now you can change the topic information and publish different messages to that topic.