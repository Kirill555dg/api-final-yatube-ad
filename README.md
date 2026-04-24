# API для Yatube

## Описание проекта

API для социальной сети Yatube. Позволяет пользователям публиковать посты, комментировать записи других пользователей и подписываться на авторов.

## Технологии

- Python 3.10
- Django 3.2.16
- Django REST Framework 3.12.4
- Simple JWT 4.7.2

## Установка

1. Клонируйте репозиторий:
```bash
git clone <url-репозитория>
cd api-final-yatube-ad
```

2. Создайте и активируйте виртуальное окружение:
```bash
python3.10 -m venv .venv
source .venv/bin/activate  # для Linux/macOS
# или
.venv\Scripts\activate  # для Windows
```

3. Установите зависимости:
```bash
pip install -r requirements.txt
```

4. Выполните миграции:
```bash
python yatube_api/manage.py migrate
```

5. Создайте суперпользователя:
```bash
python yatube_api/manage.py createsuperuser
```

6. Запустите сервер:
```bash
python yatube_api/manage.py runserver
```

7. Запустите тесты:
```bash
pytest
```

## Документация API

После запуска сервера документация доступна по адресу:
http://127.0.0.1:8000/redoc/

## Примеры запросов

### Получение JWT-токена

```
POST /api/v1/jwt/create/
Content-Type: application/json

{
    "username": "your_username",
    "password": "your_password"
}
```

### Получение списка постов

```
GET /api/v1/posts/
Authorization: Bearer <your_token>
```

### Создание поста

```
POST /api/v1/posts/
Authorization: Bearer <your_token>
Content-Type: application/json

{
    "text": "Текст поста",
    "group": 1
}
```

### Получение комментариев к посту

```
GET /api/v1/posts/{post_id}/comments/
Authorization: Bearer <your_token>
```

### Создание комментария

```
POST /api/v1/posts/{post_id}/comments/
Authorization: Bearer <your_token>
Content-Type: application/json

{
    "text": "Текст комментария"
}
```

### Подписка на пользователя

```
POST /api/v1/follow/
Authorization: Bearer <your_token>
Content-Type: application/json

{
    "following": "username"
}
```

### Получение списка подписок

```
GET /api/v1/follow/
Authorization: Bearer <your_token>
```

### Поиск по подпискам

```
GET /api/v1/follow/?search=username
Authorization: Bearer <your_token>
```

## Автор

Проект выполнен в рамках курса Яндекс.Практикум
