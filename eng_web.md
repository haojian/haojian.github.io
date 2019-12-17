Web
===========

## React

- This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).
- backend nodejs.
- frontend react code.
- [What is “export default” in javascript?](https://stackoverflow.com/questions/21117160/what-is-export-default-in-javascript)


## Fast website hack

- Backend: a restful service api
	- [Build Node.js RESTful APIs in 10 Minutes](https://www.codementor.io/olatundegaruba/nodejs-restful-apis-in-10-minutes-q0sgsfhbd)
	



## Content publish platform

- Ghost configuration on ubuntu
	- [install node.js with Node Version Manager](http://www.hostingadvice.com/how-to/install-nodejs-ubuntu-14-04/)
	- [official ghost installation](http://support.ghost.org/installing-ghost-linux/)
		- for network error: `npm config set registry https://registry.npmjs.org/`
	- [change the directory permission](http://askubuntu.com/questions/162866/correct-permissions-for-var-www-and-wordpress)
	- [deployment](http://support.ghost.org/getting-started/)
		- [deploy ghost through init script](http://support.ghost.org/deploying-ghost/#init-script)
		- [nginx guide](http://support.ghost.org/basic-nginx-config/)
			- [test nginx in localhost](http://stackoverflow.com/questions/10095219/how-to-test-nginx-subdomains-on-localhost)
				- (/etc/hosts in *nix).
			- make it work in through ip directly: modify the remote machine's /etc/hosts
- Ghost development
	- [private api](https://api.ghost.org/docs/getting-started)
	- [all the endpoints](https://github.com/TryGhost/Ghost/wiki/%5BWIP%5D-API-Documentation#endpoints)
	
- idea image host: [aws s3 + amazon cloud front cdn](http://stackoverflow.com/questions/12148390/how-do-i-use-aws-s3-to-store-user-uploaded-pictures)

- ghost localization: i18n for ghost;  [Transifex code injection approach](https://docs.transifex.com/integrations/ghost/)

- common ghost commands
	- `sudo service ghost restart`
	
- host multiple ghost on the same machine.
	- [How To Serve Multiple Ghost Blogs on One VPS Using Nginx Server Blocks](https://www.digitalocean.com/community/tutorials/how-to-serve-multiple-ghost-blogs-on-one-vps-using-nginx-server-blocks)
		- P.S. 1. pay attention to the user access. the default user access for upstart script is root users. However, by default root users have no access to node or npm.
			- two ways to hack this problem. 1. add node package and npm to root users. 2. specify the user id in the upstart script or the original System V script.
		- P.S. soft link the files in nginx configuration (sites-available and sites-enabled.)
		- `init-checkconf ghost-main.conf `
		- install npm for root users. `sudo apt-get install npm`
		- install node for root users. `sudo ln -s /home/ubuntu/.nvm/versions/node/v4.2.6/bin/node /usr/bin/node`

- [ghost-sqlite3-to-mysql](http://blog.benoitblanchon.fr/ghost-sqlite3-to-mysql/)
- [MySQL: How to clone a database](https://makandracards.com/makandra/1605-mysql-how-to-clone-a-database) *working version*

## web deployment.

- [使用Tornado+Nginx部署Django的一种尝试](http://fendou.org/post/2012/06/01/tornad-nginx-django/)
- [Idiomatic Django Deployment - The Definitely Definitive Guide](http://rogueleaderr.com/post/65157477648/the-idiomatic-guide-to-deploying-django-in)


## Lightweight webserver.
- `python -m SimpleHTTPServer` The local directory would be the web directory.
	- super simple and fast. but doesn't support audio/video streaming.
- nodejs solution: `npm install http-server -g`; `http-server -p 8000`
- `twistd -no web --path=.`


## programmable CSS

- tool: Koala
- [SASS用法指南](http://www.ruanyifeng.com/blog/2012/06/sass.html)

##Security

##Jetty

##Apache

- [How to install apache and php on Mac](http://machiine.com/2013/how-to-install-apache-and-php-on-a-mac-with-osx-10-8-mamp-part-1/)
- [在OS X 10.8 Mountain Lion上配置Web服务器（Apache+PHP）](http://blog.shengbin.me/posts/os-x-10.8-mountain-lion-setup-web-server-apache-php/)
- [Nice note regarding config](http://note.rpsh.net/posts/2013/11/27/osx-10-9-apache-server-php-mysql)
- [apache on mac](http://osxdaily.com/2012/09/02/start-apache-web-server-mac-os-x/)



##PHP
-[Write Post data to file with PHP](http://stackoverflow.com/questions/4742898/write-post-data-to-file-with-php)
- [Upgrade the default php in mac](https://www.computersnyou.com/68/how-to-upgrade-php-in-mac-osx-compiling-from-source/)
- [Multiple PHP version](http://getgrav.org/blog/mac-os-x-apache-setup-multiple-php-versions)
- manually install the php:
```./configure  --with-apxs2=/usr/sbin/apxs   --with-mysql   --with-gd   --with-jpeg-dir  --enable-gd-native-ttf    --with-freetype-dir
```
- [ssh in localhost](https://plus.google.com/+FrancoisBeaufort/posts/5rWjum26uVY)


##Chrome extension
- [Sending Messages Between the Background and the Content Script of a Chrome Extension](http://willvk.blogspot.com/2013/05/sending-messages-between-background-and.html)

**AWS**


for amazon normal linux machine
```
yum install lapack lapack-devel blas blas-devel
pip install numpy
pip install scipy
```

for ubuntu
```
sudo apt-get install python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose
```




