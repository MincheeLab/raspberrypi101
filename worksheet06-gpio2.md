# Setting up a simple web page

## Requirements:

- Raspbian (usually with Python preinstalled)

## Introduction

In this worksheet, we will go throught basic installation of Flask - very minimum web framework for Python.

*reference: http://flask.pocoo.org/docs/0.10/installation/#installation*

### Step 1: install required software packages

```
sudo pip install virtualenv
sudo pip install flask
sudo pip install RPi.GPIO
```



### Step 2: create a project

```
cd ~
mkdir hello_world
cd hello_world
virtualenv venv
```

Switch to ROOT is more convenience. **ROOT permissions is required for using GPIO !!!**

```
sudo su
```

Activate **VirtualEnv**

```
. venv/bin/activate
```

Then you will see a new prefix "(venv)"

### Step 4: Program some application

Use editor to create a new file

```
nano hello.py

```

Copy and paste the following line:

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```

What this does is serving a webpage display 'Hello World !'. You can definitely do much more than that !


### Step 5: Web and GPIO !!

Replace the content of "hello.py" with the following code

*NOTE: You should now have installed RPi.GPIO on previous worksheet. If not, please refer to previous worksheet.*


```
from flask import Flask
import RPi.GPIO as GPIO
import time

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

@app.route('/blink')
def blinkit():
    GPIO.setup(11, GPIO.OUT)
    for i in range(0,10):
        blink(11)
    GPIO.cleanup()
    return 'blink blink !'

def blink(pin):
    GPIO.output(pin,GPIO.HIGH)
    time.sleep(0.1)
    GPIO.output(pin,GPIO.LOW)
    time.sleep(0.1)
    return

if __name__ == '__main__':
    GPIO.setmode(GPIO.BOARD)
    app.debug=True
    app.run(host='0.0.0.0')

```