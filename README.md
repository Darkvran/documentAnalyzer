# Тестовое задание

Реализовать веб-приложение. В качестве интерфейса сделать страницу с формой для загрузки текстового файла, после загрузки и обработки файла отображается таблица с 50 словами с колонками:
- слово
- tf, сколько раз это слово встречается в тексте
- idf, обратная частота документа
### Вывод упорядочить по уменьшению idf.
---
## Структура проекта
### server.py
Содержит в себе экземляр Flask приложение и эндпоинты.

### handling.py
Содержит в себе объявление функции обработки текстовых файлов и экземляр базы данных.

### data.py
Содержит в себе объявление класса базы данных.

### metric.py
Содержит в себе объявление класса MetricsCollector, отвечающего за сбор и сохранение метрик.

### nginx/default.conf
Содержит в себе конфигурацию nginx.

### Dockerfile 
Содержит в себе инструкции по контеинеризации приложения.

### docker-compose.yml
Содержит в себе инструкции по оркестровке приложения.

### .env
Содержит в себе все конфигурируемые параметры:
1. FLASK_SECRET_KEY
Секретный ключ Flask приложения
2. FLASK_PORT
Порт, по которому будет работать Flask приложение.
3. FLASK_HOST
IP-адрес, по которому будет работать Flask приложение.
4. FLASK_DEBUG
Флаг, отвечающий за debug-mode
5. MONGODB_URI
Адрес mongodb.
6. MONGODB_DB_NAME
Наименование mongodb.
7. APP_VERSION
Текущая версия приложения
8. APP_ALLOWED_EXTENSIONS
Множество допустимых расширений. Все иные расширения не могут быть загружены и обработаны.
---
## Change-log
### 1.0.0
- Переход от Sqlite к MongoDB
- Добавление API:
1. Добавление логики метрик. Создание класса MetricsCollector и эндпоинта /metrics
2. Добавление проверки статуса приложения - эндпоинт /status.
3. Добавление проверки текущей версии приложения - эндпоинт /version.
- files_processed - необходима для отслеживания количества файлов, обработанных приложением.
- min_time_processed, avg_time_processed, max_time_processed - отслеживание нагрузки на приложение, сколько уходит времени на обработку файлов.
- latest_file_processed_timestamp - отслеживание времени обработки последнего файла.
## Инструкция по установке
### Standart 
1. git clone https://github.com/Darkvran/document_analyzer
2. cd document_analyzer
3. python -m venv venv
4. venv\Scripts\activate.bat
5. pip install -r requirements.txt

Для запуска использовать:

flask --app server run
(!) Для запуска необходимо находиться в директории с server.py

### Docker-images
1. git clone https://github.com/Darkvran/document_analyzer
2. cd document_analyzer
3. docker compose up -d --build
