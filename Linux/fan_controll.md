## Setup fans on Ubuntu

```
sudo apt-get install fancontrol lm-sensors

sensors
sudo pwmconfig
```

/etc/fancontrol
```
# Configuration file generated by pwmconfig, changes will be lost
INTERVAL=10
DEVPATH=hwmon0= hwmon2=devices/platform/nct6775.656
DEVNAME=hwmon0=acpitz hwmon2=nct6779
FCTEMPS=hwmon2/pwm5=hwmon0/temp1_input hwmon2/pwm4=hwmon0/temp1_input hwmon2/pwm3=hwmon0/temp1_input hwmon2/pwm1=hwmon0/temp1_input
FCFANS=hwmon2/pwm5=hwmon2/fan5_input hwmon2/pwm4=hwmon2/fan4_input hwmon2/pwm3=hwmon2/fan3_input hwmon2/pwm1=hwmon2/fan1_input
MINTEMP=hwmon2/pwm5=20 hwmon2/pwm4=20 hwmon2/pwm3=20 hwmon2/pwm1=20
MAXTEMP=hwmon2/pwm5=60 hwmon2/pwm4=60 hwmon2/pwm3=60 hwmon2/pwm1=60
MINSTART=hwmon2/pwm5=80 hwmon2/pwm4=80 hwmon2/pwm3=80 hwmon2/pwm1=80
MINSTOP=hwmon2/pwm5=20 hwmon2/pwm4=20 hwmon2/pwm3=20 hwmon2/pwm1=20
```

ATI card fan control
```
aticonfig --pplib-cmd "set fanspeed 0 10"
```

/lib/systemd/system-sleep/script
```
#!/bin/sh
case $1/$2 in
  pre/*)
    echo "Going to $2..."
    exit 0
    ;;
  post/*)
    echo "Waking up from $2..."
    /usr/bin/aticonfig --pplib-cmd "set fanspeed 0 10"
    service network-manager restart
    service fancontrol restart
    ;;
esac
```

```
sudo chmod a+x /lib/systemd/system-sleep/script
```
