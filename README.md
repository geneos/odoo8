# Instalacion de odoo 8

Actualizamos el sistema.

**sudo apt-get update**

Creamos el usuario odoo, que será con la que ejecutaremos la aplicación.

**adduser --system --home=/opt/odoo --group odoo**

Instalando la basde de datos

**apt-get install postgresql**

Iniciamos sesion con el de postgres

**su - postgres**

Creando el usuario de Odoo ERP en postgreSql y asignandole un password.

**createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt odoo**

Finalizamos la sesión de postgres

**exit**

Instalando los paquetes necesarios de python para Odoo ERP.

**sudo apt-get install python-dateutil python-feedparser python-gdata python-ldap python-libxslt1 python-lxml python-mako python-openid python-psycopg2 python-pybabel python-pychart python-pydot python-pyparsing python-reportlab python-simplejson python-tz python-vatnumber python-vobject python-webdav python-werkzeug python-xlwt python-yaml python-zsi python-docutils python-psutil wget python-unittest2 python-mock python-jinja2 python-dev libpq-dev poppler-utils python-pdftools antiword python-setuptools python-requests python-pypdf python-decorator python-passlib**

Ingresamos a la carpeta odoo

**cd /opt/odoo**

Descargamos Odoo v8

**wget https://github.com/odoo/odoo/archive/8.0.zip**

Descomprimimos

**unzip 8.0.zip**

Cambiamos los permisos

**chown -R odoo: odoo-8.0**

Renombrando la carpeta  odoo-8.0 a server

**mv odoo-8.0 server**

Configurando Odoo ERP

**cp /opt/odoo/server/debian/openerp-server.conf /etc/odoo-server.conf
chown odoo: /etc/odoo-server.conf
chmod 640 /etc/odoo-server.conf**

Editamos el archivo odoo-server.conf y modificamos a **db_user =odoo y db_password=False por db_password=nuestropassword colocado en el paso 5.**

**nano /etc/odoo-server.conf**

Agregamos también en odoo-server.conf la linea siguiente, es un archivo donde se veran los logs de Odoo colocamos la ruta donde estarán los addons

**logfile = /var/log/odoo/odoo-server.log
addons_path = /opt/odoo/server/addons/**

Iniciamos sesion con el usuario odoo.

**su - odoo -s /bin/bash**

Iniciamos el servidor odoo

**/opt/odoo/server/openerp-server**
**cd /etc/init.d/**

descargamos el siguiente archivo

**git clone https://github.com/geneos/odoo8/blob/master/odoo-server**

Damos permiso al archivo odoo-server

**chmod 755 /etc/init.d/odoo-server
chown root: /etc/init.d/odoo-server**

Creamos el el directorio y la carpeta para guardar los logs de odoo y le damos los permisos correspondientes

**mkdir /var/log/odoo
chown odoo:root /var/log/odoo**

Haciendo que openerp se inicie automaticamente

**update-rc.d odoo-server defaults**

Iniciando el servidor con cambios finales

**/etc/init.d/odoo-server start**

Podemos ir a un navegador web y probar

**http://IP_or_domain.com:8069**