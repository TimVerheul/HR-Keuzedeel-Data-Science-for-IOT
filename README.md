# HR-Keuzedeel-Data-Science-for-IOT
## Story
Living in a newly built home is notoriously known for its high humidity. This might attract insects that I don't like. Most insects only survive at a certain humid and temperature. This IoT project is made to give insight in the living condition of my bedroom by monitoring the humidity and temperature of my bedroom remotely. When the temperature or humidity get too high, I will now know when to open some windows for more ventilation. This will increase air circulation in the room and reduce the temperature.
The idea behind this project is to implement a humidity and temperature detector, DHT22 with a Raspberry Pi 4 and visualize the data with the Home app on my iPhone. With the help of Homebridge, I will be able to see the sensor data directly on my iPhone. A Python script that is constantly running will show the historical data over time. This is even more convenient with the Home app being installed on my iPhone, where accessing the readings of humidity and temperature in my bedroom is just a touch away. If the temperature and humidity are too high, I now know when to open a window in my bedroom. This will increase the living condition in my room.
## Pipeline of this IoT Project
Pipeline of this IoT project can be found in file:"My IoT Pipeline.png". The pipeline diagram depicts the problem narrated in the "Story" paragraph to solution of it.

## Things needed
### Hardware components
- Raspberry Pi 4
- 8GB or more Micro SD Card
- Breadboard 
- 3x F-M jumperwires
- DHT22 (AM2303) Humidity and Temperature sensor (The AM2303 got a resistor included) 
- Ethernet cable
- Power adapter Raspberry Pi 4 USB-C
- An IOS device with the Home app

### Software
- Python 3
- Homebridge 
- Putty
- Apple Home app (easier access with mobile phone for monitoring of humidity and temperature)

## Hardware Setup
In this section, the process of connecting DHT22 sensor to Raspberry Pi is described
### Overview of DHT22 
DHT22 is a sensor that is able to detect humidity in % and temperature in °C and °F. Refer to file:"DHT22 with numbered pins.png" for pins numbering. Pinout descriptions are as follows:
- Pin 1 = DATA, data out
- Pin 2 = VCC, power supply
- Pin 3 = GND, ground
### DHT22 and Pi Circuit
Steps to connect DHT22 to Raspberry Pi are described in this section. A circuit diagram can be found in the respiratory:"Circuit of DHT22 and Pi.png"
1. Place DHT22 at the top row of breadboard.
2. Wire Physical Pin 6 Pi(GPIO 4) to Pin 1 DHT22. (refer to black wire)
3. Wire Physical Pin 1 Pi(3v3 power) to Pin 2 DHT22. (refer to red wire)
4. Wire Physical Pin 7 Pi to Pin 3(Ground) DHT22. (refer to yellow wire)

### Preparing raspberry pi
Plug in the power adapter and the ethernet cable and connect it to the Raspberry Pi. Then, connect to the Raspberry Pi with Putty.

Now, the hardware is all connected and the next software setup can be proceeded.

## Software Setup
To setup your new Raspberry Pi, refer to "THE OFFICIAL Raspberry Pi Beginner's Guide, Chapter 2". 
1. Once it's all set and ready, let's proceed to updating the Raspberry Pi by running the following commands:
* sudo apt full-upgrade
* sudo reboot
2. First, install the prerequisites:
* sudo apt install -y build-essential tk-dev libncurses5-dev libncursesw5-dev libreadline6-dev libdb5.3-dev libgdbm-dev libsqlite3-dev libssl-dev libbz2-dev libexpat1-dev liblzma-dev zlib1g-dev libffi-dev tar wget vim
3. Now, let's install both python 3 and pip with the following command:
* sudo apt  install python3-dev python3-pip
4. Then, update the setuptools, wheel and pip of python packages to the latest version:
* sudo python3 -m pip install --upgrade pip setuptools wheel
5. Lastly, using pip to install Adafruit's DHT library to Raspberry Pi by writing the following command in the terminal. This allows Python library to interact with DHT22. 
* git clone https<span>://</span>github.com/adafruit/Adafruit_CircuitPython_DHT.git
* sudo python3 setup.py install

## Preparing Homebridge
1. Install Node.js: 
* curl -sL https<span>://</span>deb.nodesource.com/setup_14.x | sudo bash -
* sudo apt install -y nodejs gcc g++ make python net-tools
2. Install Homebridge: 
* sudo npm install -g --unsafe-perm homebridge homebridge-config-ui-x
* sudo hb-service install --user homebridge
2. Install Homebridge DHT plugin: 
* Navigate to the IP of Homebridge using: hostname -I
* Login with the username admin and the password admin
* Go to the Plugins tab and search for 'homebridge-dht' and install it
3. Configure the DHT sensor: 
* Paste the following code in the Config Editor of Homebridge:
```json
"accessories": [
        {
            "accessory": "Dht",
            "name": "Temp/Humidity Sensor",
            "service": "dht22",
            "gpio": "4"
        }
    ],
```
4. Press Save and restart Homebridge
5. The sensor should now be visible in the Accessories tab

## Running the code on the Raspberry Pi
Use Putty to run the Python file directly. The codes with comments can be found in DHT22.py in this repository. Make sure that the pins are wired like written above.

## Visualization of Data on the Raspberry Pi
Refer to file:"DHT22 sensor data visualization.png". The output will show the humidity and temperature readings of my bedroom respectively against time. 
To get the output you need to run: python dht.py

## Viewing the visualization on your Phone
To access the visualized signal data on your phone, you first need to link Homebridge with your iPhone Home app. This can be done by opening the Home app on your iPhone and scanning the QR code found at the homescreen of the Homebridge dashboard. After scanning the QR code, the accessory will be added automatically to your Home app. In the file:"HomebridgeVisualization.png" it shows the visualization of humidity and temperature readings in my bedroom at the current time. 

## Video
Refer to file "demonstration.txt" for the link to the demonstration video.
The video shows the real world prototype working and a simulation experiment is done to test the functionality of this IoT project. The humid and temperature condition in my bedroom is simulated by breathing out in the direction of the DHT22 sensor (breath contains water and is a higher temperature than the room is). This will make the humidity and temperature change temporary. The temperature and humidity is measured by the Home app and the Python script.


## Recommendation:
This project could be done better if the DHT22 is integrated directly into Raspberry Pi 4. This would make the size much smaller without the need of a breadboard.