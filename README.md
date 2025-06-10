# Проект 5. Трекер привычек

# Адрес сервера 130.193.41.24

### Технологический стек:
- Python 3.11
- Django 4.2
- Django REST Framework
- Celery
- Redis
- PostgreSQL
- Telegram Bot API

### Установка и запуск локально:
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

### Развертывание на удалённом сервере (Ubuntu-based):
1. sudo apt update && sudo apt upgrade -y
2. sudo apt install docker.io docker-compose -y
3. настройте .env
4. sudo ufw allow 'Nginx Full'
   sudo ufw allow OpenSSH
   sudo ufw enable
5. docker-compose up --build -d


### CI/CD (GitHub Actions)
Используйте шаблон `.github/workflows/deploy.yml` для автоматического деплоя на сервер:
1. yaml
name: Deploy to VPS

on:
  push:
    branches: [main, master, dev]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Copy files to server
        uses: appleboy/scp-action@master
        with:
          host: ${{ secrets.SERVER_IP }}
          username: ${{ secrets.SERVER_USER }}
          key: ${{ secrets.SERVER_SSH_KEY }}
          source: "."
          target: "/home/${{ secrets.SERVER_USER }}/Django_REST_Framework"
      - name: Run deploy script via SSH
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.SERVER_IP }}
          username: ${{ secrets.SERVER_USER }}
          key: ${{ secrets.SERVER_SSH_KEY }}
          script: |
            cd Django_REST_Framework
            docker-compose down
            docker-compose pull
            docker-compose up --build -d

2. Заполните в настройках репозитория SECRET переменные 


