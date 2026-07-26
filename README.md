# HawkeyeF407 Custom Flight Controller for ArduPilot

HawkeyeF407 merupakan **custom Flight Controller** berbasis **STM32F407** yang dikembangkan untuk menjalankan firmware **ArduPilot** pada platform **Hybrid VTOL UAV–Rover**. Board ini dirancang menggunakan **ChibiOS Hardware Definition (hwdef)** sehingga dapat dikompilasi secara langsung sebagai target board ArduPilot tanpa memerlukan modifikasi pada source code utama.

Repositori ini menyediakan konfigurasi **Hardware Definition (`hwdef.dat`)**, **Bootloader (`hwdef-bl.dat`)**, serta dokumentasi yang diperlukan untuk membangun dan menjalankan firmware ArduPilot pada board HawkeyeF407.

---

# Repository Contents

```
HawkeyeF407/
│
├── hwdef.dat           # Hardware Definition utama
├── hwdef-bl.dat        # Hardware Definition Bootloader
├── bootloader.bin      # Binary Bootloader
├── README.md
└── ...
```

---

# Hardware Definition

File **`hwdef.dat`** merupakan konfigurasi utama hardware board yang digunakan selama proses kompilasi firmware ArduPilot. File ini mendefinisikan seluruh karakteristik perangkat keras flight controller, meliputi:

- Jenis mikrokontroler (MCU)
- Board ID
- Clock System
- Flash Memory Layout
- Timer Configuration
- GPIO Mapping
- UART Configuration
- SPI Bus
- I2C Bus
- CAN Bus
- USB Interface
- SD Card Interface
- ADC Configuration
- PWM Output Mapping
- DMA Configuration
- IMU Driver
- Barometer Driver
- Compass Configuration
- Logging Configuration
- Feature Configuration

Seluruh driver perangkat keras ArduPilot akan dikonfigurasi berdasarkan informasi yang terdapat pada file ini.

---

# Bootloader

File **`hwdef-bl.dat`** digunakan untuk membangun bootloader khusus HawkeyeF407.

Bootloader bertanggung jawab untuk:

- Inisialisasi awal mikrokontroler.
- Menyediakan antarmuka USB untuk proses flashing firmware.
- Memverifikasi Board ID.
- Memuat firmware ArduPilot dari Flash Memory.
- Mengalihkan eksekusi ke firmware utama setelah proses boot selesai.

Repositori ini juga menyertakan binary bootloader (`bootloader.bin`) sehingga pengguna tidak perlu membangun bootloader dari awal.

---

# Hardware Features

Board HawkeyeF407 memiliki spesifikasi utama sebagai berikut.

| Feature | Specification |
|----------|---------------|
| MCU | STM32F407xx Cortex-M4 @ 168 MHz |
| Flash Memory | 1 MB |
| Bootloader Reserved | 64 KB |
| USB | USB OTG Full Speed |
| UART | 5 UART + USB Virtual COM |
| SPI | IMU & Barometer |
| I2C | External Compass / Sensor |
| CAN | DroneCAN Supported |
| SD Card | SDIO Interface |
| PWM Output | 8 Channels |
| ADC | Battery Voltage, Current, RSSI |
| Buzzer | Supported |
| Status LED | Dual LED |

---

# Supported Sensors

Konfigurasi default mendukung perangkat berikut:

- MPU9250 (SPI)
- BMP280 (SPI)
- External I2C Compass
- Battery Voltage Monitor
- Battery Current Monitor
- RSSI Analog Input

Sensor lain yang didukung ArduPilot dapat ditambahkan dengan memodifikasi file `hwdef.dat`.

---

# Building Firmware

Clone repositori ini ke dalam direktori `libraries/AP_HAL_ChibiOS/hwdef/` pada source code ArduPilot.

```bash
https://github.com/setyawan-dev/HawkeyeF407.git
```

Masuk ke direktori ArduPilot.

```bash
cd ardupilot
```

Konfigurasikan board.

```bash
./waf configure --board HawkeyeF407
```

Kemudian lakukan proses kompilasi.

```bash
./waf copter
```

Firmware hasil kompilasi akan berada pada direktori:

```
build/HawkeyeF407/bin/
```

---

# Flashing Firmware

Firmware dapat diunggah menggunakan:

- Mission Planner
- STM32CubeProgrammer
- DFU Mode
- Bootloader USB

Pastikan bootloader HawkeyeF407 telah terpasang pada mikrokontroler sebelum melakukan flashing firmware.

---

# Directory Structure

```
HawkeyeF407
├── hwdef.dat
├── hwdef-bl.dat
├── bootloader.bin
├── README.md
```

---

# License

Repositori ini mengikuti lisensi yang sama dengan proyek **ArduPilot**, kecuali dinyatakan lain pada setiap berkas.

---

# Author
**Erwin Setyawan Wicaksono**

**email : erwinjosz123@gmail.com** 

**Technology Development Division**

**Dewo Robotic UNESA** 

**Custom Flight Controller Development for UAV-Multicopter**
