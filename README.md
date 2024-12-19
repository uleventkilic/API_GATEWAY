# Microservices-Based Payment System with RabbitMQ

This project is a microservices-based system designed to handle user management, order processing, and payment workflows using **RabbitMQ** as a message broker for communication between services. Each microservice is independent and includes its own **Swagger** documentation.

---

## Project Structure

```plaintext
.
├── api-gateway/                  # API Gateway Service
│   ├── app.js                    # API Gateway Logic
│   ├── package.json              # API Gateway Dependencies
│   └── Dockerfile                # API Gateway Dockerfile
│
├── services/
│   ├── user-service/             # User Service
│   │   ├── app.js
│   │   ├── package.json
│   │   └── Dockerfile
│   ├── order-service/            # Order Service
│   │   ├── app.js
│   │   ├── package.json
│   │   └── Dockerfile
│   ├── payment-service/          # Payment Service
│   │   ├── app.js
│   │   ├── package.json
│   │   └── Dockerfile
│
├── message-queue/                # RabbitMQ Message Consumers
│   ├── payment-processor.js      # Processes payments
│   ├── notification-service.js   # Sends notifications
│   └── Dockerfile                # Shared Dockerfile for message queues
│
└── docker-compose.yml            # Multi-container Docker setup
```

## YouTube Video
For a detailed explanation and code walkthrough of this project, watch the following YouTube video:

[https://youtu.be/vhdNQSE2iBQ]

---

## Technologies Used

- **Node.js**: Server-side runtime for all services
- **Express.js**: API framework for creating RESTful endpoints
- **RabbitMQ**: Message broker for asynchronous communication
- **Docker and Docker Compose**: Containerized deployment
- **Swagger**: API documentation for each microservice
- **AMQP Library**: RabbitMQ client for Node.js

---

## Running the Project with Docker

### Prerequisites
Ensure Docker and Docker Compose are installed on your system.

### Steps

1. **Start Services**
   Run the following command to build and start all services:
   ```bash
   docker-compose up --build
   ```

2. **Access Services**

   | Service            | URL                       |
   |--------------------|---------------------------|
   | API Gateway        | http://localhost:3000     |
   | User Service       | http://localhost:3001     |
   | Order Service      | http://localhost:3002     |
   | Payment Service    | http://localhost:3003     |
   | RabbitMQ Management| http://localhost:15672    |

---

## Swagger API Documentation

Each service includes its own Swagger UI for API documentation:

| Service          | Swagger URL                  |
|------------------|------------------------------|
| API Gateway      | http://localhost:3000/api-docs |
| User Service     | http://localhost:3001/api-docs |
| Order Service    | http://localhost:3002/api-docs |
| Payment Service  | http://localhost:3003/api-docs |

---

## Microservices Overview

### 1. API Gateway
Acts as the single entry point for all services. Routes incoming requests to the appropriate microservice.

#### Endpoints:
| Method | Route           | Description               |
|--------|-----------------|---------------------------|
| GET    | /api/users      | Fetch list of users       |
| GET    | /api/orders     | Fetch list of orders      |
| POST   | /api/payments   | Initiate a new payment process |

### 2. User Service
Handles user-related operations.

#### Endpoints:
| Method | Route           | Description         |
|--------|-----------------|---------------------|
| GET    | /users          | Fetch a list of users |

### 3. Order Service
Manages order information.

#### Endpoints:
| Method | Route           | Description         |
|--------|-----------------|---------------------|
| GET    | /orders         | Fetch a list of orders |

### 4. Payment Service
Processes payments and sends payment messages to RabbitMQ.

#### Endpoints:
| Method | Route           | Description                         |
|--------|-----------------|-------------------------------------|
| POST   | /payments       | Sends payment info to RabbitMQ      |

### 5. RabbitMQ Queue Processors
- **Payment Processor**: Consumes payment messages and processes them.
- **Notification Service**: Sends notifications to users after payment is processed.

---

## RabbitMQ Management

You can monitor queues and messages in RabbitMQ using the Management UI:

- **URL**: http://localhost:15672
- **Username**: guest
- **Password**: guest

---

## Sample API Requests

### Create a Payment
**Endpoint**: `POST /api/payments` (API Gateway)

**Request Body:**
```json
{
  "user": "ali@gmail.com",
  "paymentType": "credit",
  "cardNo": "1234-5678-9012-3456"
}
```

**Response:**
```json
{
  "status": "Payment processed",
  "user": "ali@gmail.com",
  "paymentType": "credit",
  "cardNo": "1234-5678-9012-3456"
}
```

---

## Troubleshooting

### Common Issues and Solutions

#### Docker Container Connection Errors

- **Issue**: Errors encountered in communication between services.
- **Solution**: Checked port definitions in the `docker-compose.yml` file and added correct network configurations.

#### RabbitMQ Management Panel Access Error

- **Issue**: Received "Connection Refused" error when connecting to RabbitMQ.
- **Solution**: Inspected Docker logs for the RabbitMQ service and fixed missing configurations.

#### API Gateway Routing Errors

- **Issue**: API Gateway failed to route requests to the correct services.
- **Solution**: Fixed route definitions in `app.js` and tested through Swagger documentation.

### Logs

If a service is not running, check its logs using:
```bash
docker logs <container_name>
```

### RabbitMQ Issues
Ensure RabbitMQ is healthy using the Management UI.
