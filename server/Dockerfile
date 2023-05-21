# Базовый image
FROM python:3.10-alpine

# Создание каталога /app и назначение его как рабочей директории
WORKDIR /app

# Добавление файла с текстом "Hello world"
RUN echo "Hello world" > hello.html

# Обеспечение запуска web-сервера от имени пользователя с uid 1001
USER 1001

# Команда запуска web-сервера
CMD ["python3", "-m", "http.server", "8000"]