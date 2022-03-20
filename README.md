# kh-nut-ups
Installation for Nut and parser to send data to influxdb

```
sudo apt update
sudo apt full-upgrade
sudo apt install nut
```

Running `lsusb` should show that the UPS is connected
```
pi@raspberrypi:~ $ lsusb
Bus 001 Device 005: ID 051d:0002 American Power Conversion Uninterruptible Power Supply
Bus 001 Device 004: ID 0424:7800 Microchip Technology, Inc. (formerly SMSC)
Bus 001 Device 003: ID 0424:2514 Microchip Technology, Inc. (formerly SMSC) USB 2.0 Hub
Bus 001 Device 002: ID 0424:2514 Microchip Technology, Inc. (formerly SMSC) USB 2.0 Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

Contents of `/etc/nut/ups.conf`
```
maxretry = 3
[ups]
        driver = usbhid-ups
        port = auto
```

Contents of `/etc/nut/upsd.users`
```
[monuser]
   password = secret
   instcmds = ALL
   upsmon master
```

Contents of `/etc/nut/upsdmon.conf`
```
MONITOR ups@localhost 1 monuser secret master
```

Contents of `/etc/nut/nut.conf`
```
MODE=netserver
```
