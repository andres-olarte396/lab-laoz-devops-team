# Go Stack - High-Performance Services on Azure

## 📋 Overview

Stack optimizado para aplicaciones Go en Azure, ideal para microservices de alto rendimiento y servicios de baja latencia.

### Ideal Para
- ✅ High-performance microservices
- ✅ REST/gRPC APIs
- ✅ CLI tools y automation
- ✅ Network services
- ✅ Real-time systems
- ✅ Container-native apps
- ✅ Cloud-native tooling

### NO Usar Cuando
- ❌ Rapid prototyping (considerar Python/Node.js)
- ❌ Legacy system integration
- ❌ GUI desktop applications

### Ventajas
- ⚡ Performance excepcional
- 🚀 Fast compilation
- 📦 Single binary deployment
- 🔄 Built-in concurrency (goroutines)
- 💾 Low memory footprint
- 🛠️ Simple toolchain

## 🏗️ Architecture

```
Internet → Front Door → Container Apps / AKS
                             ↓
                        Go Microservices
                             ↓
        ┌────────────────────┼────────────────────┐
        │                    │                    │
   PostgreSQL           Cosmos DB            Redis
                             │
                      gRPC / HTTP/2
```

## 🛠️ Technology Stack

### Runtime & Framework
```yaml
Go Version:
  - Go 1.22 (latest)
  - Go 1.21 (stable)

Web Frameworks:
  - Gin (high-performance HTTP)
  - Echo (minimalist, fast)
  - Fiber (Express-like)
  - Chi (lightweight router)
  - Standard lib net/http (production-ready)

gRPC:
  - google.golang.org/grpc
  - Protocol Buffers
  - Streaming support

API Documentation:
  - Swag (Swagger generator)
  - OpenAPI 3.0
```

### Web Hosting
```yaml
Primary - Azure Container Apps:
  - Native container platform
  - Scale to zero
  - Dapr integration
  - Auto-scaling (KEDA)

Alternative - AKS:
  - Full Kubernetes control
  - Service mesh (Istio/Linkerd)
  - Advanced networking

Functions (Preview):
  - Custom handlers
  - Event-driven
```

### Database
```yaml
Relational:
  - PostgreSQL
    - Driver: pgx (high-performance)
    - ORM: GORM, sqlx
  
  - Azure SQL
    - Driver: go-mssqldb

NoSQL:
  - Cosmos DB
    - SDK: azure-sdk-for-go/sdk/data/azcosmos
  
  - Redis
    - go-redis/redis

Connection Pooling:
  - pgxpool
  - database/sql pool
```

### Messaging
```yaml
Azure Service Bus:
  - SDK: azservicebus
  - Topics & Queues

gRPC:
  - Bidirectional streaming
  - Load balancing
  - Interceptors

NATS:
  - High-performance messaging
  - Pub/sub patterns
```

### Caching
```yaml
Redis:
  - go-redis/redis
  - Clustering support
  - Pipeline support

In-Memory:
  - sync.Map
  - groupcache
  - ristretto
```

### Security
```yaml
Authentication:
  - JWT (golang-jwt/jwt)
  - OAuth2 (golang.org/x/oauth2)
  - Azure AD SDK

Secrets:
  - Azure Key Vault SDK
  - Environment variables
  - Viper configuration

Crypto:
  - Standard lib crypto
  - x/crypto
```

### Observability
```yaml
Metrics:
  - Prometheus client
  - OpenTelemetry

Logging:
  - zerolog (structured, fast)
  - zap (uber's logger)
  - logrus (popular)

Tracing:
  - OpenTelemetry
  - Application Insights SDK

Health Checks:
  - /health endpoint
  - /ready endpoint
```

## 📁 Project Structure

```
my-go-app/
├── cmd/
│   └── api/
│       └── main.go              # Application entry
├── internal/                    # Private code
│   ├── config/
│   │   └── config.go
│   ├── handler/
│   │   ├── user_handler.go
│   │   └── health_handler.go
│   ├── service/
│   │   └── user_service.go
│   ├── repository/
│   │   └── user_repository.go
│   ├── model/
│   │   └── user.go
│   ├── middleware/
│   │   ├── auth.go
│   │   ├── logging.go
│   │   └── cors.go
│   └── util/
│       └── response.go
├── pkg/                         # Public libraries
│   └── logger/
│       └── logger.go
├── api/
│   ├── openapi.yaml
│   └── proto/
│       └── user.proto
├── migrations/
│   ├── 001_create_users.up.sql
│   └── 001_create_users.down.sql
├── infrastructure/
│   └── main.bicep
├── .github/
│   └── workflows/
│       └── deploy.yml
├── Dockerfile
├── go.mod
├── go.sum
├── Makefile
└── README.md
```

## 🚀 Sample Implementation

### Main Application
```go
// cmd/api/main.go
package main

import (
    "context"
    "fmt"
    "net/http"
    "os"
    "os/signal"
    "syscall"
    "time"

    "github.com/gin-gonic/gin"
    "github.com/rs/zerolog"
    "github.com/rs/zerolog/log"
    
    "myapp/internal/config"
    "myapp/internal/handler"
    "myapp/internal/repository"
    "myapp/internal/service"
    "myapp/pkg/database"
    "myapp/pkg/redis"
)

func main() {
    // Configure logger
    zerolog.TimeFieldFormat = zerolog.TimeFormatUnix
    log.Logger = log.Output(zerolog.ConsoleWriter{Out: os.Stderr})

    // Load configuration
    cfg, err := config.Load()
    if err != nil {
        log.Fatal().Err(err).Msg("Failed to load configuration")
    }

    // Initialize database
    db, err := database.NewPostgres(cfg.DatabaseURL)
    if err != nil {
        log.Fatal().Err(err).Msg("Failed to connect to database")
    }
    defer db.Close()

    // Initialize Redis
    rdb := redis.NewClient(cfg.RedisURL)
    defer rdb.Close()

    // Initialize repositories
    userRepo := repository.NewUserRepository(db)

    // Initialize services
    userService := service.NewUserService(userRepo, rdb)

    // Initialize handlers
    userHandler := handler.NewUserHandler(userService)
    healthHandler := handler.NewHealthHandler(db, rdb)

    // Setup router
    router := setupRouter(userHandler, healthHandler)

    // Create server
    srv := &http.Server{
        Addr:         fmt.Sprintf(":%s", cfg.Port),
        Handler:      router,
        ReadTimeout:  15 * time.Second,
        WriteTimeout: 15 * time.Second,
        IdleTimeout:  60 * time.Second,
    }

    // Start server
    go func() {
        log.Info().Msgf("Starting server on port %s", cfg.Port)
        if err := srv.ListenAndServe(); err != nil && err != http.ErrServerClosed {
            log.Fatal().Err(err).Msg("Failed to start server")
        }
    }()

    // Graceful shutdown
    quit := make(chan os.Signal, 1)
    signal.Notify(quit, syscall.SIGINT, syscall.SIGTERM)
    <-quit

    log.Info().Msg("Shutting down server...")

    ctx, cancel := context.WithTimeout(context.Background(), 30*time.Second)
    defer cancel()

    if err := srv.Shutdown(ctx); err != nil {
        log.Fatal().Err(err).Msg("Server forced to shutdown")
    }

    log.Info().Msg("Server exited")
}

func setupRouter(userHandler *handler.UserHandler, healthHandler *handler.HealthHandler) *gin.Engine {
    router := gin.New()
    router.Use(gin.Recovery())
    router.Use(middleware.Logger())
    router.Use(middleware.CORS())

    // Health endpoints
    router.GET("/health", healthHandler.Health)
    router.GET("/ready", healthHandler.Ready)

    // API v1
    v1 := router.Group("/api/v1")
    {
        users := v1.Group("/users")
        {
            users.GET("", userHandler.GetAll)
            users.GET("/:id", userHandler.GetByID)
            users.POST("", userHandler.Create)
            users.PUT("/:id", userHandler.Update)
            users.DELETE("/:id", userHandler.Delete)
        }
    }

    return router
}
```

### Configuration
```go
// internal/config/config.go
package config

import (
    "os"
    "github.com/joho/godotenv"
)

type Config struct {
    Port        string
    DatabaseURL string
    RedisURL    string
    Environment string
    AzureAD     AzureADConfig
}

type AzureADConfig struct {
    TenantID     string
    ClientID     string
    ClientSecret string
}

func Load() (*Config, error) {
    // Load .env file if exists (for local development)
    _ = godotenv.Load()

    return &Config{
        Port:        getEnv("PORT", "8080"),
        DatabaseURL: getEnv("DATABASE_URL", ""),
        RedisURL:    getEnv("REDIS_URL", ""),
        Environment: getEnv("ENVIRONMENT", "development"),
        AzureAD: AzureADConfig{
            TenantID:     getEnv("AZURE_TENANT_ID", ""),
            ClientID:     getEnv("AZURE_CLIENT_ID", ""),
            ClientSecret: getEnv("AZURE_CLIENT_SECRET", ""),
        },
    }, nil
}

func getEnv(key, defaultValue string) string {
    if value := os.Getenv(key); value != "" {
        return value
    }
    return defaultValue
}
```

### Handler
```go
// internal/handler/user_handler.go
package handler

import (
    "net/http"
    "strconv"

    "github.com/gin-gonic/gin"
    "github.com/rs/zerolog/log"
    
    "myapp/internal/model"
    "myapp/internal/service"
)

type UserHandler struct {
    userService *service.UserService
}

func NewUserHandler(userService *service.UserService) *UserHandler {
    return &UserHandler{
        userService: userService,
    }
}

func (h *UserHandler) GetAll(c *gin.Context) {
    page, _ := strconv.Atoi(c.DefaultQuery("page", "1"))
    limit, _ := strconv.Atoi(c.DefaultQuery("limit", "10"))

    users, total, err := h.userService.GetAll(c.Request.Context(), page, limit)
    if err != nil {
        log.Error().Err(err).Msg("Failed to get users")
        c.JSON(http.StatusInternalServerError, gin.H{
            "error": "Failed to retrieve users",
        })
        return
    }

    c.JSON(http.StatusOK, gin.H{
        "data": users,
        "pagination": gin.H{
            "page":  page,
            "limit": limit,
            "total": total,
        },
    })
}

func (h *UserHandler) GetByID(c *gin.Context) {
    id, err := strconv.ParseInt(c.Param("id"), 10, 64)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }

    user, err := h.userService.GetByID(c.Request.Context(), id)
    if err != nil {
        log.Error().Err(err).Int64("id", id).Msg("Failed to get user")
        c.JSON(http.StatusNotFound, gin.H{
            "error": "User not found",
        })
        return
    }

    c.JSON(http.StatusOK, gin.H{
        "data": user,
    })
}

func (h *UserHandler) Create(c *gin.Context) {
    var req model.CreateUserRequest
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }

    user, err := h.userService.Create(c.Request.Context(), &req)
    if err != nil {
        log.Error().Err(err).Msg("Failed to create user")
        c.JSON(http.StatusInternalServerError, gin.H{
            "error": "Failed to create user",
        })
        return
    }

    c.JSON(http.StatusCreated, gin.H{
        "data": user,
    })
}

func (h *UserHandler) Update(c *gin.Context) {
    id, err := strconv.ParseInt(c.Param("id"), 10, 64)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }

    var req model.UpdateUserRequest
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": err.Error(),
        })
        return
    }

    user, err := h.userService.Update(c.Request.Context(), id, &req)
    if err != nil {
        log.Error().Err(err).Int64("id", id).Msg("Failed to update user")
        c.JSON(http.StatusInternalServerError, gin.H{
            "error": "Failed to update user",
        })
        return
    }

    c.JSON(http.StatusOK, gin.H{
        "data": user,
    })
}

func (h *UserHandler) Delete(c *gin.Context) {
    id, err := strconv.ParseInt(c.Param("id"), 10, 64)
    if err != nil {
        c.JSON(http.StatusBadRequest, gin.H{
            "error": "Invalid user ID",
        })
        return
    }

    if err := h.userService.Delete(c.Request.Context(), id); err != nil {
        log.Error().Err(err).Int64("id", id).Msg("Failed to delete user")
        c.JSON(http.StatusInternalServerError, gin.H{
            "error": "Failed to delete user",
        })
        return
    }

    c.Status(http.StatusNoContent)
}
```

### Service Layer
```go
// internal/service/user_service.go
package service

import (
    "context"
    "encoding/json"
    "fmt"
    "time"

    "github.com/go-redis/redis/v8"
    
    "myapp/internal/model"
    "myapp/internal/repository"
)

type UserService struct {
    repo  *repository.UserRepository
    cache *redis.Client
}

func NewUserService(repo *repository.UserRepository, cache *redis.Client) *UserService {
    return &UserService{
        repo:  repo,
        cache: cache,
    }
}

func (s *UserService) GetAll(ctx context.Context, page, limit int) ([]*model.User, int64, error) {
    offset := (page - 1) * limit
    return s.repo.FindAll(ctx, offset, limit)
}

func (s *UserService) GetByID(ctx context.Context, id int64) (*model.User, error) {
    // Try cache first
    cacheKey := fmt.Sprintf("user:%d", id)
    cached, err := s.cache.Get(ctx, cacheKey).Result()
    if err == nil {
        var user model.User
        if err := json.Unmarshal([]byte(cached), &user); err == nil {
            return &user, nil
        }
    }

    // Fetch from database
    user, err := s.repo.FindByID(ctx, id)
    if err != nil {
        return nil, err
    }

    // Cache the result
    userJSON, _ := json.Marshal(user)
    s.cache.Set(ctx, cacheKey, userJSON, 5*time.Minute)

    return user, nil
}

func (s *UserService) Create(ctx context.Context, req *model.CreateUserRequest) (*model.User, error) {
    user := &model.User{
        Email:     req.Email,
        Username:  req.Username,
        FirstName: req.FirstName,
        LastName:  req.LastName,
    }

    return s.repo.Create(ctx, user)
}

func (s *UserService) Update(ctx context.Context, id int64, req *model.UpdateUserRequest) (*model.User, error) {
    user, err := s.repo.FindByID(ctx, id)
    if err != nil {
        return nil, err
    }

    if req.Email != nil {
        user.Email = *req.Email
    }
    if req.FirstName != nil {
        user.FirstName = *req.FirstName
    }
    if req.LastName != nil {
        user.LastName = *req.LastName
    }

    updatedUser, err := s.repo.Update(ctx, user)
    if err != nil {
        return nil, err
    }

    // Invalidate cache
    cacheKey := fmt.Sprintf("user:%d", id)
    s.cache.Del(ctx, cacheKey)

    return updatedUser, nil
}

func (s *UserService) Delete(ctx context.Context, id int64) error {
    if err := s.repo.Delete(ctx, id); err != nil {
        return err
    }

    // Invalidate cache
    cacheKey := fmt.Sprintf("user:%d", id)
    s.cache.Del(ctx, cacheKey)

    return nil
}
```

### Repository
```go
// internal/repository/user_repository.go
package repository

import (
    "context"
    "database/sql"
    
    "myapp/internal/model"
)

type UserRepository struct {
    db *sql.DB
}

func NewUserRepository(db *sql.DB) *UserRepository {
    return &UserRepository{db: db}
}

func (r *UserRepository) FindAll(ctx context.Context, offset, limit int) ([]*model.User, int64, error) {
    query := `
        SELECT id, email, username, first_name, last_name, created_at, updated_at
        FROM users
        ORDER BY id
        LIMIT $1 OFFSET $2
    `

    rows, err := r.db.QueryContext(ctx, query, limit, offset)
    if err != nil {
        return nil, 0, err
    }
    defer rows.Close()

    var users []*model.User
    for rows.Next() {
        var user model.User
        if err := rows.Scan(
            &user.ID,
            &user.Email,
            &user.Username,
            &user.FirstName,
            &user.LastName,
            &user.CreatedAt,
            &user.UpdatedAt,
        ); err != nil {
            return nil, 0, err
        }
        users = append(users, &user)
    }

    // Get total count
    var total int64
    countQuery := "SELECT COUNT(*) FROM users"
    if err := r.db.QueryRowContext(ctx, countQuery).Scan(&total); err != nil {
        return nil, 0, err
    }

    return users, total, nil
}

func (r *UserRepository) FindByID(ctx context.Context, id int64) (*model.User, error) {
    query := `
        SELECT id, email, username, first_name, last_name, created_at, updated_at
        FROM users
        WHERE id = $1
    `

    var user model.User
    err := r.db.QueryRowContext(ctx, query, id).Scan(
        &user.ID,
        &user.Email,
        &user.Username,
        &user.FirstName,
        &user.LastName,
        &user.CreatedAt,
        &user.UpdatedAt,
    )
    if err != nil {
        return nil, err
    }

    return &user, nil
}

func (r *UserRepository) Create(ctx context.Context, user *model.User) (*model.User, error) {
    query := `
        INSERT INTO users (email, username, first_name, last_name)
        VALUES ($1, $2, $3, $4)
        RETURNING id, created_at, updated_at
    `

    err := r.db.QueryRowContext(
        ctx,
        query,
        user.Email,
        user.Username,
        user.FirstName,
        user.LastName,
    ).Scan(&user.ID, &user.CreatedAt, &user.UpdatedAt)

    if err != nil {
        return nil, err
    }

    return user, nil
}

func (r *UserRepository) Update(ctx context.Context, user *model.User) (*model.User, error) {
    query := `
        UPDATE users
        SET email = $1, first_name = $2, last_name = $3, updated_at = NOW()
        WHERE id = $4
        RETURNING updated_at
    `

    err := r.db.QueryRowContext(
        ctx,
        query,
        user.Email,
        user.FirstName,
        user.LastName,
        user.ID,
    ).Scan(&user.UpdatedAt)

    if err != nil {
        return nil, err
    }

    return user, nil
}

func (r *UserRepository) Delete(ctx context.Context, id int64) error {
    query := "DELETE FROM users WHERE id = $1"
    _, err := r.db.ExecContext(ctx, query, id)
    return err
}
```

## 🐳 Dockerfile

```dockerfile
# Build stage
FROM golang:1.22-alpine AS builder

WORKDIR /app

# Install dependencies
RUN apk add --no-cache git ca-certificates

# Copy go mod files
COPY go.mod go.sum ./
RUN go mod download

# Copy source code
COPY . .

# Build binary
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build \
    -ldflags='-w -s -extldflags "-static"' \
    -o /bin/app \
    ./cmd/api

# Runtime stage
FROM scratch

# Copy CA certificates
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/

# Copy binary
COPY --from=builder /bin/app /app

EXPOSE 8080

ENTRYPOINT ["/app"]
```

## 📦 Dependencies (go.mod)

```go
module myapp

go 1.22

require (
    github.com/gin-gonic/gin v1.9.1
    github.com/go-redis/redis/v8 v8.11.5
    github.com/jackc/pgx/v5 v5.5.1
    github.com/joho/godotenv v1.5.1
    github.com/rs/zerolog v1.31.0
    github.com/Azure/azure-sdk-for-go/sdk/azidentity v1.4.0
    github.com/Azure/azure-sdk-for-go/sdk/data/azcosmos v1.0.0
)
```

## 🚀 CI/CD Pipeline

```yaml
name: Go Deploy to Azure

on:
  push:
    branches: [ main ]

env:
  GO_VERSION: '1.22'
  AZURE_CONTAINER_REGISTRY: myacr
  IMAGE_NAME: mygoapp

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Set up Go
      uses: actions/setup-go@v5
      with:
        go-version: ${{ env.GO_VERSION }}
        cache: true
    
    - name: Run tests
      run: go test -v -race -coverprofile=coverage.out ./...
    
    - name: Build
      run: go build -v ./cmd/api
    
    - name: Login to ACR
      uses: azure/docker-login@v1
      with:
        login-server: ${{ env.AZURE_CONTAINER_REGISTRY }}.azurecr.io
        username: ${{ secrets.ACR_USERNAME }}
        password: ${{ secrets.ACR_PASSWORD }}
    
    - name: Build and push Docker image
      run: |
        docker build -t ${{ env.AZURE_CONTAINER_REGISTRY }}.azurecr.io/${{ env.IMAGE_NAME }}:${{ github.sha }} .
        docker push ${{ env.AZURE_CONTAINER_REGISTRY }}.azurecr.io/${{ env.IMAGE_NAME }}:${{ github.sha }}
```

## 💰 Cost Estimation

```yaml
Production (Container Apps):
  - Container Apps (1M requests): ~$40/month
  - PostgreSQL (GP 2 vCores): ~$220/month
  - Redis (Standard C1): ~$15/month
  Total: ~$275/month

Note: Go's efficiency means lower compute costs
```

## ⚡ Quick Start

```bash
# 1. Initialize module
go mod init myapp

# 2. Install dependencies
go get github.com/gin-gonic/gin
go get github.com/jackc/pgx/v5

# 3. Run locally
go run cmd/api/main.go

# 4. Build
go build -o app cmd/api/main.go

# 5. Deploy
docker build -t mygoapp .
az containerapp up --name mygoapp --image mygoapp
```

---

**Owner**: Platform Engineer  
**Última actualización**: Diciembre 2025
