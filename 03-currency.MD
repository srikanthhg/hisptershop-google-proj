## 03-currency service

* currency is a microservice that we ca select different currencies in hipstershop application.

* Developer has chosen NodeJs, Check with developer which version of NodeJS is needed. Developer has set a context that it can work with NodeJS =>20

*Install NodeJS, We would like to enable 20 version and install list.

### Install node version manager (nvm) by typing the following at the command line.
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
```
We will use nvm to install Node.js because nvm can install multiple versions of Node.js and allow you to switch between them.

Activate nvm by typing the following at the command line.
```
. ~/.nvm/nvm.sh
```
Use nvm to install the latest LTS version of Node.js by typing the following at the command line.
```
nvm install --lts
```
Installing Node.js also installs the Node Package Manager (npm), so you can install additional modules as needed.

Test that Node.js is installed and running correctly by typing the following at the command line.
```
node -e "console.log('Running Node.js ' + process.version)"
```
This displays the following message that shows the version of Node.js that is running.

Running Node.js VERSION 

### Install git.
```
yum install git -y
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
mkdir /currency
```
### Copying contents to currency directory and change directory.
```
cp -r google-10-microservices-project/currencyservice/* /currency/
cd /currency
```
### Lets download the dependencies.
```
npm install 
```
We need to setup a new service in systemd so systemctl can manage this service

Setup SystemD currency Service
```
vi /etc/systemd/system/currency.service
```
```
[Unit]
Description=currency

[Service]
User=hipstershop
WorkingDirectory=/currency
Environment=PORT=7000
Environment=DISABLE_PROFILER=1

ExecStart=node /currency/server.js
SyslogIdentifier=currencyservice

[Install]
WantedBy=multi-user.target
```
### Load the service.
```
systemctl daemon-reload
```
```
systemctl start currency
```
```
systemctl enable currency
```
```
systemctl status currency
```
### If security vulnerabilities are found and updates are available, you can either:

Run the `npm audit fix` subcommand to automatically install compatible updates to vulnerable dependencies.
    
Run the recommended commands individually to install updates to vulnerable dependencies.
    `npm fund`


