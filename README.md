* Build and Test environment: CentOS Linux release 7.2.1511 (Core) 

Docker install
=======================

Step 1: Installation of Docker
-----

``` bash
yum -y update && yum -y install docker docker-registry
```

Step 2: Start Docker and Make Sure Docker Starts on Boot
-----

``` bash
systemctl enable docker.service

systemctl start docker.service

systemctl status docker.service
```

Install Official OCS Inventory Docker Image Released by Richardson Lima
=======================
Step - 1 Pulling our image from the Docker repository
```bash
docker pull richardsonlima/ocs-inventory-ng
```

Step - 2 Run container
``` bash
docker run -d -p 80:80 -p 3306:3306 richardsonlima/ocs-inventory-ng
```

Make sure to change tagname with your desired image repository TAG.

https://hub.docker.com/r/richardsonlima/ocs-inventory-ng/

Install from git repo - docker-ocs-inventory-ng
=======================

Out-of-the-box OCS-Inventory-NG Server image based on CentOS 6.6

Usage
-----

```bash
yum install git -y 
git clone https://github.com/richardsonlima/docker-ocs-inventory-ng.git
```

To create the image `yourname/ocs-inventory-ng`, execute the following command on the docker-ocs-inventory-ng folder:
```bash
	docker build -t yourname/ocs-inventory-ng .
```

You could push your new image to the registry
```bash
	docker push yourname/ocs-inventory-ng
```

Running your OCS-inventory-ng docker image
------------------------------------------

Start your image binding the external ports 80 and 3306 in all interfaces to your container:
```bash
	docker run -d -p 80:80 -p 3306:3306 yourname/ocs-inventory-ng
```

Test your deployment:
```bash
	curl http://localhost/ocsreports/
```

Technical Detail
----------------

This approach is based on [official wiki server installation guide](http://wiki.ocsinventory-ng.org/index.php/Documentation:Server). In other word, it includes all LAMP module plus perl, mod_perl, and it's dependencies.

To mount your existing inventory database (MySQL), do this:
```bash
	docker run -d -p 80:80 -p 3306:3306 -v /path/to/your/mysql/directory:/var/lib/mysql -v  /path/to/your/mysql/setting/dbconfig.inc.php:/usr/share/ocsinventory-reports/ocsreports/dbconfig.inc.php yourname/ocs-inventory-ng
```

It also expose port 3306 for MySQL connection; just in case you need it.
