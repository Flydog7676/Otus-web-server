# Otus-web-server
1. Для тестовой эксплуатации выключаем selinux:
- setenforce 0
- в файле /etc/selinux/config пишем SELINUX=disable 
2. Установка Apache в систему   yum install httpd
3. Создаем папки с виртуальными серверами в apache   
- в папке /var/www создаем папки k dir 808{1..3}
- копируем в папки тестовую html страницу
- cp /usr/share/httpd/noindex/index.html /var/www/8081/index.html
- cp /usr/share/httpd/noindex/index.html /var/www/8082/index.html
- cp /usr/share/httpd/noindex/index.html /var/www/8083/index.html
4. Для проверки меняем названия в index.html в папках:
- в 8081 заменяем строчку Testing 123.. на Testing 8081..
- в 8082 заменяем строчку Testing 123.. на Testing 8082..
- в 8083 заменяем строчку Testing 123.. на Testing 8083..
5. Настройка виртуальные сервера httpd на разные порты 8081,8082,8083
- Открываем файл конфигурации httpd /etc/httpd/conf/httpd.conf
- Заменяем строчку Listen 80 на :
- Listen 8081
- Listen 8082
- Listen 8083
6. Создаем файлы описания виртуальных вебсерверов:
-  создаем файл server1.conf в /etc/httpd/conf.d/
-  <VirtualHost *:8081>
-  ServerAdmin alex@ulnanotech.com
-  DocumentRoot /var/www/8081
-  </VirtualHost>
7. Cоздаем файл server2.conf в /etc/httpd/conf.d/
-  <VirtualHost *:8082>
-  ServerAdmin alex@ulnanotech.com
-  DocumentRoot /var/www/8082
-  </VirtualHost>
8. Cоздаем файл server3.conf в /etc/httpd/conf.d/
-  <VirtualHost *:8083>
-  ServerAdmin alex@ulnanotech.com
-  DocumentRoot /var/www/8083
-  </VirtualHost>
8. Проверим на ошибки синтаксиса конфигурации httpd    httpd -t
- Устанавливаем NGINX и прописываем UPSTREAM
9. создаем новую запись на репозитарий
- создаем файл nginx.repo в /etc/yum.repo.d/ c данными:
- [nginx-stable]
- name=nginx stable repo
- baseurl=http://nginx.org/packages/centos/$releasever/$basearch
- gpgcheck=1
- enabled=1
- gpgkey=https://nginx.org/keys/nginx_signing.key
- module_hotfixes=true
-
