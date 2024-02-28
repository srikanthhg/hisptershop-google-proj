## 07-emailservice

* Sends users an order confirmation email (mock).

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
mkdir /email
```
### Copying contents to frontend directory and change directory.
```
cp -r google-10-microservices-project/emailservice/* /email/
cd /email
```
### Install dependencies
```
pip3.12 install -r requirements.txt
```
### Create a systemd file.
```
vi /etc/systemd/system/email.service
```
```
[Unit]
Description=email

[Service]
User=hipstershop
WorkingDirectory=/email
Environment=DISABLE_PROFILER=1
Environment=PYTHONUNBUFFERED=1
Environment=PORT=8080

ExecStart=python3.12 /email/email_server.py
SyslogIdentifier=emailservice

[Install]
WantedBy=multi-user.target
```

### Load the service.
```
systemctl daemon-reload
```
```
systemctl start email
```
```
systemctl enable email
```
```
systemctl status email
```