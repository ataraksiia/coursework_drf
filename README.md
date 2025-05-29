# Проект 5. Трекер привычек

### Технологический стек:
- Python 3.11
- Django 4.2
- Django REST Framework
- Celery
- Redis
- PostgreSQL
- Telegram Bot API

### Установка и запуск:
1. Клонируйте репозиторий 
   git clone <url-репозитория> <папка-проекта>
2. Активируйте виртуальное окружение
   python -m venv venv
   source venv/bin/activate
3. Установите зависимости 
   pip install -r requirements.txt
4. Заполните .env по шаблону .env.example
5. Примените миграции 
   python manage.py migrate
6. Создайте суперпользователя
   python manage.py createsuperuser
7. Запустите Redis
8. Запустите Celery worker:
   celery -A config worker -l INFO
9. Запустите сервер:
   python manage.py runserver