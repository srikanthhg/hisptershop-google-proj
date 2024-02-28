## 01-Frontend

* The Web/Frontend is the service in hipsterShop to serve the web content over go lang.

* This will have the web page for the web application.

* Developer has chosen go lang.  we are using latest go lang

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
yum install golang -y
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
mkdir /frontend
```
### Copying contents to frontend directory and change directory.
```
cp -r google-10-microservices-project/frontend/* /frontend/
cd /frontend
```
### Build the application.
```
go build -o myfrontend
```
### Create a systemd file.
```
vi /etc/systemd/system/frontend.service
```
```
[Unit]
Description=frontend

[Service]
User=hipstershop
WorkingDirectory=/frontend
Environment=PRODUCT_CATALOG_SERVICE_ADDR=<PRODUCT_CATALOG_SERVICE_ADDR>:3550
Environment=CURRENCY_SERVICE_ADDR=<CURRENCY_SERVICE_ADDR>:7000
Environment=CART_SERVICE_ADDR=<CART_SERVICE_ADDR>:7070
Environment=RECOMMENDATION_SERVICE_ADDR=<RECOMMENDATION_SERVICE_ADDR>:8080
Environment=CHECKOUT_SERVICE_ADDR=<CHECKOUT_SERVICE_ADDR>:5050
Environment=SHIPPING_SERVICE_ADDR=<SHIPPING_SERVICE_ADDR>:50051
Environment=AD_SERVICE_ADDR=<AD_SERVICE_ADDR>:9555
Environment=ENV_PLATFORM=onprem
Environment=PORT=8080

ExecStart=/frontend/myfrontend
SyslogIdentifier=frontend

[Install]
WantedBy=multi-user.target
```
Ensure you replace the corresponding servers ip address

### Load the service.
```
systemctl daemon-reload
```
```
systemctl start frontend
```
```
systemctl enable frontend
```
```
systemctl status frontend
```