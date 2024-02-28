## 09-recommendationservice

* Recommends other products based on what's given in the cart.

* Developer has chosen python lang, Check with developer which version of python is needed. Developer has set a context that it can work with python 3.11

### Update Packages.
```
sudo yum update -y
```
### Install git.
```
yum install git -y
```

### Install python.
```
wget https://www.python.org/ftp/python/3.12.2/Python-3.12.2.tgz

tar -xvf Python-3.12.2.tgz
cd Python-3.12.2
sudo yum -y groupinstall "Development Tools"
sudo yum -y install gcc openssl-devel bzip2-devel libffi-devel
sudo yum install gcc-c++ -y
./configure
sudo make
sudo make altinstall
python3.12 --version
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
mkdir /recommendation
```
### Copying contents to frontend directory and change directory.
```
cp -r google-10-microservices-project/recommendationservice/* /recommendation/
cd /recommendation
```
### Install dependencies
```
pip3.12 install -r requirements.txt
```
### Create a systemd file.
```
vi /etc/systemd/system/recommendation.service
```
```
[Unit]
Description=recommendation

[Service]
User=hipstershop
WorkingDirectory=/recommendation
Environment=DISABLE_PROFILER=1
Environment=PYTHONUNBUFFERED=1
Environment=PRODUCT_CATALOG_SERVICE_ADDR=<PRODUCT_CATALOG_SERVICE_ADDR>:3550
Environment=PORT=8080

ExecStart=python3.12 /recommendation/recommendation_server.py
SyslogIdentifier=recommendationservice

[Install]
WantedBy=multi-user.target
```
Ensure you replace the corresponding server ip address

### Load the service.
```
systemctl daemon-reload
```
```
systemctl start recommendation
```
```
systemctl enable recommendation
```
```
systemctl status recommendation
```