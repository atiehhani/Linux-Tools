
### login to your desire db
```
mongo --host=192.168.243.75 --port=27017 --username=newthirdparty --password='Zz151170!?' --authenticationDatabase=thirdparty --authenticationMechanism=SCRAM-SHA-256 thirdparty
```
### checking stat of a collection in that db
```
db.sabteahval.stats()
```
### for having the size of dump that you will have
* its size is in KB so "size" : 314887163344, is equal to 297 GB so you need atleast 300 GB free in your disk
```
{
	"ns" : "thirdparty.sabteahval",
	"size" : 314887163344,
	"count" : 11958891,
	"avgObjSize" : 26330,
	"storageSize" : 63749804032,
	"freeStorageSize" : 581095424,
	"capped" : false,
	"wiredTiger" : {
		"metadata" : {
			"formatVersion" : 1
		},
		"creationString" : "access_pattern_hint=none,allocation_size=4KB,app_metadata=(formatVersion=1),assert=(commit_timestamp=none,durable_timestamp=none,read_timestamp=none,write_timestamp=off),block_allocation=best,block_compressor=snappy,cache_resident=false,checksum=on,colgroups=,collator=,columns=,dictionary=0,encryption=(keyid=,name=),exclusive=false,extractor=,format=btree,huffman_key=,huffman_value=,ignore_in_memory_cache_size=false,immutable=false,import=(enabled=false,file_metadata=,repair=false),internal_item_max=0,internal_key_max=0,internal_key_truncate=true,internal_page_max=4KB
```


### dump your desire db
```
mongodump --host=192.168.243.75 --port=27017 --db=thirdparty --collection=sabteahval --username=newthirdparty --password='Zz151170!?' --authenticationDatabase=thirdparty --authenticationMechanism=SCRAM-SHA-256 --out=/root/backup/
```
* then scp dump to your destination mongo server

### restore dump NOTE : CAREFULL , IT WILL DROP OR ERASE CURRENT COLLECTION COMPLETELLY
```
mongorestore   --host=192.168.249.75   --port=27017   --username=newthirdparty   --password='Zz151170!?'   --authenticationDatabase=thirdparty   --authenticationMechanism=SCRAM-SHA-256  --drop  --nsInclude="thirdparty.sabteahval"   /root/backup/
```


## other usefull commands in mongo cli
* show the size of whole current database that we already >use db for ex: thirdparty
```
show dbs
```
