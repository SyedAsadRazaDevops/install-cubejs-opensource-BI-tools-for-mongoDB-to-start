
install-cubejs-opensource-BI-tools-for-mongoDB-to-start

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
# 20-To Deploy on Docker run this command:

```
docker-compose up
```



thank you ! you are ready to go!
  
