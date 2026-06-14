# new works on servers for timezone:  
1-Download the package tzdata2022b.tar.gz and decompress (you should be root user); see All Packages. 
__(OS)__
```bash 
#1-1) 
mkdir /timezone 
#1-2)
cd /timezone
#2-)    
tar -xzvf tzdata2022b.tar.gz
#3) 
zic asia 
#4)
zic -l Asia/Tehran
#4)  
rm -rf /etc/localtime
#5) 
ln -s /usr/share/zoneinfo/Asia/Tehran /etc/localtime
#6) 
zdump -v /etc/localtime ====> last line must be 2022 ====> normal before dst is 2499
#7)set time manaully ===> 
date -s "21 Mar 2025 23:55:00"
```
8) reset core and batch   
================================================================================================================  
# for java timezone :  
see version of java on java app:   
for example if java version is jdk1.08.231   
```bash
cd /opt/jdk1.08.231/bin 
```
download 2 file:   
__1- tzupdate file__   
__2- download tzdata.tar.gz__   

```bash
/opt/java/jdk-17.0.1/bin/ -jar tzupdater.jar -l file:///opt/java/jdk1.8.0_231/bin/tzdata-latest.tar.gz
```

reset services
