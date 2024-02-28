## 02-productcatalogservice

* productcatalogatalogue is a microservice that is responsible for serving the list of products that displays in  hipstershop application.

* Developer has chosen go lang, Check with developer which version of go lang is needed.  we are using latest go lang.

### Update Packages.
```
sudo yum update -y
```
### Install git.
```
yum install git -y
```

### Install go lang.
```
yum install go lang -y
```
### Cloning repository.
```
git clone https://github.com/srikanthhg/google-10-microservices-project.git
```
### Add application User
```
useradd hipstershop
```
### Create directory.
```
mkdir /productcatalog
```
### Copying contents to productcatalog directory and change directory.
```
cp -r google-10-microservices-project/productcatalogservice/* /productcatalog/
cd /productcatalog
```
### Build the application.
```
go build -o mycatalog
```
### Create a systemd file.
```
vi /etc/systemd/system/productcatalog.service
```
```
[Unit]
Description=productcatalog

[Service]
User=hipstershop
WorkingDirectory=/productcatalog
Environment=PORT=3550

ExecStart=/productcatalog/mycatalog
SyslogIdentifier=productcatalogservice

[Install]
WantedBy=multi-user.target
```

### Load the service.
```
systemctl daemon-reload
```
```
systemctl start productcatalog
```
```
systemctl enable productcatalog
```
```
systemctl status productcatalog
```