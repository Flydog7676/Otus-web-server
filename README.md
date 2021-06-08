# Otus-web-server
1. Для тестовой эксплуатации выключаем selinux:
- setenforce 0
- в файле /etc/selinux/config пишем SELINUX=disable 
2. Установка Apache в систему   yum install httpd
3. Создаем папки с виртуальными серверами в apache   
- в папке /var/www создаем папки k dir 808{1..2}
- копируем в папки тестовую html страницу
- cp /usr/share/httpd/noindex/index.html /var/www/8081/index.html
- cp /usr/share/httpd/noindex/index.html /var/www/8082/index.html
4. Для проверки меняем названия в index.html в папках:
- в 8081 заменяем строчку Testing 123.. на Testing 8081..
- в 8082 заменяем строчку Testing 123.. на Testing 8082..
5. Настройка виртуальные сервера httpd на разные порты 8081,8082
- Открываем файл конфигурации httpd /etc/httpd/conf/httpd.conf
- Заменяем строчку Listen 80 на :
- Listen 8081
- Listen 8082
6. Создаем файлы описания виртуальных вебсерверов:
  создаем файл server1.conf в /etc/httpd/conf.d/
  <VirtualHost *:8081>
  ServerAdmin alex@ulnanotech.com
  DocumentRoot /var/www/8081
  </VirtualHost>
  создаем файл server2.conf в /etc/httpd/conf.d/
  <VirtualHost *:8082>
  ServerAdmin alex@ulnanotech.com
  DocumentRoot /var/www/8082
  </VirtualHost>
  
  
  
  
 Проверим на ошибки синтаксиса конфигурации httpd    httpd -t
 
