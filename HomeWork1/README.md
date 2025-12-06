# Order Service Microservice

## 📁 Проектная структура

```
HomeWorks/
├── HomeWork1/
│   ├── contracts/                          # Контракты между сервисами
│   │   ├── inventory_service_contracts.md
│   │   ├── order_service_contracts.md
│   │   └── payment_service_contracts.md
│   │
│   ├── inventory/                          # Сервис инвентаризации
│   │   └── cmd/
│   │       └── main.go
│   │
│   ├── order/                              # Сервис заказов (основной)
│   │   └── cmd/
│   │       └── main.go
│   │
│   ├── payment/                            # Сервис платежей
│   │   └── cmd/
│   │       └── main.go
│   │
│   └── shared/                             # Общие ресурсы
│       └── api/
│           └── order/
│               └── v1/
│                   ├── components/         # Переиспользуемые компоненты OpenAPI
│                   │   ├── enums/         # Перечисления
│                   │   │   ├── order_status.yaml
│                   │   │   └── payment_method.yaml
│                   │   │
│                   │   └── errors/        # Стандартные ошибки API
│                   │       ├── bad_gateway_error.yaml
│                   │       ├── bad_request_error.yaml
│                   │       ├── conflict_error.yaml
│                   │       ├── forbidden_error.yaml
│                   │       ├── generic_error.yaml
│                   │       ├── internal_server_error.yaml
│                   │       ├── not_found_error.yaml
│                   │       ├── rate_limit_error.yaml
│                   │       ├── service_unavailable_error.yaml
│                   │       ├── unauthorized_error.yaml
│                   │       └── validation_error.yaml
│                   │
│                   ├── create_order_request.yaml
│                   ├── create_order_response.yaml
│                   ├── get_order_response.yaml
│                   ├── order_dto.yaml
│                   ├── pay_order_request.yaml
│                   └── pay_order_response.yaml
│                   │
│                   ├── params/             # Параметры пути
│                   │   └── order_uuid.yaml
│                   │
│                   ├── paths/              # Определения эндпоинтов
│                   │   ├── order_by_uuid.yaml
│                   │   ├── order_cancel.yaml
│                   │   ├── order_pay.yaml
│                   │   └── orders.yaml
│                   │
│                   └── order.openapi.yaml  # Основной файл спецификации
│
├── MW.hw.md                                # Методические указания
├── README.md                               # Основная документация
└── Taskfile.yml                           # Файл задач для автоматизации
```

## 🏗️ Архитектура

Проект реализует **микросервисную архитектуру** с тремя основными сервисами:

### 1. **Order Service** (`order/`)
Основной сервис управления заказами. Отвечает за:
- Создание заказов
- Получение информации о заказах
- Отмену заказов
- Интеграцию с платежной системой

### 2. **Inventory Service** (`inventory/`)
Сервис управления инвентарем. Отвечает за:
- Учет товаров на складе
- Проверку доступности товаров
- Резервирование товаров при оформлении заказа

### 3. **Payment Service** (`payment/`)
Сервис обработки платежей. Отвечает за:
- Обработку платежных операций
- Интеграцию с платежными шлюзами
- Ведение истории транзакций

### СКОРО ПОЯВЯТСЯ ФАЙЛЫ pkg НО ОНИ БУДУТ ПРОИГНОРИРОВАНЫ ГИТОМ

### Компоненты (`components/`)
- **Enums** – перечисления (статусы заказов, методы оплаты)
- **Errors** – стандартизированные ошибки API (11 типов ошибок)

### Модели данных
- `order_dto.yaml` – основная модель заказа
- `create_order_request.yaml` – запрос на создание заказа
- `create_order_response.yaml` – ответ при создании заказа
- `get_order_response.yaml` – ответ при получении заказа
- `pay_order_request.yaml` – запрос на оплату
- `pay_order_response.yaml` – ответ об оплате

## 🛠️ Технологический стек

- **Язык**: Go (Golang)
- **Документация API**: OpenAPI 3.0 (YAML)
- **Оркестрация**: Taskfile (автоматизация задач)
- **Архитектура**: Микросервисы
- **Коммуникация**: REST API
- **Коммуникация**: gRPC

## 🚀 Запуск проекта

### Предварительные требования
- Go 1.19+
- Установленный Taskfile runner

## 🤝 Взаимодействие сервисов

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Клиент    │────▶│ Order Service│────▶│Inventory Srv│
└─────────────┘     └─────────────┘     └─────────────┘
                          │                    │
                          ▼                    ▼
                    ┌─────────────┐     ┌─────────────┐
                    │Payment Srv  │◀────┤   База      │
                    └─────────────┘     │   данных    │
                                         └─────────────┘
```

## 📝 Контракты между сервисами

Документация по взаимодействию сервисов находится в папке `contracts/`:
- `order_service_contracts.md` – контракты Order Service
- `inventory_service_contracts.md` – контракты Inventory Service
- `payment_service_contracts.md` – контракты Payment Service
