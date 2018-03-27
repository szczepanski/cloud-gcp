Piotr Szczepanski

# Ravelin - https load balancing configuration

## Set Up Instance Template 
Compute Engine/Instance Template
- g1-small (1 vCPU, 1.7 GB memory)
- Add Start Up script:

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

## Set Instance Group 
in 2 regions (FTHA):
  - europe-west2 London
  - europe-west1 - Belgium

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
