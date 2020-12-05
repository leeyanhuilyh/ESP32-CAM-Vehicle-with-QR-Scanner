# ESP32-CAM-Vehicle-with-QR-Scanner

This repository will contain the instructions to build the vehicle, and the files that need to be uploaded to the ESP32-CAM board.

## Pre-requisites

Firstly, please download and install [PlatformIO](https://platformio.org/install/ide?install=vscode).

Then, download the files in this project and extract to any folder.

## Starting a new project on PlatformIO

Follow the official guide on [PlatformIO](https://docs.platformio.org/en/latest/integration/ide/vscode.html#quick-start) to start a new project.

Choose the "AI-Thinker ESP32-CAM" as the Board and select Arduino as the Framework.

Choose a name for your project. This would be your working directory from here onwards.

## Extracting the files into your project folder

Extract the files found in the "src" folder into your working directory's "src" folder.

Replace the platformio.ini file in your working directory with the downloaded platformio.ini file.

## Editing WiFi settings

Go to main.cpp and search for the lines:

const char* ssid = "XXXXX";
const char* password = "XXXXX";

Replace this with your WiFi Access Point credentials

(Note: the best way to ensure stable connection with your vehicle is to have your vehicle connect to your laptop's hotspot, and have your laptop connect to your mobile phone's hotspot, with the mobile phone having only the mobile data switched on [1]. Don't worry, your mobile data would not be used during the camera stream as no actual connection to the internet is made, as the camera stream still works even if the mobile data is turned off, but you run the risk of losing connection to your vehicle.)

If you're working with 2 ESP32-CAM boards, in order to use the other board as a viewfinder, please visit this [link](https://github.com/leeyanhuilyh/ESP32-CAM-Vehicle-Viewfinder) and configure the WiFi settings to the same credentials.

## Preparing to upload the code

To begin uploading to the ESP32-CAM, please follow this [wiring guide](https://i1.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/12/ESP32-CAM-FTDI-programmer-5V-supply.png?w=750&quality=100&strip=all&ssl=1). Once it's wired up properly, click on the tick in the blue bar at the bottom of the window to verify your code. After it's verified, click on the arrow icon beside it to begin uploading your code!

## Wiring up the board

Please follow this [wiring guide](https://imgur.com/W20d9TJ) and wire up the boards accordingly.

## Connecting to the vehicle

Upon powering up the vehicle, the LED would flash a couple of times. This means that it is connecting to the WiFi access point. When it stops flashing, it means that it has successfully connected to the access point. If it continues to flash, please check your WiFi setup or credentials.

Enter 192.168.137.20 into your web browser on either your phone or your PC.

The vehicle should now be working as intended! Try scanning a few QR codes [2] to test it out!

### Additional notes:

[1] The rationale for this is the ESP32-CAM always assigns a new IP address to the ESP32-CAM upon connection, but we need a static IP address in order to control the ESP32-CAM board consistently, and without hassle. Only a PC hotspot is able to achieve this. Mobile phone hotspots do not offer the feature of assigning a static IP address.

[2] The QR scanner only works on specially encrypted QR codes. Scanning normal QR codes would only produce gibberish.
