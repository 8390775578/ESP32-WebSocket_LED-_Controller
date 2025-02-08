ESP32 WebSocket LED Controller

flow to run this code 

step 1) Build the Project:     
         a) Run idf.py build to build the project.   
         b)For a new project, 
         c)Use idf.py create-project project1.
step 2) idf.py menuconfig (this should be in code file directory)
        a)GUI will open 
        b)Navigate to EXAMPLE CONNECTION CONFIGURATION and set the WiFi SSID (WiFi name) and WiFi Password (Ensure you use the correct WiFi credentials,            as they are case-sensitive).
step 3)idf.py set-target esp32s3/esp32
step 4) idf.py flash
step 5) idf.py monitor

  a)In the output, you will receive an IPv4 address (e.g., XXX.XXX.XXX.XXX).
  b)Copy and paste this IP address into your browser’s URL bar and press Enter.
  c)In the same URL, append /ws at the end (e.g., XXX.XXX.XXX.XXX/ws) and press Enter.
  d)If the connection is successful, you should see confirmation. Copy XXX.XXX.XXX.XXX/ws and paste it into Postman WebSocket or a Simple WebSocket      Client extension.
step 6) Now you are ready to go          


This project implements a WebSocket Echo Server on an ESP32, allowing users to control an LED remotely via WebSocket messages. The ESP32 connects to a network and listens for WebSocket messages to toggle the LED on or off.

## Features
- WebSocket server running on ESP32
- Echo functionality (sends received messages back)
- LED control via WebSocket commands:
  - Send "start" → Turns LED **ON**
  - Send "stop" → Turns LED **OFF**

## Requirements
- ESP32 Development Board
- ESP-IDF installed and configured
- A WebSocket client (e.g., a web app or tool like **WebSocket King**, **Postman**, or **Python WebSocket Client**)
- Wi-Fi connection



## Setup & Compilation

### 1. Install ESP-IDF
Follow the official ESP-IDF setup guide:
https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/

### 2. Clone This Repository
```
git clone https://github.com/your-repo/esp32-ws-led.git
cd esp32-ws-led
```

### 3. Configure the Project
Set up your Wi-Fi credentials:
```
idf.py menuconfig
```
Navigate to **Example Connection Configuration** and enter your Wi-Fi SSID & Password.

### 4. Build and Flash
```
idf.py build flash monitor
```
This will compile and upload the firmware to the ESP32.

## WebSocket API

| Command | Action |
|---------|--------|
| "start" | Turns LED **ON** |
| "stop"  | Turns LED **OFF** |

You can use a WebSocket client to send these messages to:
```
ws://<ESP32_IP>/ws
```

## Example WebSocket Client (Python)
```python
import websocket

ws = websocket.WebSocket()
ws.connect("ws://<ESP32_IP>/ws")

ws.send("start")  # Turn LED ON
print(ws.recv())  # Response from ESP32

ws.send("stop")   # Turn LED OFF
print(ws.recv())

ws.close()
```

## License
This project is in the **Public Domain (CC0 licensed)** – use, modify, and distribute freely.

