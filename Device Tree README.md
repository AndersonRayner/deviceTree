#Hardware
Modified from original file in ardupilot GIT repo.

## Load device tree
To load the BBBMINI device tree type `startup.sh load`.

## Build dtbo file
To rebuild the dtbo file type `make` and then `make install`to copy the dtbo file to `/lib/firmware`.

## Busses used
SPI0  - LSM9DSO (CS0,CS1)
	CS0 - P9.17 (LSM9DSO XM)
	CS1 - P8.09 (LSM9DSO G)
	CS2 - P8.07 (External)
SPI1  - MPU9150, Baro
	CS0 - P9.28 (MPU9150)
	CS1 - P9.42 (Baro)
I2C2  - LED, Airspeed, RTC, Wingtip Boards (RPM (x4) and elevator (x2))
UART4 - Telemetry Radio
UART5 - GPS

## Extra pins
P9.25 - GPIO3_21   - MPU9150_INT 
P9.27 - GPIO3_19   - Heartbeat LED
P8.34 - UART3_RTSN - GYRO_INT 
P8.12 - GPIO1_12   - TRIG
P8.16 - GPIO1_14   - ECHO
P8.08 - TIMER7     - ACCEL_INT
P8.10 - TIMER6     - MAG_INT 
P8.11 - GPIO1_13   - ARDU_SYNC_3V3
P8.15 - GPIO1_15   - RC_IN
P8.28 -            - RC1
P8.27 -            - RC2
P8.30 -            - RC3
P8.29 -            - RC4
P8.40 -            - RC5
P8.39 -            - RC6
P8.42 -            - RC7
P8.41 -            - RC8
P8.44 -            - RC9
P8.43 -            - RC10
P8.46 -            - RC11
P8.45 -            - RC12
P9.15 - GPIO1_16   - ARDU_RESET_3V3

## Pin assigment
### Baro MS 5611 (Works)
BBB               | MS 5611       | I/O | Remark 
------------      | ------------- | --- | -------------
P9.01 GND         | 3 GND         | -   |
-     3V3_SENSORS | 1 VDD         | -   |
P9.29 SPI1_MISO   | 6 MISO / SDO  | IN  | 3.3 Volt
P9.30 SPI1_MOSI   | 7 MOSI / SD1  | OUT | 3.3 Volt
P9.31 SPI1_SCL    | 8 SCLK / SCL  | OUT | 3.3 Volt
P9.42 SPI1_CS1    | 5 CSB2        | OUT | 3.3 Volt

### IMU LSM9DS0
BBB               | LSM9DS0       | I/O | Remark
------------      | ------------- | --- | -------------
P9.01 GND         |  2 GND        |               
P9.03 3V3         | 18 VDD_IO     |               
-     3V3_SENSORS | 15 VDD        |
P9.18 SPI0_MOSI   | 24 SDA        |
P9.22 SPI0_SCL    | 21 SCL        |
P9.21 SPI0_MISO   | 23 SDO(XM)    |
P9.17 SPI0_CS0    | 20 CS(XM)     |
P9.21 SPI0_MISO   | 22 SDO(G)     |
P8.09 SPI0_CS1    | 19 CS(G)      |
P8.08 ACCEL_INT   | 14 INT2(XM)   |
P8.10 MAG_INT     | 13 INT1(XM)   |
P8.34 GYRO_INT    | 12 DRDY(G)    |

### IMU MPU-9150 (Need new chip)
BBB               | MPU-9150      | I/O | Remark
------------      | ------------- | --- | -------------
P9.01 GND         | 15 GND        | -   |
P9.03 3V3         |  8 VLOGIC     | -   |
-     3v3_SENSORS |  3 VDD        | -   |
P9.28 SPI1_CS0    | 22 CLKOUT     |     |
P9.29 SPI1_MISO   |  9 MISO / SD0 |     |
P9.30 SPI1_MOSI   | 24 MOSI / SDA |     |
P9.31 SPI1_SCLK   | 23 SCLK / SCL |     |
P9.25 MPU9250_INT | 12 INT        | IN  |

### DS3231 Realtime Clock
BBB               | DS3231        | I/O | Remark
------------      | ------------- | --- | -------------
P9.48 GND         | 13 GND        | -   | 
P9.49 3V3         |  2 VCC        | -   |
-     V_BATT      | 14 VBAT       | -   |
P9.20 I2C2_SDA    | 15 SDA        | 
P9.19 I2C2_SCL    | 16 SCL        |

### LEDS
BBB               | LED           | I/O | Remark
------------      | ------------- | --- | -------------
P9.27 HEARTBEAT   |               | OUT |
P9.20 I2C2_SDA    | I2C2_SDA_5V   |
P9.19 I2C2_SCL    | I2C2_SCL_5V   |

### RCInput
BBB               | RC Receiver   | I/O | Remark
------------      | ------------- | --- | -------------
P9.01 GND         | -             | -   |
P9.03 3V3         | +             | -   |
P8.15 RC_IN       | S             | IN  | 

### RCOutput
BBB               | ESC / Servo   | I/O | Remark
------------      | ------------- | --- | -------------
P8.01 GND         | GND           | -   | 
P8.28 RC-BBB_1    | RC1           | OUT | 3.3 Volt
P8.27 RC-BBB_2    | RC2           | OUT | 3.3 Volt
P8.30 RC-BBB_3    | RC3           | OUT | 3.3 Volt
P8.29 RC-BBB_4    | RC4           | OUT | 3.3 Volt
P8.40 RC-BBB_5    | RC5           | OUT | 3.3 Volt
P8.39 RC-BBB_6    | RC6           | OUT | 3.3 Volt
P8.42 RC-BBB_7    | RC7           | OUT | 3.3 Volt
P8.41 RC-BBB_8    | RC8           | OUT | 3.3 Volt
P8.44 RC-BBB_9    | RC9           | OUT | 3.3 Volt
P8.43 RC-BBB_10   | RC10          | OUT | 3.3 Volt
P8.46 RC-BBB_11   | RC11          | OUT | 3.3 Volt
P8.45 RC-BBB_12   | RC12          | OUT | 3.3 Volt

### Arduino Communications
BBB               | Arduino       | I/O | Remark
------------      | ------------- | --- | -------------
P9.26 ARDU_RX     | 64 ARDU_TX    | IN  |
P9.24 ARDU_TX     | 63 ARDU_RX    | OUT |
P9.15 ARDY_RESET  | 30 RESET      | OUT |
P8.11 ARDU_SYNC   | 45 ARDU_SYNC  | OUT |
 
### UART4 MAVLink radio module - Baudrate 57600, 8, n, 1
BBB               | Radio         | I/O | Remark
------------      | ------------- | --- | -------------
P9.01 GND         | GND           | -   |
P9.13 TX          | RADIO_RX      | OUT | 3.3 Volt 
P9.11 RX          | RADIO_TX      | IN  | 3.3 Volt

### UART5 GPS - Baudrate 38400, 8, n, 1
BBB               | GPS           | I/O | Remark
------------      | ------------- | --- | -------------
P8.01 GND         | GND           | -
P8.37 TX          | GPS_RX        | OUT | 3.3 Volt 
P8.38 RX          | GPS_TX        | IN  | 3.3 Volt

=====================	