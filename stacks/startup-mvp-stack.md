# Startup MVP Stack - Rapid Launch

## 📋 Overview

Stack optimizado para startups que necesitan lanzar un MVP (Minimum Viable Product) rápidamente con presupuesto limitado, pero con capacidad de escalar.

### Ideal Para
- ✅ Startups en etapa seed/pre-seed
- ✅ MVPs y prototipos
- ✅ Validación de producto
- ✅ Pruebas de mercado
- ✅ Demos para inversionistas
- ✅ Hackathons y POCs
- ✅ Side projects con potencial comercial

### NO Usar Cuando
- ❌ Aplicaciones enterprise desde día 1
- ❌ Requisitos de compliance estrictos (HIPAA, PCI-DSS)
- ❌ Alto volumen de tráfico garantizado (>100K usuarios/mes)
- ❌ Mission-critical systems

### Ventajas
- 💰 **Costo ultra bajo**: $50-300/mes
- ⚡ **Time-to-market**: 1-2 semanas
- 🚀 **Escalabilidad incorporada**: Fácil upgrade cuando creces
- 🔧 **Low maintenance**: Servicios managed
- 🎯 **Focus en producto**: Menos infraestructura, más features
- 📊 **Analytics desde día 1**: Insights de usuarios

### Principios MVP
```yaml
1. Ship Fast: Lanzar en semanas, no meses
2. Minimize Costs: Cada dólar cuenta
3. Validate First: Probar antes de escalar
4. Keep It Simple: KISS principle
5. Measure Everything: Data-driven decisions
6. Plan for Growth: Arquitectura que escala
```

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────┐
│              Users (Web/Mobile)                 │
└────────────────────┬────────────────────────────┘
                     │
                     ▼
         ┌───────────────────────┐
         │   Azure Front Door    │ ← CDN + WAF
         │   (Optional, later)   │
         └───────────┬───────────┘
                     │
         ┌───────────▼────────────┐
         │   Azure App Service    │ ← Main App (B1)
         │   (Linux, Node/Python) │
         └───────────┬────────────┘
                     │
         ┌───────────┼────────────┐
         │           │            │
    ┌────▼───┐  ┌───▼────┐  ┌───▼────────┐
    │ Azure  │  │ Azure  │  │ Blob       │
    │ SQL DB │  │ Redis  │  │ Storage    │
    │ (Basic)│  │ (Basic)│  │ (Hot tier) │
    └────────┘  └────────┘  └────────────┘
         │
         ▼
    ┌──────────────────┐
    │ Application      │
    │ Insights         │
    └──────────────────┘
```

## 🛠️ Technology Stack

### Backend Options (Pick One)

#### Option 1: Node.js + Express (Recommended for speed)
```yaml
Runtime: Node.js 20 LTS
Framework: Express.js
ORM: Prisma
Advantages:
  - Rapid development
  - Huge ecosystem (npm)
  - Full-stack JavaScript
  - Easy deployment
  - Serverless compatible
```

#### Option 2: Python + FastAPI (Recommended for ML/AI)
```yaml
Runtime: Python 3.11
Framework: FastAPI
ORM: SQLAlchemy
Advantages:
  - ML/AI integration
  - Type safety (Pydantic)
  - Auto documentation
  - Async support
  - Data science ready
```

#### Option 3: .NET (Recommended for enterprise potential)
```yaml
Runtime: .NET 8
Framework: ASP.NET Core Minimal APIs
ORM: Entity Framework Core
Advantages:
  - Performance
  - Strong typing
  - Azure integration
  - Easy to scale to enterprise
```

### Frontend Options

#### Option 1: React + Vite (Most popular)
```yaml
Framework: React 18
Build: Vite
UI: Tailwind CSS / Chakra UI
State: React Query + Zustand
```

#### Option 2: Next.js (SEO critical)
```yaml
Framework: Next.js 14
Rendering: App Router (SSR/SSG)
UI: shadcn/ui + Tailwind
```

#### Option 3: Vue.js (Simpler learning curve)
```yaml
Framework: Vue 3
Build: Vite
UI: Vuetify / PrimeVue
```

### Database Strategy

#### Primary Database
```yaml
Development/Early MVP:
  - Azure SQL Basic ($5/month)
  - PostgreSQL Flexible Server B1ms ($12/month)
  
Growing (>1K users):
  - SQL Database S1 ($30/month)
  - PostgreSQL GP B2s ($60/month)
```

#### Caching (Optional, add when needed)
```yaml
Start: In-memory (Node-cache, cachetools)
Growth: Azure Cache for Redis Basic C0 ($16/month)
```

#### File Storage
```yaml
Azure Blob Storage:
  - Hot tier for active files
  - Cool tier for archives
  - ~$1-5/month initially
```

### Hosting

```yaml
Azure App Service:
  Development:
    - B1 (Basic): $13/month
    - 1.75GB RAM, 1 vCPU
    - Custom domains + SSL
    - Auto-scale ready
  
  Production (later):
    - P1V3: $124/month
    - 8GB RAM, 2 vCPU
    - Deployment slots
```

### Authentication

```yaml
Quick Start:
  - Azure AD B2C Free tier (50K users)
  - Social logins (Google, GitHub, etc.)
  
Alternatives:
  - Auth0 free tier (7K users)
  - Supabase Auth (unlimited)
  - Firebase Auth (free up to 10K/day)
```

### CI/CD

```yaml
GitHub Actions (Free):
  - Unlimited minutes for public repos
  - 2,000 minutes/month private repos
  - Deploy on every push
  - Automated testing
```

### Monitoring

```yaml
Application Insights:
  - Free tier: 5GB/month
  - Performance monitoring
  - Error tracking
  - User analytics
  
Alternatives:
  - Sentry (free tier)
  - LogRocket (sessions tracking)
```

## 📁 Project Structure (Node.js MVP)

```
startup-mvp/
├── frontend/                    # React app
│   ├── src/
│   │   ├── components/
│   │   │   ├── auth/
│   │   │   │   ├── LoginForm.jsx
│   │   │   │   └── SignupForm.jsx
│   │   │   ├── common/
│   │   │   │   ├── Header.jsx
│   │   │   │   ├── Footer.jsx
│   │   │   │   └── LoadingSpinner.jsx
│   │   │   └── dashboard/
│   │   │       └── Dashboard.jsx
│   │   ├── pages/
│   │   │   ├── Home.jsx
│   │   │   ├── Pricing.jsx
│   │   │   └── Dashboard.jsx
│   │   ├── hooks/
│   │   │   └── useAuth.js
│   │   ├── services/
│   │   │   └── api.js
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   └── vite.config.js
├── backend/                     # Express API
│   ├── src/
│   │   ├── routes/
│   │   │   ├── auth.routes.js
│   │   │   ├── user.routes.js
│   │   │   └── api.routes.js
│   │   ├── controllers/
│   │   │   ├── auth.controller.js
│   │   │   └── user.controller.js
│   │   ├── middleware/
│   │   │   ├── auth.middleware.js
│   │   │   ├── error.middleware.js
│   │   │   └── validation.middleware.js
│   │   ├── models/
│   │   │   └── user.model.js
│   │   ├── services/
│   │   │   ├── email.service.js
│   │   │   └── storage.service.js
│   │   ├── config/
│   │   │   └── database.js
│   │   ├── utils/
│   │   │   └── logger.js
│   │   └── server.js
│   ├── prisma/
│   │   └── schema.prisma
│   ├── package.json
│   └── Dockerfile
├── .github/
│   └── workflows/
│       └── deploy.yml
├── infrastructure/
│   └── main.bicep
└── README.md
```

## 🚀 Complete MVP Implementation

### Backend API (Express + Prisma)

```javascript
// backend/src/server.js
import express from 'express';
import cors from 'cors';
import helmet from 'helmet';
import morgan from 'morgan';
import { PrismaClient } from '@prisma/client';
import authRoutes from './routes/auth.routes.js';
import userRoutes from './routes/user.routes.js';
import { errorHandler } from './middleware/error.middleware.js';

const app = express();
const prisma = new PrismaClient();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(helmet());
app.use(cors());
app.use(express.json());
app.use(morgan('combined'));

// Health check
app.get('/health', (req, res) => {
  res.json({ status: 'healthy', timestamp: new Date() });
});

// Routes
app.use('/api/auth', authRoutes);
app.use('/api/users', userRoutes);

// Error handling
app.use(errorHandler);

// Graceful shutdown
process.on('SIGTERM', async () => {
  await prisma.$disconnect();
  process.exit(0);
});

app.listen(PORT, () => {
  console.log(`🚀 Server running on port ${PORT}`);
});
```

```javascript
// backend/src/routes/auth.routes.js
import express from 'express';
import bcrypt from 'bcryptjs';
import jwt from 'jsonwebtoken';
import { PrismaClient } from '@prisma/client';
import { z } from 'zod';

const router = express.Router();
const prisma = new PrismaClient();

const signupSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
  name: z.string().min(2)
});

// Signup
router.post('/signup', async (req, res, next) => {
  try {
    const { email, password, name } = signupSchema.parse(req.body);

    // Check if user exists
    const existingUser = await prisma.user.findUnique({ where: { email } });
    if (existingUser) {
      return res.status(400).json({ error: 'User already exists' });
    }

    // Hash password
    const hashedPassword = await bcrypt.hash(password, 10);

    // Create user
    const user = await prisma.user.create({
      data: {
        email,
        password: hashedPassword,
        name
      },
      select: {
        id: true,
        email: true,
        name: true,
        createdAt: true
      }
    });

    // Generate token
    const token = jwt.sign(
      { userId: user.id },
      process.env.JWT_SECRET,
      { expiresIn: '7d' }
    );

    res.status(201).json({ user, token });
  } catch (error) {
    next(error);
  }
});

// Login
router.post('/login', async (req, res, next) => {
  try {
    const { email, password } = req.body;

    const user = await prisma.user.findUnique({ where: { email } });
    if (!user) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }

    const validPassword = await bcrypt.compare(password, user.password);
    if (!validPassword) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }

    const token = jwt.sign(
      { userId: user.id },
      process.env.JWT_SECRET,
      { expiresIn: '7d' }
    );

    res.json({
      user: {
        id: user.id,
        email: user.email,
        name: user.name
      },
      token
    });
  } catch (error) {
    next(error);
  }
});

export default router;
```

```prisma
// backend/prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        String   @id @default(cuid())
  email     String   @unique
  name      String
  password  String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  posts     Post[]
  @@index([email])
}

model Post {
  id        String   @id @default(cuid())
  title     String
  content   String?
  published Boolean  @default(false)
  authorId  String
  author    User     @relation(fields: [authorId], references: [id])
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  @@index([authorId])
}
```

### Frontend (React + Vite)

```jsx
// frontend/src/services/api.js
import axios from 'axios';

const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL || '/api',
  headers: {
    'Content-Type': 'application/json'
  }
});

// Add auth token to requests
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// Handle errors
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem('token');
      window.location.href = '/login';
    }
    return Promise.reject(error);
  }
);

export const authAPI = {
  signup: (data) => api.post('/auth/signup', data),
  login: (data) => api.post('/auth/login', data),
  me: () => api.get('/auth/me')
};

export const userAPI = {
  getProfile: () => api.get('/users/profile'),
  updateProfile: (data) => api.put('/users/profile', data)
};

export default api;
```

```jsx
// frontend/src/components/auth/LoginForm.jsx
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { authAPI } from '../../services/api';

export default function LoginForm() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState('');
  const [loading, setLoading] = useState(false);
  const navigate = useNavigate();

  const handleSubmit = async (e) => {
    e.preventDefault();
    setError('');
    setLoading(true);

    try {
      const { data } = await authAPI.login({ email, password });
      localStorage.setItem('token', data.token);
      localStorage.setItem('user', JSON.stringify(data.user));
      navigate('/dashboard');
    } catch (err) {
      setError(err.response?.data?.error || 'Login failed');
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="min-h-screen flex items-center justify-center bg-gray-50">
      <div className="max-w-md w-full space-y-8 p-8 bg-white rounded-lg shadow">
        <h2 className="text-3xl font-bold text-center">Sign In</h2>
        
        {error && (
          <div className="bg-red-50 text-red-600 p-3 rounded">
            {error}
          </div>
        )}

        <form onSubmit={handleSubmit} className="space-y-6">
          <div>
            <label className="block text-sm font-medium text-gray-700">
              Email
            </label>
            <input
              type="email"
              value={email}
              onChange={(e) => setEmail(e.target.value)}
              required
              className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md"
            />
          </div>

          <div>
            <label className="block text-sm font-medium text-gray-700">
              Password
            </label>
            <input
              type="password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              required
              className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md"
            />
          </div>

          <button
            type="submit"
            disabled={loading}
            className="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-blue-600 hover:bg-blue-700 disabled:opacity-50"
          >
            {loading ? 'Signing in...' : 'Sign In'}
          </button>
        </form>
      </div>
    </div>
  );
}
```

### Infrastructure (Bicep)

```bicep
// infrastructure/main.bicep
param location string = resourceGroup().location
param appName string
param environment string = 'dev'

var appServicePlanName = '${appName}-plan-${environment}'
var webAppName = '${appName}-${environment}'
var sqlServerName = '${appName}-sql-${environment}'
var databaseName = '${appName}-db'

// App Service Plan (B1 for MVP)
resource appServicePlan 'Microsoft.Web/serverfarms@2022-09-01' = {
  name: appServicePlanName
  location: location
  sku: {
    name: 'B1'
    tier: 'Basic'
    capacity: 1
  }
  kind: 'linux'
  properties: {
    reserved: true
  }
}

// Web App
resource webApp 'Microsoft.Web/sites@2022-09-01' = {
  name: webAppName
  location: location
  properties: {
    serverFarmId: appServicePlan.id
    siteConfig: {
      linuxFxVersion: 'NODE|20-lts'
      appSettings: [
        {
          name: 'DATABASE_URL'
          value: 'postgresql://${sqlAdmin}:${sqlPassword}@${sqlServer.properties.fullyQualifiedDomainName}:5432/${databaseName}?ssl=true'
        }
        {
          name: 'JWT_SECRET'
          value: '@Microsoft.KeyVault(SecretUri=${keyVault.properties.vaultUri}secrets/jwt-secret/)'
        }
        {
          name: 'NODE_ENV'
          value: 'production'
        }
      ]
      ftpsState: 'Disabled'
      minTlsVersion: '1.2'
      http20Enabled: true
    }
    httpsOnly: true
  }
}

// PostgreSQL Flexible Server (B1ms for MVP)
resource sqlServer 'Microsoft.DBforPostgreSQL/flexibleServers@2023-03-01-preview' = {
  name: sqlServerName
  location: location
  sku: {
    name: 'Standard_B1ms'
    tier: 'Burstable'
  }
  properties: {
    administratorLogin: sqlAdmin
    administratorLoginPassword: sqlPassword
    version: '15'
    storage: {
      storageSizeGB: 32
    }
    backup: {
      backupRetentionDays: 7
      geoRedundantBackup: 'Disabled'
    }
  }
}

resource database 'Microsoft.DBforPostgreSQL/flexibleServers/databases@2023-03-01-preview' = {
  parent: sqlServer
  name: databaseName
}

// Application Insights
resource appInsights 'Microsoft.Insights/components@2020-02-02' = {
  name: '${appName}-insights'
  location: location
  kind: 'web'
  properties: {
    Application_Type: 'web'
  }
}

output webAppUrl string = 'https://${webApp.properties.defaultHostName}'
output databaseHost string = sqlServer.properties.fullyQualifiedDomainName
```

### CI/CD Pipeline

```yaml
# .github/workflows/deploy.yml
name: Deploy MVP

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

env:
  AZURE_WEBAPP_NAME: myapp-dev
  NODE_VERSION: '20.x'

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
          
      - name: Install dependencies
        run: |
          cd backend
          npm ci
          
      - name: Run tests
        run: |
          cd backend
          npm test

  build-and-deploy:
    needs: test
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ env.NODE_VERSION }}
          
      - name: Build backend
        run: |
          cd backend
          npm ci --production
          npx prisma generate
          
      - name: Build frontend
        run: |
          cd frontend
          npm ci
          npm run build
          
      - name: Deploy to Azure
        uses: azure/webapps-deploy@v2
        with:
          app-name: ${{ env.AZURE_WEBAPP_NAME }}
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
          package: ./backend
```

## 💰 Cost Breakdown (MVP Budget)

### Minimal Setup ($50/month)
```yaml
App Service B1: $13/month
PostgreSQL B1ms: $12/month
Blob Storage: $2/month
Application Insights: Free tier
GitHub Actions: Free
Domain (.com): $12/year
SSL Certificate: Free (Let's Encrypt)

Total: ~$27/month + $12/year domain
```

### Recommended Setup ($150/month)
```yaml
App Service B1: $13/month
PostgreSQL B2s: $60/month
Redis Basic C0: $16/month
Blob Storage: $5/month
SendGrid (emails): $15/month (40K emails)
Application Insights: Free tier
Azure AD B2C: Free tier

Total: ~$109/month
```

### Growth Ready ($300/month)
```yaml
App Service P1V3: $124/month
PostgreSQL GP B2s: $60/month
Redis Standard C1: $76/month
Blob Storage: $10/month
CDN: $10/month
SendGrid: $15/month

Total: ~$295/month
```

## 📊 MVP Metrics to Track

```yaml
Product Metrics:
  - Daily Active Users (DAU)
  - Weekly Active Users (WAU)
  - Retention rate (D1, D7, D30)
  - Feature usage
  - User flows/funnels
  
Technical Metrics:
  - Response time (< 500ms)
  - Error rate (< 1%)
  - Uptime (> 99%)
  - API success rate
  
Business Metrics:
  - Signup conversion rate
  - Time to first value
  - Customer Acquisition Cost (CAC)
  - Monthly Recurring Revenue (MRR)
```

## ⚡ Quick Start (15 minutes)

```bash
# 1. Clone template
git clone https://github.com/yourorg/mvp-template.git myapp
cd myapp

# 2. Install dependencies
cd backend && npm install
cd ../frontend && npm install

# 3. Setup environment
cp backend/.env.example backend/.env
# Edit .env with your credentials

# 4. Initialize database
cd backend
npx prisma migrate dev --name init

# 5. Run locally
npm run dev  # Backend on :3000
cd ../frontend
npm run dev  # Frontend on :5173

# 6. Deploy to Azure
az group create --name rg-myapp --location eastus
az deployment group create --resource-group rg-myapp --template-file infrastructure/main.bicep

# 7. Configure CI/CD
# Add AZURE_WEBAPP_PUBLISH_PROFILE to GitHub Secrets
# Push to main branch → auto-deploy
```

## 🎯 MVP Launch Checklist

```yaml
Pre-Launch:
  ✓ Core features working
  ✓ Authentication implemented
  ✓ Basic error handling
  ✓ Mobile responsive
  ✓ Analytics setup
  ✓ Error tracking (Sentry)
  ✓ SSL certificate
  ✓ Privacy policy
  ✓ Terms of service

Launch Day:
  ✓ Deploy to production
  ✓ DNS configured
  ✓ Monitoring active
  ✓ Backup strategy
  ✓ Support email setup

Post-Launch:
  ✓ Monitor errors
  ✓ Track user behavior
  ✓ Collect feedback
  ✓ Iterate quickly
  ✓ Plan scaling
```

## 🚀 Growth Path

```yaml
Month 1-3 (Validation):
  - MVP on B1 App Service
  - Basic tier database
  - ~100-500 users
  - Cost: $50-150/month

Month 3-6 (Traction):
  - Upgrade to P1V3
  - Add Redis caching
  - ~500-5K users
  - Cost: $300-500/month

Month 6-12 (Scale):
  - Multi-region
  - CDN + Front Door
  - Auto-scaling
  - ~5K-50K users
  - Cost: $1,000-3,000/month

Year 2+ (Enterprise):
  - Migrate to Scale-Up stack
  - Microservices consideration
  - Advanced features
  - 50K+ users
```

---

**Owner**: Full Stack Developer / Startup CTO  
**Última actualización**: Diciembre 2025
