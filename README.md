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

## Binding Device with an Application

To bind our kits with a web application first we need to run getInfo example in examples folder. The output looks like this:

![Result of getInfo](https://github.com/TolgaSari/NUCLEO-LRWAN1/blob/main/LRWAN_Reference/getInfo_1.png)

Here the important fields are DevEUI, ApplicationEUI and ApplicationKey(AppKey). These fields are required to associate the device with an application.

