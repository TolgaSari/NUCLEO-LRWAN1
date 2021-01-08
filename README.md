# NUCLEO-LRWAN1

This project shows basic usage of I-NUCLEO-LRWAN1 shield on NUCLEO-L053R8 board. 

## Installing Arduino

Arduino toolchain must be installed normally. Nucleo boards can also be configured using arduino. Plus, LRWAN shield already has drivers available to arduino. Next, [this website](https://www.instructables.com/Quick-Start-to-STM-Nucleo-on-Arduino-IDE/) has great tutorial on installing Nucleo drivers to arduino.

## Accessing LoRa Shield

LoRa shield is designed to communicate using its pins **D0-D1**. Sadly, these pins on the Nucleo Boards are inaccessible to the user applications and are reserved for ST-LINK. Which can be seen on the figure below. **PA_2-PA_3** pins in the CN9 bank, corresponds **D0-D1** pins of the shield.

![The pinout of the board](https://raw.githubusercontent.com/TolgaSari/NUCLEO-LRWAN1/main/NUCLEO_Reference/nucleo_l053r8_2017_9_25_mor_right.png)

To access the shield, we have to use different UART interface. Fortunately, pins **PA_10** and **PB_6** can be used as UART Rx-Tx pair. In addition the this, they are accessible from arduino as pins **D2** and **D10** respectively. To utilize them, **PA_10** must be connected to **shield's D0** and **PB_6** must be connected to **shield's D1** using female to male jumper cables. The resulting connections are shown in the figure below.

![Jumper connections](https://raw.githubusercontent.com/TolgaSari/NUCLEO-LRWAN1/main/LRWAN_Reference/jumperConnections.jpeg)

Next, default Rx/Tx pins must be overriden in all of the arduino codes. 

    HardwareSerial SerialLora(D2, D10);

By default the shield operates with 115200 Baudrate, so any serial ports must be configured as

    Serial.begin(115200);
    
After this step Nucleo board should communicate with the shield thus, the examples must work without any problems.

# Connecting to LoRa Network

We will use https://community.thingpark.org/ to develop our applications. Thinkgpark Community is provided by Actility, and it consists of community available LoRaWAN Base Stations that can be used in personal LoRaWAN applications. To connect our kits to the network first, we need to open an account => https://community.thingpark.org/index.php/register/

## Creating Test Application

To create a dummy application https://webhook.site/ is used. 

![webhookApp](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/webHookSite.png)

Then from the https://community.thingpark.io/tpe/#/applications/create a new application is created.

![appCreate](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/testApp.png)

After this step, the application can be associated with the device.

## Registering LoRa Enabled Device

To bind our kits with a web application first we need to run getInfo example in examples folder. The output looks like this:

![Result of getInfo](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/getInfo_1.png)

Here the important fields are DevEUI, ApplicationEUI and ApplicationKey(AppKey). These fields are required to associate the device with an application.

From https://community.thingpark.io/tpe/#/devices/create?vendorId=generic the device will be registered using the dummy application and the results of getInfo example.

![Create Dev](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/testDev.png)

Notice that Over-The-Air-Activation(OTAA) mode is selected when registering the device.

## Running the Application

Right now, the Thingpark Community network knows where to route the packets that come from our device. Running LoRaWANOTAA will connect our device to the Thingpark Community network. 

![joinOTAA](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/joinOTAA.png)

After this step the device can be observed at devices tab.

![dashboard](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/deviceDashboard.png)

If the device connects successfully then we can send packets to the device using **Send Downlink** button.

![sendDownlink](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/sendDownlink.png)

We can only send hex data to specified ports of the device. The sent packet will be seen on the console when the device receives it.

![loopback](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/joinOTAA_loopback.png)

Using weebhook.site we can see POST requests of our device.

![webhookResults](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/webHookResults.png)

In application dashboard we can see our device's requests too.

![applicationDashboard](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/applicationDashboard.png)


 



