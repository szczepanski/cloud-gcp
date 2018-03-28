Piotr Szczepanski

# Ravelin - https load balancing configuration

## Set Up Instance Template 

Compute Engine/Instance Template
- g1-small (1 vCPU, 1.7 GB memory)
- Add Start Up script(replace index and feedback hostname - landing server check):

```shell 
#! /bin/bash
apt-get update -y
apt-get install apache2 -y
apt-get install php7.0 -y
mv /var/www/html/index.html /var/www/html/index.php
cat <<EOF > /var/www/html/index.php
<html>
<body> HO!!!<br></br>
<?php
echo gethostname(),
?>
</body>
</html>
EOF
```

## Set up 2 Instance Groups (Fault Toleranace, High Availilbility)

1st:
set it multi-zone - europe-west2 London
select the instance template
autoscaling on - based on:
- CPU Usage - 40% => scale up
- auto-scaling group = 1 and max = 2
- add new HTTPS based health check 
- initial delay 150 sec

2nd:
  - set it multi-zone - europe-west1 - Belgium
select the instance template
autoscaling on - based on:
- CPU Usage - 40% => scale up
- auto-scaling group = 1 and max = 2
- add new HTTPS based health check 
- initial delay 150 sec

## Configure External Static IP address

VPC Network/External IP addresses/Reserve static IP addresses
- enable IPv4 global type
- reserve it

## Setup Load Balancing
Network Services/Load Balancing

 
