---
title: "Các thư viện cần thiết"
weight: 2
chapter: false
pre: " <b> 1.2 </b> "
---

![Overview](/images/08.png)

## Các file code để giao tiếp với màn hình.

1. Chúng ta tạo một file `i2c_lcd.py`:

```python
"""Implements a HD44780 character LCD connected via PCF8574 on I2C. 
   This was tested with: https://www.wemos.cc/product/d1-mini.html""" 
from lcd_api import LcdApi 
from machine import I2C 
from time import sleep_ms 
# The PCF8574 has a jumper selectable address: 0x20 - 0x27 
#DEFAULT_I2C_ADDR = 0x20 
# Defines shifts or masks for the various LCD line attached to the PCF8574 
MASK_RS = 0x01 
MASK_RW = 0x02 
MASK_E = 0x04 
SHIFT_BACKLIGHT = 3 
SHIFT_DATA = 4 
class I2cLcd(LcdApi): 
    """Implements a HD44780 character LCD connected via PCF8574 on I2C.""" 
    def __init__(self, i2c, i2c_addr, num_lines, num_columns): 
        self.i2c = i2c 
        self.i2c_addr = i2c_addr 
        self.i2c.writeto(self.i2c_addr, bytearray([0])) 
        sleep_ms(20)   # Allow LCD time to powerup 
        # Send reset 3 times 
        self.hal_write_init_nibble(self.LCD_FUNCTION_RESET) 
        sleep_ms(5)    # need to delay at least 4.1 msec 
        self.hal_write_init_nibble(self.LCD_FUNCTION_RESET) 
        sleep_ms(1) 
        self.hal_write_init_nibble(self.LCD_FUNCTION_RESET) 
        sleep_ms(1) 
        # Put LCD into 4 bit mode 
        self.hal_write_init_nibble(self.LCD_FUNCTION) 
        sleep_ms(1) 
        LcdApi.__init__(self, num_lines, num_columns) 
        cmd = self.LCD_FUNCTION 
        if num_lines > 1: 
            cmd |= self.LCD_FUNCTION_2LINES 
        self.hal_write_command(cmd) 
    def hal_write_init_nibble(self, nibble): 
        """Writes an initialization nibble to the LCD. 
        This particular function is only used during initialization. 
        """ 
        byte = ((nibble >> 4) & 0x0f) << SHIFT_DATA 
        self.i2c.writeto(self.i2c_addr, bytearray([byte | MASK_E])) 
        self.i2c.writeto(self.i2c_addr, bytearray([byte])) 
    def hal_backlight_on(self): 
        """Allows the hal layer to turn the backlight on.""" 
        self.i2c.writeto(self.i2c_addr, bytearray([1 << SHIFT_BACKLIGHT])) 
    def hal_backlight_off(self): 
        """Allows the hal layer to turn the backlight off.""" 
        self.i2c.writeto(self.i2c_addr, bytearray([0])) 
    def hal_write_command(self, cmd): 
        """Writes a command to the LCD. 
        Data is latched on the falling edge of E. 
        """ 
        byte = ((self.backlight << SHIFT_BACKLIGHT) | (((cmd >> 4) & 0x0f) << SHIFT_DATA)) 
        self.i2c.writeto(self.i2c_addr, bytearray([byte | MASK_E])) 
        self.i2c.writeto(self.i2c_addr, bytearray([byte])) 
        byte = ((self.backlight << SHIFT_BACKLIGHT) | ((cmd & 0x0f) << SHIFT_DATA)) 
        self.i2c.writeto(self.i2c_addr, bytearray([byte | MASK_E])) 
        self.i2c.writeto(self.i2c_addr, bytearray([byte])) 
        if cmd <= 3: 
            # The home and clear commands require a worst case delay of 4.1 msec 
            sleep_ms(5) 
    def hal_write_data(self, data): 
        """Write data to the LCD.""" 
        byte = (MASK_RS | (self.backlight << SHIFT_BACKLIGHT) | (((data >> 4) & 0x0f) << SHIFT_DATA)) 
        self.i2c.writeto(self.i2c_addr, bytearray([byte | MASK_E])) 
        self.i2c.writeto(self.i2c_addr, bytearray([byte])) 
        byte = (MASK_RS | (self.backlight << SHIFT_BACKLIGHT) | ((data & 0x0f) << SHIFT_DATA)) 
        self.i2c.writeto(self.i2c_addr, bytearray([byte | MASK_E])) 
        self.i2c.writeto(self.i2c_addr, bytearray([byte]))
```

2. Chúng ta tạo một file `lcd_api.py`:

```python
"""Provides an API for talking to HD44780 compatible character LCDs.""" 
import time 
class LcdApi: 
    """Implements the API for talking with HD44780 compatible character LCDs. 
    This class only knows what commands to send to the LCD, and not how to get 
    them to the LCD. 
    It is expected that a derived class will implement the hal_xxx functions. 
    """ 
    # The following constant names were lifted from the avrlib lcd.h 
    # header file, however, I changed the definitions from bit numbers 
    # to bit masks. 
    # 
    # HD44780 LCD controller command set 
    LCD_CLR = 0x01              # DB0: clear display 
    LCD_HOME = 0x02             # DB1: return to home position 
    LCD_ENTRY_MODE = 0x04       # DB2: set entry mode 
    LCD_ENTRY_INC = 0x02        # --DB1: increment 
    LCD_ENTRY_SHIFT = 0x01      # --DB0: shift 
    LCD_ON_CTRL = 0x08          # DB3: turn lcd/cursor on 
    LCD_ON_DISPLAY = 0x04       # --DB2: turn display on 
    LCD_ON_CURSOR = 0x02        # --DB1: turn cursor on 
    LCD_ON_BLINK = 0x01         # --DB0: blinking cursor 
    LCD_MOVE = 0x10             # DB4: move cursor/display 
    LCD_MOVE_DISP = 0x08        # --DB3: move display (0-> move cursor) 
    LCD_MOVE_RIGHT = 0x04       # --DB2: move right (0-> left) 
    LCD_FUNCTION = 0x20         # DB5: function set 
    LCD_FUNCTION_8BIT = 0x10    # --DB4: set 8BIT mode (0->4BIT mode) 
    LCD_FUNCTION_2LINES = 0x08  # --DB3: two lines (0->one line) 
    LCD_FUNCTION_10DOTS = 0x04  # --DB2: 5x10 font (0->5x7 font) 
    LCD_FUNCTION_RESET = 0x30   # See "Initializing by Instruction" section 
    LCD_CGRAM = 0x40            # DB6: set CG RAM address 
    LCD_DDRAM = 0x80            # DB7: set DD RAM address 
    LCD_RS_CMD = 0 
    LCD_RS_DATA = 1 
    LCD_RW_WRITE = 0 
    LCD_RW_READ = 1 
    def __init__(self, num_lines, num_columns): 
        self.num_lines = num_lines 
        if self.num_lines > 4: 
            self.num_lines = 4 
        self.num_columns = num_columns 
        if self.num_columns > 40: 
            self.num_columns = 40 
        self.cursor_x = 0 
        self.cursor_y = 0 
        self.implied_newline = False 
        self.backlight = True 
        self.display_off() 
        self.backlight_on() 
        self.clear() 
        self.hal_write_command(self.LCD_ENTRY_MODE | self.LCD_ENTRY_INC) 
        self.hide_cursor() 
        self.display_on() 
    def clear(self): 
        """Clears the LCD display and moves the cursor to the top left 
        corner. 
        """ 
        self.hal_write_command(self.LCD_CLR) 
        self.hal_write_command(self.LCD_HOME) 
        self.cursor_x = 0 
        self.cursor_y = 0 
    def show_cursor(self): 
        """Causes the cursor to be made visible.""" 
        self.hal_write_command(self.LCD_ON_CTRL | self.LCD_ON_DISPLAY | 
                               self.LCD_ON_CURSOR) 
    def hide_cursor(self): 
        """Causes the cursor to be hidden.""" 
        self.hal_write_command(self.LCD_ON_CTRL | self.LCD_ON_DISPLAY) 
    def blink_cursor_on(self): 
        """Turns on the cursor, and makes it blink.""" 
        self.hal_write_command(self.LCD_ON_CTRL | self.LCD_ON_DISPLAY | 
                               self.LCD_ON_CURSOR | self.LCD_ON_BLINK) 
    def blink_cursor_off(self): 
        """Turns on the cursor, and makes it no blink (i.e. be solid).""" 
        self.hal_write_command(self.LCD_ON_CTRL | self.LCD_ON_DISPLAY | 
                               self.LCD_ON_CURSOR) 
    def display_on(self): 
        """Turns on (i.e. unblanks) the LCD.""" 
        self.hal_write_command(self.LCD_ON_CTRL | self.LCD_ON_DISPLAY) 
    def display_off(self): 
        """Turns off (i.e. blanks) the LCD.""" 
        self.hal_write_command(self.LCD_ON_CTRL) 
    def backlight_on(self): 
        """Turns the backlight on. 
        This isn't really an LCD command, but some modules have backlight 
        controls, so this allows the hal to pass through the command. 
        """ 
        self.backlight = True 
        self.hal_backlight_on() 
    def backlight_off(self): 
        """Turns the backlight off. 
        This isn't really an LCD command, but some modules have backlight 
        controls, so this allows the hal to pass through the command. 
        """ 
        self.backlight = False 
        self.hal_backlight_off() 
    def move_to(self, cursor_x, cursor_y): 
        """Moves the cursor position to the indicated position. The cursor 
        position is zero based (i.e. cursor_x == 0 indicates first column). 
        """ 
        self.cursor_x = cursor_x 
        self.cursor_y = cursor_y 
        addr = cursor_x & 0x3f 
        if cursor_y & 1: 
            addr += 0x40    # Lines 1 & 3 add 0x40 
        if cursor_y & 2:    # Lines 2 & 3 add number of columns 
            addr += self.num_columns 
        self.hal_write_command(self.LCD_DDRAM | addr) 
    def putchar(self, char): 
        """Writes the indicated character to the LCD at the current cursor 
        position, and advances the cursor by one position. 
        """ 
        if char == '\n': 
            if self.implied_newline: 
                # self.implied_newline means we advanced due to a wraparound, 
                # so if we get a newline right after that we ignore it. 
                pass 
            else: 
                self.cursor_x = self.num_columns 
        else: 
            self.hal_write_data(ord(char)) 
            self.cursor_x += 1 
        if self.cursor_x >= self.num_columns: 
            self.cursor_x = 0 
            self.cursor_y += 1 
            self.implied_newline = (char != '\n') 
        if self.cursor_y >= self.num_lines: 
            self.cursor_y = 0 
        self.move_to(self.cursor_x, self.cursor_y) 
    def putstr(self, string): 
        """Write the indicated string to the LCD at the current cursor 
        position and advances the cursor position appropriately. 
        """ 
        for char in string: 
            self.putchar(char) 
    def custom_char(self, location, charmap): 
        """Write a character to one of the 8 CGRAM locations, available 
        as chr(0) through chr(7). 
        """ 
        location &= 0x7 
        self.hal_write_command(self.LCD_CGRAM | (location << 3)) 
        self.hal_sleep_us(40) 
        for i in range(8): 
            self.hal_write_data(charmap[i]) 
            self.hal_sleep_us(40) 
        self.move_to(self.cursor_x, self.cursor_y)
        
    def hal_backlight_on(self): 
        """Allows the hal layer to turn the backlight on. 
        If desired, a derived HAL class will implement this function. 
        """ 
        pass 
    def hal_backlight_off(self): 
        """Allows the hal layer to turn the backlight off. 
        If desired, a derived HAL class will implement this function. 
        """ 
        pass 
    def hal_write_command(self, cmd): 
        """Write a command to the LCD. 
        It is expected that a derived HAL class will implement this 
        function. 
        """ 
        raise NotImplementedError 
    def hal_write_data(self, data): 
        """Write data to the LCD. 
        It is expected that a derived HAL class will implement this 
        function. 
        """ 
        raise NotImplementedError 
    def hal_sleep_us(self, usecs): 
        """Sleep for some time (given in microseconds).""" 
        time.sleep_us(usecs)
```

3. Tạo một file `main.py` để test:

```python
import network
import time
from machine import Pin, I2C
import dht
import ujson
from umqtt.simple import MQTTClient
from i2c_lcd import I2cLcd  # Import the custom I2C_LCD class

# MQTT Server Parameters
MQTT_CLIENT_ID = "micropython-weather-demo"
MQTT_BROKER    = "broker.mqttdashboard.com"
MQTT_USER      = ""
MQTT_PASSWORD  = ""
MQTT_TOPIC     = "wokwi-weather"

# DHT22 sensor setup
sensor = dht.DHT22(Pin(15))

# I2C and LCD setup (adjust the I2C address if necessary)
i2c = I2C(0, sda=Pin(21), scl=Pin(22), freq=400000)  # SDA to pin 27, SCL to pin 26
I2C_ADDR = 0x27  # Default I2C address for the LCD
lcd = I2cLcd(i2c, I2C_ADDR, 2, 16)  # Assuming a 16x2 LCD

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
client = MQTTClient(MQTT_CLIENT_ID, MQTT_BROKER, user=MQTT_USER, password=MQTT_PASSWORD)
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
    
    # Format the message for MQTT
    message = ujson.dumps({
        "temp": temp,
        "humidity": humidity,
    })
    
    # Display temperature and humidity on the LCD
    lcd.clear()
    lcd.putstr("Temp: {:.1f} C".format(temp))
    lcd.move_to(0, 1)
    lcd.putstr("Humidity: {:.1f}%".format(humidity))
    
    # Publish to MQTT if there is a change in the readings
    if message != prev_weather:
        print("Updated!")
        print("Reporting to MQTT topic {}: {}".format(MQTT_TOPIC, message))
        client.publish(MQTT_TOPIC, message)
        prev_weather = message
    else:
        print("No change")
        
    time.sleep(2)
```

Chúng ta sẽ được kết quả như sau:

![Overview](/images/09.png)