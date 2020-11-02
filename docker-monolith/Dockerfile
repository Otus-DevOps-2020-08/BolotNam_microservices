FROM ubuntu:18.04

# Обновление кэш и установка пакетов
RUN apt-get update
RUN apt-get install -y mongodb-server ruby-full ruby-dev build-essential git
RUN gem install bundler

# Установка monolith из github
RUN git clone -b monolith https://github.com/express42/reddit.git

#  Копируем файлы конфигурации подготовленные ранее
COPY mongod.conf /etc/mongod.conf
COPY db_config /reddit/db_config
COPY start.sh /start.sh

# Установка зависимостей и настройка
RUN cd /reddit && rm Gemfile.lock && bundle install
RUN chmod 0777 /start.sh

# Стартуем сервис
CMD ["/start.sh"]
