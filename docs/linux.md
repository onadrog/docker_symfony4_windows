## First of all:
Be sure you have docker installed on your machine, else check this link:
https://docs.docker.com/engine/install/<br>
Ok! Now we can start real projects like pros !

If you don't have composer installed go for it : https://getcomposer.org/download/


## Instalation:
Start your symfony project with:
```html
$ composer create-project symfony/skeleton your-project-name
```
or<br>
```html
$ composer create-project symfony/website-skeleton your-project-name
```

Then paste the docker directory in your project directory root.

#### Architecture:
Now you should have something like this:<br>
```bash
Your-project-name
|_docker
|  |__php74
|  |  |___Dockerfile
|  |   |__php.ini
|  |_vhosts
|  | |_vhosts.conf
|  |_docker-compose.yml
|_bin
|_composer.json  
|_composer.lock  
|_config  
|_data  
|_public  
|_src  
|_symfony.lock  
|_templates  
|_var  
|_vendor  
```
-----
### Configuration:

If you want the latest mysql insted of mysql 5 just change
```tmml
db:
    image: mysql:5
```
with:
```html
db:
    image: mysql
```
or whatever version you want.
#### Initialisation:
In the docker directory open the terminal and run:
```html
$ docker-compose build
$ docker-compose up -d
```

### Finally:
In your brower open:<br> 
http://localhost:8000 for your Symfony project<br>
http://localhost:8080 for phpMyadmin (user=root, and no pass)<br>
http://localhost:8002 for maildev<br>

---
# Going further :

## The following guide is only if you're running your project on different OS (here ubuntu distros and windows) :
If you want to change the ip to be the same if you're working on windows machine (and don't want to change the .env file each time) you can type the following command:

```html
$ docker-compose down
$ sudo service docker stop
$ sudo gedit /lib/systemd/system/docker.service
```
Add this line at the end of  "`ExecStart=/usr/bin/dockerd`"  line:
```html
--bip "192.168.99.100/24" 
```

reload deamon and docker:

```html
$ sudo systemctl daemon-reload
$ sudo service docker start
```

### If you're lazy:
In your brower open:<br> 
http://192.168.99.100:8000 for your Symfony project<br>
http://192.168.99.100:8080 for phpMyadmin (user=root, and no pass)<br>
http://192.168.99.100:8002 for maildev<br>

### Adding your own host name:

type:<br>

```html
$ sudo gedit /etc/hosts
```


Add your new ip address at the end of hosts file, like this:

````html
192.168.99.100 exampledev.dock
````

Save, then restart your containers: <br>
```html
$ docker-compose down
$ docker-compose up -d
```

Use whatever name you want.<br>
Nice! we can use:<br>
http://exampledev.dock:8000 for the project Symfony project<br>
http://exampledev.dock:8080 for phpmyAdmin <br>
http://exampledev.dock:8002 for maildev <br>

### For stoping docker, run:
```html
$ docker-comppose down
```
### If you want to delete all the containers, network and images, run:
```html
$ docker system prune -a
```

----
Hope that help you and enjoy coding :)