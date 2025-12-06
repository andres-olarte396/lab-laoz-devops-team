# Node.js Stack - Azure App Service + Container Apps

## 📋 Overview

Stack optimizado para aplicaciones Node.js modernas en Azure, con soporte para Express, Nest.js, y arquitecturas serverless.

### Ideal Para
- ✅ REST APIs con Express/Fastify
- ✅ Aplicaciones Nest.js enterprise
- ✅ GraphQL servers (Apollo)
- ✅ Real-time apps (Socket.io, WebSockets)
- ✅ Server-side rendering (Next.js, Nuxt.js)
- ✅ Microservices livianos
- ✅ Equipos JavaScript/TypeScript

### NO Usar Cuando
- ❌ CPU-intensive workloads (usar .NET/Go)
- ❌ Heavy numerical computation
- ❌ Legacy Node.js <16

### Ventajas
- 🚀 Desarrollo rápido
- 📦 NPM ecosystem masivo
- ⚡ Event-driven, non-blocking I/O
- 🔄 Isomorfismo (client + server)
- 👥 Amplio talento disponible
- 🛠️ Tooling moderno (TypeScript, ESM)

## 🏗️ Architecture Options

### Option 1: App Service (Simple deployment)
```
Internet → Front Door → App Service (Node.js)
                             ↓
                      PostgreSQL / MongoDB
                      Redis Cache
                      Blob Storage
```

### Option 2: Container Apps (Microservices)
```
Internet → Front Door → Container Apps
                             ↓
                      Cosmos DB
                      Service Bus
                      Dapr Integration
```

### Option 3: Serverless (Event-driven)
```
HTTP/Events → Azure Functions (Node.js)
                   ↓
             Cosmos DB
             Storage Queue
```

## 🛠️ Technology Stack

### Runtime & Framework
```yaml
Node.js Version:
  - Node.js 20 LTS (recommended, support until April 2026)
  - Node.js 18 LTS (support until April 2025)

Language:
  - TypeScript 5.x (strongly recommended)
  - JavaScript ES2023

Web Frameworks:
  - Express.js 4.x (minimalist, flexible)
  - Fastify (high performance)
  - Nest.js (enterprise, opinionated)
  - Koa.js (next-gen Express)
  
API Styles:
  - REST (standard)
  - GraphQL (Apollo Server)
  - tRPC (type-safe RPC)
  - gRPC (microservices)

Real-time:
  - Socket.io
  - ws (WebSocket library)
  - Server-Sent Events
```

### Web Hosting
```yaml
Option A - Azure App Service:
  - Tier: Premium P1V3 or higher
  - OS: Linux (recommended)
  - Runtime: Node 20 LTS
  - Auto-scale: 2-10 instances
  - PM2 for process management

Option B - Azure Container Apps:
  - Dockerfile-based deployment
  - Scale to zero capability
  - Dapr integration
  - Better for microservices

Option C - Azure Functions:
  - Serverless Node.js
  - Event-driven
  - Consumption or Premium plan
```

### Database
```yaml
Relational:
  - Azure Database for PostgreSQL
    - ORM: Prisma, TypeORM, Sequelize
  - Azure SQL Database
    - Driver: mssql, tedious

NoSQL:
  - Cosmos DB (MongoDB API or SQL API)
    - SDK: @azure/cosmos
  - MongoDB Atlas (alternative)

ORM/Query Builders:
  - Prisma (modern, type-safe)
  - TypeORM (enterprise)
  - Sequelize (mature)
  - Drizzle (lightweight)
  - Knex.js (query builder)
```

### Caching & Queues
```yaml
Caching:
  - Azure Cache for Redis
    - Library: ioredis
  - In-memory: node-cache

Message Queue:
  - Azure Service Bus
    - SDK: @azure/service-bus
  - Azure Storage Queue
  - RabbitMQ (self-hosted on AKS)
  
Pub/Sub:
  - Azure Event Grid
  - Redis Pub/Sub
```

### Authentication
```yaml
Azure AD / B2C:
  - Library: @azure/msal-node
  - Passport.js strategies
  
JWT:
  - jsonwebtoken
  - jose (modern, secure)
  
OAuth 2.0:
  - Passport.js
  - Grant
```

### Observability
```yaml
Application Insights:
  - SDK: applicationinsights
  - Auto-instrumentation
  - Custom telemetry

Logging:
  - Winston (structured logging)
  - Pino (high performance)
  - Morgan (HTTP request logging)

Distributed Tracing:
  - OpenTelemetry
  - Application Insights

Health Checks:
  - Custom /health endpoint
  - @godaddy/terminus
```

### Security
```yaml
Secrets:
  - Azure Key Vault
  - SDK: @azure/keyvault-secrets
  - Environment variables

API Security:
  - Helmet.js (HTTP headers)
  - express-rate-limit
  - cors
  - express-validator
  - joi / zod (validation)

Dependency Scanning:
  - npm audit
  - Snyk
  - Dependabot
```

## 📁 Project Structure

### Express + TypeScript Structure
```
my-nodejs-app/
├── src/
│   ├── controllers/
│   │   ├── user.controller.ts
│   │   ├── auth.controller.ts
│   │   └── order.controller.ts
│   ├── services/
│   │   ├── user.service.ts
│   │   └── email.service.ts
│   ├── repositories/
│   │   └── user.repository.ts
│   ├── models/
│   │   └── user.model.ts
│   ├── middleware/
│   │   ├── auth.middleware.ts
│   │   ├── error.middleware.ts
│   │   └── validation.middleware.ts
│   ├── routes/
│   │   ├── index.ts
│   │   ├── user.routes.ts
│   │   └── auth.routes.ts
│   ├── config/
│   │   ├── database.ts
│   │   ├── redis.ts
│   │   └── app.ts
│   ├── utils/
│   │   ├── logger.ts
│   │   └── errors.ts
│   ├── types/
│   │   └── express.d.ts
│   ├── app.ts
│   └── server.ts
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── infrastructure/
│   └── main.bicep
├── .github/
│   └── workflows/
│       └── deploy.yml
├── package.json
├── tsconfig.json
├── .env.example
├── Dockerfile
├── .dockerignore
├── .eslintrc.js
├── .prettierrc
└── README.md
```

## 🚀 Sample Implementation

### TypeScript Configuration
```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "commonjs",
    "lib": ["ES2022"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist", "tests"]
}
```

### Application Entry Point
```typescript
// src/server.ts
import app from './app';
import config from './config/app';
import logger from './utils/logger';

const PORT = config.port || 3000;

const server = app.listen(PORT, () => {
  logger.info(`Server running on port ${PORT} in ${config.environment} mode`);
});

// Graceful shutdown
process.on('SIGTERM', () => {
  logger.info('SIGTERM received, shutting down gracefully');
  server.close(() => {
    logger.info('Process terminated');
    process.exit(0);
  });
});

process.on('unhandledRejection', (reason, promise) => {
  logger.error('Unhandled Rejection at:', promise, 'reason:', reason);
  server.close(() => process.exit(1));
});

export default server;
```

### Express Application Setup
```typescript
// src/app.ts
import express, { Application, Request, Response, NextFunction } from 'express';
import helmet from 'helmet';
import cors from 'cors';
import compression from 'compression';
import morgan from 'morgan';
import rateLimit from 'express-rate-limit';
import { ApplicationInsights } from 'applicationinsights';
import routes from './routes';
import { errorHandler } from './middleware/error.middleware';
import logger from './utils/logger';
import config from './config/app';

// Initialize Application Insights
if (config.appInsights.connectionString) {
  ApplicationInsights.setup(config.appInsights.connectionString)
    .setAutoDependencyCorrelation(true)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .setAutoCollectConsole(true)
    .setUseDiskRetryCaching(true)
    .start();
}

const app: Application = express();

// Security middleware
app.use(helmet());
app.use(cors({
  origin: config.corsOrigins,
  credentials: true
}));

// Rate limiting
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // limit each IP to 100 requests per windowMs
  message: 'Too many requests from this IP, please try again later.'
});
app.use('/api/', limiter);

// Body parsing
app.use(express.json({ limit: '10mb' }));
app.use(express.urlencoded({ extended: true, limit: '10mb' }));

// Compression
app.use(compression());

// HTTP request logging
app.use(morgan('combined', {
  stream: { write: message => logger.info(message.trim()) }
}));

// Health check endpoint
app.get('/health', (req: Request, res: Response) => {
  res.status(200).json({
    status: 'healthy',
    timestamp: new Date().toISOString(),
    uptime: process.uptime()
  });
});

// API routes
app.use('/api', routes);

// 404 handler
app.use((req: Request, res: Response) => {
  res.status(404).json({
    error: 'Not Found',
    message: `Cannot ${req.method} ${req.path}`
  });
});

// Error handling middleware
app.use(errorHandler);

export default app;
```

### Controller Example
```typescript
// src/controllers/user.controller.ts
import { Request, Response, NextFunction } from 'express';
import { UserService } from '../services/user.service';
import { CreateUserDto, UpdateUserDto } from '../types/user.types';
import { AppError } from '../utils/errors';
import logger from '../utils/logger';

export class UserController {
  constructor(private userService: UserService) {}

  async getAllUsers(req: Request, res: Response, next: NextFunction) {
    try {
      const page = parseInt(req.query.page as string) || 1;
      const limit = parseInt(req.query.limit as string) || 10;

      const users = await this.userService.findAll(page, limit);
      
      res.status(200).json({
        success: true,
        data: users,
        pagination: {
          page,
          limit,
          total: users.length
        }
      });
    } catch (error) {
      next(error);
    }
  }

  async getUserById(req: Request, res: Response, next: NextFunction) {
    try {
      const { id } = req.params;
      const user = await this.userService.findById(id);

      if (!user) {
        throw new AppError(404, 'User not found');
      }

      res.status(200).json({
        success: true,
        data: user
      });
    } catch (error) {
      next(error);
    }
  }

  async createUser(req: Request, res: Response, next: NextFunction) {
    try {
      const createUserDto: CreateUserDto = req.body;
      const user = await this.userService.create(createUserDto);

      logger.info(`User created: ${user.id}`);

      res.status(201).json({
        success: true,
        data: user
      });
    } catch (error) {
      next(error);
    }
  }

  async updateUser(req: Request, res: Response, next: NextFunction) {
    try {
      const { id } = req.params;
      const updateUserDto: UpdateUserDto = req.body;

      const user = await this.userService.update(id, updateUserDto);

      if (!user) {
        throw new AppError(404, 'User not found');
      }

      res.status(200).json({
        success: true,
        data: user
      });
    } catch (error) {
      next(error);
    }
  }

  async deleteUser(req: Request, res: Response, next: NextFunction) {
    try {
      const { id } = req.params;
      await this.userService.delete(id);

      res.status(204).send();
    } catch (error) {
      next(error);
    }
  }
}
```

### Service Layer with Prisma
```typescript
// src/services/user.service.ts
import { PrismaClient } from '@prisma/client';
import { CreateUserDto, UpdateUserDto } from '../types/user.types';
import { AppError } from '../utils/errors';
import bcrypt from 'bcryptjs';

const prisma = new PrismaClient();

export class UserService {
  async findAll(page: number, limit: number) {
    const skip = (page - 1) * limit;

    return await prisma.user.findMany({
      skip,
      take: limit,
      select: {
        id: true,
        email: true,
        name: true,
        createdAt: true,
        // Exclude password
      }
    });
  }

  async findById(id: string) {
    return await prisma.user.findUnique({
      where: { id },
      select: {
        id: true,
        email: true,
        name: true,
        createdAt: true
      }
    });
  }

  async create(data: CreateUserDto) {
    // Check if user exists
    const existing = await prisma.user.findUnique({
      where: { email: data.email }
    });

    if (existing) {
      throw new AppError(400, 'User with this email already exists');
    }

    // Hash password
    const hashedPassword = await bcrypt.hash(data.password, 10);

    return await prisma.user.create({
      data: {
        ...data,
        password: hashedPassword
      },
      select: {
        id: true,
        email: true,
        name: true,
        createdAt: true
      }
    });
  }

  async update(id: string, data: UpdateUserDto) {
    return await prisma.user.update({
      where: { id },
      data,
      select: {
        id: true,
        email: true,
        name: true,
        updatedAt: true
      }
    });
  }

  async delete(id: string) {
    return await prisma.user.delete({
      where: { id }
    });
  }
}
```

### Error Handling Middleware
```typescript
// src/middleware/error.middleware.ts
import { Request, Response, NextFunction } from 'express';
import { AppError } from '../utils/errors';
import logger from '../utils/logger';

export function errorHandler(
  err: Error,
  req: Request,
  res: Response,
  next: NextFunction
) {
  logger.error('Error:', {
    message: err.message,
    stack: err.stack,
    url: req.url,
    method: req.method
  });

  if (err instanceof AppError) {
    return res.status(err.statusCode).json({
      success: false,
      error: {
        message: err.message,
        statusCode: err.statusCode
      }
    });
  }

  // Prisma errors
  if (err.name === 'PrismaClientKnownRequestError') {
    return res.status(400).json({
      success: false,
      error: {
        message: 'Database error',
        statusCode: 400
      }
    });
  }

  // Default error
  res.status(500).json({
    success: false,
    error: {
      message: process.env.NODE_ENV === 'production' 
        ? 'Internal server error' 
        : err.message,
      statusCode: 500
    }
  });
}
```

## 🐳 Dockerfile

```dockerfile
# Build stage
FROM node:20-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./
COPY tsconfig.json ./

# Install dependencies
RUN npm ci

# Copy source code
COPY src ./src

# Build TypeScript
RUN npm run build

# Production stage
FROM node:20-alpine

WORKDIR /app

# Install production dependencies only
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

# Copy built files from builder
COPY --from=builder /app/dist ./dist

# Create non-root user
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

USER nodejs

EXPOSE 3000

CMD ["node", "dist/server.js"]
```

## 🚀 CI/CD Pipeline

### GitHub Actions
```yaml
name: Node.js Deploy to Azure

on:
  push:
    branches: [ main, develop ]

env:
  NODE_VERSION: '20.x'
  AZURE_WEBAPP_NAME: app-mynodeapp-prod

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: ${{ env.NODE_VERSION }}
        cache: 'npm'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run linter
      run: npm run lint
    
    - name: Run tests
      run: npm test
    
    - name: Build TypeScript
      run: npm run build
    
    - name: Upload artifact
      uses: actions/upload-artifact@v4
      with:
        name: node-app
        path: |
          dist/
          package*.json
          node_modules/

  deploy:
    runs-on: ubuntu-latest
    needs: build
    if: github.ref == 'refs/heads/main'
    
    steps:
    - name: Download artifact
      uses: actions/download-artifact@v4
      with:
        name: node-app
    
    - name: Login to Azure
      uses: azure/login@v1
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}
    
    - name: Deploy to App Service
      uses: azure/webapps-deploy@v3
      with:
        app-name: ${{ env.AZURE_WEBAPP_NAME }}
        package: .
    
    - name: Health Check
      run: |
        sleep 30
        curl -f https://${{ env.AZURE_WEBAPP_NAME }}.azurewebsites.net/health || exit 1
```

## 📦 Package.json

```json
{
  "name": "my-nodejs-app",
  "version": "1.0.0",
  "description": "Node.js API on Azure",
  "main": "dist/server.js",
  "scripts": {
    "dev": "ts-node-dev --respawn --transpile-only src/server.ts",
    "build": "tsc",
    "start": "node dist/server.js",
    "test": "jest --coverage",
    "test:watch": "jest --watch",
    "lint": "eslint src/**/*.ts",
    "lint:fix": "eslint src/**/*.ts --fix",
    "format": "prettier --write \"src/**/*.ts\"",
    "prisma:generate": "prisma generate",
    "prisma:migrate": "prisma migrate deploy"
  },
  "dependencies": {
    "express": "^4.18.2",
    "helmet": "^7.1.0",
    "cors": "^2.8.5",
    "compression": "^1.7.4",
    "express-rate-limit": "^7.1.5",
    "morgan": "^1.10.0",
    "applicationinsights": "^2.9.1",
    "@prisma/client": "^5.7.1",
    "ioredis": "^5.3.2",
    "@azure/identity": "^4.0.0",
    "@azure/keyvault-secrets": "^4.7.0",
    "@azure/service-bus": "^7.9.3",
    "bcryptjs": "^2.4.3",
    "jsonwebtoken": "^9.0.2",
    "winston": "^3.11.0",
    "joi": "^17.11.0"
  },
  "devDependencies": {
    "@types/express": "^4.17.21",
    "@types/node": "^20.10.5",
    "@types/bcryptjs": "^2.4.6",
    "@types/jsonwebtoken": "^9.0.5",
    "@types/morgan": "^1.9.9",
    "@types/compression": "^1.7.5",
    "@types/cors": "^2.8.17",
    "@typescript-eslint/eslint-plugin": "^6.15.0",
    "@typescript-eslint/parser": "^6.15.0",
    "eslint": "^8.56.0",
    "prettier": "^3.1.1",
    "ts-node-dev": "^2.0.0",
    "typescript": "^5.3.3",
    "jest": "^29.7.0",
    "@types/jest": "^29.5.11",
    "ts-jest": "^29.1.1",
    "supertest": "^6.3.3",
    "@types/supertest": "^6.0.2",
    "prisma": "^5.7.1"
  },
  "engines": {
    "node": ">=20.0.0",
    "npm": ">=10.0.0"
  }
}
```

## 💰 Cost Estimation

```yaml
Production (App Service):
  - App Service P1V3 (2 instances): ~$380/month
  - PostgreSQL (GP 2 vCores): ~$220/month
  - Redis (Standard C1): ~$15/month
  - App Insights: ~$50/month
  Total: ~$665/month

Production (Container Apps):
  - Container Apps (1M requests): ~$40/month
  - PostgreSQL: ~$220/month
  - Redis: ~$15/month
  Total: ~$275/month (if low traffic)
```

## ⚡ Quick Start

```bash
# 1. Create project
mkdir my-nodejs-app && cd my-nodejs-app
npm init -y

# 2. Install dependencies
npm install express helmet cors compression
npm install -D typescript @types/node @types/express ts-node-dev

# 3. Initialize TypeScript
npx tsc --init

# 4. Create basic server
# (copy src/server.ts and src/app.ts from examples above)

# 5. Run locally
npm run dev

# 6. Deploy to Azure
az webapp up --runtime "NODE:20-lts" --name mynodeapp
```

---

**Owner**: Platform Engineer  
**Última actualización**: Diciembre 2025
