## 04-cart service

* cart is a microservice that is responsible for cart Service in hipsterShop e-commerce portal.

* Developer has chosen Dotnet, Check with developer which version of Dotnet is needed.

### update packages
```
yum update -y
```
### Install git.
```
yum install git -y
```

### Setup the Dotnet repo file
```
vim /etc/yum.repos.d/dotnet.repo
```
```
[fedora37prod]
name=fedora/37/prod
baseurl=https://packages.microsoft.com/fedora/37/prod/
repo_gpgcheck=0
gpgcheck=0
enabled=1
gpgkey=https://packages.microsoft.com/fedora/37/prod/repodata/repomd.xml.key
```
### Install Dotnet.
```
sudo dnf install -y dotnet-sdk-8.0
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
mkdir /cart
```
### Copying contents to cart directory and change directory.
```
cp -r google-10-microservices-project/cartservice/* /cart/
cd /cart/src
```

### Lets download the dependencies.
```
dotnet restore cartservice.csproj -r linux-musl-x64
dotnet publish cartservice.csproj \
    -p:PublishSingleFile=true \
    -r linux-musl-x64 \
    --self-contained true \
    -p:PublishTrimmed=True \
    -p:TrimMode=Full \
    -c release \
    -o /tmp/cartservice-publish \
    --no-restore
dotnet publish -c Release -o out
```
We need to setup a new service in systemd so systemctl can manage this service

Setup SystemD cart Service
```
vi /etc/systemd/system/cart.service
```
```
[Unit]
Description=cart

[Service]
User=hipstershop
WorkingDirectory=/cart/src
Environment=REDIS_ADDR=<REDIS_ADDR>:6379
Environment=PORT=7070
ExecStart=dotnet /cart/src/bin/Release/net8.0/cartservice.dll --urls http://0.0.0.0:7070
SyslogIdentifier=cartservice

[Install]
WantedBy=multi-user.target
```
Ensure you replace the corresponding server ip address
### Load the service.
```
systemctl daemon-reload
```
```
systemctl start cart
```
```
systemctl enable cart
```
```
systemctl status cart
```

