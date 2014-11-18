# Raspberry Pi 101

## Worksheet 3 - Acessing the Pi via SSH, and initial configuration

---

### Step 1 - SSH into the Pi using your Pi IP address

This will depend on your computer (Windows/Mac/Linux). Your instructor will guide you through it.

For Mac/Linux users:

```ssh pi@your_pi_ip_address```

Windows users should use Putty for this.

You may be prompted with a message such as:

```
The authenticity of host 'x.x.x.x (x.x.x.x)' can't be established.
RSA key fingerprint is 76:54:43:78:3a:6e:0e:50:51:43:d2:f4:63:33:8a:05.
Are you sure you want to continue connecting (yes/no)? yes
```

Make sure to type 'yes' and Enter.

Use the same password as in the previous exercise (raspberry).

Again you may see the message:

```
"NOTICE: the software on this Raspberry Pi has not been fully configured. Please run 'sudo raspi-config'"
```

We will address that now.

### Step 2 - Configuring your Pi

Type:

```
sudo raspi-config
```

We need to change the following options (follow the instructor on screen):

* Internationalisation -> Change TimeZone
* Advanced -> Hostname (change the hostname, and make sure to add a FQDN after it. ie: mypi.mydomain.com)
* Finish -> and select OK to reboot

### Step 3 - Rebooting your Pi


Whilst rebooting you may want to ping your Pi IP to check when it comes back online.


Wait a few more seconds and SSH back to the Pi (if initial attempts to SSH fail, wait and try again. The Pi's SSH service may take a while to startup)

