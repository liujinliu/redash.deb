# REDASH.DEB
[redash](https://redash.io/) is a fantastic software.  
This repo aimed to make a deb package of redash

## USAGE

#### package build
```
cd build && make
```

#### package install
```
sudo dpkg -i redash_1.0.1_amd64.deb 
## should deal with the dependencies by yourself
```

#### server install
```
## should be done following this order
cd /opt/redash
sudo make create_user
sudo make venv
sudo make package_install_pre
sudo make package_install
make create_database
sudo cp /opt/redash/conf/supervisor_conf/redash.conf /etc/supervisor/conf.d/
sudo supervisorctl update
sudo supervisorctl restart all 
```

The server will run at ```"http://127.0.0.1:5000"```
