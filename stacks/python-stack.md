# Python Stack - Azure App Service + Container Apps

## 📋 Overview

Stack optimizado para aplicaciones Python modernas en Azure, con soporte para FastAPI, Django, Flask, y data science workloads.

### Ideal Para
- ✅ REST APIs con FastAPI/Flask
- ✅ Web applications con Django
- ✅ Machine Learning APIs
- ✅ Data processing pipelines
- ✅ Automation scripts
- ✅ Microservices livianos
- ✅ Scientific computing workloads

### NO Usar Cuando
- ❌ High-performance real-time systems
- ❌ CPU-bound tasks con concurrencia masiva
- ❌ Legacy Python 2.x

### Ventajas
- 🚀 Desarrollo rápido y productivo
- 📊 Excelente para Data Science/ML
- 📦 PyPI ecosystem masivo
- 🔧 Sintaxis clara y legible
- 🤖 Amplio soporte ML/AI (TensorFlow, PyTorch)
- 👥 Gran comunidad y recursos

## 🏗️ Architecture Options

### Option 1: App Service (Web Apps)
```
Internet → Front Door → App Service (Python)
                             ↓
                      PostgreSQL
                      Redis Cache
                      Blob Storage
```

### Option 2: Container Apps (Microservices)
```
Internet → Front Door → Container Apps
                             ↓
                      Cosmos DB
                      Service Bus
                      Azure ML
```

### Option 3: Functions (Serverless)
```
HTTP/Events → Azure Functions (Python)
                   ↓
             Cosmos DB
             Storage Queue
             ML Model Endpoint
```

## 🛠️ Technology Stack

### Runtime & Framework
```yaml
Python Version:
  - Python 3.12 (latest)
  - Python 3.11 (recommended, stable)
  - Python 3.10 (widely supported)

Web Frameworks:
  - FastAPI (modern, async, type hints)
  - Flask (lightweight, flexible)
  - Django (batteries-included, ORM)
  - Sanic (async, high performance)
  - Tornado (async networking)

API Documentation:
  - FastAPI: Auto-generated OpenAPI
  - Flask: Flask-RESTX, Flasgger
  - Django: drf-spectacular
```

### Web Hosting
```yaml
Option A - Azure App Service:
  - Tier: Premium P1V3 or higher
  - OS: Linux (recommended)
  - Runtime: Python 3.11
  - WSGI Server: Gunicorn
  - Workers: 4-8 per instance
  - Auto-scale: 2-10 instances

Option B - Azure Container Apps:
  - Dockerfile-based
  - Scale to zero
  - Dapr integration
  - Better for ML workloads

Option C - Azure Functions:
  - Serverless Python
  - Event-driven
  - ML inference endpoints
```

### Database
```yaml
Relational:
  - Azure Database for PostgreSQL
    - ORM: SQLAlchemy, Django ORM
    - Driver: psycopg2-binary
  
  - Azure SQL Database
    - Driver: pyodbc, pymssql

NoSQL:
  - Cosmos DB (SQL API, MongoDB API)
    - SDK: azure-cosmos
  
  - MongoDB Atlas

ORM/Query:
  - SQLAlchemy (industry standard)
  - Django ORM (built-in)
  - Tortoise ORM (async)
  - Peewee (lightweight)
```

### Caching & Queues
```yaml
Caching:
  - Azure Cache for Redis
    - Library: redis-py
  - In-memory: cachetools

Message Queue:
  - Azure Service Bus
    - SDK: azure-servicebus
  - Azure Storage Queue
  - Celery + Redis/RabbitMQ

Task Queue:
  - Celery (distributed task queue)
  - Dramatiq
  - RQ (Redis Queue)
```

### Authentication
```yaml
Azure AD:
  - MSAL for Python
  - FastAPI/Flask middleware

JWT:
  - PyJWT
  - python-jose

OAuth 2.0:
  - Authlib
  - FastAPI OAuth2PasswordBearer
```

### Observability
```yaml
Application Insights:
  - SDK: opencensus-ext-azure
  - Azure Monitor OpenTelemetry

Logging:
  - Python logging (built-in)
  - Loguru (modern alternative)
  - structlog (structured logging)

Monitoring:
  - OpenTelemetry
  - Prometheus client
  - Sentry (error tracking)

Health Checks:
  - /health endpoint
  - healthcheck library
```

### Data Science & ML
```yaml
ML Frameworks:
  - TensorFlow / Keras
  - PyTorch
  - scikit-learn
  - XGBoost

Azure ML:
  - azureml-sdk
  - Model deployment
  - Managed endpoints

Data Processing:
  - Pandas
  - NumPy
  - Polars (faster alternative)
  - Dask (parallel computing)
```

## 📁 Project Structure

### FastAPI Structure
```
my-python-app/
├── app/
│   ├── __init__.py
│   ├── main.py                  # FastAPI app entry
│   ├── config.py                # Configuration
│   ├── dependencies.py          # DI
│   ├── api/
│   │   ├── __init__.py
│   │   ├── v1/
│   │   │   ├── __init__.py
│   │   │   ├── endpoints/
│   │   │   │   ├── users.py
│   │   │   │   ├── auth.py
│   │   │   │   └── orders.py
│   │   │   └── router.py
│   ├── models/
│   │   ├── __init__.py
│   │   ├── user.py
│   │   └── order.py
│   ├── schemas/
│   │   ├── __init__.py
│   │   ├── user.py              # Pydantic models
│   │   └── order.py
│   ├── services/
│   │   ├── __init__.py
│   │   ├── user_service.py
│   │   └── email_service.py
│   ├── repositories/
│   │   ├── __init__.py
│   │   └── user_repository.py
│   ├── middleware/
│   │   ├── __init__.py
│   │   ├── auth.py
│   │   └── logging.py
│   ├── utils/
│   │   ├── __init__.py
│   │   ├── logger.py
│   │   └── exceptions.py
│   └── core/
│       ├── __init__.py
│       ├── database.py
│       ├── security.py
│       └── cache.py
├── tests/
│   ├── __init__.py
│   ├── unit/
│   ├── integration/
│   └── conftest.py
├── alembic/                     # DB migrations
│   ├── versions/
│   └── env.py
├── infrastructure/
│   └── main.bicep
├── .github/
│   └── workflows/
│       └── deploy.yml
├── requirements.txt
├── requirements-dev.txt
├── pyproject.toml               # Modern Python config
├── Dockerfile
├── .dockerignore
├── .env.example
├── alembic.ini
└── README.md
```

## 🚀 Sample Implementation

### FastAPI Application
```python
# app/main.py
from fastapi import FastAPI, Request
from fastapi.middleware.cors import CORSMiddleware
from fastapi.middleware.gzip import GZipMiddleware
from fastapi.responses import JSONResponse
from contextlib import asynccontextmanager
import logging
from opencensus.ext.azure.log_exporter import AzureLogHandler

from app.api.v1.router import api_router
from app.config import settings
from app.core.database import engine, Base
from app.middleware.logging import LoggingMiddleware
from app.utils.exceptions import AppException

# Configure logging
logger = logging.getLogger(__name__)
if settings.APPLICATIONINSIGHTS_CONNECTION_STRING:
    logger.addHandler(
        AzureLogHandler(
            connection_string=settings.APPLICATIONINSIGHTS_CONNECTION_STRING
        )
    )

@asynccontextmanager
async def lifespan(app: FastAPI):
    # Startup
    logger.info("Starting application...")
    async with engine.begin() as conn:
        await conn.run_sync(Base.metadata.create_all)
    yield
    # Shutdown
    logger.info("Shutting down application...")
    await engine.dispose()

app = FastAPI(
    title=settings.PROJECT_NAME,
    version=settings.VERSION,
    openapi_url=f"{settings.API_V1_PREFIX}/openapi.json",
    docs_url="/docs",
    redoc_url="/redoc",
    lifespan=lifespan
)

# CORS
app.add_middleware(
    CORSMiddleware,
    allow_origins=settings.ALLOWED_ORIGINS,
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# Compression
app.add_middleware(GZipMiddleware, minimum_size=1000)

# Custom logging middleware
app.add_middleware(LoggingMiddleware)

# Exception handler
@app.exception_handler(AppException)
async def app_exception_handler(request: Request, exc: AppException):
    return JSONResponse(
        status_code=exc.status_code,
        content={"detail": exc.message}
    )

# Health check
@app.get("/health")
async def health_check():
    return {
        "status": "healthy",
        "version": settings.VERSION
    }

# Include API router
app.include_router(api_router, prefix=settings.API_V1_PREFIX)

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(
        "app.main:app",
        host="0.0.0.0",
        port=8000,
        reload=settings.DEBUG,
        workers=4
    )
```

### Configuration
```python
# app/config.py
from pydantic_settings import BaseSettings
from typing import List
from functools import lru_cache

class Settings(BaseSettings):
    # App
    PROJECT_NAME: str = "My Python API"
    VERSION: str = "1.0.0"
    DEBUG: bool = False
    API_V1_PREFIX: str = "/api/v1"
    
    # Database
    DATABASE_URL: str
    
    # Redis
    REDIS_URL: str
    
    # Azure
    AZURE_STORAGE_CONNECTION_STRING: str | None = None
    APPLICATIONINSIGHTS_CONNECTION_STRING: str | None = None
    
    # Security
    SECRET_KEY: str
    ALGORITHM: str = "HS256"
    ACCESS_TOKEN_EXPIRE_MINUTES: int = 30
    
    # CORS
    ALLOWED_ORIGINS: List[str] = ["*"]
    
    class Config:
        env_file = ".env"
        case_sensitive = True

@lru_cache()
def get_settings() -> Settings:
    return Settings()

settings = get_settings()
```

### Database Setup (SQLAlchemy 2.0)
```python
# app/core/database.py
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession, async_sessionmaker
from sqlalchemy.orm import DeclarativeBase
from app.config import settings

# Create async engine
engine = create_async_engine(
    settings.DATABASE_URL,
    echo=settings.DEBUG,
    pool_pre_ping=True,
    pool_size=5,
    max_overflow=10
)

# Session factory
AsyncSessionLocal = async_sessionmaker(
    engine,
    class_=AsyncSession,
    expire_on_commit=False
)

# Base class for models
class Base(DeclarativeBase):
    pass

# Dependency for FastAPI
async def get_db():
    async with AsyncSessionLocal() as session:
        try:
            yield session
            await session.commit()
        except Exception:
            await session.rollback()
            raise
        finally:
            await session.close()
```

### Model Example
```python
# app/models/user.py
from sqlalchemy import String, Boolean, DateTime
from sqlalchemy.orm import Mapped, mapped_column
from datetime import datetime
from app.core.database import Base

class User(Base):
    __tablename__ = "users"
    
    id: Mapped[int] = mapped_column(primary_key=True, index=True)
    email: Mapped[str] = mapped_column(String(255), unique=True, index=True)
    username: Mapped[str] = mapped_column(String(50), unique=True)
    hashed_password: Mapped[str] = mapped_column(String(255))
    is_active: Mapped[bool] = mapped_column(Boolean, default=True)
    is_superuser: Mapped[bool] = mapped_column(Boolean, default=False)
    created_at: Mapped[datetime] = mapped_column(DateTime, default=datetime.utcnow)
    updated_at: Mapped[datetime] = mapped_column(
        DateTime, 
        default=datetime.utcnow, 
        onupdate=datetime.utcnow
    )
```

### Pydantic Schemas
```python
# app/schemas/user.py
from pydantic import BaseModel, EmailStr, Field
from datetime import datetime

class UserBase(BaseModel):
    email: EmailStr
    username: str = Field(..., min_length=3, max_length=50)

class UserCreate(UserBase):
    password: str = Field(..., min_length=8)

class UserUpdate(BaseModel):
    email: EmailStr | None = None
    username: str | None = None
    password: str | None = None

class UserInDB(UserBase):
    id: int
    is_active: bool
    is_superuser: bool
    created_at: datetime
    updated_at: datetime
    
    class Config:
        from_attributes = True

class User(UserInDB):
    pass
```

### API Endpoint
```python
# app/api/v1/endpoints/users.py
from fastapi import APIRouter, Depends, HTTPException, status
from sqlalchemy.ext.asyncio import AsyncSession
from typing import List

from app.core.database import get_db
from app.schemas.user import User, UserCreate, UserUpdate
from app.services.user_service import UserService

router = APIRouter()

@router.get("/", response_model=List[User])
async def get_users(
    skip: int = 0,
    limit: int = 100,
    db: AsyncSession = Depends(get_db)
):
    """Get all users with pagination."""
    service = UserService(db)
    users = await service.get_users(skip=skip, limit=limit)
    return users

@router.get("/{user_id}", response_model=User)
async def get_user(
    user_id: int,
    db: AsyncSession = Depends(get_db)
):
    """Get user by ID."""
    service = UserService(db)
    user = await service.get_user(user_id)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail="User not found"
        )
    return user

@router.post("/", response_model=User, status_code=status.HTTP_201_CREATED)
async def create_user(
    user_in: UserCreate,
    db: AsyncSession = Depends(get_db)
):
    """Create new user."""
    service = UserService(db)
    
    # Check if user exists
    if await service.get_user_by_email(user_in.email):
        raise HTTPException(
            status_code=status.HTTP_400_BAD_REQUEST,
            detail="Email already registered"
        )
    
    user = await service.create_user(user_in)
    return user

@router.put("/{user_id}", response_model=User)
async def update_user(
    user_id: int,
    user_in: UserUpdate,
    db: AsyncSession = Depends(get_db)
):
    """Update user."""
    service = UserService(db)
    user = await service.update_user(user_id, user_in)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail="User not found"
        )
    return user

@router.delete("/{user_id}", status_code=status.HTTP_204_NO_CONTENT)
async def delete_user(
    user_id: int,
    db: AsyncSession = Depends(get_db)
):
    """Delete user."""
    service = UserService(db)
    success = await service.delete_user(user_id)
    if not success:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail="User not found"
        )
```

### Service Layer
```python
# app/services/user_service.py
from sqlalchemy import select
from sqlalchemy.ext.asyncio import AsyncSession
from passlib.context import CryptContext

from app.models.user import User
from app.schemas.user import UserCreate, UserUpdate

pwd_context = CryptContext(schemes=["bcrypt"], deprecated="auto")

class UserService:
    def __init__(self, db: AsyncSession):
        self.db = db
    
    async def get_users(self, skip: int = 0, limit: int = 100):
        result = await self.db.execute(
            select(User).offset(skip).limit(limit)
        )
        return result.scalars().all()
    
    async def get_user(self, user_id: int):
        result = await self.db.execute(
            select(User).where(User.id == user_id)
        )
        return result.scalar_one_or_none()
    
    async def get_user_by_email(self, email: str):
        result = await self.db.execute(
            select(User).where(User.email == email)
        )
        return result.scalar_one_or_none()
    
    async def create_user(self, user_in: UserCreate):
        hashed_password = pwd_context.hash(user_in.password)
        
        db_user = User(
            email=user_in.email,
            username=user_in.username,
            hashed_password=hashed_password
        )
        
        self.db.add(db_user)
        await self.db.flush()
        await self.db.refresh(db_user)
        
        return db_user
    
    async def update_user(self, user_id: int, user_in: UserUpdate):
        user = await self.get_user(user_id)
        if not user:
            return None
        
        update_data = user_in.model_dump(exclude_unset=True)
        
        if "password" in update_data:
            update_data["hashed_password"] = pwd_context.hash(
                update_data.pop("password")
            )
        
        for field, value in update_data.items():
            setattr(user, field, value)
        
        await self.db.flush()
        await self.db.refresh(user)
        
        return user
    
    async def delete_user(self, user_id: int):
        user = await self.get_user(user_id)
        if not user:
            return False
        
        await self.db.delete(user)
        return True
```

## 🐳 Dockerfile

```dockerfile
# Build stage
FROM python:3.11-slim as builder

WORKDIR /app

# Install system dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc libpq-dev && \
    rm -rf /var/lib/apt/lists/*

# Copy requirements
COPY requirements.txt .

# Install Python dependencies
RUN pip wheel --no-cache-dir --no-deps --wheel-dir /app/wheels -r requirements.txt

# Production stage
FROM python:3.11-slim

WORKDIR /app

# Install runtime dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends libpq5 && \
    rm -rf /var/lib/apt/lists/*

# Copy wheels from builder
COPY --from=builder /app/wheels /wheels
COPY --from=builder /app/requirements.txt .

# Install Python packages
RUN pip install --no-cache /wheels/*

# Copy application code
COPY ./app ./app
COPY alembic.ini .
COPY ./alembic ./alembic

# Create non-root user
RUN useradd -m -u 1000 appuser && chown -R appuser:appuser /app
USER appuser

# Expose port
EXPOSE 8000

# Run with Gunicorn
CMD ["gunicorn", "app.main:app", \
     "--workers", "4", \
     "--worker-class", "uvicorn.workers.UvicornWorker", \
     "--bind", "0.0.0.0:8000", \
     "--timeout", "120", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

## 📦 Dependencies

### requirements.txt
```txt
# Web Framework
fastapi==0.109.0
uvicorn[standard]==0.27.0
gunicorn==21.2.0
python-multipart==0.0.6

# Database
sqlalchemy[asyncio]==2.0.25
asyncpg==0.29.0
alembic==1.13.1

# Redis
redis==5.0.1
hiredis==2.3.2

# Azure SDKs
azure-identity==1.15.0
azure-keyvault-secrets==4.7.0
azure-storage-blob==12.19.0
azure-servicebus==7.11.4

# Security
passlib[bcrypt]==1.7.4
python-jose[cryptography]==3.3.0
pydantic[email]==2.5.3
pydantic-settings==2.1.0

# Monitoring
opencensus-ext-azure==1.1.13
opencensus-ext-requests==0.13.0
opencensus-ext-sqlalchemy==0.1.4

# Utilities
python-dotenv==1.0.0
httpx==0.26.0
```

### requirements-dev.txt
```txt
# Testing
pytest==7.4.4
pytest-asyncio==0.23.3
pytest-cov==4.1.0
httpx==0.26.0

# Linting & Formatting
black==24.1.1
ruff==0.1.14
mypy==1.8.0

# Database testing
pytest-postgresql==5.0.0
```

## 🚀 CI/CD Pipeline

```yaml
name: Python Deploy to Azure

on:
  push:
    branches: [ main, develop ]

env:
  PYTHON_VERSION: '3.11'
  AZURE_WEBAPP_NAME: app-mypythonapp-prod

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Set up Python
      uses: actions/setup-python@v5
      with:
        python-version: ${{ env.PYTHON_VERSION }}
        cache: 'pip'
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt -r requirements-dev.txt
    
    - name: Lint with ruff
      run: ruff check app/
    
    - name: Type check with mypy
      run: mypy app/
      continue-on-error: true
    
    - name: Run tests
      run: |
        pytest --cov=app --cov-report=xml --cov-report=html
    
    - name: Upload coverage
      uses: codecov/codecov-action@v3
      with:
        file: ./coverage.xml
    
    - name: Build artifact
      run: |
        zip -r app.zip app/ requirements.txt alembic/ alembic.ini
    
    - name: Upload artifact
      uses: actions/upload-artifact@v4
      with:
        name: python-app
        path: app.zip

  deploy:
    runs-on: ubuntu-latest
    needs: build
    if: github.ref == 'refs/heads/main'
    
    steps:
    - name: Download artifact
      uses: actions/download-artifact@v4
      with:
        name: python-app
    
    - name: Unzip artifact
      run: unzip app.zip
    
    - name: Login to Azure
      uses: azure/login@v1
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}
    
    - name: Deploy to App Service
      uses: azure/webapps-deploy@v3
      with:
        app-name: ${{ env.AZURE_WEBAPP_NAME }}
        package: .
    
    - name: Run migrations
      run: |
        # Install alembic
        pip install alembic asyncpg
        # Run migrations
        alembic upgrade head
      env:
        DATABASE_URL: ${{ secrets.DATABASE_URL }}
    
    - name: Health Check
      run: |
        sleep 30
        curl -f https://${{ env.AZURE_WEBAPP_NAME }}.azurewebsites.net/health || exit 1
```

## 💰 Cost Estimation

```yaml
Production (App Service):
  - App Service P1V3 (2 instances): ~$380/month
  - PostgreSQL (GP 2 vCores): ~$220/month
  - Redis (Standard C1): ~$15/month
  - App Insights: ~$50/month
  Total: ~$665/month

With ML Workload:
  - Add Azure ML Managed Endpoint: ~$100-500/month
  - Add GPU instances (if needed): ~$500-2000/month
```

## ⚡ Quick Start

```bash
# 1. Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 2. Install FastAPI
pip install "fastapi[all]" sqlalchemy asyncpg

# 3. Create basic app
# (copy app/main.py from examples above)

# 4. Run locally
uvicorn app.main:app --reload

# 5. Deploy to Azure
az webapp up --runtime "PYTHON:3.11" --name mypythonapp --sku B1
```

---

**Owner**: Platform Engineer  
**Última actualización**: Diciembre 2025
