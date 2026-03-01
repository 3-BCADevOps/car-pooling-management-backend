# Car Pooling Management System - Backend

Spring Boot REST API for car pooling management system.

## Features
- User Management APIs
- Ride Management APIs
- Booking Management APIs

## Technologies
- Spring Boot
- Spring Data JPA
- H2 Database
- Maven

## Setup

```bash
mvn clean install
mvn spring-boot:run
```

Server runs on `http://localhost:8080`

## Deploy on Render (with PostgreSQL)

This repository includes a Render Blueprint file at `render.yaml` for one-click deployment.

### Option 1: Blueprint Deploy (recommended)

1. Push your latest backend code to GitHub.
2. In Render, select **New +** → **Blueprint**.
3. Connect this repository and deploy.

Render will provision:
- A web service (`car-pooling-management-backend`)
- A PostgreSQL database (`carpooling-db`)

### Runtime details

- Build command: `./mvnw clean package -DskipTests`
- Start command: `java -Dspring.profiles.active=render -jar target/demo-0.0.1-SNAPSHOT.jar`

### Spring profiles

- Local/default: `application.properties` (H2)
- Render/prod: `application-render.properties` (PostgreSQL)

When deployed via `render.yaml`, Render injects database connection variables used by the `render` profile.

## API Endpoints

### Users
- GET `/api/users`
- GET `/api/users/{id}`
- POST `/api/users`
- PUT `/api/users/{id}`
- DELETE `/api/users/{id}`

### Rides
- GET `/api/rides`
- GET `/api/rides/{id}`
- POST `/api/rides`
- PUT `/api/rides/{id}`
- DELETE `/api/rides/{id}`

### Bookings
- GET `/api/bookings`
- GET `/api/bookings/{id}`
- POST `/api/bookings`
- PUT `/api/bookings/{id}`
- DELETE `/api/bookings/{id}`
