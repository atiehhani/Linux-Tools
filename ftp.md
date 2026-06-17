## ftp command for connect to a ftp server

Connect to FTP server  
> `ftp ftp.example.com`  
or with specific port  
> `ftp ftp.example.com 2121`  

Once connected, enter username and password  

Navigate to desired directory  
> `cd /path/to/remote/directory`  

List files to see what's available  
> `ls`  

Download a single file  
> `get filename.txt`  

Download multiple files  
> `mget *.txt`  

Download entire directory (must enable prompt first)  
> `prompt`  
> `mget *`  

Or use recursive download (if supported)  
> `recursive`  
> `mget *`  

Exit  
> `bye`

Download all directories recursively  
> `wget -r -np -nH --cut-dirs=1 ftp://username:password@ftp.example.com/`  

Or download specific directories  
> `wget -r -np -nH --cut-dirs=1 ftp://username:password@ftp.example.com/1404-08-06/`  
> `wget -r -np -nH --cut-dirs=1 ftp://username:password@ftp.example.com/1404-08-10/`  

