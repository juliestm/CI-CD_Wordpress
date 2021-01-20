Использован Vagrant + Ansible playbooks

Поднимаются следующие виртуалки с операционной системой ubuntu/focal64:

1) Application server (Nginx+PHP7+Wordpress)
2) Database server (MariaDB)
3) Monitoring server (Prometheus+Grafana)

Создаем пустой каталог, в терминале переходим в него и выполняем команду:

git clone https://github.com/yulia-matveeva/CI-CD_Wordpress

Затем выполняем команду:

vagrant up 

Переходим в браузер, по умолчанию:

Сайт доступен через http://localhost:8888

Prometheus: http://localhost:9999

Grafana: http://localhost:3333 

В prometheus собираются метрики со всех нод через node_exporter.

Можно добавить в Grafana хороший дашборд:
https://grafana.com/grafana/dashboards/1860

Для того чтобы загрузить реальный wordpress сайт вместо заглушки - нужно заменить файлы в provision/files/wordpress (нужен архив с файлами и дамп БД).
