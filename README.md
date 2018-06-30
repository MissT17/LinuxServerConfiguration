# Project Description
This project is dedicated to the deployment of two applications on Ubuntu server with IP: 52.47.160.192:
- [restaurant application](http://restaurants.52.47.160.192.xip.io) 
- [bestrecs application](https://bestrecs.miss-t.ch)

## Access Instructions
Both applications are accessible via two links mentioned above. In order to get connected to the server, please connect to the mentioned above applications via ssh by following the instructions below:
1. Clone the Github repository to your local machine
```
$ git clone https://github.com/MissT17/LinuxServerConfiguration.git <optional folder name>
``` 
2. Save the key mentioned in the submission note in the key.pem file and save it locally
3. Connect to the server by using the following command line:
```
$ ssh -i ./path/to/the/key.pem grader@52.47.160.192 -p 2200
``` 
2200 is the configured `ssh` port


## Configurations
1. The list of the following software was installed for the project:
- `apache2` - as standard installation for Ubuntu 16.04
- `git` - allows to push/pull code directly to github
- `mod_wsgi` - Apache module necessary to run Python-based `restaurants` application 
- `python-pip` - necessary to install Python dependencies
- `certbot` - as the `bestrecs` app requires users to share their location, an `https` connection is required for the application. The Let's Encrypt client `certbot` allows to generate, renew and set up the SSL certificate for the application
- `mod_rewrite` - necessary to redirect traffic from http site to https
2. The firewall has been adjusted as such:
- Lightsail firewall: ports 80(HTTP), 443(HTTPS), 2200(SSH), and 123(NTP) were opened
- Ubuntu firewall: ports 80, 443, 123 and 2200
- Apache firewall: ports 80 & 443, i.e. Apache Full active
3. Both applications have the following directory structure:
- the document roots are placed in /var/www folder;
- each application has a `public_html` folder that contains all the application files
- virtual hosts configuration files(`bestrecs.conf`, `bestrecs-le-ssl.conf`, `restaurants.conf`) are under `/etc/apache2/sites-available` and contain `ServerName`, `ServerAlias`, `DocumentRoot`, `SSL keys`, path to `WSGI file`
- `/bestrecs/public_html` also contains an `.htaccess` file that contains rules related to redirections from http to https for the application 
3. `Xip.io` has been used to create a substitute domain name for the restaurants application
4. Documents have the following permissions:
- bestrecs all folders give `root` 755 permissions
- restaurants applications provides 755 (folders) and 644 (files) permissions to www-data user in order to write and read data related to the database 


## Expected Outcome
Both applications should be accessible online via provided URLs.
- Betsrecs applications should allow the user to share his/her geolocation and get additional information on the place of his/her choice both on the map and in the section "More details"
- Restaurants application should allow the user to consult, create and edit restaurants after login with social media accounts. 
- Applications should be accessible with `grader` user via `ssh`. 

## License:
In the restaurants application, the photos are taken from [http://kaboompics.com/](http://kaboompics.com/) and are available according to kaboompics own [license](https://kaboompics.com/page/license-and-faq) for free use with the exception of redistribution.
In the bestrecs application, additional information about places is provided by Foursquare.