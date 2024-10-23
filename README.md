# -Zabbix-1-
«Система мониторинга Zabbix, 1 часть» Васяева Ирина
# Задание 1.
*Установка PostgreSQL* <br/>
   sudo apt update <br/>
   sudo apt install postgresql postgresql-contrib <br/>
   sudo systemctl start postgresql <br/>
   sudo systemctl enable postgresql <br/>
*Установка Zabbix Server и веб-интерфейса* <br/>
   wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-1+debian11_all.deb <br/>
   sudo dpkg -i zabbix-release_6.0-1+debian11_all.deb <br/>
   sudo apt update <br/>
   sudo apt install zabbix-server-pgsql zabbix-frontend-php zabbix-apache-conf <br/>
   sudo apt install php php-pgsql php-mbstring php-xml php-bcmath php-gd php-json <br/>
*Настройка базы данных для Zabbix* <br/>
   sudo -u postgres psql <br/>
   CREATE DATABASE zabbix OWNER zabbix; <br/>
   CREATE USER zabbix WITH PASSWORD '12345'; <br/>
   GRANT ALL PRIVILEGES ON DATABASE zabbix TO zabbix; <br/>
   \q <br/>
   cd /usr/share/doc/zabbix-server-pgsql/examples/ <br/>
   zcat create schema.sql.gz | sudo -u zabbix psql zabbix <br/>
*Настройка Zabbix Server* <br/>
   sudo nano /etc/zabbix/zabbix_server.conf <br/>
   DBPassword=12345 <br/>
   sudo systemctl restart zabbix-server <br/>
   sudo systemctl restart apache2 <br/>
   sudo systemctl status zabbix-server <br/>
*Настройка веб-интерфейса* <br/>
   http://<192.168.100.100>/zabbix <br/>
