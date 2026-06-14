# timedatectl
You can use this command to enable NTP synchronization:  
```bash
sudo timedatectl set-ntp true
```
To verify that NTP synchronization is active, run:  
```bash
timedatectl
```
Look for lines in the output that confirm NTP service: active and System clock synchronized: yes  
