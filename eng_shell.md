Shell commands
===========

## common shells

- [what process has open linux port](http://www.cyberciti.biz/faq/what-process-has-open-linux-port/)



sudo chown -R $(whoami) /data

## Use screen for nohup session

You want to be using GNU Screen. It is super awesome!

```
ssh me@myserver.com
screen               #start a screen session
run-a-long-process
```

CTRL+a , d to detatch from your screen session
```
exit                 #disconnect from the server, while run-a-long-process continues
```

When you come back to your laptop:

```
ssh me@myserver.com
screen -ls  # list the running screen session
screen -r            #resume the screen session
```
Then check out the progress of your long-running process!

To start a new session with a name
```
screen -S your_session_name
```

Kill a screen session:
```
screen -S your_session_name -X quit
```


<!-- -->


## 

- get the total size of files: `du -ch debug/* | grep total`


## Avoid password during the login

```
ssh-keygen -t dsa
cd ~/.ssh
cat id_dsa.pub | ssh ubuntu@ip 'cat - >> ~/.ssh/authorized_keys'
```


## Remote debugging
- Mounting a remote folder on OS X over SSH:
	`sshfs username@hostname:/remote/directory/path /local/mount/point`

## text processing shell

- `echo -e 'hello\nworld' | sed ':a;N;$!ba;s/\n/\\n/g'`


## Brew shells

- list the brew packages: `brew list`
- [reinstall a package with homebrew](http://superuser.com/questions/324980/how-do-you-re-install-a-package-with-homebrew-mac)
- Check all available options for ffmpeg with: `brew options ffmpeg`
- Check if your Homebrew installation is up to date and working with `brew doctor`

## Common Aws shells

- check available disk space on aws: `df -h`



[How To scp, ssh and rsync without prompting for password
](https://blogs.oracle.com/jkini/entry/how_to_scp_scp_and)



## Examples:

** file replacement **

```
files=`find .  -name "local.properties.default"`
for ff in $files; do
    dd=`dirname $ff`
    echo $ff    $dd;
    cat $ff | sed "s/android\.sdk\.dir=CHANGE ME/android\.sdk\.dir=\/Users\/haojian\/Development\/adt-bundle-mac-x86_64-20130717\/sdk/g"  > $dd/local.properties
done
```

## Keep task running even disconnect SSH

nohup command



## Background running

```
ctrl + z //stop
bg //running in background
fg //running in foreground
ps //print running process
```

```
ctrl + z //stop
bg //running in background
disown -h [job-spec] where [job-spec] is the job number (like %1 for the first running job; find about your number with the jobs command) so that the job isn't killed when the terminal closes.
ps //print running process
```


```
history | tail
```



## Network

**cURL**
- Get with JSON: `curl -i -H "Accept: application/json" -H "Content-Type: application/json" http://hostname/resource
`
- Get with XML: `curl -H "Accept: application/xml" -H "Content-Type: application/xml" -X GET http://hostname/resource
`
- Data post: `curl --data "param1=value1&param2=value2" http://hostname/resource
`
- File post: `curl --form "fileupload=@filename.txt" http://hostname/resource
`
- Logging: `curl -d "username=admin&password=admin&submit=Login" --dump-header headers http://localhost/Login
curl -L -b headers http://localhost/`


**SSL/HTTPS**

```
openssl s_client -showcerts -connect mobilelogs.labs.yahoo.com:443
```


## Disk Util

View all available HDD's/partitions: `sudo lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL`


### for gfw:

- [official website](http://www.shadowsocks.org/en/index.html)