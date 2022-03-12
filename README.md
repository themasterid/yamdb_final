
![Yamdb Workflow Status](https://github.com/themasterid/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg?branch=master&event=push)
# API_YAMDB 
REST API проект для сервиса YaMDb — сбор отзывов о фильмах, книгах или музыке. 

Проект развернут по адресу: http://themasterid.sytes.net/redoc/
## Описание 
 
Проект YaMDb собирает отзывы пользователей на произведения. 
Произведения делятся на категории: «Книги», «Фильмы», «Музыка». 
Список категорий  может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»). 
### Как запустить проект: 
Все описанное ниже относится к ОС Linux. 
Клонируем репозиторий и и переходим в него: 
```bash 
git clone git@github.com:themasterid/yamdb_final.git
cd yamdb_final 
cd api_yamdb 
``` 
 
Создаем и активируем виртуальное окружение: 
```bash 
python3 -m venv venv 
source /venv/bin/activate (source /venv/Scripts/activate - для Windows) 
python -m pip install --upgrade pip 
``` 
 
Ставим зависимости из requirements.txt: 
```bash 
pip install -r requirements.txt 
``` 

Переходим в папку с файлом docker-compose.yaml: 
```bash 
cd infra 
``` 
 
Поднимаем контейнеры (infra_db_1, infra_web_1, infra_nginx_1): 
```bash 
docker-compose up -d --build 
``` 

Выполняем миграции: 
```bash 
docker-compose exec web python manage.py makemigrations reviews 
``` 
```bash 
docker-compose exec web python manage.py migrate --run-syncdb
``` 

Создаем суперпользователя: 
```bash 
docker-compose exec web python manage.py createsuperuser 
``` 

Србираем статику: 
```bash 
docker-compose exec web python manage.py collectstatic --no-input 
``` 

Создаем дамп базы данных (нет в текущем репозитории): 
```bash 
docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json 
``` 

Останавливаем контейнеры: 
```bash 
docker-compose down -v 
``` 

### Шаблон наполнения .env (не включен в текущий репозиторий) расположенный по пути infra/.env 
``` 
DB_ENGINE=django.db.backends.postgresql 
DB_NAME=postgres 
POSTGRES_USER=postgres 
POSTGRES_PASSWORD=postgres 
DB_HOST=db 
DB_PORT=5432 
``` 
### Документация API YaMDb 
Документация доступна по эндпойнту: http://themasterid.sytes.net/redoc/ 
