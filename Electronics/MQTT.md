Great, this is a **classic ESP32 ↔ Ubuntu Mosquitto MQTT lab setup** 
I’ll give you **working, minimal, and expandable code** with **clear explanations**, assuming:

- **ESP32** using **Arduino framework**
    
- **Mosquitto broker** running on **Ubuntu**
    
- **Potentiometer → ESP32 ADC**
    
- **LED control from Ubuntu → ESP32 via MQTT**
    

---

## 1️⃣ System Architecture (Clear Mental Model)

```
Potentiometer
     ↓
   ESP32  ---- publish ---->  Mosquitto (Ubuntu)
     ↑                           |
     |---- subscribe <-----------|
           LED ON / OFF command
```

### Topics Used

|Purpose|Topic|
|---|---|
|Potentiometer value|`esp32/pot`|
|LED control|`esp32/led`|

---

## 2️⃣ Ubuntu: Mosquitto Broker Setup (Quick Check)

Make sure Mosquitto is running:

```bash
sudo systemctl status mosquitto
```

Find Ubuntu IP (important):

```bash
ip a
```

Example:

```
192.168.1.100
```

👉 Use this IP in ESP32 code.

Test manually:

```bash
mosquitto_sub -t esp32/pot
mosquitto_pub -t esp32/led -m "ON"
mosquitto_pub -t esp32/led -m "OFF"
```

---

## 3️⃣ ESP32 MQTT Publisher + Subscriber Code

### 🔧 Connections

|Component|ESP32 Pin|
|---|---|
|Potentiometer|GPIO 34 (ADC)|
|LED|GPIO 2|

---

## 4️⃣ Required Arduino Libraries

Install from **Arduino Library Manager**:

- **WiFi**
    
- **PubSubClient** (by Nick O’Leary)
    

---

## 5️⃣ Complete ESP32 Code (Publisher + Subscriber)

```cpp
#include <WiFi.h>
#include <PubSubClient.h>

/* WiFi Credentials */
const char* ssid = "YOUR_WIFI_NAME";
const char* password = "YOUR_WIFI_PASSWORD";

/* MQTT Broker (Ubuntu IP) */
const char* mqtt_server = "192.168.1.100";

/* Topics */
const char* pot_topic = "esp32/pot";
const char* led_topic = "esp32/led";

/* Hardware Pins */
#define POT_PIN 34
#define LED_PIN 2

WiFiClient espClient;
PubSubClient client(espClient);

/* MQTT Callback */
void callback(char* topic, byte* message, unsigned int length)
{
  String msg = "";
  for (int i = 0; i < length; i++)
    msg += (char)message[i];

  Serial.print("Message received: ");
  Serial.println(msg);

  if (String(topic) == led_topic)
  {
    if (msg == "ON")
      digitalWrite(LED_PIN, HIGH);
    else if (msg == "OFF")
      digitalWrite(LED_PIN, LOW);
  }
}

/* WiFi Connection */
void setup_wifi()
{
  delay(10);
  Serial.println("Connecting to WiFi...");
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }

  Serial.println("\nWiFi connected");
  Serial.print("ESP32 IP: ");
  Serial.println(WiFi.localIP());
}

/* MQTT Reconnect */
void reconnect()
{
  while (!client.connected())
  {
    Serial.print("Connecting to MQTT...");
    if (client.connect("ESP32Client"))
    {
      Serial.println("connected");
      client.subscribe(led_topic);
    }
    else
    {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      delay(2000);
    }
  }
}

void setup()
{
  Serial.begin(115200);

  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, LOW);

  setup_wifi();

  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
}

void loop()
{
  if (!client.connected())
    reconnect();

  client.loop();

  int potValue = analogRead(POT_PIN);

  char potString[8];
  itoa(potValue, potString, 10);

  client.publish(pot_topic, potString);

  Serial.print("Potentiometer Value: ");
  Serial.println(potValue);

  delay(1000);
}
```

---

## 6️⃣ Ubuntu: Control LED from Terminal

### Subscribe to pot value:

```bash
mosquitto_sub -t esp32/pot
```

### Turn LED ON:

```bash
mosquitto_pub -t esp32/led -m "ON"
```

### Turn LED OFF:

```bash
mosquitto_pub -t esp32/led -m "OFF"
```

---

## 7️⃣ MQTT Concepts Used (Important for Exams & Interviews)

|Concept|Where Used|
|---|---|
|Publisher|ESP32 → pot value|
|Subscriber|ESP32 → LED topic|
|Broker|Mosquitto (Ubuntu)|
|Callback|`client.setCallback()`|
|QoS|Default QoS 0 (fast & simple)|

---

## 8️⃣ How to Increase Project Complexity (Next Steps)

Since you’re doing **Embedded + IoT + Edge computing**, you can extend this into:

- ✔ JSON payload instead of raw values
    
- ✔ QoS 1 for reliable delivery
    
- ✔ Node-RED dashboard on Ubuntu
    
- ✔ Multiple ESP32 nodes
    
- ✔ Add timestamp from Ubuntu
    
- ✔ Store pot data in InfluxDB / SQLite
    
- ✔ Secure MQTT with username/password
    

---

If you want next:  
👉 **Node-RED dashboard**  
👉 **QoS 1 & retained messages**  
👉 **Secure MQTT (username/password)**  
👉 **ESP32 + FreeRTOS MQTT task separation**

Just tell me 👍