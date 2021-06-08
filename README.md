# Otus-web-server
Установка Apache в систему   yum install httpd
Создаем папки с виртуальными серверами в apache   
  в папке /var/www создаем папки k dir 808{1..2}
  копируем в папки тестовую html страницу
  cp /usr/share/httpd/noindex/index.html /var/www/8081/index.html
  cp /usr/share/httpd/noindex/index.html /var/www/8082/index.html
Для проверки меняем названия в index.html в папках:
  в 8081 заменяем строчку <h1>Testing 123..</h1> на <h1>Testing 8081..</h1>
  в 8082 заменяем строчку <h1>Testing 123..</h1> на <h1>Testing 8082..</h1>
Настройка виртуальные сервера httpd на разные порты 8081,8082
  Открываем файл конфигурации httpd /etc/httpd/conf/httpd.conf
  Заменяем строчку Listen 80 на :
  Listen 8081
  Listen 8082
Создаем файлы описания виртуальных вебсерверов:
  создаем файл server1 в /etc/httpd/conf.d/
  <VirtualHost *:8081>
  ServerAdmin alex@ulnanotech.com
  DocumentRoot /var/www/8081
  </VirtualHost>
  создаем файл server2 в /etc/httpd/conf.d/
  <VirtualHost *:8082>
  ServerAdmin alex@ulnanotech.com
  DocumentRoot /var/www/8082
  </VirtualHost>
  
  
  
  
 Проверим на ошибки синтаксиса конфигурации httpd    httpd -t
 
