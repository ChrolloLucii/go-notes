# Go Notes - Сервис управления заметками

Микросервисное приложение для хранения и управления личными заметками.

##  Описание проекта

Проект представляет собой веб-приложение с микросервисной архитектурой для создания, редактирования, удаления и просмотра личных заметок пользователей.

##  Архитектура

Проект состоит из следующих компонентов:

- **API Gateway** (порт 8080) - маршрутизация запросов к микросервисам
- **Notes Service** (порт 8081) - CRUD операции с заметками
- **Auth Service** (порт 8082) - аутентификация и регистрация пользователей
- **Storage Service** (порт 8083) - взаимодействие с MongoDB
- **MongoDB** (порт 27017) - база данных
- **Prometheus** (порт 9090) - сбор метрик
- **Grafana** (порт 3000) - визуализация метрик

##  Структура проекта

```
go-notes/
├── api-gateway/          # API Gateway
│   ├── main.go
│   ├── go.mod
│   └── Dockerfile
├── services/
│   ├── notes/           # Микросервис заметок
│   │   ├── main.go
│   │   ├── go.mod
│   │   └── Dockerfile
│   ├── auth/            # Микросервис аутентификации
│   │   ├── main.go
│   │   ├── go.mod
│   │   └── Dockerfile
│   └── storage/         # Микросервис хранения данных
│       ├── main.go
│       ├── go.mod
│       └── Dockerfile
├── frontend/            # Веб-интерфейс
│   ├── index.html
│   ├── app.js
│   └── styles.css
├── monitoring/          # Конфигурация мониторинга
│   └── prometheus.yml
├── .github/
│   └── workflows/
│       └── ci.yml       # CI/CD Pipeline
├── docker-compose.yml
├── Makefile
└── README.md
```

##  Быстрый старт

### Требования

- Docker и Docker Compose
- Go 1.21+ (для локальной разработки)
- Make (опционально)

### Запуск проекта

1. **Клонируйте репозиторий:**
```bash
git clone https://github.com/ChrolloLucii/go-notes.git
cd go-notes
```

2. **Запустите все сервисы:**
```bash
make run
# или
docker-compose up -d
```

3. **Проверьте статус сервисов:**
```bash
make ps
# или
docker-compose ps
```

### Доступ к сервисам

- API Gateway: http://localhost:8080
- Frontend: откройте `frontend/index.html` в браузере
- Prometheus: http://localhost:9090
- Grafana: http://localhost:3000 (логин: admin, пароль: admin)

##  Команды Make

```bash
make build    # Собрать все Docker-контейнеры
make run      # Запустить все сервисы
make stop     # Остановить все сервисы
make clean    # Удалить контейнеры и volumes
make test     # Запустить тесты
make logs     # Показать логи всех сервисов
make ps       # Показать статус сервисов
```

## API Endpoints

### Auth Service
- `POST /api/auth/register` - Регистрация пользователя
- `POST /api/auth/login` - Авторизация пользователя

### Notes Service
- `GET /api/notes` - Получить все заметки
- `GET /api/notes/:id` - Получить заметку по ID
- `POST /api/notes` - Создать новую заметку
- `PUT /api/notes/:id` - Обновить заметку
- `DELETE /api/notes/:id` - Удалить заметку

## Технологии

- **Backend:** Go 1.21
- **Database:** MongoDB 7.0
- **Контейнеризация:** Docker, Docker Compose
- **Мониторинг:** Prometheus, Grafana
- **CI/CD:** GitHub Actions
- **Аутентификация:** JWT (planned)

## Разработка

### Локальный запуск микросервиса

```bash
cd services/notes
go run main.go
```

### Запуск тестов

```bash
make test
```

### Форматирование кода

```bash
gofmt -w .
```

## CI/CD Pipeline

При каждом push или pull request в ветки `dev` или `main` автоматически запускается:

1. Сборка всех микросервисов
2. Запуск unit-тестов
3. Проверка форматирования кода
4. Сборка Docker-образов
5. Тестирование Docker Compose конфигурации

## 👨‍💻 Автор

**Зарипов Ренат Александрович**  
ИПТИП, 5 семестр  
Дисциплина: Инструменты DevOps

## 📄 Лицензия

Проект создан в образовательных целях.

