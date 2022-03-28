
install-cubejs-opensource-BI-tools-for-scratch-with-mongoDB

# Install MongoDB Community Edition on Ubuntu
# 1-Import the public key used by the package management system-
```
sudo apt-get install gnupg
```
```
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```

# 2-Create a list file for MongoDB.
```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
```

# 3-Reload local package database.
```
sudo apt-get update
```

# 4-Install the MongoDB packages.
```
sudo apt-get install -y mongodb-org
```
```
echo "mongodb-org hold" | sudo dpkg --set-selections
echo "mongodb-org-database hold" | sudo dpkg --set-selections
echo "mongodb-org-server hold" | sudo dpkg --set-selections
echo "mongodb-org-shell hold" | sudo dpkg --set-selections
echo "mongodb-org-mongos hold" | sudo dpkg --set-selections
echo "mongodb-org-tools hold" | sudo dpkg --set-selections
```

# 5-Start MongoDB.
```
sudo systemctl start mongod
```

# 6-Verify that MongoDB has started successfully.
```
sudo systemctl status mongod
```

# 6.5-repalace your runing mongodb dump into new mongo.
```
sudo mongorestore --db <dbname> --verbose ./usr/local/src/dbackups/<dbname>/
```
# 7-To verify OpenSSL is installed on your system, run the following command:
```
dpkg -l | grep -i openssl
```
# 8-Download the MongoDB Connector for BI.()
```
https://info-mongodb-com.s3.amazonaws.com/mongodb-bi/v2/mongodb-bi-linux-x86_64-ubuntu2004-v2.14.4.tgz
```
# 9-Extract the .tar archive you downloaded.
```
tar -xvzf mongodb-bi-linux-{arch}-{platform}-{version}.tgz
```
# 10-Install the programs within the bin/ directory into a directory listed in your system PATH.
```
sudo install -m755 ./mongodb-bi-linux-x86_64-ubuntu2004-v2.14.4/bin/mongo* /usr/local/bin
```
# 11-To help you get started

BI Connector requires a configuration file with the mongosqld.systemLog.path setting specified when running as a system service. Using your preferred text editor, create a mongosqld.conf file. 

see Configuration File. For example:
```
systemLog:
  path: '/logs/mongosqld.log'
net:
  bindIp: '127.0.0.1'
  port: 3307

```
# 12-To install and run mongosqld as a system service, run the following commands:
```
sudo mongosqld install --config <pathToConfigFile>/mongosqld.conf
```
```
sudo systemctl start mongosql.service
```
# 13-To enable the service so it starts automatically at boot time, run the following:
```
systemctl enable mongosql.service
```
  
# 14-Connect BI Tools

After you install and configure the BI Connector, you can use ODBC and JDBC drivers to connect from many BI Tools and clients. The sections below provide basic instructions for connecting to BI Connector using each tool.

>Tableau Desktop
>Microsoft Power BI Desktop
>Microsoft Excel
>MySQL Client

# 15-install cubejs in ubuntu 
**NOTE:** if you pull from github and you already build it,**then skip it.**
```
npm install -g cubejs-cli
```
```
npx cubejs-cli create CubeBI -d mongobi
```
# 16-edit .env file into the cubejs project
```
CUBEJS_DB_TYPE=mongobi
CUBEJS_DB_HOST=127.0.0.1
CUBEJS_DB_PORT=3307 
CUBEJS_DB_NAME=ticket2
CUBEJS_DB_USER=
CUBEJS_DB_PASS=
```
# 17-Install Docker Engine on Ubuntu

Install using the repository

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

**Set up the repository**
```
 sudo apt-get update
 ```
 ```
 sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release```
```
**Add Docker’s official GPG key:**
```
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
 ```
**Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below.**
 ```
 echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```
**Install Docker Engine**
```
 sudo apt-get update
 ```
 ```
 sudo apt-get install docker-ce docker-ce-cli containerd.io  
```
**Verify that Docker Engine is installed correctly by running the hello-world image.**
```
 sudo docker run hello-world
```
# 18-install docker-compose for deploy the Cubejs

On Linux, you can download the Docker Compose binary from the Compose repository release page on GitHub. Follow the instructions from the link, which involve running the curl command in your terminal to download the binaries. These step-by-step instructions are also included below.

>Run this command to download the current stable release of Docker Compose:

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
>Apply executable permissions to the binary:

```
sudo chmod +x /usr/local/bin/docker-compose
```

>Test the installation.

```
docker-compose --version
```
# 19-install mysql
**Step 1: Add MySQL APT repository in Ubuntu20.04|22.04**
```
wget https://dev.mysql.com/get/mysql-apt-config_0.8.20-1_all.deb
```
Once downloaded, install the repository by running the command below:
```
sudo dpkg -i mysql-apt-config_0.8.20-1_all.deb
```
On Ubuntu 22.04, choose **MySQL ubuntu focal** if there warned detected OS is not supported.

![image](https://user-images.githubusercontent.com/71556060/160337009-bd3b28df-e96c-41b9-8683-3789ecdf1cce.png)

he next prompt shows MySQL 8.0 chosen by **default**. Choose the first option and **click OK**

![image](https://user-images.githubusercontent.com/71556060/160337039-f44a0926-0626-4b0e-b794-f688a8e4d7f1.png)

In the next prompt, select **MySQL 8.0 ** server and **click OK**.

![image](https://user-images.githubusercontent.com/71556060/160337096-9103a04a-4ae0-46ee-bd41-7ab1d1f3b963.png)

The next prompt selects MySQL8 by default. Choose the last option **Ok** and **click OK**.

**Step 2: Update MySQL Repository on Ubuntu20.04|22.04**
```
sudo apt update
```
Now search for **MySQL 8.0 using apt cache** as shown below:
```
sudo apt-cache policy mysql-server
```
**Step 3: Install MySQL 8.0 on Ubuntu20.04|22.04**

```
sudo apt install mysql-client mysql-community-server mysql-server
```
>Hit the y key to start the installation:

Set a strong password for root MySQL user

![image](https://user-images.githubusercontent.com/71556060/160337846-98c5a040-b331-4327-b9ba-df0336728db7.png)

Confirm root password by typing it again.

![image](https://user-images.githubusercontent.com/71556060/160337936-9dd32b7d-0051-48ff-bc41-93ee38e2c792.png)

Set default authentication plugin. Use Strong Password Encryption mechanism.

![image](https://user-images.githubusercontent.com/71556060/160338209-4ecfb2f3-03a9-499c-9433-065be5257a36.png)

**Step 4: Secure MySQL Installationon Ubuntu20.04|22.04**

Run the command
```
sudo mysql_secure_installation
```
**Press Enter**. When prompted for **password**, provide the **root password set** above
```
Enter current password for root (enter for none): <Enter password>
VALIDATE PASSWORD PLUGIN can be used to test passwords 
and improve security. It checks the strength of password 
and allows the users to set only those passwords which are 
secure enough. Would you like to setup VALIDATE PASSWORD plugin? 

Press y|Y for Yes, any other key for No: **Y** 

There are three levels of password validation policy: 

LOW    Length >= 8 
MEDIUM Length >= 8, numeric, mixed case, and special characters 
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file 

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: **1**
Using existing password for root. 

Estimated strength of the password: 25  
Change the password for root ? ((Press y|Y for Yes, any other key for No) : n


Remove anonymous users? [Y/n] **Y** 
Disallow root login remotely? [Y/n] **Y **
Remove test database and access to it? [Y/n]** Y** 
Reload privilege tables now? [Y/n] **Y **

```
**Step 5) Validate MySQL 8.0 Installation on Ubuntu 20.04|22.04**

Connect to MySQL to check MySQL installed version. To connect to **MySQL**, run the below command:
```
mysql
```
>Provide the root password set above and once connected.

**To restart mysql**
```
sudo systemctl restart mysql
```



# 20-

```
mysql --protocol=tcp --port=3307
```
# 21-To Deploy on Docker run this command:

```
docker-compose up
```
# 22-change the docker-compose.file 
in my case ,we are deplying mongo without docker container, run it simplay on server.
So the docker compose yaml did not access the mongo ,because it run on **server/localhost:27017**
>so,in this case you need to change the docker-compose file.
need to add "**network**" = "**host**"
```
version: '2.2'

services:
  cube:
    image: cubejs/cube:v0.29.28
    ports:
      # It's better to use random port binding for 4000/3000 ports
      # without it you will not able to start multiple projects inside docker
      - 3339:4000  # Cube.js API and Developer Playground
      - 3001:3000  # Dashboard app, if created
    env_file: .env
    volumes:
      - .:/cube/conf
      # We ignore Cube.js deps, because they are built-in inside the official Docker image
      - .empty:/cube/conf/node_modules/@cubejs-backend/
    network_mode: host
```
![MicrosoftTeams-image](https://user-images.githubusercontent.com/71556060/159915412-3fd724a0-0f3c-4870-95c4-0a4a3ef5c9ac.png)

**thank you ! you are ready to go!**

_____________________________________________________________________________________________________________________

 **issues-in-deplyments**

# 1-ERROR:while loading db schema error: unable to connect to foreign data source: mongodb at promiseconnection.
**this case is occure then your mongodb is not in runing ,you can check the status by this command**:
```
sudo service mongod status
```
**As a solution assing the permission by runing the commands**

```
sudo chown -R mongodb:mongodb /var/lib/mongodb
```
```
sudo chown mongodb:mongodb /tmp/mongodb-27017.sock    
```
```
sudo service mongod restart
```
```
sudo systemctl enable mongod.service
```
# 2-ERROR: this port is already in used.

```
sudo netstat -pna | grep 3307
```
# 3-ERROR: Performing query: scheduler-c4a683d1-9ab1-4fa3-9e7c-bd9067c597d3 
**Error while querying: scheduler-c4a683d1-9ab1-4fa3-9e7c-bd9067c597d3 (5002ms)
Error querying db: scheduler-5fbbcfc4-68f4-4f7a-bb61-5a9ac1876989 
Refresh Scheduler Error: scheduler-5fbbcfc4-68f4-4f7a-bb61-5a9ac1876989**



# 4-ERROR: connect ECONNREFUSED 127.0.0.1:3307
cube_1  |     at QueryQueue.parseResult (/cube/node_modules/@cubejs-backend/query-orchestrator/src/orchestrator/QueryQueue.js:138:13)

**To attach mongodb to mongosql**
1) find "mongodrdl" in my local system it is in "/usr/local/bin"
2) run this command:
```
mongodrdl --uri=mongodb://127.0.0.1:27017/testone
```
>testone is db name
3) restart mongosql 
```
sudo service mongosql restart
```
________________________________________________________________________________________________________________________________________

# some usefull links:

1- **https://www.cloudsavvyit.com/14114/how-to-connect-to-localhost-within-a-docker-container/**
2- **https://www.mongodb.com/docs/bi-connector/current/launch/**
3- https://computingforgeeks.com/how-to-install-mysql-8-on-ubuntu/
4- **https://stackoverflow.com/questions/48092353/failed-to-start-mongod-service-unit-mongod-service-not-found**
5- https://stackoverflow.com/questions/54025995/tableau-and-mongodb-warning-access-control-is-not-enabled-for-mongosqld
6- **https://stackoverflow.com/questions/41615574/mongodb-server-has-startup-warnings-access-control-is-not-enabled-for-the-dat**
7- https://real-time-dashboard.cube.dev/cube-js-api-with-mongo-db
8- **https://docs.mongodb.com/bi-connector/current/launch/#std-label-start-msqld-cli**
9- **https://devhints.io/docker-compose**
