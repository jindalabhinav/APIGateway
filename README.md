# API Gateway Service

## Project Overview
This is a Spring Cloud Gateway service that acts as an API Gateway for a microservices architecture. It provides centralized routing and load balancing capabilities for the underlying microservices.

## Technologies Used
- Java 17
- Spring Boot 3.4.1
- Spring Cloud Gateway
- Spring Cloud Netflix Eureka Client
- Spring Cloud LoadBalancer
- Spring Boot Actuator
- Micrometer (for metrics)
- Maven (for build and dependency management)
- Lombok (for reducing boilerplate code)

## Key Features
1. **Service Discovery**: Integrates with Eureka Server for service registration and discovery
2. **Dynamic Routing**: Routes requests to appropriate microservices based on path-based routing rules
3. **Load Balancing**: Provides client-side load balancing for microservices
4. **Monitoring**: Exposes metrics and health checks through Spring Boot Actuator
5. **Prometheus Integration**: Includes Micrometer registry for Prometheus metrics collection

## Project Structure
```
APIGateway/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── org/example/apigateway/
│   │   │       └── ApiGatewayApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/
│           └── org/example/apigateway/
│               └── ApiGatewayApplicationTests.java
└── pom.xml
```

## Configuration
The application is configured with the following properties in `application.properties`:
- Application name: `apigateway`
- Eureka client configuration for service discovery
- Reactive web application type
- Gateway routes configuration for:
  - Products service (`/products/**`)
  - Users service (`/users/**`)

## Build Instructions

### Prerequisites
- Java 17 or higher
- Maven 3.6 or higher

### Steps to Build
1. Clone the repository
2. Navigate to the project root directory
3. Run the following command:
```bash
./mvnw clean install
```

### Running the Application
To run the application locally:
```bash
./mvnw spring-boot:run
```

The API Gateway will start on the default port and register itself with the Eureka Server running at `http://localhost:8761/eureka/`.

## Service Routes
The API Gateway is configured with the following routes:
1. Products Service
   - Path: `/products/**`
   - Load balanced routing to the "products" service

2. Users Service
   - Path: `/users/**`
   - Load balanced routing to the "users" service

## Monitoring and Metrics
- All actuator endpoints are exposed (configured via `management.endpoints.web.exposure.include=*`)
- Prometheus metrics are available through the Micrometer registry
- Health checks and other actuator endpoints can be accessed through the standard actuator endpoints

## Dependencies
Key dependencies include:
- Spring Cloud Gateway for API Gateway functionality
- Spring Cloud LoadBalancer for client-side load balancing
- Spring Cloud Netflix Eureka Client for service discovery
- Spring Boot Actuator for monitoring and metrics
- Micrometer Prometheus registry for metrics collection
- Lombok for reducing boilerplate code
- Spring Boot DevTools for development convenience

## Development Notes
- The application is configured as a reactive web application
- It uses Spring Cloud Gateway instead of the deprecated Zuul
- Client-side load balancing is handled by Spring Cloud LoadBalancer
- The project uses Spring Boot 3.4.1 and Spring Cloud 2024.0.0

## Testing
The project includes basic test setup with Spring Boot Test. To run tests:
```bash
./mvnw test
```