# 🐈‍⬛ Kittygram 🐈‍⬛

## Tech Stack

- **Docker/Docker Compose**
- **Nginx**
- **PostgreSQL**
- **Terraform (с помощью Yandex.Cloud)**
- **GitHub Actions**
- **Python/Django (backend)**
- **React (frontend)**

## Структура проекта

```
kittygram-final
├── backend/                   # Django
├── frontend/                  # React
├── nginx/                     # Nginx
├── infra/                     # Terraform
├── .github/workflows/         # CI/CD
└── docker-compose.production.yml
```

## Установка и запуск

1. Запустить контейнеры:

```bash
docker-compose -f docker-compose.production.yml up -d
```

2. Миграция:

```bash
docker-compose -f docker-compose.production.yml exec -T kitty_backend python manage.py migrate
docker-compose -f docker-compose.production.yml exec -T kitty_backend python manage.py collectstatic --noinput
```

## Развёртывание в Yandex.Cloud

1. Инициализация через Terraform:

```bash
cd infra/
terraform init
```

2. Применить конфигурацию:

```bash
terraform apply -auto-approve
```

После завершения работы, Terraform выдаст адрес и название ВМ.

## Автоматизация через GitHub Actions

Используется:

- Линтер Django (`flake8`)
- Тесты фронтэнда (`npm test`)
- Сборка образов Docker
- Развёртывание сервера
- Автоматические тесты
- Оповещение о готовности в Телеграм

## Необходимые GitHub Secrets

| Secret |  Описание   |
|--------|-------------|
| `DOCKER_USERNAME`, `DOCKER_PASSWORD` | DockerHub |
| `SSH_PRIVATE_KEY`, `SERVER_HOST`, `SERVER_USER` | Для развёртывания на удалённом сервере |
| `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`, `DB_HOST`, `DB_PORT` | Настройки БД |
| `YC_CLOUD_ID`, `YC_FOLDER_ID`, `YC_KEY_JSON`, `SSH_KEY` | Yandex.Cloud |
| `YC_ACCESS_KEY`, `YC_SECRET_KEY` | Terraform backend access |
| `TELEGRAM_TOKEN`, `TELEGRAM_TO` | Telegram notification |

## 🔗 URLs после развёртывания

- Основная: `http://<EXTERNAL_IP>/`
- Админская панель Django: `http://<EXTERNAL_IP>/admin/`
