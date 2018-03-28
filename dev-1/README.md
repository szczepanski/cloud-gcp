Piotr Szczepanski

# Ravelin - http load balancing configuration

More Complex 3 Tier AWS infustructure: 

https://github.com/szczepanski/cloud-aws

Simple GCP Load Balancing below: 

## Set Up Instance Template 

Compute Engine/Instance Template
- g1-small (1 vCPU, 1.7 GB memory)
- add startup script(replace index and feedback hostname - landing server check):

```shell 
#! /bin/bash
apt-get update -y
apt-get install apache2 -y
apt-get install php7.0 -y
mv /var/www/html/index.html /var/www/html/index.php
cat <<EOF > /var/www/html/index.php
 <html>
 <body><br>{“foo”: “barr”}</br>
<br>
<br>
<br>Server name / zone:</br>
<br>
 <?php
 echo gethostname();
 ?>
</body>
</html>
EOF

```

## Set up 2 Instance Groups (Fault Tolerance, High Availability)

1st:
set it multi-zone - europe-west-2 London
select the instance template
autoscaling on - based on:
- cpu usage - 40% => scale up
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
- name it
- backend configuration/create https backend service - eu-west-2
  - select instance group - eu-west-2
  - set balancing mode to rate - requests per second (rps)
  - maximum rate: 1, capacity 100 %
 
- add 2nd backend configuration/create https backend service - eu-west-1
  - select instance group - eu-west-1
  - set balancing mode to rate - requests per second (rps)
  - maximum rate: 1, capacity 100 %
 
- create new https health check 
- traffic affinity (how the traffic is to be routed) 
  - leave at none (session stickiness/ persistence) - new traffic to be directed to the same instance

- host and path rules (leave at default) => https backend service
- frontend configuration
  - name it
  - protocol https
  - ip address - select gcp-dev-1 IP
  - create new certificate
    ```shell
    sudo su
    service apache2 reload
    mkdir /etc/apache2/ssl
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
    chmod 600 /etc/apache2/ssl/*
    vi /etc/apache2/sites-enabled/default-ssl.conf
    
    ServerName example.com:443
    SSLCertificateFile /etc/apache2/ssl/apache.crt
    SSLCertificateKeyFile/etc/apache2/ssl/apache.key
    
    service apache2 reload
    
    
    # testing
    openssl s_client -connect localhost:443

    ```
## Testing Load Balancing: 
    - access Load Balancer from instance running from Belgium zone and Uk Zone
    
## Testing Auto Scaling - CPU  
install following py script to boost CPU utilization above 40% and test autoscaling

```shell
    #!/usr/bin/env python
"""
Produces load on all available CPU cores
"""

from multiprocessing import Pool
from multiprocessing import cpu_count

def f(x):
    while True:
        x*x

if __name__ == '__main__':
    processes = cpu_count()
    print 'utilizing %d cores\n' % processes
    pool = Pool(processes)
    pool.map(f, range(processes))
    
```    
 and
 ```shell
 apt-get install cpulimit
 python python-cpu.py &
 ```
