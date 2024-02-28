## 08-checkoutservice

* Retrieves user cart, prepares order and orchestrates the payment, shipping and the email notification.

* Developer has chosen go lang. we are using latest go lang

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
mkdir /checkout
```
### Copying contents to frontend directory and change directory.
```
cp -r google-10-microservices-project/checkoutservice/* /checkout/
cd /checkout
```
### Build the application.
```
go build -o mycheckout
```
### Create a systemd file.
```
vi /etc/systemd/system/checkout.service
```
```
[Unit]
Description=checkout

[Service]
User=hipstershop
WorkingDirectory=/checkout
Environment=PRODUCT_CATALOG_SERVICE_ADDR=<PRODUCT_CATALOG_SERVICE_ADDR>:3550
Environment=SHIPPING_SERVICE_ADDR=<SHIPPING_SERVICE_ADDR>:50051
Environment=PAYMENT_SERVICE_ADDR=<PAYMENT_SERVICE_ADDR>:50051
Environment=EMAIL_SERVICE_ADDR=<EMAIL_SERVICE_ADDR>:8080
Environment=CURRENCY_SERVICE_ADDR=<CURRENCY_SERVICE_ADDR>:7000
Environment=CART_SERVICE_ADDR=<CART_SERVICE_ADDR>:7070

Environment=PORT=5050
Environment=DISABLE_PROFILER=1

ExecStart=/checkout/mycheckout
SyslogIdentifier=checkoutservice

[Install]
WantedBy=multi-user.target
```
Ensure you replace the corresponding servers ip address

### Load the service.
```
systemctl daemon-reload
```
```
systemctl start checkout
```
```
systemctl enable checkout
```
```
systemctl status checkout
```