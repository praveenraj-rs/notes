### Raspberry Pi UART/Serial communication

#### Installing dependencies in Raspberry pi:

```shell
sudo apt-get update  
sudo apt-get -y install python3-pip  
pip3 install pyserial
```
**Configuring UART:** 
```shell
	sudo raspi-config
```  
1. Select -> **interfacing options**
2. Select **serial** option to enable UART.
3. Login shell to be accessible over Serial, select **No** shown as follows.
4. Enabling Hardware Serial port, select **Yes,**
5. UART is **enabled** for Serial Communication on RX and TX pin of Raspberry Pi.
6. reboot the Raspberry Pi.

**_Code for Raspberry pi that will send and receive data from NodeMCU.(communicator.py)_**
```python
import serial
import time
if __name__ == '__main__':
    # if connected via USB cable
    ser = serial.Serial('/dev/ttyUSB0', 9600, timeout=1) #9600 is baud rate(must be same with that of NodeMCU)
    # if connected via serial Pin(RX, TX)
    ser = serial.Serial('/dev/ttyS0', 9600, timeout=1) #9600 is baud rate(must be same with that of NodeMCU)
    ser.flush()
while True:
        string = input("enter string:") #input from user
        string = string +"\n" #"\n" for line seperation
        string = string.encode('utf_8')
        ser.write(string)
        line = ser.readline().decode('utf-8').rstrip()
        print("received: ",line)
        time.sleep(1) #delay of 1 second
```

**_Here is the basic code for Node MCU which will resend/echo the data received from raspberry pi. Use arduino IDE to upload it to Node MCU._**
```c
void setup() {
  Serial.begin(9600);//here 9600 is baud rate
}
void loop() {
  if (Serial.available() > 0) { //checking data availability
    String data = Serial.readStringUntil('\n'); //reading line
    Serial.print("You sent me: "); //retransmitting
    Serial.println(data); //retransmitting
  }
}
```


### RPI To LCD

Reference: 
Youtube: https://youtu.be/ThmO6QYlhf8?si=2uK0k-bJw9Rt8YZV
Github: https://github.com/AllanGallop/RPi_GPIO_i2c_LCD
#### Step 1
Connect the LCD I2C Pins to RPI With the help of rpi pin diagrams
- Connect the VCC pin of the LCD to 5V on the Raspberry Pi.
- Connect the GND pin of the LCD to GND on the Raspberry Pi.
- Connect the SDA pin of the LCD to the SDA pin on the Raspberry Pi (GPIO2).
- Connect the SCL pin of the LCD to the SCL pin on the Raspberry Pi (GPIO3).

#### Step 2
2.1 Open the raspi-config
2.2 Enable I2C Communication
2.3 Check pin layout by running `sudo i2cdetect -y 1`

#### Step 3
Install dependencies
```shell
pip3 install RPi-GPIO-I2C-LCD
```

#### Step 4
```python
from RPi_GPIO_i2c_LCD import lcd
from time import sleep

## Address of backpack
i2c_address = 0x27

## Initalize display
lcdDisplay = lcd.HD44780(i2c_address)

## Set string value to buffer
lcdDisplay.set("Praveenraj R S",1)
lcdDisplay.set("World",2)

sleep(1)
```