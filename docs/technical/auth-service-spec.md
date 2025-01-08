# Auth Service Спецификация

## 1. Общее описание
Auth Service отвечает за аутентификацию и авторизацию пользователей в системе Network Capital App. Сервис реализует безопасное управление доступом и интегрируется с другими сервисами системы.

## 2. Функциональные требования

### 2.1 Аутентификация
- Регистрация новых пользователей
- Вход по email/password
- OAuth 2.0 интеграции (Google, LinkedIn)
- Двухфакторная аутентификация (2FA)
- Восстановление пароля
- Управление сессиями

### 2.2 Авторизация
- Role-Based Access Control (RBAC)
- Управление ролями и правами
- Проверка прав доступа
- Делегирование прав
- Аудит действий

### 2.3 Токены и сессии
- Генерация JWT токенов
- Управление refresh токенами
- Контроль активных сессий
- Принудительный выход
- Автоматическое продление сессий

## 3. Технические характеристики

### 3.1 API Endpoints
```yaml
POST /auth/register
  - Регистрация нового пользователя
  - Request: {email, password, name}
  - Response: {userId, token}

POST /auth/login
  - Аутентификация пользователя
  - Request: {email, password}
  - Response: {token, refreshToken}

POST /auth/refresh
  - Обновление токена
  - Request: {refreshToken}
  - Response: {newToken}

POST /auth/logout
  - Выход из системы
  - Request: {token}
  - Response: {success}

GET /auth/me
  - Получение информации о текущем пользователе
  - Response: {userId, email, roles}
```

### 3.2 Модель данных
```sql
-- Users
CREATE TABLE users (
    id UUID PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    name VARCHAR(255),
    created_at TIMESTAMP,
    updated_at TIMESTAMP
);

-- Roles
CREATE TABLE roles (
    id UUID PRIMARY KEY,
    name VARCHAR(50) UNIQUE NOT NULL,
    description TEXT
);

-- User Roles
CREATE TABLE user_roles (
    user_id UUID REFERENCES users(id),
    role_id UUID REFERENCES roles(id),
    PRIMARY KEY (user_id, role_id)
);

-- Sessions
CREATE TABLE sessions (
    id UUID PRIMARY KEY,
    user_id UUID REFERENCES users(id),
    refresh_token VARCHAR(255),
    expires_at TIMESTAMP,
    created_at TIMESTAMP
);
```

## 4. Безопасность

### 4.1 Хранение данных
- Хеширование паролей (Argon2)
- Шифрование чувствительных данных
- Безопасное хранение токенов

### 4.2 Защита от атак
- Rate limiting
- Защита от брутфорс атак
- CSRF токены
- XSS защита
- SQL инъекции

## 5. Интеграции

### 5.1 Внутренние сервисы
- Contact Service
- Notification Service
- Analytics Service

### 5.2 Внешние сервисы
- Google OAuth
- LinkedIn OAuth
- SMS-шлюз для 2FA

## 6. Метрики и мониторинг

### 6.1 Основные метрики
- Количество активных сессий
- Время ответа API
- Количество неудачных попыток входа
- Использование refresh токенов

### 6.2 Алерты
- Множественные неудачные попытки входа
- Аномальная активность
- Ошибки сервиса
- Истечение SSL сертификатов

## 7. Требования к развертыванию

### 7.1 Окружение
- Docker контейнер
- PostgreSQL 14+
- Redis для кэширования
- Nginx reverse proxy

### 7.2 Масштабирование
- Горизонтальное масштабирование
- Репликация базы данных
- Распределенное кэширование
- Балансировка нагрузки 