# ML gRPC Service

Этот проект представляет собой реализацию gRPC-сервиса для обслуживания ML-модели (логистическая регрессия на датасете Iris). Сервис упакован в Docker-контейнер и предоставляет API для проверки состояния и получения предсказаний.

## Структура репозитория

```text
ml_grpc_service/
├── protos/
│   └── model.proto
├── server/
│   └── server.py
├── client/
│   └── client.py
├── models/
│   └── model.pkl
├── requirements.txt
├── Dockerfile
└── README.md

## Описание проекта

Проект содержит:

*   **Protos**: Описание gRPC контракта (`model.proto`) с методами `Health` и `Predict`.
*   **Server**: Реализация сервера на Python, который загружает модель и обрабатывает запросы.
*   **Client**: Клиентский скрипт для проверки работоспособности сервиса.
*   **Docker**: Конфигурация для сборки и запуска сервиса в изолированном контейнере.

## Команды сборки и запуска

Для запуска сервиса необходимо наличие установленного Docker.

### 1\. Сборка Docker-образа

```
docker build -t grpc-ml-service .
```

### 2\. Запуск контейнера

```
docker run -p 50051:50051 grpc-ml-service
```

## Примеры вызовов

После запуска контейнера можно проверить работоспособность сервиса следующими способами.

### Проверка Health (через grpcurl)

Команда для проверки статуса сервиса:

```
grpcurl -proto protos/model.proto -plaintext localhost:50051 mlservice.v1.PredictionService/Health
```

### Получение предсказания (через Python-клиент)

Команда для отправки данных (параметры цветка Iris) и получения предсказания:

```
python -m client.client
```

## Скриншоты работы

### 1\. Успешный запуск контейнера и проверка Health

<img width="963" height="97" alt="Screenshot 2025-12-06 at 19 50 42" src="https://github.com/user-attachments/assets/14ac9fa2-cf9b-43de-b78b-d6b58fcb8ac8" />

### 2\. Работа Python-клиента (Predict)

<img width="766" height="81" alt="Screenshot 2025-12-06 at 19 47 15" src="https://github.com/user-attachments/assets/7117f1fd-c35a-4579-80d5-9365063279be" />

