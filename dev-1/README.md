## Simple Load balancing 


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
