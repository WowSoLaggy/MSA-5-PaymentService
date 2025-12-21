# Таблица Тест Кейсов

## Интеграционные тесты

| Название | Тип | Компоненты | Предусловия |
|----------|-----|------------|-------------|
| **Блокировка суммы - Успешная** | Integration | Orchestration Service, Payment Service | Пользователь с достаточным балансом |
| **Блокировка суммы - Недостаточный баланс** | Integration | Orchestration Service, Payment Service | Пользователь с недостаточным балансом |
| **Блокировка суммы - Retry при временном сбое** | Integration | Orchestration Service, Payment Service | Временный сбой Payment Service при block_amount |
| **Разблокировка суммы - Компенсация** | Integration | Orchestration Service, Payment Service | Сумма заблокирована, требуется компенсация |
| **Проверка на мошенничество - Успешная** | Integration | Orchestration Service, Fraud Detection Service | Валидная транзакция |
| **Проверка на мошенничество - Обнаружено** | Integration | Orchestration Service, Fraud Detection Service | Мошенническая транзакция |
| **Проверка на мошенничество - Ручная проверка** | Integration | Orchestration Service, Fraud Detection Service | Транзакция требует ручной проверки |
| **Проверка на мошенничество - Timeout** | Integration | Orchestration Service, Fraud Detection Service | Fraud Detection Service не отвечает в течение timeout |
| **Проверка на мошенничество - Retry** | Integration | Orchestration Service, Fraud Detection Service | Временный сбой при send_fraud_check |
| **Выполнение платежа - Успешное** | Integration | Orchestration Service, Payment Service | Fraud проверка пройдена, сумма заблокирована |
| **Выполнение платежа - Ошибка** | Integration | Orchestration Service, Payment Service | Fraud проверка пройдена, но Payment Service отклонил транзакцию |
| **Выполнение платежа - Timeout** | Integration | Orchestration Service, Payment Service | Payment Service не отвечает при execute_payment |
| **Выполнение платежа - Retry** | Integration | Orchestration Service, Payment Service | Временный сбой при execute_payment |
| **Уведомление об успехе** | Integration | Orchestration Service, Notification Service | Платеж выполнен успешно |
| **Уведомление о неудаче** | Integration | Orchestration Service, Notification Service | Платеж отклонён |
| **Уведомление - Сервис недоступен** | Integration | Orchestration Service, Notification Service | Notification Service недоступен |
| **Идемпотентность запроса** | Integration | Orchestration Service, Payment Service | Повторный запрос с тем же transaction_id |
| **Circuit Breaker - Payment Service** | Integration | Orchestration Service, Payment Service | Payment Service недоступен, защита от каскадных сбоев |
| **Circuit Breaker - Fraud Detection Service** | Integration | Orchestration Service, Fraud Detection Service | Fraud Detection Service недоступен, защита от каскадных сбоев |
| **Восстановление состояния Saga** | Integration | Orchestration Service, Payment Service | Оркестратор упал во время обработки, восстановление состояния |

## End-to-End тесты

| Название | Тип | Компоненты | Предусловия |
|----------|-----|------------|-------------|
| **Happy Path - Успешный платеж** | E2E | Orchestration Service, Payment Service, Fraud Detection Service, Notification Service | Пользователь с достаточным балансом, валидные платежные данные |
| **Happy Path - Платеж с ручной проверкой (одобрен)** | E2E | Orchestration Service, Payment Service, Fraud Detection Service, Notification Service | Пользователь с достаточным балансом, транзакция требует ручной проверки, одобрена |
| **Happy Path - Платеж с ручной проверкой (timeout)** | E2E | Orchestration Service, Payment Service, Fraud Detection Service, Notification Service | Пользователь с достаточным балансом, cut-off-time истёк без ответа |
| **Fraud Detected - Автоматическая проверка** | E2E | Orchestration Service, Payment Service, Fraud Detection Service, Notification Service | Пользователь с достаточным балансом, мошенническая транзакция |
| **Fraud Detected - Ручная проверка отклонена** | E2E | Orchestration Service, Payment Service, Fraud Detection Service, Notification Service | Пользователь с достаточным балансом, транзакция отклонена при ручной проверке |
| **Payment Failure - Ошибка проведения платежа** | E2E | Orchestration Service, Payment Service, Fraud Detection Service, Notification Service | Fraud проверка пройдена, но Payment Service отклонил execute_payment |
| **Недостаточный баланс - Полный flow** | E2E | Orchestration Service, Payment Service, Notification Service | Пользователь с недостаточным балансом |
| **SLA - Производительность** | E2E | Orchestration Service, Payment Service, Fraud Detection Service, Notification Service | Все сервисы работают в штатном режиме, проверка 5 сек в 90% случаев |
