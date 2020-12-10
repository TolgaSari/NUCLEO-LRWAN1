# NUCLEO-LRWAN1

This project shows basic usage of I-NUCLEO-LRWAN1 shield on NUCLEO-L053R8 board. 

## Installing Arduino

Arduino toolchain must be installed normally. Nucleo boards can also be configured using arduino. Plus, LRWAN shield already has drivers available to arduino. Next, [this website](https://www.instructables.com/Quick-Start-to-STM-Nucleo-on-Arduino-IDE/) has great tutorial on installing Nucleo drivers to arduino.

## Accessing LoRa Shield

LoRa shield is designed to communicate using its pins **D0-D1**. Sadly, these pins on the Nucleo Boards are inaccessible to the user applications and are reserved for ST-LINK. Which can be seen on the figure below. **PA_2-PA_3** pins in the CN9 bank, corresponds **D0-D1** pins of the shield.

![The pinout of the board](https://raw.githubusercontent.com/TolgaSari/NUCLEO-LRWAN1/main/NUCLEO_Reference/nucleo_l053r8_2017_9_25_mor_right.png)

To access the shield, we have to use different UART interface. Fortunately, pins **PA_10** and **PB_6** can be used as UART RX-TX pair. In addition the this, they are accessible from arduino as pins **D2** and **D10** respectively. To utilize them, **PA_10** must be connected to **shield's D0** and **PB_6** must be connected to **shield's D1** using female to male jumper cables. The resulting connections are shown in the figure below.

