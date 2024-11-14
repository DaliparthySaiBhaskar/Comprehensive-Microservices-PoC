# Dispatch Configuration
## 1. Install GoLang
```sh
sudo dnf install golang -y
```

## 2. Create Application User
```sh
sudo useradd -m -s /sbin/nologin robotshop
```

## 3. Setup Application Directory
```sh
sudo mkdir /app
```

## 4. Download Application Code
```sh
curl -L -o /tmp/dispatch.zip https://robotshop-builds.s3.us-east-1.amazonaws.com/dispatch.zip
``` 
```sh
cd /app
```
```sh
sudo unzip /tmp/dispatch.zip
```

## 5. Install Dependencies and Build the Application
```sh
cd /app
```
```sh
go mod init dispatch
```

Download required dependencies:
```sh
go get
```

Build the application:
```sh
go build
```
This will create an executable named `dispatch` in the `/app` directory.

## 6. Configure Systemd Service for Dispatch
```sh
sudo vim /etc/systemd/system/dispatch.service
```

Add the following configuration:
```sh
[Unit]
Description=Dispatch Service

[Service]
User=robotshop
Environment=AMQP_HOST=<RABBITMQ-IP>
Environment=AMQP_USER=robotshop
Environment=AMQP_PASS=robotshop123
ExecStart=/app/dispatch
SyslogIdentifier=dispatch

[Install]
WantedBy=multi-user.target
```

**Note:** Replace `RABBITMQ-IP`

## 7. Enable and Start Dispatch Service
```sh
sudo systemctl daemon-reload
```
```sh
sudo systemctl enable dispatch
```
```sh
sudo systemctl start dispatch
```

