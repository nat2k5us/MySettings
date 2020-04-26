### AWS User Data Script

```#!/bin/bash
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd.service
sudo systemctl enable httpd.service
EC2_AVAIL_ZONE=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)
sudo echo "<h1>Hello World From Natraj at at $(hostname -f) in AZ '$EC2_AVAIL_ZONE' </h1>" > /var/www/html/index.html
  ```
