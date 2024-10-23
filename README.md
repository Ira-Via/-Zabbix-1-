# -Zabbix-1-
«Система мониторинга Zabbix, 1 часть» Васяева Ирина
# Задание 1.
**1. Установка PostgreSQL** <br/>
   sudo apt update <br/>
   sudo apt install postgresql postgresql-contrib <br/>
   sudo systemctl start postgresql <br/>
   sudo systemctl enable postgresql <br/>
**2. Установка Zabbix Server и веб-интерфейса** <br/>
   wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-1+debian11_all.deb <br/>
   sudo dpkg -i zabbix-release_6.0-1+debian11_all.deb <br/>
   sudo apt update <br/>
   sudo apt install zabbix-server-pgsql zabbix-frontend-php zabbix-apache-conf <br/>
   sudo apt install php php-pgsql php-mbstring php-xml php-bcmath php-gd php-json <br/>
**3. Настройка базы данных для Zabbix** <br/>
   sudo -u postgres psql <br/>
   CREATE DATABASE zabbix OWNER zabbix; <br/>
   CREATE USER zabbix WITH PASSWORD '12345'; <br/>
   GRANT ALL PRIVILEGES ON DATABASE zabbix TO zabbix; <br/>
   \q <br/>
   cd /usr/share/doc/zabbix-server-pgsql/examples/ <br/>
   zcat create schema.sql.gz | sudo -u zabbix psql zabbix <br/>
**4. Настройка Zabbix Server** <br/>
   sudo nano /etc/zabbix/zabbix_server.conf <br/>
   DBPassword=12345 <br/>
   sudo systemctl restart zabbix-server <br/>
   sudo systemctl restart apache2 <br/>
   sudo systemctl status zabbix-server <br/>
**5. Настройка веб-интерфейса** <br/>
   http://<192.168.100.100>/zabbix <br/>
# Задание 2.
**1. Установка Zabbix Agent** (на две виртуальные машины) <br/>
   sudo apt update <br/>
   sudo apt install zabbix-agent <br/>
**2. Настройка Zabbix Agent**
   sudo nano /etc/zabbix/zabbix_agentd.conf <br/>
   Server=<196.168.100.100> <br/>
**3. Запуск и включение Zabbix Agent** <br/>
   sudo systemctl restart zabbix-agent <br/>
   sudo systemctl enable zabbix-agent <br/>
**4. Добавление агентов в Zabbix Server** <br/>
**5. Проверка подключения** <br/>
   sudo tail -f /var/log/zabbix/zabbix_agentd.log <br/>
