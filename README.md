# express42task
Привет. Выполняю тестовое задание.
Предполагается что docker, а также docker compose и git установлены.

Все взял из этого репозитория, велосипед решил не придумывать. https://github.com/sameersbn/docker-redmine

***Docker engine*** 

> https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository

***Docker Compose*** 

> https://docs.docker.com/compose/install

***Git***

> https://git-scm.com/download/linux 

1. Скачиваем файлы 

> git clone https://github.com/Konstnt/express42task.git

2. Перемещаемся в директорию 

> cd ex42-redmine/ 

3. Собираем образ с помощью инструкций в Dockerfile 

> docker build -t ex42-redmine .

4. Стартуем 2 контейнера вручную. Второй контейнер линкуем с контейнером с БД.

4.1 Контейнер Postgresql

> docker run --name=postgresql-redmine -d \
  --env='DB_NAME=redmine_production' \
  --env='DB_USER=redmine' --env='DB_PASS=password' \
  --volume=/srv/docker/redmine/postgresql:/var/lib/postgresql \
  sameersbn/postgresql:9.6-4

4.2. Контейнер Redmine

> docker run --name=redmine -d \
  --link=postgresql-redmine:postgresql --publish=10083:80 \
  --env='REDMINE_PORT=10083' \
  --volume=/srv/docker/redmine/redmine:/home/redmine/data \
  ex42-redmine

5. Docker-compose Запускаем контейнеры в виде сервисов (Останавливаем контейнеры из п4. У меня была проблема не стартовали сервисы, пришлоь удалять оба volume с хоста)
> docker-compose up -d

# TRAVIS-CI.ORG
Файл .travis.yml
 *Задает тест сборки образа и его деплой в бранч gh-pages
> https://github.com/Konstnt/express42task/tree/gh-pages
