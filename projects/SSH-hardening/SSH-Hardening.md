# SSH Hardening

The purpose of SSH Hardening is to add protections to my server that reduce the attack surface without making the server super hard to manage.

## Goal

Harden SSH to reduce the attack surface while not making the server any more difficult to manage.

## SSH Keygen

I created a Key Using
```bash
ssh-keygen -t ed25519 -C "jack-homelab"
```

Then I copied it over to the server using
```bash
ssh-copy-id jack@192.168.0.150
```

Now I'm able to log in with my SSH key using
```bash
ssh jack@SERVER_IP
```

Now that this works properly, we can move on to SSH configuration, where we can disable password authentication and rely on the generated key for logging in remotely.

## SSH Configuration Changes

On the server, you can access your SSH configuration in the following ways:
```bash
sudo nano /etc/ssh/sshd_config
```
Here is the list of changes I made to better secure SSH:
PasswordAuthentication no - Disable passwords, secures against brute-force attacks.
PermitRootLogin no    - Disables the ability to log in as root using SSH.
MaxAuthTries 3 - Limit failed login attempts
PubkeyAuthentication yes - Enables SSH public key auth, highly secure passwordless login
X11Forwarding no -  disables the ability to tunnel graphical user interface (GUI) applications from a remote server to your local machine.
AllowAgentForwarding no - Disable agent forwarding.


These changes are validated with:
```bash
sudo sshd -t
sudo systemctl reload ssh
```

## Notes

I may make additional SSH hardening changes in the future, but some planned homelab projects may require certain SSH features to remain enabled.



