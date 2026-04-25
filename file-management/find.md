## find
Search file.  
-iname = not case sensitive.  
-type f = just file type.  
-cmin = change minute  
```bash
find / -name hani
find / -iname hani
find / -iname hani -type f
find / -iname *.pdf -exec cp {} /home \;
find / -iname *.pdf -exec rm -rf {} \;
find / -type f -size +500M -iname "*.log*" -exec truncate -s 0 '{}' \;
find -type f -iname "test.jar*" -exec ls -lthr {} + | head -n 20 | awk '{print $9}' | xargs rm -v
find . -type f -iname "*.gz" -mtime +3 -delete
find /home -type f -iname  "api-gateway.log.*.gz" -mtime +3 -exec rm -f {} \;
find / -type f -size +500M -exec ls -lh {} \; 2>/dev/null | sort -k5 -h
sudo find /var/lib/docker/volumes/sentry-redis/_data/ -type f -name "temp-*.rdb" -delete
find . -maxdepth 1 -type f -printf '%T@ %p\n' |sort -n |head -n 5
```
