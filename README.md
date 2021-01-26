# ДЗ kubernetes-3

1. Тестим влияние kube-dns
2. вспоминаем cluster ip и NodePort
3. тестим Loadbalancer
4. тестим Ingress
5. тестим ingress+tls
6. тестим network policy для разделения трафика
7. тестим подключение баз stateful, persistent volume

ДЗ kubernetes-2
# ДЗ kubernetes-2

1. Создал ветку kubernetes-2
2. Устанавливаем kubectl
3. Устанавливаем Minikube
4. Запускаем minikube
		minikube start
5. проверяем что кластер развернут
		kubectl get nodes
6. Проверка какой контекст используется по умолчанию
		kubeclt config current-context
7. Список всех контекстов
		kubectl config get-contexts
8. Изменяем ui-deployment.yml и запускаем его
		kubectl apply -f ui-deployment.yml
		### Для удаления используем kubectl delete deployment ui
9. Убеждаемся что запустились все реплики ui. запускаются долго !!!
		kubectl get deployment
10. Пробрасываем сетевые порты POD-ов на локальную машину
		kubectl get pods --selector component=ui
		kubectl port-forward <pod-name> 8080:9292
		проверяем зайдя на локальной машине на http://localhost:8080
11. Создаем comment/post/mongo-deployment.yml
12. Просмотреть всех pod
		kubectl get pod -o wide
13. Для связи comment/post/mongodb создаем services *-services.yml
		Для просмотра запущенных сервисов kubectl get service
		Для удаления используем kubectl delete service имя_сервиса
14. По label-ам должны были быть найдены соответствующие POD-ы.
		Посмотреть можно с помощью:
		kubectl describe service comment | grep Endpoints
15. А изнутри любого POD-а должно разрешаться:
		 kubectl exec -ti <pod-name> nslookup comment #у меня не получается. ругается что нет cmlet nslookup
		 kubectl exec -ti <pod-name> ping ip
16. Для связи pod из comment/post с mongodb создаем commentpost/-mongodb-service.yml
		Добавляем данные по БД в comment/post-deployment
17. Создаем ui-service для доступа с ip локальной машины
18. Знакомимся с minikube service list, minikube addon list
19. Запускаем minikube dashboard, знакомимся с фунционалом.
20. Создаем namespace dev с помощью dev-deployment.yml
		kubectl apply -f dev-namespace.yml
21. Запускаем приложение в namespace вум
		kubectl apply -f -n dev ./
22.	Развертывание кластера в yandex kubernetes. Подключаем кластер по мануалу https://cloud.yandex.ru/docs/managed-kubernetes/quickstart?utm_source=console&utm_medium=side-bar-left&utm_campaign=managed-kubernetes
23. Изменим default context на кластер yc
		kubectl config current-context yc-nbt-otus-kube
24. И развернем окружение в namespace dev
		kubectl apply -f ./ -n dev


ДЗ kubernetes-1
1. созданы тестовые post,ui,comment,mongo-deployment.yml
2. пройден (с помощью коллег) the_hard_way
Сложно для виндового админа (((

ДЗ logging-1
1. Создана ветка logging-1
2. Подготавливаем окружение, обновляем reddit, собираем и пушим образы в dockerhub
3. Устанавливаем язык Go, настраиваем драйвер для работы с Yandex.Cloud
4. Создаем ВМ в Yandex.Cloud
5. Создаем docker-compose-logging.yml для системы логгирования
6. Создаем Dockerfile, fluent.conf для Fluentd и собираем Docker образ
7. Подключаемся к ВМ и запускаем контейнеры и наблюдаем как пишутся логи
8. добавляем драйвер fluentd для сервиса post
9. запускаем контейнер логирования и перезапускаем остальные контейнеры
10. Делаем тестовые посты
11. Заходим на Kibana и наблюдаем логи.
12. Добавляем фильтры во fluentd для service.post
13. добавляем драйвер fluentd для сервиса ui и перезапускаем сервис ui
14. Добавляем фильтры во fluentd для service.ui и перезапускаем сервис fluentd
15. заменяем шаблоны с регулярными выражениями на grok-шаблоны, сначала с одним потом с несколькими
16. Распределенный трейсинг. Добавляем сервис  Zipkin в docker-compose-logging.yml.
17. Включаем его в docker-compose.yml.
18. Переподнимаем инфраструктуру.
19. Заходим на web-интерфейс Zipkin на порту 9411, смотрим и тд.

ДЗ monitoring-1
ссылка на dockerhub https://hub.docker.com/bobastik1982

ДЗ gitlab-ci-1
1. создание ВМ с заданными параметрами с помощью packer
2. установка Docker на ВМб с помощью docker-machine
3. подготовка к развертыванию gitlab на ВМ
    - директории /srv/gitlab/config /srv/gitlab/data /srv/gitlab/logs
    - файл docker-compose.yml
4. развертывание контейнера gitlab на ВМ с помощью docker-compose
5. смена пароль root, отключение регистрации, создание группы, создание проекта, push в gitlab
6. создание pipeline для gitlab (.gitlab-ci.yml)
7. добавление, регистрация и проверка runner
8. добавление reddit в проект gitlab
9. добавление тестов в pipeline
10. добавление окружений dev, stage и production
11. добавление условий (в нашем случае тэг)
12. тестирование динамических окружений.

ДЗ docker-3
1. подключаемся к ранее созданному инстансу на yandex cloud
2. скачиваем папку с шаблонами
3. собираем образы post-py, comment, ui
4. создаем bridge-сеть "reddit" для контейнеров
5. запускаем собранные образы post-py, comment, ui  и проверяем "постим что-ить"
6. cоздаем bridge-сеть "hw-reddit", удаляем и перезапускаем все контейнеры. Проверяем что все работает.
7. останавливаем контейнеры, проверяем размер образов
8. пересобираем образ ui с помощью исходника ubuntu и проверяем что образ 2.0 меньше первого.
9. останавливаем и заново запускаем образы. видим что наши "посты ичезли"
10. создаем  раздел
11. останавливаем и заново запускаем образы с указанием reddit_db:/data/db
12. постим и снова перезапускаем образы: проверяем что посты остались


ДЗ docker-2
1. Создание ветки
2. установка docker? docker-machine, docker-compose
3. Запуск image 'hello world'
4. запуск docker с командами run/start/attach/exec/commit/kill/stop/system df/rm/rmi
5. установка yc
6. Создание instance с помощью yc
7. Деплой docker на удаленном instance с помощью docker-machine
8. Создание docker-контейнера используя Dockerfile, mongod.conf, db_config, start.sh
9. загрузка полчившегося образа на docker hub.
10. развертывание орбраза из docker hub на локальном хосте.
