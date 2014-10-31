# Raspberry Pi 101

## Worksheet 2 - Acessing the Pi via the serial port

---

### Step 0 - Unplug your Pi from the Power

Make sure your Pi is powered off before continuing.

Also, unplug the keyboard if it is still plugged in.


### Step 1 - Install the drivers for the serial cable in your computer

This will depend on your computer (Windows/Mac/Linux). Your instructor will guide you through it.


### Step 2 - Get to know the GPIO


![GPIO](http://www.element14.com/community/servlet/JiveServlet/previewBody/68203-102-6-294412/GPIO.png)


### Step 3 - Plug a network cable to the Pi

![Serial 01](https://raw.githubusercontent.com/MincheeLab/raspberrypi101/master/images/serial/serial01.jpg)


### Step 4 - Plug the serial cable to the Pi

![Serial 02](https://raw.githubusercontent.com/MincheeLab/raspberrypi101/master/images/serial/serial02.jpg)


### Step 5 - Check Pi setup

![Serial 03](https://raw.githubusercontent.com/MincheeLab/raspberrypi101/master/images/serial/serial03.jpg)

### Step 6 - Plug the serial cable to your computer

![Serial 04](https://raw.githubusercontent.com/MincheeLab/raspberrypi101/master/images/serial/serial04.jpg)

### Step 7 - Start your serial software

This will depend on your computer. Our instructors will assist you.

For Mac users, open a terminal and type:

```
screen /dev/tty.usbserial 115200
```

### Step 8 - Plug your Pi to the power

This will depend on your computer. Our instructors will assist you.


A series of messages will scroll across the screen.
Ignore error messages such as

```"Failed to create debugfs directory"```

Eventually the login prompt should appear:

```
raspberrypi login: 
```

Login with:

```
login: pi
password: raspberry
```

You should now be logged in.

You may also see the message:

```"NOTICE: the software on this Raspberry Pi has not been fully configured. Please run 'sudo raspi-config'"```

Do not worry about this message, you will configure your Pi shortly.

### Step 9 - Find your Pi IP address

Firstly find the IP address assigned to your Raspberry Pi. Type:

```
ifconfig
```

You will see an output such as:

```
pi@raspberrypi:~$ ifconfig
eth0      Link encap:Ethernet  HWaddr b8:27:eb:f5:85:b1  
          inet addr:192.168.2.7  Bcast:192.168.2.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:36 errors:0 dropped:0 overruns:0 frame:0
          TX packets:28 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:6044 (5.9 KiB)  TX bytes:3264 (3.1 KiB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```


The "inet addr" under "eth0" is your current LAN IP address. You will now use it to SSH into your Pi over the network.


### Step 10 - Log out and disconnect serial

Type "Ctrl-D" in the console. This will log you out. You can now safely disconnect the serial USB from your computer.

(Mac users may find that upon disconnection from the serial port, the terminal looses the ability to print new lines. Just close that terminal and open a new one to continue).