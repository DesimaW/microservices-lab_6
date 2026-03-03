# SE4010 Microservices Lab (Docker + API Gateway) 

## System Overview
This project implements a microservices architecture with:

- Item Service (Port 8081)
- Order Service (Port 8082)
- Payment Service (Port 8083)
- API Gateway (Port 8080)

All services are containerized using Docker and orchestrated with Docker Compose.

## How to Run

### Build Services
mvn clean package (inside each service)

### Run with Docker
docker-compose build
docker-compose up

### Stop
docker-compose down

## API Endpoints

GET /items  
POST /items  
GET /orders  
POST /orders  
GET /payments  
POST /payments/process  

All requests must be accessed through:
http://localhost:8080

## Run (Docker Compose)

From the project root:

```bash
docker-compose build
docker-compose up
```

To run detached:

```bash
docker-compose up -d
```

Stop everything:

```bash
docker-compose down
```

## Test through the API Gateway (port 8080)

### Item Service
- `GET http://localhost:8080/items`
- `POST http://localhost:8080/items`

Body:

```json
{ "name": "Headphones" }
```

- `GET http://localhost:8080/items/1`

### Order Service
- `GET http://localhost:8080/orders`
- `POST http://localhost:8080/orders`

Body:

```json
{ "item": "Laptop", "quantity": 2, "customerId": "C001" }
```

- `GET http://localhost:8080/orders/1`

### Payment Service
- `GET http://localhost:8080/payments`
- `POST http://localhost:8080/payments/process`

Body:

```json
{ "orderId": 1, "amount": 1299.99, "method": "CARD" }
```

- `GET http://localhost:8080/payments/1`

## Notes
- All data is persisted in MongoDB Atlas (database `Lab05`).
- Services do not call each other directly; routing is done via the API Gateway.
