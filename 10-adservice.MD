## 10-adservice

* Provides text ads based on given context words.

* Developer has chosen java lang. Check with developer which version of Java is needed. Developer has set a context that it can work with Java 19.

### Update Packages.
```
sudo yum update -y
```
### Install git.
```
yum install git -y
```

### Install Java.
```
wget https://download.oracle.com/java/19/archive/jdk-19.0.2_linux-x64_bin.rpm
yum install jdk-19.0.2_linux-x64_bin.rpm -y
```
### check the java version.
```
java --version
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
mkdir /ad
```
### Copying contents to frontend directory and change directory.
```
cp -r google-10-microservices-project/adservice/* /ad/
cd /ad
```
### Build the application.
```
chmod +x gradlew
./gradlew downloadRepos

./gradlew installDist
```
###  Download Stackdriver Profiler Java agent
```
mkdir -p /opt/cprof && \
wget -q -O- https://storage.googleapis.com/cloud-profiler/java/latest/profiler_java_agent.tar.gz \
    | tar xzv -C /opt/cprof && \
    rm -rf profiler_java_agent.tar.gz
```
### Create a systemd file.
```
vi /etc/systemd/system/ad.service
```
```
[Unit]
Description=ad

[Service]
User=hipstershop
WorkingDirectory=/ad

Environment=DISABLE_PROFILER=1
Environment=PORT=9555

ExecStart=/ad/build/install/hipstershop/bin/AdService
SyslogIdentifier=adservice

[Install]
WantedBy=multi-user.target
```


### Load the service.
```
systemctl daemon-reload
```
```
systemctl start ad
```
```
systemctl enable ad
```
```
systemctl status ad
```