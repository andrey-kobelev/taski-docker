# Taski

> Taski - инструмент для планирования задач, иначе говоря «трекер». Структура этого приложения : фронтенд (SPA-приложение на React) и бэкенд (Django-приложение).

Настроил запуск приложения (Django) на WSGI-сервере Gunicorn и настроил веб-сервер Nginx. Автоматизировал процесс получения и настройки SSL-сертификата при помощи пакета cerbot. Наладил мониторинг доступности и сбор ошибок проекта подключив сервис UptimeRobot. Так же настроил: Запуск проекта в Docker-контейнерах; Автоматическое тестирование и деплой этого проекта на удалённый сервер (CI/CD) с помощью сервиса GitHub Actions.

### Как развернуть проект локально  
  
Клонировать репозиторий и перейти в него в командной строке:    
    
```  
git clone https://github.com/andrey-kobelev/taski-docker.git
```    
    
```  
cd taski-docker
```    
    
Cоздать и активировать виртуальное окружение:    
    
```  
python3 -m venv venv  
```    
    
```  
source venv/bin/activate  
```    
    
Установить зависимости из файла requirements.txt:    
    
```  
python3 -m pip install --upgrade pip  
```    
    
```  
pip install -r requirements
```    
    
Выполнить миграции:    

```  
cd backend
``` 
    
```  
python3 manage.py migrate 
```  
    
Запустить проект (только бэк):    
    
```  
python3 manage.py runserver  
```    

## Запустить проект с фронтом локально

Файл `.env`, для локального запуска должен быть таким и находиться в корневой директории проекта:

```
POSTGRES_USER=django_user  
POSTGRES_PASSWORD=123456789django  
POSTGRES_DB=django_taski
DB_HOST=db  
DB_PORT=5432  
SECRET_KEY=<django_secret_key_from_settings> 
ALLOWED_HOSTS=<domain>,<server_ip>,127.0.0.1,localhost,0.0.0.0  
DEBUG_VALUE=True  
SQLITE=True
```

Далее в корневой директории выполните команду:

```
sudo docker compose -f docker-compose.yml up -d --build
```

> В проекте два файла docker compose: один для продакшена другой для локального запуска. `docker-compose.yml` - для локального запуска.

Далее поочередно выполните следующие команды так же находясь в корневой директории проекта:

```
sudo docker compose -f docker-compose.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.yml exec backend cp -r /app/collected_static/. /backend_static/static/
```


## В проекте были использованы технологии:    
* #### [Django REST](https://www.django-rest-framework.org/)    
* #### [ Python 3.9](https://www.python.org/downloads/release/python-390/)  
* #### [Gunicorn](https://gunicorn.org/)  
* #### [Nginx](https://www.nginx.com/)  
* #### [JS]()  
* #### [Node.js](https://nodejs.org/en)  
* #### [PostgreSQL](https://www.postgresql.org/)  
* #### [Docker](https://www.docker.com/)  
* #### [React](https://ru.legacy.reactjs.org/)  


### Над проектом работал:    
* [Kobelev Andrey](https://github.com/andrey-kobelev)
