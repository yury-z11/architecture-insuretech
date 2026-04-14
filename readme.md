# InsureTech архитектурный проект 🏗️
---
Агрегатор страховых продуктов для B2C и B2B
Цель  высокая доступность масштабирование отказоустойчивость и ОСАГО онлайн

Технологии
• Kubernetes PostgreSQL Kafka или NATS Redis Drawio GraphQL Locust Python
Ветки
• main как целевая
• Tasks для работы
Документация
• Task1 Task2 Task3 Task4 Task5

# Что внутри 📦
---
• Task1  технологическая архитектура to be с мультизонным и мультирегиональным дизайном RTO 45 мин RPO 15 мин
• Task2  автоскейлинг в Kubernetes через HPA и нагрузочное тестирование Locust
• Task3  событийные интеграции и Transactional Outbox
• Task4  ОСАГО онлайн сервис osago-aggregator и устойчивые вызовы
• Task5  GraphQL для client-info схема и примеры

# Структура проекта 🧭
---
```text
.
├─ Task1
│  ├─ README.md
│  └─ InsureTech_технологическая_архитектура_to-be.drawio.xml
├─ Task2
│  ├─ deployment.yaml
│  ├─ service.yaml
│  ├─ hpa.yaml
│  ├─ locustfile.py
│  └─ README.md
├─ Task3
│  ├─ risks_and_problems.md
│  ├─ README.md
│  └─ InsureTech_C4_сontainer-diagram_to-be_task3.drawio.xml
├─ Task4
│  ├─ README.md
│  └─ InsureTech_C4_сontainer-update-diagram.drawio.xml
├─ Task5
│  ├─ schema.graphql
│  └─ README.md
└─ pintr
   └─ докс и библиотеки фигур для drawio
```

# На Linux
---
• Установить Docker и Docker Compose
• Установить Python 3.11 и pip
• Установить kubectl и minikube при необходимости

Task2 запуск HPA
Windows
```powershell
minikube start
minikube addons enable metrics-server
kubectl apply -f Task2\deployment.yaml
kubectl apply -f Task2\service.yaml
kubectl apply -f Task2\hpa.yaml
minikube service scaletestapp --url
python -m pip install locust
locust -f Task2\locustfile.py --host http://127.0.0.1:30080
```

Linux
```bash
minikube start
minikube addons enable metrics-server
kubectl apply -f Task2/deployment.yaml
kubectl apply -f Task2/service.yaml
kubectl apply -f Task2/hpa.yaml
minikube service scaletestapp --url
python3 -m pip install locust
locust -f Task2/locustfile.py --host http://127.0.0.1:30080
```

Task5 GraphQL 
Файлы  Task5/schema.graphql и Task5/README.md
Можно выбирать только нужные поля и связи одним запросом
Пример
```graphql
query GetClient($id: ID!) {
  client(id: $id) {
    id
    name
    documents { id type number }
    relatives { id relationType name }
  }
}
```

# Диаграммы 
---
Файлы drawio находятся в Task1 Task3 Task4
