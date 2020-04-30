### AWS User Data Script

```#!/bin/bash
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd.service
sudo systemctl enable httpd.service
EC2_AVAIL_ZONE=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)
sudo echo "<h1>Hello World From Natraj at at $(hostname -f) in AZ '$EC2_AVAIL_ZONE' </h1>" > /var/www/html/index.html
  ```
  
  ```#!/bin/bash
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd.service
sudo systemctl enable httpd.service
sudo echo "<h1> At $(hostname -f) </h1>" > /var/www/html/index.html
  ```
```
#!/bin/bash
sudo su
yum update -y
yum install -y httpd
systemctl start httpd.service
systemctl enable httpd.service
echo "<h1> At $(hostname -f) </h1>" > /var/www/html/index.html
echo "*/1 * * * * ec2-user date --from-cron" >> /var/spool/cron/ec2-user
```

```
#!/bin/bash
yum update -y
yum install httpd php php-mysql -y
cd /var/www/html
echo "healthy" > healthy.html
wget https://wordpress.org/wordpress-5.1.1.tar.gz
tar -xzf wordpress-5.1.1.tar.gz
cp -r wordpress/* /var/www/html/
rm -rf wordpress
rm -rf wordpress-5.1.1.tar.gz
chmod -R 755 wp-content
chown -R apache:apache wp-content
wget https://s3.amazonaws.com/bucketforwordpresslab-donotdelete/htaccess.txt
mv htaccess.txt .htaccess
chkconfig httpd on
service httpd start
```
```
#!/bin/bash
yum update -y
aws s3 sync --delete s3://uourbucker-code1234 /var/www/html
```

```
yum install -y httpd mariadb-server
systemctl start httpd
systemctl enable httpd
usermod -a -G apache ec2-user
chown -R ec2-user:apache /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} \;
find /var/www -type f -exec chmod 0664 {} \;
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```
### Print CPU Usage
```ps -Ao user,uid,comm,pid,pcpu,tty -r | head -n 6```

### crontab
```
sudo su
crontab -u ec2-user -l
echo -e "*/1 * * * * ~/aws-scripts-mon/mon-put-instance-data.pl -mem-util --mem-used --mem-avail --swap-util --disk-space-util --disk-space-used --disk-space-avail --memory-units=megabytes --disk-path=/dev/xvda1 --from-cron " | crontab -u ec2-user -
exit
```
### User Data Script to setup cloud watch
```
#!/bin/sh
yum install -y perl-Switch perl-DateTime perl-Sys-Syslog perl-LWP-Protocol-https perl-Digest-SHA unzip
cd /home/ec2-user
curl http://aws-cloudwatch.s3.amazonaws.com/downloads/CloudWatchMonitoringScripts-1.2.1.zip -O
unzip CloudWatchMonitoringScripts-1.2.1.zip
rm -rf CloudWatchMonitoringScripts-1.2.1.zip
chown ec2-user:ec2-user aws-scripts-mon
echo "* * * * * ec2-user /home/ec2-user/aws-scripts-mon/mon-put-instance-data.pl --mem-util --swap-util --aggregated --auto-scaling --from-cron" >> /var/spool/cron/ec2-user
echo "0 * * * * ec2-user /home/ec2-user/aws-scripts-mon/mon-put-instance-data.pl --disk-space-used --disk-space-avail --disk-space-util --disk-path=/  --aggregated --auto-scaling --from-cron" >> /var/spool/cron/ec2-user
```
