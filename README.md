# ESP32-CAM-Vehicle-with-QR-Scanner

This repository will contain the the files that need to be uploaded to the ESP32-CAM board and the nstructions to build the vehicle.

# Software

## Pre-requisites

Firstly, please download and install [PlatformIO](https://platformio.org/install/ide?install=vscode).

Next, clone this repository into your working directory. For the purpose of this tutorial, assume this is the working directory.

```
C:\repo\ESP32-CAM-Vehicle-with-QR-Scanner
```

You would also need an [FTDI programmer](https://randomnerdtutorials.com/program-upload-code-esp32-cam/) to upload the code onto the ESP32-CAM. If you have an Arduino Uno, it can also be used as an FTDI programmer. Please follow [this](https://technoreview85.com/how-to-program-esp-32-cam-using-arduino-uno-board/) guide instead

## Starting a new project on PlatformIO

Follow the official guide on [PlatformIO](https://docs.platformio.org/en/latest/integration/ide/vscode.html#quick-start) to start a new project.

Choose the "AI-Thinker ESP32-CAM" as the Board and select Arduino as the Framework.

Choose a name for your project. This would be your working directory from here onwards.

## Extracting the files into your project folder

Extract the files found in the "src" folder into your working directory's "src" folder.

```
C:\repo\ESP32-CAM-Vehicle-with-QR-Scanner\src
```

Replace the platformio.ini file in your working directory with the downloaded platformio.ini file.

## Editing WiFi settings

Go to main.cpp and search for the lines:

```
const char* ssid = "XXXXX";
const char* password = "XXXXX";
```

Replace this with your WiFi Access Point credentials

(Note: the best way to ensure stable connection with your vehicle is to have your vehicle connect to your laptop's hotspot, and have your laptop connect to your mobile phone's hotspot, with the mobile phone having only the mobile data switched on [1]. Don't worry, your mobile data would not be used during the camera stream as no actual connection to the internet is made, as the camera stream still works even if the mobile data is turned off, but you run the risk of losing connection to your vehicle.)

If you're working with 2 ESP32-CAM boards, in order to use the other board as a viewfinder, please visit this [link](https://github.com/leeyanhuilyh/ESP32-CAM-Vehicle-Viewfinder) and configure the WiFi settings to the same credentials.

## Preparing to upload the code

![](https://i1.wp.com/randomnerdtutorials.com/wp-content/uploads/2019/12/ESP32-CAM-FTDI-programmer-5V-supply.png?w=750&quality=100&strip=all&ssl=1)

To begin uploading to the ESP32-CAM, you would need an FTDI programmer. Please follow the wiring guide above. 

![](https://docs.platformio.org/en/latest/_images/platformio-ide-vscode-build-project.png)
Once it's wired up properly, verify your code first, then upload the code.

# Hardware

## Materials needed

1. 1 x Corrugated Board
2. 2 x Wheel + Motor
3. 1 x Front Wheel
4. 1 x Dual Battery Holder
5. 2 x Rechargeable AA Batteries
6. 2 x ESP32-CAM
7. 1 x FTDI Programmer (or Arduino Uno)
8. 1 x Switch
9. 2 x [3D printed ESP32-CAM Holders](https://github.com/leeyanhuilyh/ESP32-CAM_Holder)
10. Jumper wires
11. Tape
12. 4 x M4 Screws
13. 3M Velcro (optional)

## Building the vehicle

![Wiring Guide](/doc/imgs/wiring.png)

1. Cut a 8 x 20 cm of the corrugated boards.
2. Cut another piece of the same dimension. (Note: cut the board with the tracks facing the perpendicular direction for better reinforcement)
3. Glue the two pieces of cut boards together.
4. Solder 2 jumper wires to the contacts of the motors.
5. Affix the L298N motor driver to the end of one side of the board.
6. Position the motor holders such that they line up with the end of the L298N motor driver.
7. Poke holes where the holes of the motor holder should be.
8. Secure the motors (with the wires facing inwards) and connect the motor wires with the L298N driver.
9. Prepare the wiring for the battery holder. The + terminal should be able to connect to the +12V terminal on the L298N, and the 5V ends on the 2 ESP32-CAM boards, making it a total of 3 terminals. This is the same for the - terminal.
10. Leave about 3cm of space between the L298N and affix the battery holder.
11. Connect the battery holder with the L298N
12. Position the front wheel on the underside of the body. Poke holes where the screws should go. The screws should be immediately after (or just a small gap) the battery holder.
13. Screw in the front wheel.
14. 3D print the ESP32-CAM holders. 3D models available [here](https://github.com/leeyanhuilyh/ESP32-CAM_Holder)
15. Screw down the holders where there is space.
16. Finally, cut out a small hole in front of the holders for the switch to fit through.
17. Connect the switch. This could be done either by soldering the wires to the contacts, or by using quick connects.
18. Upload the code to the boards (Please refer to previous sections).
19. Make the connections of the ESP32-CAM and the switch.
20. Test it out!

(Note: if the ESP32-CAM boards are not stable, affix them to the holders with tape)

## Connecting to the vehicle

Upon powering up the vehicle, the LED would flash a couple of times. This means that it is connecting to the WiFi access point. When it stops flashing, it means that it has successfully connected to the access point. If it continues to flash, please check your WiFi setup or credentials.

Enter 192.168.137.20 into your web browser on either your phone or your PC. You should see a page similar to the one below.

![html](/doc/imgs/html.png)

Try moving the vehicle around with the controls and scanning a few QR codes [2].

### Additional notes:

[1] The rationale for this is the ESP32-CAM always assigns a new IP address to the ESP32-CAM upon connection, but we need a static IP address in order to control the ESP32-CAM board consistently, and without hassle. Only a PC hotspot is able to achieve this. Mobile phone hotspots do not offer the feature of assigning a static IP address.

[2] The QR scanner only works on specially encrypted QR codes. Scanning normal QR codes would only produce gibberish.
