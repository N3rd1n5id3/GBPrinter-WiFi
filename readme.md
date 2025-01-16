# GBPrinter WiFi
A GameBoy printer emulator which provides the received data over a WiFi connection.  
This code is based on HerrZatacke’s [WiFi GBP Emulator](https://github.com/HerrZatacke/wifi-gbp-emulator) and optimized for [LOLIN D1 Mini](https://aliexpress.com/item/32529101036.html?spm=a2g0o.productlist.main.17.1478403elprMIB&algo_pvid=44bd4326-8e4d-4c67-9ccc-cf0f8b44deac&algo_exp_id=44bd4326-8e4d-4c67-9ccc-cf0f8b44deac-8&pdp_npi=4%40dis%21EUR%216.40%210.97%21%21%216.51%210.99%21%402103868817354014291093411ed0d3%2159008795982%21sea%21IT%210%21ABX&curPageLogUid=QIdy8dpbzogS&utparam-url=scene%3Asearch%7Cquery_from%3A) connected to [OLED 0.96 Shield](https://aliexpress.com/item/1005001804136025.html?spm=a2g0o.productlist.main.1.28b9253eUk2Q11&algo_pvid=11f2fde6-d1c2-4610-ad5b-6de6649ad847&algo_exp_id=11f2fde6-d1c2-4610-ad5b-6de6649ad847-0&pdp_npi=4%40dis%21EUR%214.32%214.32%21%21%214.39%214.39%21%40211b804117354016018647166ed29d%2112000017661511797%21sea%21IT%214310778699%21X&curPageLogUid=o8tTI1zG2pOH&utparam-url=scene%3Asearch%7Cquery_from%3A) with a [I2C cable](https://aliexpress.com/item/32867490848.html?pdp_npi=4%40dis%21EUR%21€%201%2C60%21€%201%2C60%21%21%211.63%211.63%21%4021039fae17354016399644025e5ae5%2165534940046%21sh01%21IT%214310778699%21X&spm=a2g0o.store_pc_home.productList_2009695634917.32867490848)


## Setup
## Step 1: Flash the board

In this first step we will setup your computer to communicate with the LOLIN D1 Mini and flash it. 

### 1.1 Install the Arduino IDE 
Download the Arduino IDE (Windows/MacOS) from [here](https://www.arduino.cc/en/Main/Software) and follow the basic installation process.
 It is recommended for Linux Users to use your packet manager to install the IDE. 

### 1.2 Install ESP8266 in Arduino
Start the Arduino IDE and navigate to ```File -> Preferences``` and add the following line to "Additional Boards Manager URLs:"

````
http://arduino.esp8266.com/stable/package_esp8266com_index.json
````
Confirm with "OK" and navigate to ```Tools -> Board -> Board Manager```. In the filter mask search for ```esp8266``` and install the package. 

Lastly navigate to ```Tools -> Board``` and select your LOLIN D1 Mini

### 1.3 Install Arduino Libraries

Go to ``` Tools -> Manage Libraries``` and search in the filter mask for ArduinoJSON. Additional installation procedures can be found [here](https://arduinojson.org/v6/doc/installation/)

Go to ``` Tools -> Manage Libraries ``` to search for and install the "Adafruit SSD1306" library.

### 1.4 Download the GBPrinter WiFi github code and additional data

Download the full code from [here](https://github.com/N3rd1n5id3/GBPrinter-WiFi) as a ZIP file and extract it to your home directory.
In your file browser navigate into the extracted folder and then into the ```gbprinter-wifi``` subfolder. Here create a copy of the ```config.h.sample.txt```. Rename the new file to ```config.h``` 

Download the additional data for the GB-Printer-Web interface.

#### Windows
Go to your Start Menu, type ```powershell``` and navigate to the directory you just extracted (e.g. cd ```YourUsername\Downloads\GBPrinter-WiFi-main\```)
Run the download script with ```.\update_w.ps1```

#### MacOS / Linux
Open your Terminal and navigate to the files you just extracted (e.g. ```cd ~/Downloads/GBPrinter-WiFi-main/```)
Type ```chmod +x update_w.sh```
Type ```./update_w.sh```

### 1.5 Upload the code and data

Connect your LOLIN D1 Mini via USB to your PC. Navigate to ```File -> Open ...``` navigate to the folder you unzipped in the previous step. Open the ```gbprinter-wifi.ino``` 

To confirm that the code was downloaded correctly navigate to ```Sketch -> Verify/Compile```. Ensure at this point that the correct board is selected in ``` Tools -> Board ```. If everything works go to ```Sketch -> Upload``` and wait until the upload is finished.

### 1.6  Test the board

Unplug your LOLIN D1 Mini from your PC and replug it. Open your WiFi Monitor and wait for it to finish scanning for available networks. You should see a wifi network named ```gameboyprinter``` with the password ```gameboyprinter```. 

After you connected to the WiFi open your browser and type in the URL ```http://gameboyprinter.local```. The Gameboy Printer Web Emulator should load. If it doesn't please try to connect to ```https://192.168.4.1``` instead. 

## Step 2: Preparing the Hardware

Now that you've got your LOLIN D1 Mini running with the GBPrinter WiFi it's time to connect your Gameboy to it to actually copy your images. There are non-destructive ways ([Example](https://github.com/Palmr/gb-link-cable)) but for easy of access we will have to cut up a link cable. You can either obtain those cheap from [AliExpress](https://aliexpress.com/item/1005006341381073.html?spm=a2g0o.productlist.main.21.77b0seOkseOk31&algo_pvid=459a9e05-63c2-4963-a7ee-df8e586c5df3&algo_exp_id=459a9e05-63c2-4963-a7ee-df8e586c5df3-10&pdp_npi=4%40dis%21EUR%217.62%212.38%21%21%2156.25%2117.58%21%40211b804117370230059254266ece56%2112000036832298734%21sea%21IT%214310778699%21X&curPageLogUid=1CWC4GcoZzbb&utparam-url=scene%3Asearch%7Cquery_from%3A). 

### 2.1 Link Cable connection with a multimeter

#### 2.1.1 Preperation
Take your Link Cable and cut it in half. You will find six (6) thin wires inside. Carefully remove the cable shielding for 2cm / 1 inch close to where you cut the cable to expose the six wires. Now take your multimeter and check which wire has continuitiy to which port on the connector and write it down. 

#### 2.1.2 Preparing the connection wires 

We now will connect the wires to LOLIN D1 Mini. Take your exposed connector and look at it from the front with the straight side up.

![Front view of Link Cable](/images/link_cable_connector.jpg)

### 2.2 Connecting your Gameboy to the LOLIN D1 Mini

We are now going to connect the link cable to the LOLIN D1 Mini. Solder the following cables to the pins on the LOLIN D1 Mini:

```
 _________
|  6 4 2  |
 \_5_3_1_/

| Link Cable | LOLIN D1 Mini |
|------------|---------------|
| Pin 1      | SS (GPIO 15)  |
| Pin 2      | MOSI (GPIO 13)|
| Pin 3      | MISO (GPIO 12)|
| Pin 5      | SCK (GPIO 14) |
| Pin 6      | GND           |

```

## Step 3: Testing your Installation

Plug in your Link Cable to your Gameboy and start the LOLIN D1 Mini though connecting it to a USB power source. Start your Gameboy with the Gameboy Camera inserted. Navigate to a picture you want to print and select ```Print```. You should see the ```Transferring``` screen and a short flashing of ```Printing``` -- You are done! Your GBPrinter works successfully! _Tip: If you want to transfer all of your pictures right away press "Select" on your Gameboy in the main screen and use the Print Menu_

Disconnect the link cable and power cycle the LOLIN D1 Mini; connect to the wireless access point and open the website as explained in Step 1.6. Change to the "Import" tab, click on "check printer" and you should should be able to import your pictures. From there on you can download pictures through the gallery, change the color palette (re-import afterwards).

Pat yourself on the back and have fun! Also make sure to join the [Gameboy Camera Club on Discord](https://bit.ly/gbccd) and share your pictures or participate in the Bi-Weekly challenges. 

## Adding the OLED Screen

Connect the OLED Screen to LOLIN D1 Mini with I2C cable.