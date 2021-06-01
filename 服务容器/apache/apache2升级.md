cp -rf /etc/apache2/sites-available/ /tmp/apache2-available
cp -rf /etc/apache2/sites-enabled/ /tmp/apache2-enabled
ls -al /etc/apache2/sites-enabled/

apache2 -version
add-apt-repository ppa:ondrej/apache2
apt update && apt list --upgradable
apt-get install --only-upgrade apache2
apache2 -version
ls -al /etc/apache2/sites-enabled/