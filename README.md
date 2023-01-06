# تثبيت اودو 14 في مخدم بنظام اوبنتو  18 و ديبيان
# Install odoo 14 on ubuntu 18.04 server (+Debian)

##  تحديث السيرفر     
## Server Update
```
sudo apt-get install software-properties-common
sudo add-apt-repository universe && apt-get update && sudo apt-get upgrade -y 
```
##  انشاء مستخدم أودو في اوبنتو
## Create new odoo user 
```                      
sudo adduser -system -home=/opt/odoo -group odoo 
```
##  تثبيت بوستجريسكل
## Install PostgreSql
```
sudo apt-get install postgresql -y 
```                
##  انشاء مستخدم أودو في البوستجريسكل
## Create odoo user in PostgreSql 
```
sudo su - postgres -c "createuser -s odoo" 2> /dev/null || true 
```                 
##  تثبيت البايثون وادواتها اللازمة لتشغيل اودو
## Install python & necessary tools for running odoo
```
sudo apt-get install git python3 python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less libjpeg-dev gdebi -y
 ```                   
##  تثبيت ادوات الادوات والمكتبات الضرورية لتشغيل اودو، عن طريق البيب
## Install tools & libraries for odoo using PIP
```
sudo apt install libpq-dev python3-dev
```
```
sudo -H pip3 install -r https://raw.githubusercontent.com/odoo/odoo/master/requirements.txt 
   ```                 
##  تثبيت ادوات اخرى ضرورية                  
## Install other tools
```
sudo apt-get install nodejs npm -y && sudo npm install -g rtlcss 
```
##  تثبيت حزم Wkhtmltopdf
## Install Wkhtmltopdf
```
sudo apt-get install xfonts-75dpi && sudo wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.bionic_amd64.deb &&sudo dpkg -i wkhtmltox_0.12.6-1.bionic_amd64.deb && sudo cp /usr/local/bin/wkhtmltoimage /usr/bin/wkhtmltoimage && sudo cp /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
  ``` 

```
sudo apt-get -f install
```
##  انشاء مجلد لحفظ سجلات الاستخدام
## Create logs directory
```
sudo mkdir /var/log/odoo && sudo chown odoo:odoo /var/log/odoo
  ```                  
##  تثبيت أودو، النسخة 14.0
## Install Odoo V14.0
```
sudo git clone --depth 1 --branch 14.0 https://www.github.com/odoo/odoo /odoo/odoo-server
```                 

##  تغيير صلاحيات مجلد اودو الرئيسي واعطاء ملكيته لمستخدم اودو الذي قمنا بانشاءه سلفا
## Change odoo permession and grant to odoo user that already created 
```
sudo chown -R odoo:odoo /odoo/*
```                  
##  انشاء ملف الاعدادات الرئيسي لأودو
## Create file configuration
```
sudo nano /etc/odoo-server.conf

```
##  ملأ الملف بالاعدادات اللازمة
## Fill in the file with the necessary settings
```
sudo su root -c "printf '[options] \n; This is the password that allows database operations:\n' >> /etc/odoo-server.conf" && sudo su root -c "printf 'admin_passwd = admin\n' >> /etc/odoo-server.conf" && sudo su root -c "printf 'xmlrpc_port = 8069\n' >> /etc/odoo-server.conf" && sudo su root -c "printf 'logfile = /var/log/odoo/odoo-server.log\n' >> /etc/odoo-server.conf" && sudo su root -c "printf 'addons_path=/odoo/odoo-server/addons\n' >> /etc/odoo-server.conf"
sudo chown odoo:odoo /etc/odoo-server.conf && sudo chmod 640 /etc/odoo-server.conf 
```                    

##  تشغيل اودو
## Run Odoo
```
sudo su - odoo -s /bin/bash && cd /odoo/odoo-server                 
```
    
```
./odoo-bin -c /etc/odoo-server.conf                    
```
                    

##  تثبيت على الجهاز الشخصي - للتجربة فقط
## Install On localhost
```
sudo apt install postgresql -y
dpkg -i odoo_14.0.latest_all.deb
apt-get install -f
dpkg -i odoo_14.0.latest_all.deb
```

###  لأي مساعدة يمكنك الاتصال بي عبر بيانات الاتصال الموجودة في موقعي التالي
### for any help you can contact me using information on my personal website
https://www.nacer.ma
                    
Video/فيديو:
https://www.youtube.com/watch?v=Pi9Yffgmlk4
