# تثبيت اودو 14 في مخدم بنظام اوبنتو 18
# Install odoo 14 on ubuntu 18.04 server

##  تحديث السيرفر                   
sudo add-apt-repository universe && apt-get update && sudo apt-get upgrade -y 

##  انشاء مستخدم أودو في اوبنتو                      
sudo adduser -system -home=/opt/odoo -group odoo 

##  تثبيت بوستجريسكل
sudo apt-get install postgresql -y 
                    
##  انشاء مستخدم أودو في البوستجريسكل
sudo su - postgres -c "createuser -s odoo" 2> /dev/null || true 
                    
##  تثبيت البايثون وادواتها اللازمة لتشغيل اودو
sudo apt-get install git python3 python3-pip build-essential wget python3-dev python3-venv python3-wheel libxslt-dev libzip-dev libldap2-dev libsasl2-dev python3-setuptools node-less libjpeg-dev gdebi -y
                    
##  تثبيت ادوات البيب الخاصة بالبايثون
sudo -H pip3 install -r https://raw.githubusercontent.com/odoo/odoo/master/requirements.txt 
                    
##  تثبيت ادوات اخرى ضرورية                  
sudo apt-get install nodejs npm -y && sudo npm install -g rtlcss 

##  تثبيت حزم Wkhtmltopdf
sudo apt-get install xfonts-75dpi && sudo wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.bionic_amd64.deb &&sudo dpkg -i wkhtmltox_0.12.6-1.bionic_amd64.deb && sudo cp /usr/local/bin/wkhtmltoimage /usr/bin/wkhtmltoimage && sudo cp /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
                    
##  انشاء مجلد لحفظ سجلات الاستخدام
sudo mkdir /var/log/odoo && sudo chown odoo:odoo /var/log/odoo
                    
##  تثبيت أودو، النسخة 14.0
sudo git clone --depth 1 --branch 14.0 https://www.github.com/odoo/odoo /odoo/odoo-server
                    

##  تغيير صلاحيات مجلد اودو الرئيسي واعطاء ملكيته لمستخدم اودو الذي قمنا بانشاءه سلفا
sudo chown -R odoo:odoo /odoo/*
                    
##  انشاء ملف الاعدادات الرئيسي لأودو
sudo nano /etc/odoo-server.conf
##  ملأ الملف بالاعدادات اللازمة
sudo su root -c "printf '[options] \n; This is the password that allows database operations:\n' >> /etc/odoo-server.conf" && sudo su root -c "printf 'admin_passwd = admin\n' >> /etc/odoo-server.conf" && sudo su root -c "printf 'xmlrpc_port = 8069\n' >> /etc/odoo-server.conf" && sudo su root -c "printf 'logfile = /var/log/odoo/odoo-server.log\n' >> /etc/odoo-server.conf" && sudo su root -c "printf 'addons_path=/odoo/odoo-server/addons\n' >> /etc/odoo-server.conf" && sudo chown odoo:odoo /etc/odoo-server.conf && sudo chmod 640 /etc/odoo-server.conf 
                    

##  تشغيل اودو
sudo su - odoo -s /bin/bash && cd /odoo/odoo-server
./odoo-bin -c /etc/odoo-server.conf                    



###  لأي مساعدة يمكنك الاتصال بي عبر بيانات الاتصال الموجودة في موقعي التالي
https://www.elbasri.net/
                    
