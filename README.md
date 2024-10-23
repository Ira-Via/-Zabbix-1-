# -Zabbix-1-
«Система мониторинга Zabbix, 1 часть» Васяева Ирина
# Задание 1.
Установка PostgreSQL
   sudo apt update
   sudo apt install postgresql postgresql-contrib
   sudo systemctl start postgresql
   sudo systemctl enable postgresql
Установка Zabbix Server и веб-интерфейса
   wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-1+debian11_all.deb
   sudo dpkg -i zabbix-release_6.0-1+debian11_all.deb
   sudo apt update
   sudo apt install zabbix-server-pgsql zabbix-frontend-php zabbix-apache-conf
   sudo apt install php php-pgsql php-mbstring php-xml php-bcmath php-gd php-json
Настройка базы данных для Zabbix
   sudo -u postgres psql
   CREATE DATABASE zabbix OWNER zabbix;
   CREATE USER zabbix WITH PASSWORD '12345';
   GRANT ALL PRIVILEGES ON DATABASE zabbix TO zabbix;
   \q
   cd /usr/share/doc/zabbix-server-pgsql/examples/
   zcat create schema.sql.gz | sudo -u zabbix psql zabbix
Настройка Zabbix Server
   sudo nano /etc/zabbix/zabbix_server.conf
   DBPassword=12345
   sudo systemctl restart zabbix-server
   sudo systemctl restart apache2
   sudo systemctl status zabbix-server
Настройка веб-интерфейса
   http://<192.168.100.100>/zabbix
