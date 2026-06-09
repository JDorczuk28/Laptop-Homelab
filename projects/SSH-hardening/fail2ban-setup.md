# FAIL2BAN
Fail2ban is a free, open-source intrusion prevention software that protects Linux servers from brute-force attacks

## Goal

Utilize Fail2Ban as well as SSH-hardening in order to protect my homelab server from outside SSH attacks.

## Install and Setup

We can install fail2ban using
bash```
sudo apt update
```

to make sure everything is up to date first, then:
bash```
sudo apt install fail2ban
```
which installs the software.

## Configuration

From here we can create a jail override file, which inherits all the defaults from the config file minus the changes that we make in the override file, we can do that by doing:
bash```
sudo nano /etc/fail2ban/jail.d/sshd.local
```

These are the contents of that file, which protect my server from brute force:
text```
[sshd]
enabled = true
port = 22 
filter = sshd
maxretry = 3
bantime = 6000
findtime = 600
```

[sshd] - configures jail named sshd, applies to ssh by watching auth.log
enabled = true - turns it on
port = 22 - watches ssh port
filter = sshd - Uses the built-in sshd filter rules
maxretry = 3 - you get 3 login attempts
bantime = 6000 - on failure of those 3, offending IP gets banned for 100 minutes
findtime = 600 - looks back over a 600-second, or 10-minute window. (3 failures in 10 minutes results in a 100-minute ban)

## Activation 

We can enable fail2ban using:
bash```
sudo systemctl enable fail2ban
```

Then start the service using:
bash```
sudo systemctl start fail2ban
```

We can then check the status using:
bash```
sudo fail2ban-client status sshd
```

which gives a status screen like this:
<img width="553" height="148" alt="image" src="https://github.com/user-attachments/assets/0a4a146c-c883-4c06-ab91-ead62b872455" />






