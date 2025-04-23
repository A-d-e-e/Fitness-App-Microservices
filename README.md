# Fitness App Microservices

> A full‑stack fitness tracking application built with Spring Boot microservices, React frontend, and AI‑powered recommendations.

![Architecture Diagram](docs/architecture.png)

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Tech Stack](#tech-stack)
4. [Prerequisites](#prerequisites)
5. [Getting Started](#getting-started)
   - [Clone Repository](#clone-repository)
   - [Configuration](#configuration)
   - [Running Services](#running-services)
6. [Microservice Modules](#microservice-modules)
7. [API Endpoints](#api-endpoints)
8. [Frontend Usage](#frontend-usage)
9. [Contributing](#contributing)
10. [License](#license)

---

## Project Overview
This project demonstrates how to build a resilient, scalable fitness tracking platform using a microservices architecture. Key capabilities include:
- **User Management** with secure authentication/authorization via Keycloak (OAuth2/PKCE).
- **Activity Tracking** storing workouts and health metrics in MongoDB.
- **AI Recommendations** powered by Google Gemini to deliver personalized fitness tips.
- **Event‑Driven Communication** using RabbitMQ for decoupled, asynchronous processing.
- **Service Discovery & Config** via Spring Cloud Eureka and Config Server.
- **API Gateway** for a unified entry point and routing.
- **React Frontend** with real‑time data visualization and forms.

## Features
- Secure user signup/login, profile management
- Create, read, update, delete fitness activities
- Real‑time AI‑powered suggestions after each activity
- Asynchronous messaging for high throughput
- Centralized configuration and dynamic service discovery
- Responsive React UI with OAuth2/PKCE flow

## Tech Stack
| Layer           | Technology                   |
|-----------------|------------------------------|
| Backend         | Java, Spring Boot, Spring Cloud (Eureka, Config, Gateway) |
| Security        | Keycloak, OAuth2 / PKCE      |
| Messaging       | RabbitMQ (Spring AMQP)       |
| Databases       | PostgreSQL (User data), MongoDB (Activities, AI data) |
| AI Integration  | Google Gemini API            |
| Frontend        | React, Vite, React Router, react-oauth2-code-pkce |
| DevOps & CI/CD  | Docker, Maven, GitHub Actions |

## Prerequisites
- Java 17+ and Maven 3.8+
- Node.js 16+ and npm/yarn
- Docker & Docker Compose
- Keycloak server (v17+)
- RabbitMQ broker
- PostgreSQL & MongoDB instances
- Google Cloud API key for Gemini

## Getting Started

### Clone Repository
```bash
git clone https://github.com/EmbarkXOfficial/fitness-app-microservices.git
cd fitness-app-microservices
```

### Configuration
1. Copy `.env.example` to `.env` and fill in credentials:
   ```ini
   KEYCLOAK_URL=
   KEYCLOAK_REALM=
   KEYCLOAK_CLIENT_ID=
   DB_POSTGRES_URL=jdbc:postgresql://localhost:5432/users
   DB_POSTGRES_USERNAME=
   DB_POSTGRES_PASSWORD=
   DB_MONGO_URI=mongodb://localhost:27017/activities
   RABBITMQ_HOST=localhost
   GEMINI_API_KEY=
   ```
2. Update `configserver/src/main/resources/application.yml` for your environment.

### Running Services
Use Docker Compose to launch infrastructure:
```bash
docker-compose up -d postgres mongo rabbitmq keycloak
```

Start each Spring Boot service (in separate terminals or via your IDE):
```bash
cd eureka-server && mvn spring-boot:run
cd configserver && mvn spring-boot:run
cd gateway && mvn spring-boot:run
cd userservice && mvn spring-boot:run
cd activityservice && mvn spring-boot:run
cd aiservice && mvn spring-boot:run
```

## Microservice Modules
- **eureka-server**: Service registry
- **configserver**: Centralized configuration
- **gateway**: API gateway with routing & security
- **userservice**: Manages user profiles (PostgreSQL)
- **activityservice**: Stores activities (MongoDB)
- **aiservice**: Generates recommendations (Google Gemini)

## API Endpoints
| Service         | Endpoint                         | Method | Description                         |
|-----------------|----------------------------------|--------|-------------------------------------|
| User Service    | `/api/users/register`            | POST   | Register new user                   |
|                 | `/api/users/{id}`                | GET    | Get user profile                    |
| Activity Service| `/api/activities`                | POST   | Create new activity                 |
|                 | `/api/activities/{id}`           | GET    | Fetch activity by ID                |
| AI Service      | `/api/recommendations/{userId}`  | GET    | Get AI‑powered fitness tips         |

## Frontend Usage
1. Navigate to `fitness-app-frontend`
2. Install dependencies: `npm install`
3. Start dev server: `npm run dev`
4. Open `http://localhost:3000`

## Contributing
Contributions are welcome! Please:
1. Fork the repo
2. Create a feature branch (`git checkout -b feature/XYZ`)
3. Commit your changes (`git commit -m "Add XYZ"`)
4. Push to branch (`git push origin feature/XYZ`)
5. Open a Pull Request

