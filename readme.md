0. # Настройки coursework_6.settings


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
        'drf_spectacular'
        ]
    MIDDLEWARE_CLASSES = (
        ...
        'corsheaders.middleware.CorsMiddleware',
        'django.middleware.common.CommonMiddleware',
        ...
        )

    REST_FRAMEWORK = {
        "DEFAULT_PAGINATION_CLASS": "rest_framework.pagination.PageNumberPagination",
        "PAGE_SIZE": 10,
        "DEFAULT_AUTHENTICATION_CLASSES": [
            "rest_framework_simplejwt.authentication.JWTAuthentication",
        ],
        "DEFAULT_SCHEMA_CLASS": "drf_spectacular.olpenapi.AutoShema",
    }
    SIMPLE_JWT = {
        'ACCESS_TOKEN_LIFETIME': timedelta(minutes=60),
        'REFRESH_TOKEN_LIFETIME': timedelta(days=10),
        'ROTATE_REFRESH_TOKENS': True,
        'BLACKLIST_AFTER_ROTATION': True
    }

    SPECTACULAR_SETTINGS ={
        "TITLE": "Курсовая работа №6 API",
        "DESCRIPTION": "Описание API",
        "VERSION": "0.0.1",
       }

    CORS_ORIGIN_ALLOW_ALL = True
    CORS_ALLOW_CREDENTIALS = True
    CORS_ORIGIN_WHITELIST = (
        'localhost:3030',
        )
    CORS_ORIGIN_REGEX_WHITELIST = (
        'localhost:3030',
        )
    AUTH_USER_MODEL = 'authentication.User'

1. # Подключение базы данных Postgres.
 создание докер контейнера с заданными параметрами
 docker run --name cours_6_postgres -e POSTGRES_DB=course_6 -e POSTGRES_PASSWORD=postgres123 -p 5432:5432 -d postgres
 # Настройки coursework_6.settings

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'course_6',
            'USER': 'postgres',
            'PASSWORD': 'postgres123',
            'HOST': 'localhost',
            'PORT': '5432',
        }

2. # Подключение DRF(Django REST Framework).
 poetry add djangorestframework
 poetry add djangorestframework-simplejwt
   # Настройки coursework_6.settings

    INSTALLED_APPS = [
        ...
        'rest_framework', # подключение DRF базовый
        'rest_framework_simplejwt', # подключение JWT token
        'rest_framework_simplejwt.token_blacklist', # блокирование уже исп. или скомпрометированных токенов
        ...
        ]
    REST_FRAMEWORK = {
        "DEFAULT_PAGINATION_CLASS": "rest_framework.pagination.PageNumberPagination",
        "PAGE_SIZE": 10,
        "DEFAULT_AUTHENTICATION_CLASSES": [
            "rest_framework_simplejwt.authentication.JWTAuthentication",
        ],
    }
    SIMPLE_JWT = {
        'ACCESS_TOKEN_LIFETIME': timedelta(minutes=60),
        'REFRESH_TOKEN_LIFETIME': timedelta(days=10),
        'ROTATE_REFRESH_TOKENS': True,
        'BLACKLIST_AFTER_ROTATION': True
    }
    AUTH_USER_MODEL = 'authentication.User'

 # Настройки coursework_6.urls
`  path('api-auth/', include('rest_framework.urls')) # urls с авторизацией`

3. # Подключение CORS headers.
 poetry add django-cors-headers
  # Настройки coursework_6.settings

    INSTALLED_APPS = [
        ...
        'corsheaders', # включение CORS
        ...
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
 

4. # Подключение Swagger.
 авто документация проекта django
 poetry add drf-spectacular
  # Настройки coursework_6.settings
 
    INSTALLED_APPS = [
        ...
        'drf_spectacular', # включение автодокументации 
        ]
    REST_FRAMEWORK = {
    ...
    "DEFAULT_SCHEMA_CLASS": "drf_spectacular.olpenapi.AutoShema",
    }
    SPECTACULAR_SETTINGS ={
        "TITLE": "Курсовая работа №6 API",
        "DESCRIPTION": "Описание API",
        "VERSION": "0.0.1",
       }
 # Настройки coursework_6.urls
`  path('api/schema/', SpectacularAPIView.as_view(), name='schema') # urls c JSON `
`  path('api/schema/swagger-ui/', SpectacularSwaggerView.as_view(url_name='schema')) # графический интерфкейс  `