
## First, check if chrony is already on your system:
```bash
rpm -q chrony
```
##  Configure chrony to use your server
```bash
sudo vi /etc/chrony.conf
```
## You should comment out or remove the existing default pool lines and add a line for your server. Using the iburst option will speed up the initial synchronization.
```bash
# Comment out the default pool lines by adding a '#' at the start of the line
# pool 2.rocky.pool.ntp.org iburst

# Add your specific NTP server
server 192.168.243.100 iburst
```
## Start, enable, and check the service
```bash
sudo systemctl restart chronyd
sudo systemctl enable chronyd
```
## Use the following command to verify your server is now being used as a time source. It may take a minute for the synchronization to complete
```bash
chronyc sources -v
```
