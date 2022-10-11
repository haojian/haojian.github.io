backend
====================

**Blockchain**

- Three layers: distributed ledger database, consensus, smart contracts. [blockchains for enterprise usages](https://youtu.be/Zyv8OXyAdVk?t=500)

**Database**

- [Trouble shotting PostgreSQL](http://stackoverflow.com/questions/29937378/django-db-utils-operationalerror-could-not-connect-to-server)
	```
	It can be some issues:

	PostgreSQL is not running. Check it with sudo service postgresql status
	Your PostgresSQl is not running on port 5432. You can check it typing sudo netstat -nl | grep postgres
	You have something wrong trying to connect to your db like the username, the password or the databasename. Check that they are what postgres ask for you to connect it and that is the db_name that you want to access to.
	Problems with postmaster.pid in postgres. It can happen because of a shutdown unproperly done. It makes to remind a pid alive that doesn't allow your server start. To fix it you have to:

	 * rm /usr/local/var/postgres/postmaster.pid 
	 * pg_resetxlog -f /usr/local/var/postgres
	After this it should run properly if you make the runserver of postgres
	Help in Mac OSX: how to start postgresql server on mac os x
	```

**PostgreSQL**

- intallation on mac
	```
	For MAC:

	Install Homebrew
	brew install postgres
	initdb /usr/local/var/postgres
	/usr/local/Cellar/postgresql/<version>/bin/createuser -s postgres
	To start server at startup

	mkdir -p ~/Library/LaunchAgents
	ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
	launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
	Now, it is set up, login using psql -U postgres -h localhost or use PgAdmin for GUI.

	By default user postgres will not have any login password.

	Check this site for more articles like this: https://sites.google.com/site/nitinpasumarthy/blog/installingpostgresonmac
	```

	```
	To restart postgresql after an upgrade:
  	brew services restart postgresql
	Or, if you don't want/need a background service you can just run:
  	/usr/local/opt/postgresql/bin/postgres -D /usr/local/var/postgres
	```

	```
	# if install through brew, the default superuser name is the machine user name. 
	psql postgres
	sudo -u machineusername createuser dpppt
	```
	[instructions](https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91)
	

** Multiple machine deployment **

- [Pythonic remote execution](http://www.fabfile.org/)


**Links**

- [The WhatsApp Architecture Facebook Bought For $19 Billion](http://highscalability.com/blog/2014/2/26/the-whatsapp-architecture-facebook-bought-for-19-billion.html)
- [AWS setup](http://www.cnblogs.com/deltacat/p/3294865.html)

**crawl**

- [Pyspider](https://github.com/binux/pyspider)
	- pycurl problems in compiling: 
		- if  has some problem, run ``curl --version`` to see the version first
		
			```
			240  curl --version
  			241  sudo -E pip uninstall pycurl
  			242  export PYCURL_SSL_LIBRARY=nss
  			243  sudo -E pip install pycurl
			```
		- "Could not run curl-config": 
			``` sudo yum install curl curl-devel ``` 
			
		- "fatal error: libxml/xmlversion.h: No such file or directory ":
			`` sudo yum install libxml2-devel libxslt-devel python-devel
 ``
		
**EC2**

- [Django + Python2.7 + Apache setup for AWS EC2 - LINUX](https://gist.github.com/havencruise/8307140)
- [Apache MySQL + PYTHON ON ec2](http://fstoke.me/blog/?p=3708)
- [在Amazon的EC2上部署nginx+web.py](http://pinkyjie.com/2011/04/09/build-nginx_webpy_on_amazon_ec2/)

- AWS common products
	- S3: File storage, FTP
	- EC2: Serve website, run different code.
	- CloudFront: SSN
	
	
## Websocket
- [libwebsockets (c)](https://github.com/warmcat/libwebsockets)
	- lightweight websocket
- [pywebsocket](https://code.google.com/p/pywebsocket/)


### Common SQL commands

```
// bash terminal
mysql -u USERNAME -h HOSTNAME -p
mysql -u root -p		# login a local database server
mysqldump ghost | mysql ghost-main	# clone database; may need to add the root access and password setting
```

```
show databases;
```

- [MySQL: How to clone a database](https://makandracards.com/makandra/1605-mysql-how-to-clone-a-database) *working version*

### Postgresql

[move the data directory](https://stackoverflow.com/questions/37901481/postgresql-change-the-data-directory)



### mongodb

####  import data 

[Insert 200+ million rows into MongoDB in minutes](https://www.khalidalnajjar.com/insert-200-million-rows-into-mongodb-in-minutes/)
mongodump -d dbname --gzip --archive=dbname.dump.gz
mongorestore -d dbname --gzip --archive=dbname.dump.gz


#### Common commands to start mongodb:

1. check if mongodb is running: `ps aux |grep mongod`
2. start mongodb: `sudo /etc/init.d/mongod restart`
3. starting mongodb service to start at book and activate it:
	`sudo update-rc.d mongod on`
	`sudo /etc/init.d/mongod start`
4. [Changing mongoDB data store directory](https://stackoverflow.com/questions/5961145/changing-mongodb-data-store-directory)
5. client: `mongo`; server: `mongod`

#### Problem diagnostic

1. Failed global initialization: FileNotOpen Failed to open "/data/mongod.log":  
    - `add sudo`
2. Remove the sudo permission requirement for /data/db: 
    - `sudo chown -R mongodb:mongodb /data/db`
3. [initandlisten] exception in initAndListen: 98 Unable to create/open lock file: /data/db/mongod.lock errno:13 Permission denied Is a mongod instance already running?, terminating 
    - `sudo chown -R mongodb:mongodb /data/db`

#### Typical configration

1. dbpath:     `dbpath=/var/lib/mongodb`
2. where to log: `logpath=/var/log/mongodb/mongod.log`
3. Install mongodb on aws:
    - need to configure the dbpath to EBS
4. Install mongodb locally: [MongoDB configuration](https://ruby-china.org/topics/454)
5. Re-init mondogb replicate set. 
    - [更换复制集节点](http://docs.mongoing.com/manual-zh/tutorial/replace-replica-set-member.html)
    - [移除复制集的节点](http://docs.mongoing.com/manual-zh/tutorial/remove-replica-set-member.html)
    - [Change Hostnames in a Replica Set](http://docs.mongodb.org/manual/tutorial/change-hostnames-in-a-replica-set/)

6. Default configuration file: 
    - `/etc/mongod.conf`

#### MongoDB data query

- enter "mongo" to enter interactive terminal.

    ```
    rs.slaveOk()
    show dbs
    use one_db
    db
    db.[collection]
    db.[collection].count()
    db.[collection].find()
    db.dropDatabase() // delete the database
    db.[collection].drop() // delete the collection
    db.getCollectionNames() //list collection names
    db.[collection].find( { city: "London" } ).skip( 20 ).limit( 20 ) // show the results from document 21 to 40.
    db.player_info.find({"pid":NumberLong("4294967295")}).count()
     db.player_info.find().sort({$natural:-1})         // get the last entry
    ```

- data check and backup. [chinese guidance](http://www.jb51.net/article/40285.htm)

- check replicate set configurations. 
    - rs.status()
   
   
- Backup data.
    - [import and export](http://docs.mongodb.org/manual/core/import-export/) one handy way is do it through json. (it's actually bson rather than json)
    - use the bson package inside pymongo. pip install pymongo
    

- create text search index
    - > db.ttlsa_com.ensureIndex({"song":"text", "lyrics":"text"})
    - > db.ttlsa_com.ensureIndex({"$**": "text"})   
        - $**表示在所有的字符串字段上创建一个全文索引。
    - > db.ttlsa_com.ensureIndex({"song":"text"},{"weights":{"song": 2, "$**": 3}}) 也可以指定权重

- text search
    - db.command('text', 'collection', search='lamps')


#### Pymongo interface

- [example](https://pypi.python.org/pypi/pymongo/)
- [full text search](https://www.youtube.com/watch?v=Wk6sucAgC8k)
- db.command('text', 'pin_details', search='lamps')


## redis



#### Common commands

- print all the keys: `keys **`
- check type of the key: `TYPE keyname`
- read the basic data type: `get keyname`
- read the set data value: `SMEMBERS keyname`
- read the list data value: `LRANGE keyname 0 -1`
- print the length of list: `LLEN keyname`
- print the element of the list: `LINDEX keyname 0`
- show all dbs: `info keyspace`

#### Install Redis

- for ubuntu
	```
	sudo apt-get install -y redis-server
	sudo update-rc.d redis-server on
	sudo service redis-server restart
	redis-cli ping => verify if it works
	```
	
- the permission of dump.rdb:  `sudo chmod 640  dump.rdb`