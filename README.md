# express42task
Привет. Выполняю тестовое задание.
Предполагается что docker, а также docker compose и git установлены.

Все взял из этого репозитория, велосипед решил не придумывать. https://github.com/sameersbn/docker-redmine

***Установку Docker engine выплонял с помощью этой инструкции*** 
> https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository

***Docker Compose*** 
> https://docs.docker.com/compose/install

***Git***
> https://git-scm.com/download/linux 

1. git clone https://github.com/Konstnt/express42task.git

2. cd ex42-redmine/ 

3. Docker build -t ex42-redmine .

4. Стартуем 2 контейнера вручную. Второй контейнер линкуем с контейнером с БД.

Step 1. Launch a postgresql container

docker run --name=postgresql-redmine -d \
  --env='DB_NAME=redmine_production' \
  --env='DB_USER=redmine' --env='DB_PASS=password' \
  --volume=/srv/docker/redmine/postgresql:/var/lib/postgresql \
  sameersbn/postgresql:9.6-4

Step 2. Launch the redmine container

docker run --name=redmine -d \
  --link=postgresql-redmine:postgresql --publish=10083:80 \
  --env='REDMINE_PORT=10083' \
  --volume=/srv/docker/redmine/redmine:/home/redmine/data \
  ex42-redmine

5. Docker-compose Перемещаемся в директорию docker-redmine/
	Запускаем Docker-compose up -d
