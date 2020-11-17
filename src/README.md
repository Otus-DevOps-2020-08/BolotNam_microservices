# Micorservices
ДЗ docker-4
имя проекта зависит от директории в которой находится docker-compose.yml или docker-compose.yaml

ДЗ docker-3

подключаемся к ранее созданному инстансу на yandex cloud
скачиваем папку с шаблонами
собираем образы post-py, comment, ui
создаем bridge-сеть "reddit" для контейнеров
запускаем собранные образы post-py, comment, ui и проверяем "постим что-ить"
cоздаем bridge-сеть "hw-reddit", удаляем и перезапускаем все контейнеры. Проверяем что все работает.
останавливаем контейнеры, проверяем размер образов
пересобираем образ ui с помощью исходника ubuntu и проверяем что образ 2.0 меньше первого.
останавливаем и заново запускаем образы. видим что наши "посты ичезли"
создаем раздел
останавливаем и заново запускаем образы с указанием reddit_db:/data/db
постим и снова перезапускаем образы: проверяем что посты остались
ДЗ docker-2

Создание ветки
установка docker? docker-machine, docker-compose
Запуск image 'hello world'
запуск docker с командами run/start/attach/exec/commit/kill/stop/system df/rm/rmi
установка yc
Создание instance с помощью yc
Деплой docker на удаленном instance с помощью docker-machine
Создание docker-контейнера используя Dockerfile, mongod.conf, db_config, start.sh
загрузка полчившегося образа на docker hub.
развертывание орбраза из docker hub на локальном хосте.
