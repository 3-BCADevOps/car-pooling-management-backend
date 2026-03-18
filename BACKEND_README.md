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

## Deploy on Azure App Service (Linux, Java 17)

If Azure logs show `Could not find an executable jar in /home/site/wwwroot`, App Service is starting the default parking page because your JAR is missing or startup command does not match the deployed file name.

This project now builds a stable artifact name:
- `target/app.jar`

### Required App Service settings

In **Configuration -> Application settings**, add:
- `SPRING_PROFILES_ACTIVE=render`
- `SPRING_DATASOURCE_HOST=<your_db_host>`
- `SPRING_DATASOURCE_PORT=<your_db_port>`
- `SPRING_DATASOURCE_DB=<your_db_name>`
- `SPRING_DATASOURCE_USERNAME=<your_db_user>`
- `SPRING_DATASOURCE_PASSWORD=<your_db_password>`

In **Configuration -> General settings -> Startup Command**, set:

```bash
java -Dspring.profiles.active=render -jar /home/site/wwwroot/app.jar
```

Do not append `--server.port=$PORT` in App Service startup command. App Service can pass this as a literal string in some contexts, and your app already reads the port from `server.port=${PORT:8080}`.

### Build and deploy artifact

```bash
./mvnw clean package -DskipTests
```

Deploy `target/app.jar` to `/home/site/wwwroot/app.jar` (Zip Deploy or CI/CD).

### Verify successful startup in logs

Look for these lines:
- `Running STARTUP_COMMAND: java -Dspring.profiles.active=render -jar /home/site/wwwroot/app.jar`
- `Tomcat started on port 80`
- `Started DemoApplication`

Notes:
- `Application Insights` timeout warnings in your log are not the root cause of app startup failure.
- The critical failure is missing executable JAR or mismatched startup command.

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
