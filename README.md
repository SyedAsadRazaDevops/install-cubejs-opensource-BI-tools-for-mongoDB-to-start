
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
```
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
  
thank you ! you are ready to go!
  
