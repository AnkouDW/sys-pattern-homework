# Домашнее задание к занятию "`ELK`" - `Яковлева Александра`

# Задание 1. Elasticsearch
Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный.

Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name.

![1 (1)](https://github.com/user-attachments/assets/bca25298-7042-4e35-8e98-8eb1587a7b7e)
![2 (1)](https://github.com/user-attachments/assets/2e4a0679-68bc-48a1-adc1-49ee015c9f4a)


# Задание 2. Kibana
Установите и запустите Kibana.

Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty.

![3](https://github.com/user-attachments/assets/47f9aa42-f05f-4e69-a0fa-76643157683f)


# Задание 3. Logstash
Установите и запустите Logstash и Nginx. С помощью Logstash отправьте access-лог Nginx в Elasticsearch.

Приведите скриншот интерфейса Kibana, на котором видны логи Nginx.

<img width="1359" height="295" alt="yes1" src="https://github.com/user-attachments/assets/f71032fb-025c-41e4-b838-07997a0b4051" />
<img width="1923" height="1161" alt="yes2" src="https://github.com/user-attachments/assets/2be50c34-4e32-43f0-815b-bf8845aadb26" />

# Задание 4. Filebeat.
Установите и запустите Filebeat. Переключите поставку логов Nginx с Logstash на Filebeat.

Приведите скриншот интерфейса Kibana, на котором видны логи Nginx, которые были отправлены через Filebeat.

<img width="1370" height="765" alt="fbng" src="https://github.com/user-attachments/assets/bab9cad2-124e-4b03-8cc2-b2cf3a047800" />
<img width="1917" height="1147" alt="fbkb" src="https://github.com/user-attachments/assets/94c1a892-8643-466c-a67d-e2ea8ea50733" />


Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

# Задание 5*. Доставка данных
Настройте поставку лога в Elasticsearch через Logstash и Filebeat любого другого сервиса , но не Nginx. Для этого лог должен писаться на файловую систему, Logstash должен корректно его распарсить и разложить на поля.

Приведите скриншот интерфейса Kibana, на котором будет виден этот лог и напишите лог какого приложения отправляется.
