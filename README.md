<div id="header" align="center">
  <h1>StatusHistory</h1>
  <img src="https://img.shields.io/badge/Python-3.7.9-F8F8FF?style=for-the-badge&logo=python&logoColor=20B2AA">
  <img src="https://img.shields.io/badge/Django-3.2.23-F8F8FF?style=for-the-badge&logo=django&logoColor=00FF00">
  <img src="https://img.shields.io/badge/DjangoRestFramework-3.14.0-F8F8FF?style=for-the-badge&logo=django&logoColor=00FF00">
  <img src="https://img.shields.io/badge/Docker-555555?style=for-the-badge&logo=docker&logoColor=2496ED">
</div>

# Документация API
[clownvkkaschenko.github.io/StatusHistory](https://clownvkkaschenko.github.io/StatusHistory/)

# Описание проекта:
Есть несколько рабочих сервисов, у каждого сервиса есть состояние работает/не работает/работает нестабильно.

Написан API который:

1. Получает и сохраняет данные сервиса: имя, состояние, описание.
2. Выводит список сервисов с актуальным состоянием.
3. По id сервиса выдает историю изменения состояния и все данные по каждому состоянию.
4. По указанному интервалу выдаёт информация о том сколько не работал сервис и считает SLA в процентах до 3-й запятой.

# Описание API:
- **GET /api/services/** - выводит список сервисов с актуальным состоянием.
- **POST /api/services/** - добавление нового сервиса.
- **GET /api/history/{service_id}/** - выдает историю изменений состояния.
- **GET /api/{service_id}/{start_date}/{end_date}/**: выдаёт информация о том сколько не работал сервис и считает SLA.

# Запуск проекта:
- Клонируйте репозиторий и перейдите в него.
- Перейдите в папку **infra** и проверьте, что файл .env заполнен данными представленными ниже:
  ```
  DEBUG=True
  ALLOWED_HOSTS=127.0.0.1
  ```
- Из папки **infra** запустите docker-compose
  ```
  ~$ docker-compose up -d --build
  ```
- В контейнере web выполните миграции, создайте суперпользователя и соберите статику.
  ```
  ~$ docker-compose exec web python manage.py migrate
  ~$ docker-compose exec web python manage.py createsuperuser
  ~$ docker-compose exec web python manage.py collectstatic --no-input
  ```

После этого API проекта будет доступно по url-адресу [127.0.0.1/api/](http://127.0.0.1/api/)

Документация к API будет доступна по url-адресу [127.0.0.1/api/docs](http://127.0.0.1/api/docs/)
