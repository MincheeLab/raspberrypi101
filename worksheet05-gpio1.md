# Raspberry Pi 101

## Worksheet 5 - Using the GPIO programatically (with Python)

---

### Step 1 - SSH into the Pi

SSH into your Pi as detailed in Worksheet 3.



### Step 2 - Install GPIO python library

In order to access the GPIO from Python you need to install the necessary libraries.


```
sudo pip install RPi.GPIO
```

### Step 3 - Create a directory for your Python script
```
cd ~
mkdir mygpio
cd mygpio
```

### Step 4 - Switch to root user (required to access GPIO)
Switch to ROOT is more convenient. **ROOT permissions is required for using GPIO !!!**

```
sudo su
```

### Step 5 - Create a simple Python script

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


### Step 6 - Run your script

Back in the command line, run your script:

```
python blink.py
```