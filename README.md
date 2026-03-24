<div align="center">

# 🌟 free talks

### Reddit Clone на Go и React

</div>

## 🛠 Tech Stack

### Backend
[![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)](https://golang.org)
[![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)](https://jwt.io)
[![bcrypt](https://img.shields.io/badge/bcrypt-525252?style=for-the-badge&logo=security&logoColor=white)](https://pkg.go.dev/golang.org/x/crypto/bcrypt)

### Frontend
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org)
[![Redux](https://img.shields.io/badge/Redux-764ABC?style=for-the-badge&logo=redux&logoColor=white)](https://redux.js.org)
[![Styled Components](https://img.shields.io/badge/styled--components-DB7093?style=for-the-badge&logo=styled-components&logoColor=white)](https://styled-components.com)
[![React Router](https://img.shields.io/badge/React_Router-CA4245?style=for-the-badge&logo=react-router&logoColor=white)](https://reactrouter.com)

### Observability Stack
[![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com)
[![VictoriaMetrics](https://img.shields.io/badge/VictoriaMetrics-621773?style=for-the-badge&logo=victoriametrics&logoColor=white)](https://victoriametrics.com)
[![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)](https://grafana.com)
[![Promtail](https://img.shields.io/badge/Promtail-F29E1F?style=for-the-badge&logo=grafana&logoColor=white)](https://grafana.com/oss/promtail/)
[![Node Exporter](https://img.shields.io/badge/Node_Exporter-99A3A4?style=for-the-badge&logo=prometheus&logoColor=white)](https://prometheus.io/docs/guides/node-exporter/)

## 📋 О проекте

**asperitas** — это полнофункциональное веб-приложение, реализующее функциональность Reddit. Платформа позволяет пользователям создавать посты, оставлять комментарии, голосовать за контент и фильтровать материалы по категориям. Проект демонстрирует современный подход к разработке веб-приложений с использованием микросервисной архитектуры, контейнеризации и комплексного мониторинга.

---

## ✨ Возможности

### 👥 Пользовательская часть
- Регистрация и аутентификация с JWT-токенами
- Создание постов двух типов: ссылки и текстовые
- Голосование за посты (upvote/downvote)
- Комментирование постов
- Просмотр профиля пользователя
- Фильтрация по категориям

### ⚙️ Технические особенности
- SPA-архитектура на React с маршрутизацией
- RESTful API на Go с чистой архитектурой
- Контейнеризация всех сервисов через Docker
- Полный стек наблюдаемости (метрики, логи, дашборды)
- Адаптивный интерфейс с поддержкой тёмной темы

---

## 🏗️ Архитектура проекта

```
asperitas/
├── cmd/                      # Утилиты командной строки
│   └── ab/                   # Инструмент нагрузочного тестирования
├── internal/                 # Внутренние пакеты
│   ├── handler/              # HTTP-обработчики
│   ├── middleware/           # Промежуточные слои (аутентификация)
│   ├── post/                 # Модели и логика постов
│   └── user/                 # Модели и логика пользователей
├── static/                   # Статические файлы фронтенда
├── docker-compose.yaml       # Оркестрация сервисов
├── promtail-config.yaml      # Конфигурация сбора логов
├── vmagent-config.yml        # Конфигурация сбора метрик
├── setup.sh                  # Скрипт развертывания
└── OBSERVABILITY_STACK.md    # Документация по мониторингу
```

---

## 🚀 Быстрый старт

### Предварительные требования
- Docker и Docker Compose
- Go 1.25+ (для разработки)
- Git

### 1️⃣ Запуск стека наблюдаемости

```bash
chmod +x setup.sh
./setup.sh
```

Сервисы будут доступны по адресам:

| Сервис | URL | Назначение |
|--------|-----|------------|
| Grafana | http://localhost:3000 | Визуализация (admin/admin) |
| Victoria Metrics | http://localhost:8428 | Хранилище метрик |
| Victoria Logs | http://localhost:9428 | Хранилище логов |
| Node Exporter | http://localhost:9100 | Метрики хоста |

### 2️⃣ Запуск приложения

```bash
go run main.go
```

После запуска приложение будет доступно по адресу: http://localhost:8080

### 3️⃣ Остановка

```bash
# Остановка Go-приложения (Ctrl+C)

# Остановка стека наблюдаемости
docker-compose down

# Полное удаление всех данных
docker-compose down -v
```

---

## 📡 API Эндпоинты

### Публичные маршруты

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `POST` | `/api/register` | Регистрация |
| `POST` | `/api/login` | Вход |
| `GET` | `/api/user/{login}` | Посты пользователя |
| `GET` | `/api/posts` | Все посты |
| `GET` | `/api/posts/{category}` | Посты по категории |
| `GET` | `/api/post/{id}` | Детальная информация |

### Защищённые маршруты (требуется JWT)

| Метод | Эндпоинт | Описание |
|-------|----------|----------|
| `POST` | `/api/posts` | Создание поста |
| `POST` | `/api/post/{id}` | Добавление комментария |
| `DELETE` | `/api/post/{id}/{comment}` | Удаление комментария |
| `GET` | `/api/post/{id}/upvote` | Голос "за" |
| `GET` | `/api/post/{id}/downvote` | Голос "против" |
| `GET` | `/api/post/{id}/unvote` | Сброс голоса |
| `DELETE` | `/api/post/{id}` | Удаление поста |

---

## 🧪 Тестирование

Для нагрузочного тестирования используется встроенная утилита:

```bash
# Сборка
go build -o ab cmd/ab/main.go

# Запуск теста
./ab -c 10 -n 1000 http://localhost:8080/api/posts

# Параметры:
#   -c  количество одновременных запросов
#   -n  общее количество запросов
#   -k  использовать HTTP Keep-Alive
```

---

## 📊 Мониторинг

### Метрики
- HTTP-запросы (количество, статусы, длительность)
- Runtime-метрики Go (GC, горутины, память)
- Системные метрики (CPU, память, диски)

Эндпоинт для сбора метрик: `/metrics`

### Логи
Приложение использует структурированное логирование в JSON-формате. Логи агрегируются через Promtail и сохраняются в Victoria Logs с возможностью поиска по LogQL.

### Дашборды
Предварительно настроенные дашборды в Grafana позволяют отслеживать:
- Общую производительность приложения
- Ошибки и исключения
- Активность пользователей
- Состояние инфраструктуры

---

## 🗄️ Модели данных

### Пользователь

```go
type User struct {
    ID       string  // UUID
    Username string  // уникальное имя
    password string  // bcrypt-хеш
}
```

### Пост

```go
type Post struct {
    ID               string     // UUID
    Title            string     // заголовок
    URL              string     // ссылка (для link)
    Text             string     // текст (для text)
    Type             string     // link / text
    Category         string     // категория
    Author           *Author    // автор
    Score            int        // рейтинг
    Votes            []*Vote    // голоса
    Comments         []*Comment // комментарии
    Created          time.Time  // дата создания
    Views            int        // просмотры
    UpvotePercentage int        // % положительных
}
```

### Комментарий

```go
type Comment struct {
    ID      string    // UUID
    Author  *Author   // автор
    Body    string    // текст
    Created time.Time // дата
}
```

---

## 🔒 Безопасность

- **JWT-токены** — срок действия 24 часа
- **bcrypt** — хеширование паролей (cost factor 10)
- **Валидация** — входных данных на клиенте и сервере
- **CORS** — настроен для безопасного взаимодействия

---

## 📦 Зависимости

### Backend
| Пакет | Назначение |
|-------|------------|
| `golang.org/x/crypto/bcrypt` | Хеширование паролей |
| `github.com/golang-jwt/jwt/v5` | JWT-токены |
| `github.com/google/uuid` | Генерация идентификаторов |

### Frontend
| Пакет | Назначение |
|-------|------------|
| `react` + `react-dom` | UI-библиотека |
| `redux` + `react-redux` | Управление состоянием |
| `react-router-dom` | Маршрутизация |
| `styled-components` | Стилизация |
| `react-markdown` | Markdown-рендеринг |

---

## 📌 Известные ограничения

- Хранилище in-memory — данные не сохраняются между перезапусками
- Отсутствует пагинация — все посты загружаются сразу
- Нет поиска по контенту
- Редактирование постов и комментариев не реализовано

---

## 📄 Лицензия

Проект разработан в образовательных целях и не предназначен для промышленного использования без доработок.

---

## 🙏 Благодарности

- [React](https://reactjs.org) — за удобный UI-фреймворк
- [Go](https://golang.org) — за производительность и простоту
- [VictoriaMetrics](https://victoriametrics.com) — за эффективное хранение метрик
- [Grafana](https://grafana.com) — за отличную визуализацию
