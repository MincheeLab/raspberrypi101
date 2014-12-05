# Raspberry Pi 101

## Worksheet OP1 - Make your Pi email you when its IP address changes


---

### Step 1 - SSH into your Pi


### Step 2 - Install a mail server (postfix)

```
sudo apt-get install postfix dnsutils mailutils
```

After initial installation scripts, the following options are presented.

Make sure to select "Internet Site".

![Postfix 1](https://www.linode.com/docs/assets/77-postfix-courier-mysql-02-mail-server-type-2.png)


Next, you need to specify a fully qualified name for your email server.

This should be the hostname that you specified in Worksheet 3.

![Postfix 1](https://www.linode.com/docs/assets/78-postfix-courier-mysql-02-mail-server-type-3.png)


### Step 3 - Create the 'mailip' shell script

This solution uses a shell (bash) script that emails you when the IP on your Raspberry Pi changes.

```
cd
mkdir bin
cd bin
```

Create a new file using the nano editor:

```
nano mailip.sh
```

Copy/paste the following code to your editor

**Make sure to change the "your@email.com" in the script to match your existing personal email address.**


```
#/bin/bash

RECIPIENT_EMAIL_ADDRESS=your@email.com

LAN_IPADDRESS=$(/sbin/ifconfig eth0 | grep "inet addr" | awk -F: '{print $2}' | awk '{print $1}')
WAN_IPADDRESS=$(dig +short myip.opendns.com @resolver1.opendns.com)

EMAIL_BODY=""

touch ~/.current_ip_lan
touch ~/.current_ip_wan

if [[ "${LAN_IPADDRESS}" != $(cat ~/.current_ip_lan) ]]
then
        EMAIL_BODY+="Your RPi has a new LAN IP address: ${LAN_IPADDRESS}\n"
        echo ${LAN_IPADDRESS} >|~/.current_ip_lan
fi

if [[ "${WAN_IPADDRESS}" != $(cat ~/.current_ip_wan) ]]
then
        EMAIL_BODY+="Your RPi has a new WAN IP address: ${WAN_IPADDRESS}"
        echo ${WAN_IPADDRESS} >|~/.current_ip_wan
fi

if [[ "${EMAIL_BODY}" != "" ]]
then
        echo -e "${EMAIL_BODY}" |
        mail -s "RPi IP address change" ${RECIPIENT_EMAIL_ADDRESS}
fi
```

Remember to Ctrl-O to save your file, followed by Crtl-X to exit the editor.



### Step 4 - Test your script

Type the following command to test your script. From your home directory:

```
./bin/mailip.sh
```

After a few minutes you should receive an email at "your@emai.com" with the IP address details of your Raspberry Pi.

### Step 5 - Make your script run periodically

To make your script run regularly (i.e. once per minute) you need to create a cron job to run it automatically. Type the following:

```
crontab -e
```

This opens a new editor window (nano) with the following contents:

```
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h  dom mon dow   command
```

Scroll to the bottom of the file and, below the ```m h  dom mon dow   command``` line, copy/paste the following lines:

```
SHELL=/bin/bash
* * * * * /bin/bash ~/bin/mailip.sh
```

Note: The first line is to force cron to use Bash as a shell, which our script requires.

Save and quit nano (Ctrl-O, Ctrl-X).

Your cronjob should now run your script every minute. Next time your Pi changes location, you will be notified of its new IP address!
