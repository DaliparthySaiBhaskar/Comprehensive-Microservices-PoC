# MongoDB Configuration
## 1. Install MongoDB Community Server
```sh
sudo dnf install mongodb-org -y 
```
As MongoDB isn’t part of the official RedHat software stack, configuring the MongoDB repository ensures that you’re pulling the latest, trusted version of MongoDB directly from MongoDB’s official source, which is not included by default in Red Hat.

## 2. Configure the Repository
Create a `vim /etc/yum.repos.d/mongo.repo` file so that you can install MongoDB directly using yum/dnf. Refer Official documentation for [[Community Edition]](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-red-hat/), [[Enterprise Edition]](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-enterprise-on-red-hat/).

```sh
sudo vim /etc/yum.repos.d/mongo.repo
```
Add the following repository configuration,
```sh
[mongodb-org-7.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/9/mongodb-org/7.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://pgp.mongodb.com/server-7.0.asc
```
```sh
sudo dnf install mongodb-org -y 
```

## 3. Enable & Start MongoDB Service
```sh
sudo systemctl enable mongod
```
```sh
sudo systemctl start mongod
```

## 4. Configure MongoDB to Allow External Connections
```sh
sudo vim /etc/mongod.conf
```
```sh
# network interfaces
net:
  port: 27017
  bindIp: 0.0.0.0  # Allows external connections
```

## 5. Restart MongoDB
```sh
systemctl restart mongod
```
```sh
systemctl status mongod
```

## 6. Troubleshooting Steps
```sh
netstat -nltp
```
```sh
ping <MONGODB-SERVER-IP>
```
Install MongoDB Shell
```sh
sudo dnf install -y mongodb-mongosh
```
```sh
mongosh --host <MONGODB-SERVER-IP> --port <PORT>
```