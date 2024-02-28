### install redis
```
sudo yum install redis6 -y
```
Edit the redis config file and replace 127.0.0.1 to 0.0.0.0
```
sudo vi /etc/redis6/redis6.conf  
```
### start and enable redis service

```
systemctl restart redis6
systemctl enable redis6
```