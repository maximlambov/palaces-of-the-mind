# Docker 

## Images

`docker image my_command`

Команды для управления образами:

- build — сборка образа.
- push — отправка образа в удалённый реестр.
- ls — вывод списка образов.
- history — вывод сведений о слоях образа.
- inspect — вывод подробной информации об образе, в том числе — сведений о слоях.
- rm — удаление образа.

Добавление image

```bash

docker pull image_name (for example ngnix)

```

Посмотреть список всех images с помощью команды:

```bash

docker images

```

Удаление image

```bash

docker image rm id_image_or_first_three_chars_name

```

## Container

`docker container my_command`

Команды для управления контейнерами:

- create — создание контейнера из образа.
- start — запуск существующего контейнера.
- run — создание контейнера и его запуск.
- ls — вывод списка работающих контейнеров.
- inspect — вывод подробной информации о контейнере.
- logs — вывод логов.
- stop — остановка работающего контейнера с отправкой главному процессу контейнера сигнала SIGTERM, и, через некоторое время, SIGKILL.
- kill — остановка работающего контейнера с отправкой главному процессу контейнера сигнала SIGKILL.
- rm — удаление остановленного контейнера.

Флаг -p представляет собой сокращение для --port. Конструкция 1000:8000

Флаг -i — это сокращение для --interactive. Благодаря этому флагу поток STDIN поддерживается в открытом состоянии даже если контейнер к STDIN не подключён.

Флаг -t — это сокращение для --tty. Благодаря этому флагу выделяется псевдотерминал, который соединяет используемый терминал с потоками STDIN и STDOUT контейнера.

Для того чтобы получить возможность взаимодействия с контейнером через терминал нужно совместно использовать флаги -i и -t.

Флаг --rm автоматически удаляет контейнер после того, как его выполнение завершится.

Флаг -d — это сокращение для --detach. Эта команда запускает контейнер в фоновом режиме, для выполнения других команд во время работы контейнера.

> Посмотреть список контейнеров с помощью команды:

```bash

docker container ls (только запущенные)

docker container ls -a -s

```

Ключ -a этой команды — это сокращение для --all. Благодаря использованию этого ключа можно вывести сведения обо всех контейнерах, а не только о выполняющихся.

Ключ -s — это сокращение для --size. Он позволяет вывести размеры контейнеров.


Команда, которая выводит подробные сведения о контейнере:

`docker container inspect my_container`

Команда, выводящая логи контейнера:

`docker container logs my_container`


> Остановить контейнер

```bash

docker container stop id_container_or_first_three_chars_name

```

> Удаление контейнера 

```bash

docker container rm id_container_or_first_three_chars_name

```

> Создание образов


`docker image build -t my_repo/my_image:my_tag .`

Флаг -t — это сокращение для --tag. Он указывает Docker на то, что создаваемому образу надо назначить предоставленный в команде тег.


> Разные команды

`docker system prune -a --volumes`

Ключ -a — сокращение для --all, позволяет удалить неиспользуемые образы, а не только те, которым не назначено имя и тег.

Ключ --volumes позволяет удалить неиспользуемые тома.

## Dockerfile

- FROM — задаёт базовый (родительский) образ.
- LABEL — описывает метаданные. Например — сведения о том, кто создал и поддерживает образ.
- ENV — устанавливает постоянные переменные среды.
- RUN — выполняет команду и создаёт слой образа. Используется для установки в контейнер пакетов.
- COPY — копирует в контейнер файлы и папки.
- ADD — копирует файлы и папки в контейнер, может распаковывать локальные .tar-файлы.
- CMD — описывает команду с аргументами, которую нужно выполнить когда контейнер будет запущен. Аргументы могут быть переопределены при запуске контейнера. В файле может присутствовать лишь одна инструкция CMD.
- WORKDIR — задаёт рабочую директорию для следующей инструкции.
- ARG — задаёт переменные для передачи Docker во время сборки образа.
- ENTRYPOINT — предоставляет команду с аргументами для вызова во время выполнения контейнера. Аргументы не переопределяются.
- EXPOSE — указывает на необходимость открыть порт.
- VOLUME — создаёт точку монтирования для работы с постоянным хранилищем.


```bash
# example 1

FROM python:3.7.2-alpine3.8
LABEL maintainer="jeffmshale@gmail.com"
ENV ADMIN="jeff"
RUN apk update && apk upgrade && apk add bash
COPY . ./app
ADD https://raw.githubusercontent.com/discdiver/pachy-vid/master/sample_vids/vid1.mp4 \
/my_app_directory
RUN ["mkdir", "/a_directory"]
CMD ["python", "./my_script.py"]

```

```bash

# example 2

FROM python:3.7.2-alpine3.8
LABEL maintainer="jeffmshale@gmail.com"
# Устанавливаем зависимости
RUN apk add --update git
# Задаём текущую рабочую директорию
WORKDIR /usr/src/my_app_directory
# Копируем код из локального контекста в рабочую директорию образа
COPY . .
# Задаём значение по умолчанию для переменной
ARG my_var=my_default_value
# Настраиваем команду, которая должна быть запущена в контейнере во время его выполнения
ENTRYPOINT ["python", "./app/my_script.py", "my_var"]
# Открываем порты
EXPOSE 8000
# Создаём том для хранения данных
VOLUME /my_volume

```

## Docker-Compose 
