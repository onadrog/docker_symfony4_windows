## First of all:
Be sure you have docker and the VM installed on your machine, else check this link:
https://docs.docker.com/toolbox/toolbox_install_windows/<br>
Ok! Now we can start real projects like pros !

If you don't have composer installed go for it: https://getcomposer.org/download/

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
#### Configuration:

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
### Initialisation:
In the docker directory open the terminal and run:
```html
$ docker-machine start default
$ docker-compose build
$ docker-compose up -d
```

### Get the machine ip
Now we need to know the machine ip so in your terminal type:
```html
$ docker-machine ip
```
Ok now we have what we lookking for!<br>
We have 2 options now we can use the ip directly in the browser or we can add the ip to our host file in windows.
Ok for the example we'll considering our docker-machine ip is 192.168.99.100

### If you're lazy:
In your brower open:<br> 
http://192.168.99.100:8000 for your Symfony project<br>
http://192.168.99.100:8080 for phpMyadmin (user=root, and no pass)<br>
http://192.168.99.100:8002 for maildev<br>

### If you want to add your own host name:

Go to "C:\Windows\System32\drivers\etc"<br>


Add your docker-machine ip we get earlier in the "hosts" files like this:

````html
#
192.168.99.100 exampledev.dock
::2 example
````
Use whatever name you want.<br>
Nice! we can use:<br>
http://exampledev.dock:8000 for your Symfony project <br>
http://exampledev.dock:8080 for phpmyAdmin (user=root, and no pass)<br>
http://exampledev.dock:8002 for maildev <br>

### For stoping docker, run:
```html
$ docker-comppose kill
```
### If you want to delete all the containers, network and images, run:
```html
$ docker system prune -a
```

----
Hope that help you and enjoy coding :)