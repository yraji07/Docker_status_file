Workbook -2  
----------------- 
### Create an alpine container in interactive mode and install python 
docker run -it alpine /bin/sh
docker container run -d --name C1 alpine sleep 1d
`apk update`
`apk add python3`
`apk python3 --version`
`exit`
![preview](alpineimg/Screenshot%202023-04-18%20164646.png)
![preview](alpineimg/2.png)
![preview](alpineimg/3.png)
![preview](alpineimg/4.png)
![preview](alpineimg/5.png)

--------------------------------------------------------------------------------------
### Create an ubuntu container with sleep 1 d and then login using exec. Install python 

$ docker container run -d --name raji ubuntu sleep 1d
$ docker container exec -it raji /bin/sh
# apt update
# apt install python3
# python3 --version
# exit
![preview](2ndimgs/1img.png)
![preview](2ndimgs/2img.png)
![preview](2ndimgs/3img.png)

----------------------------------------------------------------------------------------
### Create a postgres container with user panoramic and password as trekking. Try logging in and show the databases (query for the psql)
 
$ docker container run -d --name rajipostgress -P -e POSTGRES_DB=employees -e POSTGRES_USER=panoramic -e POSTGRES_PASSWORD=trekking postgres
![preview](imgs/Screenshot%202023-04-18%20145544.png)

 `docker exec -it rajipostgress /bin/bash`

![preview](imgs/Screenshot%202023-04-18%20145629.png) 

$ CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
); 

Insert into Persons Values (1,'raji','lokesh', 'raji', 'lokesh'); Insert into Persons Values (2,'raji','lokesh', 'pragathinagar', 'hyd'); Insert into Persons Values
(3,'geetha','rayudu', 'pragathinagar', 'hyd'); Insert into Persons Values (4,'navya','ranganayakulu', 'banglore', 'banglore');

$ Select * from Persons;

$ exit 

![preview](imgs/Screenshot%202023-04-18%20145717.png)

-----------------------------------------------------------------------------------------------

### Try creating a dockerfile which runs phpinfo page, user ARG and ENV wherever appropriate o on apache server o on nginx server 
 
Dockerfile
-----------

  FROM ubuntu:22.04
  LABEL author="Raji"
  ARG DEBIAN_FRONTEND=noninteractive
  RUN apt update && apt install apache2 -y && \
      apt install php libapache2-mod-php php -y && \
      echo "<? php phpinfo();?>" > /var/www/html/info.php
  EXPOSE 80
  CMD ["apache2ctl","-D","FOREGROUND"] 

 
 $ vi Dockerfile 
$ docker image build -t php .
$ docker container run --name php1 -d -p 32000:80 php
$ docker container ls

![preview](apachepageimgs/1.png) 
![preview](apachepageimgs/2.png)
![preview](apachepageimgs/apache.png) 

-------------------------------------------------------------------------------------

### Create a Jenkins image by creating your own Dockerfile 

search from dockerhub.com for jenkins image 
now check the version of it 

Dockerfile
----------
FROM ubuntu:22.04
LABEL author="Raji"
RUN apt update && apt install openjdk-11-jdk maven curl -y
RUN curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
RUN echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
RUN apt-get update && apt-get install jenkins -y
EXPOSE 8080
CMD ["/usr/bin/jenkins"]
---

$ vi Dockerfile
$ docker image build -t jenkins .
$ docker images ls
$ docker container run --name jenkins -d -p 3000:8080 jenkins                   
$ docker container ls

![preview](jenkinsimgs/vi.png)
![preview](jenkinsimgs/cont.png) 
![preview](jenkinsimgs/jenkpage.png) 

------------------------------------------------------------

###  Create nop commerce and my-sql server containers and try to make them work by configuring
###  Create nop commerce and my-sql server containers and try to make them work by configuring
Create a docker installed vm 
Write a Docker file 

Dockerfile
---------- 
(while using this remove all quotets)
 
`FROM mcr.microsoft.com/dotnet/sdk:7.0`
`LABEL author="khaja" organization="qt" project="learning"`
`ADD https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.2/nopCommerce_4.60.2_NoSource_linux_x64.zip /nop/nopCommerce_4.60.2_NoSource_linux_x64.zip`
`WORKDIR /nop'`
`RUN apt update && apt install unzip -y && \`
   ` unzip /nop/nopCommerce_4.60.2_NoSource_linux_x64.zip && \ `
   ` mkdir /nop/bin && mkdir /nop/logs`
`EXPOSE 5000`
`CMD [ "dotnet", "Nop.Web.dll","--urls", "http://0.0.0.0:5000" ]`

Then execute this commands:
------------------------------
`  vi Dockerfile  `
`  docker image build -t nop:latest  `
`  docker network create -d bridge nop_bridge  `
`  docker volume create nop_db  `
`  docker container run -d --name mysql -e MYSQL_ROOT_PASSWORD=rajiloki123 -e MYSQL_DATABASE=employees -e MYSQL_USER=raji -e MYSQL_PASSWORD=rajiloki123 --network nop_bridge -v nop_db:/var/lib/mysql mysql:5.6 `
`  docker container run -d --name nopcommerce -e MYSQL_SERVER=mysql --network nop_bridge -P nop:latest  ` 

Now check the container and see 

![preview](nopmysql_img/1.png)

![preview](2ndimgs/2img.png)

![preview](nopmysql_img/Screenshot%202023-04-20%20170040.png) 


 










