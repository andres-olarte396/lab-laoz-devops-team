# Java Stack - Spring Boot on Azure

## 📋 Overview

Stack optimizado para aplicaciones Java/Spring Boot en Azure, enfocado en arquitecturas enterprise y microservices.

### Ideal Para
- ✅ Enterprise applications
- ✅ Spring Boot microservices
- ✅ RESTful APIs
- ✅ Reactive applications (WebFlux)
- ✅ Batch processing
- ✅ Legacy modernization
- ✅ High-performance services

### NO Usar Cuando
- ❌ Proyectos pequeños con equipos reducidos
- ❌ Prototipado rápido (considerar Python/Node.js)
- ❌ Resource-constrained environments

### Ventajas
- 🏢 Enterprise-grade ecosystem
- 🔒 Strong typing y seguridad
- 📦 Maven/Gradle dependency management
- ⚡ Performance excelente
- 🔧 Tooling maduro (IntelliJ, Eclipse)
- 🌐 Spring ecosystem completo

## 🏗️ Architecture

```
Internet → Front Door → App Service / AKS
                             ↓
                      Spring Boot Apps
                             ↓
        ┌────────────────────┼────────────────────┐
        │                    │                    │
   Azure SQL          Cosmos DB            Redis Cache
                             │
                      Service Bus / Kafka
```

## 🛠️ Technology Stack

### Runtime & Framework
```yaml
Java Version:
  - Java 21 LTS (recommended, support until Sep 2028)
  - Java 17 LTS (widely adopted, support until Sep 2026)
  - Java 11 LTS (legacy, support until Sep 2026)

Spring Boot:
  - Version: 3.2.x (Spring Framework 6.x)
  - Requires Java 17+

Build Tools:
  - Maven 3.9.x (traditional)
  - Gradle 8.x (modern, faster)

Key Spring Modules:
  - Spring Web (REST APIs)
  - Spring Data JPA (ORM)
  - Spring Data Redis
  - Spring Security (Auth)
  - Spring Cloud (Microservices)
  - Spring WebFlux (Reactive)
  - Spring Batch (Processing)
  - Spring Integration (Messaging)
```

### Web Hosting
```yaml
Option A - Azure App Service:
  - Tier: Premium P2V3 or higher
  - Runtime: Java 21 Tomcat 10
  - Auto-scale: 3-10 instances
  - Deployment: JAR/WAR

Option B - Azure Spring Apps:
  - Managed Spring Cloud platform
  - Built-in service discovery
  - Config server
  - Blue-green deployment
  - APM integration

Option C - Azure Container Apps / AKS:
  - Containerized Spring Boot
  - Kubernetes orchestration
  - Auto-scaling (KEDA)
  - Service mesh (Istio)
```

### Database
```yaml
Relational:
  - Azure SQL Database
    - JDBC driver: mssql-jdbc
    - ORM: Spring Data JPA (Hibernate)
  
  - Azure Database for PostgreSQL
    - JDBC driver: postgresql
    - R2DBC for reactive
  
  - Azure Database for MySQL
    - JDBC driver: mysql-connector-java

NoSQL:
  - Cosmos DB (SQL API)
    - SDK: azure-spring-data-cosmos
  
  - MongoDB (on Cosmos)
    - Spring Data MongoDB

Connection Pooling:
  - HikariCP (default in Spring Boot)
  - Configuration optimizada
```

### Messaging
```yaml
Azure Service Bus:
  - SDK: azure-messaging-servicebus
  - Spring Cloud Stream binder
  - Topics & Queues

Azure Event Hubs:
  - Kafka-compatible
  - Spring Kafka integration
  - Real-time streaming

RabbitMQ (on AKS):
  - Spring AMQP
  - Traditional messaging
```

### Caching
```yaml
Azure Cache for Redis:
  - Spring Data Redis
  - Spring Cache abstraction
  - Session management
  - Distributed caching

Caffeine:
  - Local caching
  - High performance
  - Spring Cache integration
```

### Security
```yaml
Authentication:
  - Spring Security
  - Azure AD / Entra ID
  - OAuth 2.0 / OIDC
  - JWT (JJWT library)

Azure Integration:
  - azure-spring-boot-starter-active-directory
  - Managed Identity support

Secrets Management:
  - Azure Key Vault
  - azure-spring-boot-starter-keyvault-secrets
```

### Observability
```yaml
Application Insights:
  - applicationinsights-spring-boot-starter
  - Auto-instrumentation
  - Distributed tracing

Logging:
  - SLF4J + Logback (default)
  - Log4j2 (alternative)
  - Structured logging (JSON)

Metrics:
  - Spring Boot Actuator
  - Micrometer
  - Prometheus endpoint

Health Checks:
  - /actuator/health
  - Custom health indicators
  - Liveness & Readiness probes
```

## 📁 Project Structure

### Multi-module Maven Project
```
my-spring-app/
├── pom.xml                          # Parent POM
├── app/                             # Main application
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── com/mycompany/app/
│   │   │   │       ├── Application.java
│   │   │   │       ├── config/
│   │   │   │       │   ├── DatabaseConfig.java
│   │   │   │       │   ├── SecurityConfig.java
│   │   │   │       │   └── RedisConfig.java
│   │   │   │       ├── controller/
│   │   │   │       │   ├── UserController.java
│   │   │   │       │   └── OrderController.java
│   │   │   │       ├── service/
│   │   │   │       │   ├── UserService.java
│   │   │   │       │   └── UserServiceImpl.java
│   │   │   │       ├── repository/
│   │   │   │       │   └── UserRepository.java
│   │   │   │       ├── model/
│   │   │   │       │   ├── User.java
│   │   │   │       │   └── Order.java
│   │   │   │       ├── dto/
│   │   │   │       │   ├── UserDto.java
│   │   │   │       │   └── CreateUserRequest.java
│   │   │   │       ├── exception/
│   │   │   │       │   ├── GlobalExceptionHandler.java
│   │   │   │       │   └── ResourceNotFoundException.java
│   │   │   │       └── util/
│   │   │   │           └── DateUtils.java
│   │   │   └── resources/
│   │   │       ├── application.yml
│   │   │       ├── application-dev.yml
│   │   │       ├── application-prod.yml
│   │   │       └── db/migration/
│   │   │           └── V1__initial_schema.sql
│   │   └── test/
│   │       └── java/
│   │           └── com/mycompany/app/
│   │               ├── controller/
│   │               ├── service/
│   │               └── repository/
│   └── pom.xml
├── common/                          # Shared utilities
│   ├── src/main/java/
│   └── pom.xml
├── infrastructure/
│   └── main.bicep
├── .github/
│   └── workflows/
│       └── deploy.yml
└── README.md
```

## 🚀 Sample Implementation

### Application Entry Point
```java
// Application.java
package com.mycompany.app;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cache.annotation.EnableCaching;
import org.springframework.scheduling.annotation.EnableAsync;

@SpringBootApplication
@EnableCaching
@EnableAsync
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

### Configuration
```yaml
# application.yml
spring:
  application:
    name: my-spring-app
  
  datasource:
    url: jdbc:sqlserver://${AZURE_SQL_SERVER}:1433;database=${AZURE_SQL_DATABASE};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
    username: ${AZURE_SQL_USERNAME}
    password: ${AZURE_SQL_PASSWORD}
    hikari:
      maximum-pool-size: 10
      minimum-idle: 5
      connection-timeout: 20000
      idle-timeout: 300000
      max-lifetime: 1200000
  
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false
    properties:
      hibernate:
        dialect: org.hibernate.dialect.SQLServerDialect
        format_sql: true
        use_sql_comments: true
  
  data:
    redis:
      host: ${AZURE_REDIS_HOST}
      port: 6380
      password: ${AZURE_REDIS_PASSWORD}
      ssl: true
      timeout: 2000ms
      lettuce:
        pool:
          max-active: 8
          max-idle: 8
          min-idle: 0
  
  cache:
    type: redis
    redis:
      time-to-live: 3600000
  
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: https://login.microsoftonline.com/${AZURE_TENANT_ID}/v2.0
          jwk-set-uri: https://login.microsoftonline.com/${AZURE_TENANT_ID}/discovery/v2.0/keys

management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  endpoint:
    health:
      show-details: when-authorized
      probes:
        enabled: true
  metrics:
    export:
      prometheus:
        enabled: true

logging:
  level:
    root: INFO
    com.mycompany.app: DEBUG
    org.springframework.web: DEBUG
  pattern:
    console: "%d{yyyy-MM-dd HH:mm:ss} - %msg%n"
    file: "%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n"
```

### REST Controller
```java
// UserController.java
package com.mycompany.app.controller;

import com.mycompany.app.dto.CreateUserRequest;
import com.mycompany.app.dto.UpdateUserRequest;
import com.mycompany.app.dto.UserDto;
import com.mycompany.app.service.UserService;
import io.swagger.v3.oas.annotations.Operation;
import io.swagger.v3.oas.annotations.tags.Tag;
import jakarta.validation.Valid;
import lombok.RequiredArgsConstructor;
import lombok.extern.slf4j.Slf4j;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.access.prepost.PreAuthorize;
import org.springframework.web.bind.annotation.*;

@Slf4j
@RestController
@RequestMapping("/api/v1/users")
@RequiredArgsConstructor
@Tag(name = "User Management", description = "APIs for managing users")
public class UserController {
    
    private final UserService userService;
    
    @GetMapping
    @Operation(summary = "Get all users", description = "Retrieve paginated list of users")
    public ResponseEntity<Page<UserDto>> getAllUsers(Pageable pageable) {
        log.info("Fetching users with pagination: {}", pageable);
        Page<UserDto> users = userService.findAll(pageable);
        return ResponseEntity.ok(users);
    }
    
    @GetMapping("/{id}")
    @Operation(summary = "Get user by ID")
    public ResponseEntity<UserDto> getUserById(@PathVariable Long id) {
        log.info("Fetching user with ID: {}", id);
        UserDto user = userService.findById(id);
        return ResponseEntity.ok(user);
    }
    
    @PostMapping
    @PreAuthorize("hasRole('ADMIN')")
    @Operation(summary = "Create new user")
    public ResponseEntity<UserDto> createUser(@Valid @RequestBody CreateUserRequest request) {
        log.info("Creating new user: {}", request.getEmail());
        UserDto user = userService.create(request);
        return ResponseEntity.status(HttpStatus.CREATED).body(user);
    }
    
    @PutMapping("/{id}")
    @Operation(summary = "Update user")
    public ResponseEntity<UserDto> updateUser(
            @PathVariable Long id,
            @Valid @RequestBody UpdateUserRequest request) {
        log.info("Updating user with ID: {}", id);
        UserDto user = userService.update(id, request);
        return ResponseEntity.ok(user);
    }
    
    @DeleteMapping("/{id}")
    @PreAuthorize("hasRole('ADMIN')")
    @Operation(summary = "Delete user")
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        log.info("Deleting user with ID: {}", id);
        userService.delete(id);
        return ResponseEntity.noContent().build();
    }
}
```

### Service Layer
```java
// UserServiceImpl.java
package com.mycompany.app.service;

import com.mycompany.app.dto.CreateUserRequest;
import com.mycompany.app.dto.UpdateUserRequest;
import com.mycompany.app.dto.UserDto;
import com.mycompany.app.exception.ResourceNotFoundException;
import com.mycompany.app.model.User;
import com.mycompany.app.repository.UserRepository;
import lombok.RequiredArgsConstructor;
import lombok.extern.slf4j.Slf4j;
import org.springframework.cache.annotation.CacheEvict;
import org.springframework.cache.annotation.Cacheable;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Slf4j
@Service
@RequiredArgsConstructor
@Transactional(readOnly = true)
public class UserServiceImpl implements UserService {
    
    private final UserRepository userRepository;
    private final PasswordEncoder passwordEncoder;
    
    @Override
    public Page<UserDto> findAll(Pageable pageable) {
        return userRepository.findAll(pageable)
                .map(this::toDto);
    }
    
    @Override
    @Cacheable(value = "users", key = "#id")
    public UserDto findById(Long id) {
        log.debug("Fetching user from database: {}", id);
        return userRepository.findById(id)
                .map(this::toDto)
                .orElseThrow(() -> new ResourceNotFoundException("User not found with id: " + id));
    }
    
    @Override
    @Transactional
    @CacheEvict(value = "users", allEntries = true)
    public UserDto create(CreateUserRequest request) {
        // Check if email already exists
        if (userRepository.existsByEmail(request.getEmail())) {
            throw new IllegalArgumentException("Email already exists");
        }
        
        User user = User.builder()
                .email(request.getEmail())
                .username(request.getUsername())
                .password(passwordEncoder.encode(request.getPassword()))
                .firstName(request.getFirstName())
                .lastName(request.getLastName())
                .build();
        
        User savedUser = userRepository.save(user);
        log.info("User created successfully: {}", savedUser.getId());
        
        return toDto(savedUser);
    }
    
    @Override
    @Transactional
    @CacheEvict(value = "users", key = "#id")
    public UserDto update(Long id, UpdateUserRequest request) {
        User user = userRepository.findById(id)
                .orElseThrow(() -> new ResourceNotFoundException("User not found with id: " + id));
        
        if (request.getEmail() != null) {
            user.setEmail(request.getEmail());
        }
        if (request.getFirstName() != null) {
            user.setFirstName(request.getFirstName());
        }
        if (request.getLastName() != null) {
            user.setLastName(request.getLastName());
        }
        
        User updatedUser = userRepository.save(user);
        log.info("User updated successfully: {}", updatedUser.getId());
        
        return toDto(updatedUser);
    }
    
    @Override
    @Transactional
    @CacheEvict(value = "users", key = "#id")
    public void delete(Long id) {
        if (!userRepository.existsById(id)) {
            throw new ResourceNotFoundException("User not found with id: " + id);
        }
        
        userRepository.deleteById(id);
        log.info("User deleted successfully: {}", id);
    }
    
    private UserDto toDto(User user) {
        return UserDto.builder()
                .id(user.getId())
                .email(user.getEmail())
                .username(user.getUsername())
                .firstName(user.getFirstName())
                .lastName(user.getLastName())
                .createdAt(user.getCreatedAt())
                .updatedAt(user.getUpdatedAt())
                .build();
    }
}
```

### Entity Model
```java
// User.java
package com.mycompany.app.model;

import jakarta.persistence.*;
import lombok.*;
import org.hibernate.annotations.CreationTimestamp;
import org.hibernate.annotations.UpdateTimestamp;

import java.time.LocalDateTime;

@Entity
@Table(name = "users", indexes = {
    @Index(name = "idx_email", columnList = "email", unique = true),
    @Index(name = "idx_username", columnList = "username", unique = true)
})
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class User {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, unique = true, length = 255)
    private String email;
    
    @Column(nullable = false, unique = true, length = 50)
    private String username;
    
    @Column(nullable = false)
    private String password;
    
    @Column(name = "first_name", length = 100)
    private String firstName;
    
    @Column(name = "last_name", length = 100)
    private String lastName;
    
    @Column(name = "is_active")
    private boolean active = true;
    
    @CreationTimestamp
    @Column(name = "created_at", nullable = false, updatable = false)
    private LocalDateTime createdAt;
    
    @UpdateTimestamp
    @Column(name = "updated_at")
    private LocalDateTime updatedAt;
}
```

### Repository
```java
// UserRepository.java
package com.mycompany.app.repository;

import com.mycompany.app.model.User;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.stereotype.Repository;

import java.util.Optional;

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    
    Optional<User> findByEmail(String email);
    
    Optional<User> findByUsername(String username);
    
    boolean existsByEmail(String email);
    
    @Query("SELECT u FROM User u WHERE u.email = ?1 AND u.active = true")
    Optional<User> findActiveUserByEmail(String email);
}
```

## 📦 Dependencies (pom.xml)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.1</version>
        <relativePath/>
    </parent>
    
    <groupId>com.mycompany</groupId>
    <artifactId>my-spring-app</artifactId>
    <version>1.0.0</version>
    <name>My Spring App</name>
    
    <properties>
        <java.version>21</java.version>
        <azure.version>5.8.0</azure.version>
    </properties>
    
    <dependencies>
        <!-- Spring Boot Starters -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-validation</artifactId>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        
        <!-- Database -->
        <dependency>
            <groupId>com.microsoft.sqlserver</groupId>
            <artifactId>mssql-jdbc</artifactId>
        </dependency>
        
        <!-- Azure SDKs -->
        <dependency>
            <groupId>com.azure.spring</groupId>
            <artifactId>spring-cloud-azure-starter-keyvault-secrets</artifactId>
        </dependency>
        
        <dependency>
            <groupId>com.azure.spring</groupId>
            <artifactId>spring-cloud-azure-starter-active-directory</artifactId>
        </dependency>
        
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>applicationinsights-spring-boot-starter</artifactId>
            <version>3.4.18</version>
        </dependency>
        
        <!-- Utilities -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        
        <dependency>
            <groupId>org.springdoc</groupId>
            <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
            <version>2.3.0</version>
        </dependency>
        
        <!-- Monitoring -->
        <dependency>
            <groupId>io.micrometer</groupId>
            <artifactId>micrometer-registry-prometheus</artifactId>
        </dependency>
        
        <!-- Testing -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        
        <dependency>
            <groupId>org.springframework.security</groupId>
            <artifactId>spring-security-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
    
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>com.azure.spring</groupId>
                <artifactId>spring-cloud-azure-dependencies</artifactId>
                <version>${azure.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

## 🐳 Dockerfile

```dockerfile
# Build stage
FROM maven:3.9-eclipse-temurin-21 AS build

WORKDIR /app

# Copy pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy source and build
COPY src ./src
RUN mvn clean package -DskipTests

# Runtime stage
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app

# Copy JAR from build stage
COPY --from=build /app/target/*.jar app.jar

# Create non-root user
RUN addgroup -g 1001 spring && adduser -S spring -u 1001 -G spring
USER spring:spring

EXPOSE 8080

# JVM options for container
ENV JAVA_OPTS="-Xms512m -Xmx2048m -XX:+UseG1GC -XX:MaxGCPauseMillis=200"

ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
```

## 🚀 CI/CD Pipeline

```yaml
name: Java Deploy to Azure

on:
  push:
    branches: [ main ]

env:
  JAVA_VERSION: '21'
  AZURE_WEBAPP_NAME: app-myjavaapp-prod

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Set up JDK
      uses: actions/setup-java@v4
      with:
        java-version: ${{ env.JAVA_VERSION }}
        distribution: 'temurin'
        cache: 'maven'
    
    - name: Build with Maven
      run: mvn clean package -DskipTests
    
    - name: Run tests
      run: mvn test
    
    - name: Upload artifact
      uses: actions/upload-artifact@v4
      with:
        name: java-app
        path: target/*.jar

  deploy:
    runs-on: ubuntu-latest
    needs: build
    
    steps:
    - name: Download artifact
      uses: actions/download-artifact@v4
      with:
        name: java-app
    
    - name: Login to Azure
      uses: azure/login@v1
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}
    
    - name: Deploy to App Service
      uses: azure/webapps-deploy@v3
      with:
        app-name: ${{ env.AZURE_WEBAPP_NAME }}
        package: '*.jar'
```

## 💰 Cost Estimation

```yaml
Production:
  - App Service P2V3 (3 instances): ~$570/month
  - Azure SQL (GP 4 vCores): ~$510/month
  - Redis (Standard C1): ~$15/month
  - App Insights: ~$50/month
  Total: ~$1,145/month

Azure Spring Apps (Alternative):
  - Standard tier: ~$500/month
  - Managed services included
```

## ⚡ Quick Start

```bash
# 1. Generate project
curl https://start.spring.io/starter.zip \
  -d dependencies=web,data-jpa,security,actuator \
  -d javaVersion=21 \
  -d type=maven-project \
  -o my-app.zip

# 2. Extract and build
unzip my-app.zip && cd my-app
mvn clean package

# 3. Run locally
mvn spring-boot:run

# 4. Deploy to Azure
az webapp up --runtime "JAVA:21-java21" --name myjavaapp
```

---

**Owner**: Platform Engineer  
**Última actualización**: Diciembre 2025
