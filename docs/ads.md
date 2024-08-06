
To block ads, append denylist entries in this file to local hosts file.

https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts

For example,

```bash
# back up existing hosts file
sudo cp -p /etc/hosts /etc/hosts.orig

# append only the 0.0.0.0 entries
grep ^0\.0\.0\.0\  hosts | sudo tee -a /etc/hosts
```
