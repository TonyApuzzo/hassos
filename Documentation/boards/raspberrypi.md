# Raspberry PI

Supported Hardware:

| Device | Board | 
|--------|-----------|
| Raspberry Pi A+/B/B+| rpi |
| Raspberry Pi Zero | rpi |
| Raspberry Pi Zero W | rpi0-w |
| Raspberry Pi 2 B | rpi2 |
| Raspberry Pi 3 B/B+ | rpi3 / rpi3-64 |

## Limitation 64bit

The 64bit version is under development by RPi-Team. It work very nice but it could have some impacts. Actual we see that the SDcard access with ext4 are a bit slower than on 32bit.

## Serial console

For access to terminal over serial console, add `console=ttyAMA0,115200` to `cmdline.txt` and `enable_uart=1`, `dtoverlay=pi3-disable-bt` into `config.txt`. GPIO pins are: 6 = GND / 8 = UART TXD / 10 = UART RXD.

## I2C

Add `dtparam=i2c1=on` and `dtparam=i2c_arm=on` to `config.txt`. After that we create a module file on host with [config usb stick][config] or direct into `/etc/modules-load.d`. 

rpi-i2c.conf:
```
i2c-dev
i2c-bcm2708
```

## Tweaks

### Bluetooth
If you don't need bluetooth, disable it by adding `dtoverlay=pi3-disable-bt` into `config.txt`.

### GPU Memory

The minimum GPU/CPU RAM split can be set by adding `gpu_mem=32` into `config.txt`. This will gain 32 MiB RAM for HASSOS. If gpu_mem is too low (e.g., 16) then the RPi will fail to boot and the green ACT LED will flash 4 times in a never ending loop. In order to use the Raspberry Pi Camera, set `gpu_mem=128`.

[config]: ../configuration.md#automatic
