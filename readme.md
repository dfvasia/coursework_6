0. # Настройки coursework_6.settings
 настройка postgresql, связана с п.1

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'course_6',
            'USER': 'postgres',
            'PASSWORD': 'postgres123',
            'HOST': 'localhost',
            'PORT': '5432',
        }

    INSTALLED_APPS = [
        'rest_framework', # подключение DRF базовый
        'rest_framework_simplejwt', # подключение JWT token
        'rest_framework_simplejwt.token_blacklist', # блокирование уже исп. или скомпрометированных токенов
        'corsheaders', # включение CORS
        ]
    MIDDLEWARE_CLASSES = (
        ...
        'corsheaders.middleware.CorsMiddleware',
        'django.middleware.common.CommonMiddleware',
        ...
        )

    CORS_ORIGIN_ALLOW_ALL = True
    CORS_ALLOW_CREDENTIALS = True
    CORS_ORIGIN_WHITELIST = (
        'localhost:3030',
        )
    CORS_ORIGIN_REGEX_WHITELIST = (
        'localhost:3030',
        )

1. # Настройки coursework_6.urls
 path('api-auth/', include('rest_framework.urls')) # urls с авторизацией


2. # Подключение базы данных Postgres.
 создание докер контейнера с заданными параметрами
 docker run --name cours_6_postgres -e POSTGRES_DB=course_6 -e POSTGRES_PASSWORD=postgres123 -p 5432:5432 -d postgres


2. # Подключение DRF(Django REST Framework).
 poetry add djangorestframework
 rest_framework'
3. # Подключение CORS headers.
 poetry add django-cors-headers
 

5. # Подключение Swagger.
 авто документация проекта django
 poetry add drf-spectacular
