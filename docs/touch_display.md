Let's take a closer look at the Red Vision Touch Display for Pico and the hardware included on it.

## 2" Capacitive Touch LCD

The Touch Display Board has a 2", 340x240px resolution capacitive touch LCD. 

## Connectors

### Pico Headers

We designed this board to mount directly to the XRP Control Board as well as a Rasbperry Pi Pico so it has a pair of 20 pin male headers that match the footprint of those two boards. These headers break out all the required pins for running and controlling both the display on this board as well as pins for the connected camera board. 

### Camera Connector

The Touch Display board has a 2x10 female connector to connect to the Red Vision Camera Board (or other compatible camera board, refer to [this list](https://github.com/sparkfun/red_vision?tab=readme-ov-file#hardware-support) for supported hardware). Note, the Camera Board has a 2x9 header so when connecting the two, make sure to align it to the side near the Qwiic connector. We cover this in more detail with photos in the [Hardware Assembly](../hardware_assembly.md) section further on in this guide.

### Qwiic Connector

The board has one Qwiic connector to allow users to easily add other Qwiic devices to their circuit if desired.

## GPIO Expander

The Touch Display includes a PCA9534PW GPIO expander to control several I/O (input and output) pins from the display, camera and SD card over I<sup>2</sup>C. Users can interact with the GPIO expander using the [SparkFun PCA9685 Python](https://github.com/sparkfun/qwiic_pca9685_py) package.

## &micro;SD Card Slot

The board includes a &micro;SD card slot to allow users to increase the memory capacity of a connected board; whether that be the XRP Control Board or a Pico.

## Reset Button

The reset button on the Touch Display board connects to the reset button on the XRP Control Board (or Pico) to allow easy access to reset the board.

## LED

The sole LED on this board is a red Power LED to indicate when the board has power.

## Solder Jumpers

The Red Vision Touch Display for Pico has a large amount of solder jumpers so we'll cover them in subsections. Note, manipulating these solder jumpers is only recommended for *advanced users* as they alter the functionality of the board, change the pins used by it and require knowledge of [working with jumper pads and PCB traces](https://learn.sparkfun.com/tutorials/how-to-work-with-jumper-pads-and-pcb-traces). 

### GPIO Expander Jumpers

This set of jumpers labeled <b>A0</b>, <b>A1</b> and <b>A2</b> control the I<sup>2</sup>C address of the GPIO Expander. All three jumpers are OPEN by default to set the GPIO Expander's address to <b>0x20</b>. Closing different combinations of these jumpers lets users select from eight I<sup>2</sup>C addresses. The table below outlines the different options to change the address. You can also refer to the [schematic](./assets/board_files/SparkFun_Red_Vision_Touch_Display_for_Pico.pdf) for more information.

<table>
    <tr>
        <th>I<sup>2</sup>C Address</th>
        <th>A0 State</th>
        <th>A1 State</th>
        <th>A2 State</th>
    </tr>
    <tr>
        <td>0x20 (Default)</td>
        <td>Open</td>
        <td>Open</td>
        <td>Open</td>
    </tr>
    <tr>
        <td>0x21</td>
        <td>Closed</td>
        <td>Open</td>
        <td>Open</td>
    </tr>
    <tr>
        <td>0x22</td>
        <td>Open</td>
        <td>Closed</td>
        <td>Open</td>
    </tr>
    <tr>
        <td>0x23</td>
        <td>Closed</td>
        <td>Closed</td>
        <td>Open</td>
    </tr>
    <tr>
        <td>0x24</td>
        <td>Open</td>
        <td>Open</td>
        <td>Closed</td>
    </tr>
    <tr>
        <td>0x25</td>
        <td>Closed</td>
        <td>Open</td>
        <td>Closed</td>
    </tr>
    <tr>
        <td>0x26</td>
        <td>Open</td>
        <td>Closed</td>
        <td>Closed</td>
    </tr>
    <tr>
        <td>0x27</td>
        <td>Closed</td>
        <td>Closed</td>
        <td>Closed</td>
    </tr>
</table>

The fourth jumper for the GPIO Expander controls whether or not the IC's enable pin connects to GPIO2 on the XRP Control Board. The jumper is OPEN by default. Close the jumper to connect the enable pin to GPIO2 for software control of the GPIO Expander.

### Camera Connections (DVP Interface) Jumpers

The solder jumper labeled <b>XCLK</b> allows users to generate an external clock to a connected camera from GPIO3. This jumper is OPEN by default. Closing this jumper connects the external clock pin on a connected camera to GPIO3 so make sure a connected camera is configured to use an external clock signal from this pin. **Note:** The Red Vision Camera Board included in this kit is configured to use an on-board external clock by default so *make sure* to adjust the board to use an external clock signal from GPIO3 prior to closing this jumper.

The two groups of solder jumpers labeled <b>1-BIT</b> and <b>8-BIT</b> allow users to change between running a connected camera in 1-Bit (Default) or 8-bit modes. Switching between 1-Bit and 8-Bit requires adjusting **all** of the related jumpers. For example, the board defaults to running a camera in 1-Bit mode by having **all** 1-Bit jumpers CLOSED and **all** 8-Bit jumpers OPEN. The tables below outline which pins a connected camera route to when set to run in 1-Bit or 8-Bit modes:


**1-Bit Camera Operation**
<table>
    <tr>
        <th>Camera Pin</th>
        <th>XRP/Pico Pin</th>
        <th>Notes</th>
    </tr>
    <tr>
        <td>CAM_DO</td>
        <td>GPIO12</td>
        <td>Camera Data 0 Out</td>
    </tr>
    <tr>
        <td>CAM_VS</td>
        <td>GPIO13</td>
        <td>Camera Frame Valid Output</td>
    </tr>
    <tr>
        <td>CAM_HS</td>
        <td>GPIO14</td>
        <td>Cam Line Valid Output</td>
    </tr>
    <tr>
        <td>CAM_PCLK</td>
        <td>GPIO15</td>
        <td>Camera Pixel Clock/Serial Clock Out</td>
    </tr>
</table>

**8-Bit Camera Operation**
<table>
    <tr>
        <th>Camera Pin</th>
        <th>XRP/Pico Pin</th>
        <th>Note</th>
    </tr>
    <tr>
        <td>CAM_DO</td>
        <td>GPIO8</td>
        <td>Camera Data 0 Out</td>
    </tr>
    <tr>
        <td>CAM_D1</td>
        <td>GPIO9</td>
        <td>Camera Data 1 Out</td>
    </tr>
    <tr>
        <td>CAM_D2</td>
        <td>GPIO10</td>
        <td>Camera Data 2 Out</td>
    </tr>
    <tr>
        <td>CAM_D3</td>
        <td>GPIO11</td>
        <td>Camera Data 3 Out</td>
    </tr>
    <tr>
        <td>CAM_D4</td>
        <td>GPIO12</td>
        <td>Camera Data 4 Out</td>
    </tr>
    <tr>
        <td>CAM_D5</td>
        <td>GPIO13</td>
        <td>Camera Data 5 Out</td>
    </tr>
    <tr>
        <td>CAM_D6</td>
        <td>GPIO14</td>
        <td>Camera Data 6 Out</td>
    </tr>
    <tr>
        <td>CAM_D7</td>
        <td>GPIO15</td>
        <td>Camera Data 7 Out</td>
    </tr>
    <tr>
        <td>CAM_PCLK</td>
        <td>GPIO20</td>
        <td>Camera Pixel Clock/Serial Clock Out</td>
    </tr>
    <tr>
        <td>CAM_VS</td>
        <td>GPIO21</td>
        <td>Camera Frame Valid Output</td>
    </tr>
    <tr>
        <td>CAM_HS</td>
        <td>GPIO22</td>
        <td>Cam Line Valid Output</td>
    </tr>
</table>

### Other Jumpers

The last jumpers we haven't covered are labeled <b>PWR</b> and <b>I2C</b>. The <b>PWR</b> solder jumper completes the Power LED circuit and is CLOSED by default. Open the solder jumper to disable the Power LED. The <b>I2C</b> jumper pulls the I<sup>2</sup>C data (SDA/GPIO4) and clock (SCL/GPIO5) pins to <b>3.3V</b> through a pair of <b>2.2k&ohm;</b> resistors. Open this three-way jumper to disable the pullup resistors on the I<sup>2</sup>C bus if necessary.

## Board Dimensions

The Red Vision Touch Display for Pico measures 2.00" x 2.225" (50.80mm x 56.515mm).

<figure markdown>
[![Red Vision Touch Display board dimensions](./assets/board_files/SparkFun_Red_Vision_Touch_Display_for_Pico.jpg){ width="600"}](./assets/board_files/SparkFun_Red_Vision_Touch_Display_for_Pico.jpg "Click to enlarge")
</figure>