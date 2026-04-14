# Task4

- Новые компоненты: `osago-aggregator` (интеграция с ОСАГО)
- Паттерны отказоустойчивости: Rate Limiting, Circuit Breaker, Retry, Timeout
- API взаимодействия:
  - core-app ⇄ osago-aggregator: REST
  - osago-aggregator ⇄ страховые: REST (polling)
  - web ⇄ core-app: REST/WebSocket для прогрессивной выдачи предложений

## Решения

- osago-aggregator хранит состояния заявок и ответы страховых в собственной БД `OSAGO DB`
- Идемпотентность по заявке через idempotency key
- Для каждого провайдера: per-provider rate limiting и circuit breaker
- Повторные попытки с экспоненциальной задержкой и джиттером, таймауты на вызовах
- core-app получает частичные результаты через поток (SSE/WebSocket)
