## 06-shipping service

* Gives shipping cost estimates based on the shopping cart. Ships items to the given address (mock)

* Developer has chosen go lang

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
mkdir /shipping
```
### Copying contents to frontend directory and change directory.
```
cp -r google-10-microservices-project/shippingservice/* /shipping/
cd /shipping
```
### Build the application.
```
go build -o myshipping
```
### Create a systemd file.
```
vi /etc/systemd/system/shipping.service
```
```
[Unit]
Description=shipping

[Service]
User=hipstershop
WorkingDirectory=/shipping
Environment=DISABLE_PROFILER=1
Environment=PORT=50051

ExecStart=/shipping/myshipping
SyslogIdentifier=shippingservice

[Install]
WantedBy=multi-user.target
```
Ensure you replace the corresponding servers ip address

### Load the service.
```
systemctl daemon-reload
```
```
systemctl start shipping
```
```
systemctl enable shipping
```
```
systemctl status shipping
```