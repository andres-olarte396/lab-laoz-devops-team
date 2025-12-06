# Static Site Stack - Azure Static Web Apps

## 📋 Overview

Stack optimizado para sitios web estáticos y aplicaciones SPA (Single Page Applications) con integración de API serverless en Azure.

### Ideal Para
- ✅ Single Page Applications (React, Vue, Angular)
- ✅ Static websites (blogs, portfolios, docs)
- ✅ JAMstack applications
- ✅ Landing pages
- ✅ Documentation sites
- ✅ E-commerce frontends
- ✅ Progressive Web Apps (PWA)

### NO Usar Cuando
- ❌ Server-side rendering crítico (usar Next.js/Nuxt en App Service)
- ❌ Real-time server updates
- ❌ Legacy monolithic apps
- ❌ Apps con lógica backend compleja

### Ventajas
- 💰 Costo muy bajo (plan Free disponible)
- ⚡ Performance excelente (CDN global)
- 🚀 Deployment automático desde Git
- 🔒 SSL gratis
- 🌐 Custom domains fácil
- 📊 Staging environments automáticos

## 🏗️ Architecture

```
                   Internet
                      │
┌─────────────────────▼─────────────────────────┐
│         Azure Static Web Apps                  │
│    (Global CDN + Edge Computing)              │
└─────────────────────┬─────────────────────────┘
                      │
        ┌─────────────┼─────────────┐
        │             │             │
┌───────▼──────┐ ┌───▼──────┐ ┌───▼────────┐
│ Static       │ │ Azure    │ │ Custom     │
│ Content      │ │ Functions│ │ API        │
│ (React/Vue)  │ │ (API)    │ │ (Backend)  │
└──────────────┘ └───┬──────┘ └───┬────────┘
                      │             │
                ┌─────▼─────────────▼───┐
                │ Cosmos DB / SQL DB    │
                │ Storage / External    │
                └───────────────────────┘
```

## 🛠️ Technology Stack

### Frontend Frameworks
```yaml
React:
  - Create React App
  - Vite + React
  - Next.js (Static Export)
  
Vue.js:
  - Vue CLI
  - Vite + Vue
  - Nuxt.js (Static Generation)
  
Angular:
  - Angular CLI
  
Svelte:
  - SvelteKit (Static Adapter)
  
Static Site Generators:
  - Hugo (Go-based, ultra-fast)
  - Jekyll (Ruby-based)
  - Gatsby (React-based)
  - Eleventy (11ty)
  - Docusaurus (documentation)
  - VitePress (docs, Vue-based)
```

### Build Tools
```yaml
Build Systems:
  - Vite (modern, fast)
  - Webpack (traditional)
  - Rollup
  - esbuild (ultra-fast)
  - Parcel (zero-config)

Package Managers:
  - npm
  - pnpm (fast, efficient)
  - yarn
  - bun (new, fast)
```

### API Layer
```yaml
Serverless Functions:
  - Azure Functions (integrated)
  - Runtime: Node.js, Python, .NET
  - HTTP triggers for API endpoints
  
Alternative APIs:
  - Azure API Management
  - External REST APIs
  - GraphQL APIs
```

### CMS (Optional)
```yaml
Headless CMS:
  - Contentful
  - Strapi (self-hosted)
  - Sanity.io
  - Prismic
  - Ghost (headless mode)
  
Azure Options:
  - Cosmos DB (content storage)
  - Azure Storage (blob content)
```

### Authentication
```yaml
Built-in:
  - Azure AD / B2C (pre-integrated)
  - GitHub
  - Twitter
  - Google
  - Facebook
  
Custom:
  - Auth0
  - Firebase Auth
  - Custom JWT
```

### Database
```yaml
For API Functions:
  - Cosmos DB (serverless)
  - Azure SQL Database
  - Azure Table Storage
  - MongoDB Atlas
  - Supabase
```

### CDN & Performance
```yaml
Azure Static Web Apps includes:
  - Global CDN (built-in)
  - Auto SSL/TLS
  - Custom domains
  - HTTP/2
  - Brotli compression
  
Performance:
  - Code splitting
  - Lazy loading
  - Image optimization
  - PWA caching
```

## 📁 Project Structure

### React + Vite Example
```
my-static-app/
├── public/
│   ├── favicon.ico
│   ├── robots.txt
│   └── manifest.json
├── src/
│   ├── assets/
│   │   ├── images/
│   │   └── styles/
│   ├── components/
│   │   ├── Header.jsx
│   │   ├── Footer.jsx
│   │   └── Layout.jsx
│   ├── pages/
│   │   ├── Home.jsx
│   │   ├── About.jsx
│   │   └── Contact.jsx
│   ├── services/
│   │   └── api.js
│   ├── hooks/
│   │   └── useAuth.js
│   ├── context/
│   │   └── AuthContext.jsx
│   ├── utils/
│   │   └── helpers.js
│   ├── App.jsx
│   ├── main.jsx
│   └── routes.jsx
├── api/                        # Azure Functions
│   ├── GetUsers/
│   │   ├── index.js
│   │   └── function.json
│   ├── CreateUser/
│   │   ├── index.js
│   │   └── function.json
│   └── host.json
├── .github/
│   └── workflows/
│       └── azure-static-web-apps.yml
├── infrastructure/
│   └── main.bicep
├── package.json
├── vite.config.js
├── .env.example
├── staticwebapp.config.json   # SWA configuration
└── README.md
```

## 🚀 Sample Implementation

### React App (Vite)
```jsx
// src/App.jsx
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import { AuthProvider } from './context/AuthContext';
import Layout from './components/Layout';
import Home from './pages/Home';
import About from './pages/About';
import Dashboard from './pages/Dashboard';
import PrivateRoute from './components/PrivateRoute';

function App() {
  return (
    <AuthProvider>
      <Router>
        <Layout>
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            <Route
              path="/dashboard"
              element={
                <PrivateRoute>
                  <Dashboard />
                </PrivateRoute>
              }
            />
          </Routes>
        </Layout>
      </Router>
    </AuthProvider>
  );
}

export default App;
```

```jsx
// src/pages/Dashboard.jsx
import { useState, useEffect } from 'react';
import { useAuth } from '../hooks/useAuth';

function Dashboard() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const { user } = useAuth();

  useEffect(() => {
    fetchUsers();
  }, []);

  const fetchUsers = async () => {
    try {
      const response = await fetch('/api/users');
      const data = await response.json();
      setUsers(data);
    } catch (error) {
      console.error('Error fetching users:', error);
    } finally {
      setLoading(false);
    }
  };

  if (loading) {
    return <div className="loading">Loading...</div>;
  }

  return (
    <div className="dashboard">
      <h1>Welcome, {user?.userDetails}</h1>
      <div className="users-list">
        <h2>Users</h2>
        {users.map(user => (
          <div key={user.id} className="user-card">
            <h3>{user.name}</h3>
            <p>{user.email}</p>
          </div>
        ))}
      </div>
    </div>
  );
}

export default Dashboard;
```

### API Function (Azure Functions)
```javascript
// api/GetUsers/index.js
const { CosmosClient } = require('@azure/cosmos');

const client = new CosmosClient(process.env.COSMOS_CONNECTION_STRING);
const database = client.database('myapp');
const container = database.container('users');

module.exports = async function (context, req) {
    context.log('GetUsers function processed a request.');

    try {
        // Check authentication
        const clientPrincipal = req.headers['x-ms-client-principal'];
        if (!clientPrincipal) {
            context.res = {
                status: 401,
                body: { error: 'Unauthorized' }
            };
            return;
        }

        // Query users from Cosmos DB
        const { resources: users } = await container.items
            .query('SELECT * FROM c ORDER BY c.createdAt DESC')
            .fetchAll();

        context.res = {
            status: 200,
            headers: {
                'Content-Type': 'application/json'
            },
            body: users
        };
    } catch (error) {
        context.log.error('Error fetching users:', error);
        context.res = {
            status: 500,
            body: { error: 'Internal server error' }
        };
    }
};
```

```json
// api/GetUsers/function.json
{
  "bindings": [
    {
      "authLevel": "anonymous",
      "type": "httpTrigger",
      "direction": "in",
      "name": "req",
      "methods": ["get"],
      "route": "users"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "res"
    }
  ]
}
```

### Static Web App Configuration
```json
// staticwebapp.config.json
{
  "routes": [
    {
      "route": "/login",
      "rewrite": "/.auth/login/aad"
    },
    {
      "route": "/logout",
      "rewrite": "/.auth/logout"
    },
    {
      "route": "/api/*",
      "allowedRoles": ["authenticated"]
    },
    {
      "route": "/dashboard/*",
      "allowedRoles": ["authenticated"]
    }
  ],
  "navigationFallback": {
    "rewrite": "/index.html",
    "exclude": ["/images/*.{png,jpg,gif}", "/css/*", "/api/*"]
  },
  "responseOverrides": {
    "401": {
      "redirect": "/login",
      "statusCode": 302
    }
  },
  "globalHeaders": {
    "X-Content-Type-Options": "nosniff",
    "X-Frame-Options": "DENY",
    "Content-Security-Policy": "default-src 'self' https:; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'"
  },
  "mimeTypes": {
    ".json": "application/json",
    ".woff2": "font/woff2"
  }
}
```

### Vite Configuration
```javascript
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import { VitePWA } from 'vite-plugin-pwa';

export default defineConfig({
  plugins: [
    react(),
    VitePWA({
      registerType: 'autoUpdate',
      includeAssets: ['favicon.ico', 'robots.txt', 'apple-touch-icon.png'],
      manifest: {
        name: 'My Static App',
        short_name: 'MyApp',
        description: 'My awesome static web app',
        theme_color: '#ffffff',
        icons: [
          {
            src: 'pwa-192x192.png',
            sizes: '192x192',
            type: 'image/png'
          },
          {
            src: 'pwa-512x512.png',
            sizes: '512x512',
            type: 'image/png'
          }
        ]
      }
    })
  ],
  build: {
    outDir: 'dist',
    sourcemap: true,
    rollupOptions: {
      output: {
        manualChunks: {
          vendor: ['react', 'react-dom', 'react-router-dom']
        }
      }
    }
  },
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:7071',
        changeOrigin: true
      }
    }
  }
});
```

## 📦 Package.json

```json
{
  "name": "my-static-app",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "eslint src --ext js,jsx",
    "test": "vitest",
    "swa:start": "swa start http://localhost:5173 --api-location ./api"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-router-dom": "^6.21.0",
    "axios": "^1.6.2"
  },
  "devDependencies": {
    "@vitejs/plugin-react": "^4.2.1",
    "vite": "^5.0.8",
    "vite-plugin-pwa": "^0.17.4",
    "@azure/static-web-apps-cli": "^1.1.6",
    "eslint": "^8.56.0",
    "eslint-plugin-react": "^7.33.2",
    "vitest": "^1.1.0"
  }
}
```

## 🚀 CI/CD Pipeline (Auto-generated)

```yaml
# .github/workflows/azure-static-web-apps.yml
name: Azure Static Web Apps CI/CD

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main

jobs:
  build_and_deploy_job:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true
      
      - name: Build And Deploy
        id: builddeploy
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          repo_token: ${{ secrets.GITHUB_TOKEN }}
          action: "upload"
          app_location: "/" # App source code path
          api_location: "api" # Api source code path - optional
          output_location: "dist" # Built app content directory
          
  close_pull_request_job:
    if: github.event_name == 'pull_request' && github.event.action == 'closed'
    runs-on: ubuntu-latest
    name: Close Pull Request Job
    steps:
      - name: Close Pull Request
        id: closepullrequest
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          action: "close"
```

## 🔒 Security Best Practices

### Environment Variables
```javascript
// .env.example
VITE_API_BASE_URL=https://myapp.azurestaticapps.net/api
VITE_APP_INSIGHTS_KEY=your-app-insights-key
VITE_AUTH_ENABLED=true

# API (Azure Functions)
COSMOS_CONNECTION_STRING=your-cosmos-connection
AZURE_STORAGE_CONNECTION_STRING=your-storage-connection
```

### Content Security Policy
```json
{
  "globalHeaders": {
    "Content-Security-Policy": "default-src 'self'; script-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com; img-src 'self' data: https:; connect-src 'self' https://*.azurestaticapps.net"
  }
}
```

## 💰 Cost Estimation

```yaml
Free Tier (Ideal for small projects):
  - 100GB bandwidth/month
  - 2 custom domains
  - Free SSL
  - Staging environments (PR previews)
  - Basic auth (Azure AD, GitHub, etc.)
  - Cost: $0/month

Standard Tier (Production apps):
  - Unlimited bandwidth
  - Unlimited custom domains
  - Advanced auth features
  - SLA 99.95%
  - Cost: ~$9/month

Additional Costs:
  - Azure Functions (if used): $0-50/month
  - Cosmos DB (if used): $25-100/month
  - Storage: ~$1-5/month
  
Total Typical: $0-165/month
```

## 📊 Performance Optimization

### Image Optimization
```javascript
// vite.config.js - Image optimization
import imagemin from 'vite-plugin-imagemin';

export default defineConfig({
  plugins: [
    imagemin({
      gifsicle: { optimizationLevel: 7 },
      mozjpeg: { quality: 80 },
      pngquant: { quality: [0.8, 0.9] },
      svgo: {
        plugins: [{ name: 'removeViewBox', active: false }]
      }
    })
  ]
});
```

### Code Splitting
```javascript
// Lazy loading routes
import { lazy, Suspense } from 'react';

const Dashboard = lazy(() => import('./pages/Dashboard'));
const Profile = lazy(() => import('./pages/Profile'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/profile" element={<Profile />} />
      </Routes>
    </Suspense>
  );
}
```

## 🔄 Migration Strategies

### From Traditional Hosting
```yaml
Step 1: Prepare (1 week)
  - Audit current site
  - Identify dynamic vs static content
  - Plan API endpoints for dynamic features
  
Step 2: Build (2-4 weeks)
  - Convert to SPA framework
  - Create API functions for backend logic
  - Setup development environment
  
Step 3: Deploy (1 week)
  - Create Static Web App resource
  - Configure custom domain
  - Setup CI/CD
  
Step 4: Cutover (1 day)
  - DNS change
  - Monitor traffic
  - Rollback plan ready
```

## ⚡ Quick Start

### Option 1: CLI
```bash
# 1. Install SWA CLI
npm install -g @azure/static-web-apps-cli

# 2. Create React app with Vite
npm create vite@latest my-app -- --template react

cd my-app

# 3. Install dependencies
npm install

# 4. Create API folder
mkdir api
cd api
func init --worker-runtime node

# 5. Run locally
swa start http://localhost:5173 --api-location ./api

# 6. Deploy
swa deploy
```

### Option 2: Azure Portal
```bash
# 1. Create repository on GitHub
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/user/repo.git
git push -u origin main

# 2. Azure Portal → Create Static Web App
# 3. Connect to GitHub repository
# 4. Configure build settings:
#    - App location: /
#    - API location: api
#    - Output location: dist
# 5. Azure creates workflow automatically
```

## 📚 Popular Use Cases

### Landing Page
```
Tech: HTML + Tailwind CSS
Build: None (pure static)
Deploy: Direct to SWA
Cost: Free tier
```

### Blog
```
Tech: Hugo / Jekyll
CMS: Contentful / Netlify CMS
Build: Hugo build / Jekyll build
Cost: Free - $9/month
```

### SaaS Dashboard
```
Tech: React + Vite
API: Azure Functions
Auth: Azure AD B2C
Database: Cosmos DB
Cost: $25-100/month
```

### E-commerce Frontend
```
Tech: Next.js (static export)
API: Shopify / Commerce.js
Payment: Stripe
Cost: $9-50/month
```

## 🎯 Best Practices

```yaml
Performance:
  - Use CDN for assets
  - Implement lazy loading
  - Optimize images (WebP)
  - Enable PWA caching
  - Minimize bundle size

SEO:
  - Pre-render with SSG
  - Meta tags for all pages
  - Sitemap.xml
  - robots.txt
  - Structured data (JSON-LD)

Security:
  - HTTPS only
  - CSP headers
  - Authentication for sensitive routes
  - API rate limiting
  - Input validation

Development:
  - TypeScript for type safety
  - ESLint + Prettier
  - Unit tests (Vitest)
  - E2E tests (Playwright)
  - Staging environments (PR previews)
```

---

**Owner**: Platform Engineer  
**Última actualización**: Diciembre 2025
