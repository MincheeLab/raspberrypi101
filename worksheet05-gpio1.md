# Raspberry Pi 101

## Worksheet 5 - Using the GPIO programatically (with Python)

---

### Step 1 - Prepare the GPIO connection

You will connect an LED and a buzzer to your Pi via the GPIO.

First you need to connect your GPIO to your breadboard via the 40 pin GPIO ribbon. 

Make sure the red strip on the ribbon is on the side of the USB ports on your Pi.


Next insert the T-Cobbler into the breadboard, as indicated on the image.

It doesn't matter the exact location of the T-Cobbler on the breadboard, just make sure it is properly seated against the breadboard.


Now, insert the other end of the GPIO ribbon into the T-Cobbler. It can only go one way, due to the small latch in the middle of the connector.

Use some jumper wires to connect GPIO port 17 (#17) and a GROUND (GND) pin to further down the breadboard.

### Step 2 - SSH into the Pi

SSH into your Pi as detailed in Worksheet 3.



### Step 3 - Install GPIO python library

In order to access the GPIO from Python you need to install the necessary libraries.


```
sudo pip install RPi.GPIO
```

### Step 4 - Create a directory for your Python script
```
cd ~
mkdir mygpio
cd mygpio
```

### Step 5 - Switch to root user (required to access GPIO)
Switch to ROOT is more convenient. **ROOT permissions is required for using GPIO !!!**

```
sudo su
```

### Step 6 - Create a simple Python script

Use nano to create a new file:

```
nano blink.py
```

Copy paste the following code to your editor:


```
import RPi.GPIO as GPIO
import time

# blinking function
def blink(pin):
        GPIO.output(pin,GPIO.HIGH)
        time.sleep(0.1)
        GPIO.output(pin,GPIO.LOW)
        time.sleep(0.1)
        return
 
# to use Raspberry Pi board pin numbers
GPIO.setmode(GPIO.BOARD)

# set up GPIO output channel
GPIO.setup(11, GPIO.OUT)

# blink GPIO11 10 times (equivalent to BCM17)
for i in range(0,10):
        blink(11)
GPIO.cleanup() 
```

Save your file and exit nano (Crtl-O and Ctrl-X)


### Step 7 - Run your script

Back in the command line, run your script:

```
python blink.py
```

Your LED should light up and your buzzer should make a sound.