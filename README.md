![Статус пайплайна](https://github.com/mgigarf/kittygram_final/actions/workflows/WORKFLOW-FILE/badge.svg)

#  Как работать с репозиторием финального задания

## Что нужно сделать

Настроить запуск проекта Kittygram в контейнерах и CI/CD с помощью GitHub Actions

## Как проверить работу с помощью автотестов

В корне репозитория создайте файл tests.yml со следующим содержимым:
```yaml
repo_owner: ваш_логин_на_гитхабе
kittygram_domain: полная ссылка (https://доменное_имя) на ваш проект Kittygram
taski_domain: полная ссылка (https://доменное_имя) на ваш проект Taski
dockerhub_username: ваш_логин_на_докерхабе
```

Скопируйте содержимое файла `.github/workflows/main.yml` в файл `kittygram_workflow.yml` в корневой директории проекта.

Для локального запуска тестов создайте виртуальное окружение, установите в него зависимости из backend/requirements.txt и запустите в корневой директории проекта `pytest`.

## Чек-лист для проверки перед отправкой задания

- Проект Taski доступен по доменному имени, указанному в `tests.yml`.
- Проект Kittygram доступен по доменному имени, указанному в `tests.yml`.
- Пуш в ветку main запускает тестирование и деплой Kittygram, а после успешного деплоя вам приходит сообщение в телеграм.
- В корне проекта есть файл `kittygram_workflow.yml`.

# Описание проекта

Сервис kittygram для публикации котиков.

# Стек
В проекте использованы следующие библиотеки:

    Python 3.9
    Django 3.2.16
    Django Rest Framework 3.12.4
    Posgresql
    Doker compose

# Запуск проекта
Скачать файл docker-compose.yml из репозитория 
``` bash
https://github.com/mgigarf/kittygram_final/blob/main/docker-compose.yml
```
Создать файл с переменными окружения .env в корне пректа
Список требуемых переменных:

    POSTGRES_DB=имя базы
    POSTGRES_USER=владелец базы
    POSTGRES_PASSWORD=пароль
    DB_NAME=имя базы
    DB_HOST=db
    DB_PORT=5432(лучше оставить так)
    SECRET_KEY=ключ приложения
    DEBUG=true/false
    ALLOWED_HOSTS=разрешенные хосты

Запустить Docker compose 
``` bash
sudo docker compose -f docker-compose.production.yml pull
sudo docker compose -f docker-compose.production.yml down
sudo docker compose -f docker-compose.production.yml up -d
```

Собрать статику и применить миграции
``` bash
sudo docker compose -f docker-compose.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.yml exec backend cp -r /app/collected_static/. /backend_static/static/ 
```

Автор проекта 
[Селиванов Михаил](https://github.com/mgigarf)