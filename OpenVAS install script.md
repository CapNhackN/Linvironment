Use Cases:
Installs Greenbone Network's OpenVAS vulnerability scanner.

```bash
#!/bin/bash

# This script will install and configure the OpenVAS vulnerability scanner from GreenBone networks on Kali Linux.

echo "Installing OpenVAS..."

sudo apt install openvas

echo "Setting up certs..."

sudo runuser -u _gvm -- gvm-manage-certs -a -f

echo "Updating feeds..."

sudo greenbone-feed-sync --type NVT

sudo greenbone-feed-sync --type SCAP

sudo greenbone-feed-sync --type CERT

sudo greenbone-feed-sync --type GVMD_DATA

echo "Modifying postgres clusters..."

# When OpenVAS installs, it auto creates postgres cluster 16 which causes errors with the designated ports. To correct this, we need to drop it and upgrade cluster 15 to version 16.

sudo pg_dropcluster --stop 16 main

sudo pg_upgradecluster 15 main

sudo runuser -u postgres -- /usr/share/gvm/create-postgresql-database

echo "Creating user account..."

sudo runuser -u _gvm -- gvmd --create-user=admin --password=admin

echo "Checking setup..."

sudo gvm-check-setup

sudo gvm-setup

echo "Starting up OpenVAS..."

sudo gvm-start

  

# To create new user:

# $ sudo runuser -u _gvm -- gvmd --create-user=admin2 --new-password=12345

  

# To change existing user password:

# sudo runuser -u _gvm -- gvmd --user=admin --new-password=new_password=admin

  

# To start/stop service:

# sudo gvm-start gvm-stop

  

# To fix cert error:

# sudo runuser -u _gvm -- gvm-manage-certs -a -f
```
