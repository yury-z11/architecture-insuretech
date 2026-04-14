# Task2

Динамическое масштабирование тестового приложения в Minikube

## Шаги запуска

1. Запустить Minikube
   
   minikube start

2. Включить metrics server
   
   minikube addons enable metrics-server

3. Применить манифесты Deployment и Service
   
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml

4. Получить URL сервиса для нагрузки
   
   minikube service scaletestapp --url

5. Применить HPA по памяти
   
   kubectl apply -f hpa.yaml

6. Сгенерировать нагрузку с помощью Locust
   
   Установить Locust и создать файл locustfile.py со сценарием из задания. Запустить:
   
   locust

   Открыть в браузере адрес http://localhost:8089 и задать количество пользователей и скорость.

7. Наблюдение
   
   minikube dashboard

   На графиках и в HPA должно быть видно увеличение числа реплик при росте утилизации памяти до целевого уровня восемьдесят процентов.

## Файлы

* deployment.yaml — развёртывание приложения с лимитом памяти 30Mi
* service.yaml — сервис на порту 8080
* hpa.yaml — HPA по памяти 80 процентов, от 1 до 10 реплик

