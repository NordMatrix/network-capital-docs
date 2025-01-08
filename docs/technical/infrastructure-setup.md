# Инфраструктура проекта

## 1. Репозитории

### 1.1 Backend сервисы
- `network-capital-auth` - Сервис аутентификации
- `network-capital-contacts` - Сервис управления контактами
- `network-capital-api-gateway` - API Gateway

### 1.2 Frontend приложения
- `network-capital-web` - Веб-приложение
- `network-capital-mobile` - Мобильное приложение

## 2. Окружения

### 2.1 Development
- Локальное окружение (Docker Compose)
- Dev сервер
- CI/CD пайплайны

### 2.2 Staging
- Тестовая среда
- Интеграционное тестирование
- Нагрузочное тестирование

### 2.3 Production
- Kubernetes кластер
- Мониторинг
- Логирование
- Бэкапы

## 3. DevOps инструменты

### 3.1 CI/CD
- GitHub Actions для сборки и тестирования
- ArgoCD для деплоя в Kubernetes
- SonarQube для анализа кода

### 3.2 Мониторинг
- Prometheus + Grafana
- ELK Stack
- Sentry для ошибок

### 3.3 Безопасность
- Vault для секретов
- Cert-manager для SSL
- Network Policies

## 4. Базы данных

### 4.1 Основные БД
- PostgreSQL для пользовательских данных
- Redis для кэширования
- Neo4j для графа связей

### 4.2 Резервное копирование
- Ежедневные бэкапы
- Репликация данных
- Процедуры восстановления

## 5. Сетевая инфраструктура

### 5.1 Внутренняя сеть
- Service Mesh (Istio)
- Внутренний DNS
- Load Balancing

### 5.2 Внешний доступ
- Ingress контроллер
- CDN
- DDoS защита 