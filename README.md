# API для Yatube

## Описание проекта

API для социальной сети Yatube. Позволяет пользователям публиковать посты, комментировать записи других пользователей и подписываться на авторов.

## Технологии

- Python 3.10
- Django 3.2.16
- Django REST Framework 3.12.4
- Simple JWT 5.3.1
- Djoser 2.2.0

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

5. Создайте суперпользователя (для доступа к админке):
```bash
python yatube_api/manage.py createsuperuser
```

6. (Опционально) Создайте группы через админку:
```
http://127.0.0.1:8000/admin/
```

7. Запустите сервер:
```bash
python yatube_api/manage.py runserver
```

8. Запустите тесты:
```bash
pytest
```

## Документация API

После запуска сервера документация доступна по адресу:
http://127.0.0.1:8000/redoc/

**Важно:** Большинство запросов требуют JWT-аутентификацию. Сначала получите токен через `/api/v1/jwt/create/`.

## Примеры запросов

### Получение JWT-токена

```
POST /api/v1/jwt/create/
Content-Type: application/json

{
    "username": "your_username",
    "password": "your_password"
}

Ответ:
{
    "refresh": "refresh_token",
    "access": "access_token"
}
```

### Получение списка постов (с пагинацией)

```
GET /api/v1/posts/
GET /api/v1/posts/?limit=10&offset=0
```

### Получение списка постов (аутентифицированный пользователь)

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

### Получение списка групп

```
GET /api/v1/groups/
```

### Получение информации о группе

```
GET /api/v1/groups/{id}/
```

## Автор

Проект выполнен в рамках курса Яндекс.Практикум
