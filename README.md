# IoT-Chatbot
An IoT Chatbot to access the peripherals of the GrovePi starter kit

# Setting up the Raspberry Pi

## 1. Download current raspbian and install on SD Card (see tutorial from raspbian install on your OS)

## 2. Configure Raspbian with
- camera on
- right locale (de/vienna)
- right timezone (at/vienna)
- right wlan (at)
- set default hostname to (tjbot-xx) where xx is your short name
- leave pi as your username
- set new default password
- reboot

## 3. upgrade raspbian
- sudo apt-get update
- sudo apt-get install
- sudo apt-get upgrade
- sudo apt-get dist-upgrade

## 4. install tools and addons (if needed)
- sudo apt install -y tightvncserver
- sudo apt install -y xrdp
- sudo apt install -y samba
- sudo reboot

## 5. upgrade nodejs to v6 LTS and NPM 3 and current Node-Red (with node-red update script)
- update-nodejs-and-nodered

## 6.1. manual update to 6.x -- if needed  (for newest informations look on nodejs webpage)
- curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
- sudo apt install nodejs

## 6.2. manual update to 7.x -- if needed  (for newest informations look on nodejs webpage)
- curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
- sudo apt install nodejs

## 7. check if tools are most current (for micro, sound, camera, ..)
- sudo apt-get install git
- sudo apt-get install python-picamera
- sudo apt-get install python-dev python-rpi.gpio
- sudo apt-get install alsa-base alsa-utils
- sudo apt-get install libasound2-dev
- npm install -g node-red-admin

## 8. install nodes for nodered
- node-red-start
- node-red-stop
- ln -s ~/.node-red ~/node-red-data
- cd ~/node-red-data
- npm install node-red-contrib-speakerpi
- npm install node-red-contrib-micropi
- npm install node-red-contrib-camerapi
- npm install node-red-contrib-ibm-watson-iot
- npm install node-red-contrib-browser-utils
- npm install node-red-contrib-facebook        
- npm install node-red-contrib-facebook-messenger-writer 
- npm install node-red-contrib-play-audio     
- npm install node-red-node-google
- npm install node-red-contrib-twitter
- npm install node-red-contrib-cognitive-services         
- npm install node-red-contrib-twitter-stream
- npm install node-red-contrib-facebook                   
- npm install node-red-contrib-twitter-text
- npm install node-red-node-watson

## 9. Install grovepi+
http://www.dexterindustries.com/GrovePi/get-started-with-the-grovepi/setting-software/
cd ~
mkdir Git
cd Git
git clone https://github.com/DexterInd/GrovePi
cd GrovePi/Script
sudo chmod +x install.sh
sudo ./install.sh

### Check grovepi+ board
sudo i2cdetect -y 1
-- if brings 04 - means that grovepi+ board has been detected

### test green light (plug into D4 the green light)
### see also http://www.dexterindustries.com/GrovePi/engineering/python-library-documentation/
cd GrovePi/Software/Python
python grove_led_blink.py

### Additional Setup - Boot with LCD (placed on I2C-1) & IPAdresse on Display
sudo apt-get install python-netifaces
cd ~/Git
git clone https://github.com/O-Hahn/RaspiTools.git

## 10. Systemctl - Startup Script
### Bring IP Adress on the LCD Display
sudo nano /lib/systemd/system/myinit.service

### Insert followin into the editor
[Unit]
Description=My Startup Service
After=multi-user.target

[Service]
Type=idle
ExecStart=/usr/bin/python /home/pi/Git/RaspiTools/myinit.py

[Install]
WantedBy=multi-user.target

## 11. Make mystartup.py executable and insert into daemon
- sudo chmod 644 /lib/systemd/system/myinit.service
- sudo systemctl daemon-reload
- sudo systemctl enable myinit.service

# References
- http://thisdavej.com/beginners-guide-to-installing-node-js-on-a-raspberry-pi/
- https://www.sunfounder.com/wiki/index.php?title=To_use_USB_mini_microphone_on_Raspbian
z. additional
- http://tutorials-raspberrypi.com/raspberry-pi-ultrasonic-sensor-hc-sr04/
- http://tutorials-raspberrypi.com/library-installation-for-multiline-m-x-n-max7219-led-matrices/
- http://tutorials-raspberrypi.de/led-dot-matrix-zusammenbau-und-installation/
- http://tutorials-raspberrypi.de/raspberry-pi-luftfeuchtigkeit-temperatur-messen-dht11-dht22/




