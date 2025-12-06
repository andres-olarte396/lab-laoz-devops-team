# QA Engineer (Quality Assurance Engineer)

## 📋 Descripción del Rol

El QA Engineer es responsable de asegurar la calidad del software mediante testing manual y automatizado, estableciendo estrategias de calidad, y trabajando de manera integrada con el equipo de desarrollo. El enfoque moderno de QA es **shift-left** - involucrarse desde el inicio del ciclo de desarrollo, no solo al final.

> **Nota**: Rol moderno de QA es muy diferente al tradicional. Hoy requiere skills de automation, coding, y colaboración estrecha con developers.

## 🎯 Responsabilidades Principales

### Test Automation (50%)
- Desarrollar y mantener test automation frameworks
- Escribir automated tests (unit, integration, E2E)
- CI/CD pipeline integration
- Performance testing automation
- Visual regression testing
- API testing automation

### Quality Strategy (25%)
- Definir estrategias de testing
- Establecer quality gates
- Test planning y estimation
- Risk-based testing
- Quality metrics y reporting
- Process improvements

### Manual Testing (15%)
- Exploratory testing
- UAT (User Acceptance Testing) coordination
- Edge cases y scenarios complejos
- New feature validation
- Regression testing (cuando automation no cubre)

### Collaboration & Advocacy (10%)
- Quality advocacy en el equipo
- Pair testing con developers
- Bug triage y prioritization
- User feedback integration
- Cross-team QA coordination

## 🛠️ Stack Tecnológico

### Test Automation Frameworks

#### E2E Testing (Frontend)
```yaml
Playwright (Recomendado):
  - Cross-browser (Chrome, Firefox, Safari, Edge)
  - Auto-wait (menos flaky tests)
  - TypeScript support
  - Parallel execution
  - Video & screenshot capture
  - Great debugging experience

Cypress:
  - JavaScript/TypeScript
  - Great DX (developer experience)
  - Time-travel debugging
  - Real-time reloads
  - Component testing

Selenium:
  - Multi-language support
  - Mature ecosystem
  - Large community
  - Legacy apps support
```

#### API Testing
```yaml
REST API:
  - Postman + Newman (CLI)
  - REST Assured (Java)
  - SuperTest (Node.js)
  - HttpClient + XUnit (.NET)

GraphQL:
  - GraphQL Inspector
  - Apollo Client testing
  - Postman GraphQL support

Contract Testing:
  - Pact (consumer-driven contracts)
  - Ensures API compatibility
```

#### Unit & Integration Testing
```yaml
Frontend:
  - Vitest / Jest (JavaScript/TypeScript)
  - React Testing Library
  - Vue Test Utils
  
Backend:
  - xUnit / NUnit (.NET)
  - Jest (Node.js)
  - pytest (Python)
  - JUnit (Java)
```

### Performance Testing
```yaml
Load Testing:
  - K6 (modern, developer-friendly)
  - JMeter (mature, GUI)
  - Gatling (Scala-based)
  - Azure Load Testing

Monitoring:
  - Lighthouse (web performance)
  - WebPageTest
  - Application Insights
```

### Visual Testing
```yaml
Tools:
  - Chromatic (Storybook integration)
  - Percy
  - Applitools
  - BackstopJS

Purpose:
  - Detect visual regressions
  - Cross-browser consistency
  - Responsive design validation
```

### Mobile Testing
```yaml
Automation:
  - Detox (React Native)
  - Appium (cross-platform)
  - XCUITest (iOS)
  - Espresso (Android)

Device Testing:
  - BrowserStack
  - Sauce Labs
  - Azure Device Farm
```

### CI/CD Integration
```yaml
Platforms:
  - GitHub Actions
  - Azure DevOps Pipelines
  - Jenkins
  - GitLab CI

Strategy:
  - Run tests on every PR
  - Parallel execution
  - Fast feedback (<10 min)
  - Quality gates before merge
```

## 📈 Niveles de Seniority

### Junior QA Engineer (0-2 años)

```yaml
Habilidades Técnicas:
  ✓ Manual testing fundamentals
  ✓ Test case writing
  ✓ Bug reporting
  ✓ Basic SQL
  ✓ Understanding de HTTP/APIs
  ✓ Testing tools basics

Responsabilidades:
  - Execute manual test cases
  - Bug reporting y tracking
  - Smoke testing
  - Simple automation scripts
  - Test data preparation

Autonomía:
  - Requiere supervisión
  - Follows test plans
  - Learning automation
```

### Mid-level QA Engineer (2-5 años)

```yaml
Habilidades Técnicas:
  ✓ Test automation (Playwright/Cypress)
  ✓ Programming (JavaScript/TypeScript/C#)
  ✓ API testing
  ✓ CI/CD integration
  ✓ SQL proficiency
  ✓ Performance testing basics

Responsabilidades:
  - Write automated tests
  - Test framework development
  - Test strategy for features
  - Performance testing
  - Mentor juniors
  - Bug triage

Autonomía:
  - Trabaja independientemente
  - Owns feature testing
  - Proactive quality advocacy
```

### Senior QA Engineer (5-8 años)

```yaml
Habilidades Técnicas:
  ✓ Advanced test automation
  ✓ Framework architecture
  ✓ Performance engineering
  ✓ Security testing
  ✓ Multiple tech stacks
  ✓ DevOps practices

Responsabilidades:
  - QA strategy & roadmap
  - Framework architecture
  - Quality metrics ownership
  - Cross-team coordination
  - Process improvements
  - Technical leadership

Liderazgo:
  - Define quality standards
  - Mentor QA team
  - Influence engineering practices
```

### Staff QA Engineer / QA Lead (8+ años)

```yaml
Habilidades Técnicas:
  ✓ Todas las anteriores
  ✓ Organization-wide quality strategy
  ✓ Test platform engineering
  ✓ Advanced performance & security

Responsabilidades:
  - Organization QA strategy
  - Quality platform development
  - Cross-team quality initiatives
  - Tool evaluation & adoption
  - Industry thought leadership

Scope:
  - Multiple teams/products
  - Company-wide impact
  - Strategic initiatives
```

## 💼 Día Típico

### Morning (9:00 - 12:00)
```
09:00 - Daily standup (15 min)
       - QA updates
       - Blockers
       - Testing status
       
09:15 - Review failed CI tests (30 min)
       - Investigate failures
       - Fix flaky tests
       - Update automation
       
09:45 - Feature testing: New Checkout Flow (2 horas)
       - Review requirements & AC (Acceptance Criteria)
       - Exploratory testing
       - Write automated E2E tests
       - API testing
       - Performance check
       - Document findings
```

### Afternoon (13:00 - 18:00)
```
13:00 - Lunch
14:00 - Pair testing con developer (1 hora)
       - Review PR together
       - Discuss edge cases
       - Add missing tests
       
15:00 - Automation work: Shopping Cart tests (1.5 horas)
       - Playwright E2E scenarios
       - Add to CI pipeline
       - Verify test stability
       
16:30 - Bug triage meeting (30 min)
       - Prioritize bugs
       - Assign severity
       - Coordinate fixes
       
17:00 - Test framework improvement (1 hora)
       - Refactor test utilities
       - Add helper functions
       - Documentation
```

## 🎓 Skills Matrix

### Must Have (Senior Level)

| Skill | Nivel | Importancia |
|-------|-------|-------------|
| Test Automation | 5/5 | ⭐⭐⭐⭐⭐ |
| Programming (JS/TS/C#) | 4/5 | ⭐⭐⭐⭐⭐ |
| Testing Strategy | 5/5 | ⭐⭐⭐⭐⭐ |
| API Testing | 4/5 | ⭐⭐⭐⭐ |
| SQL | 4/5 | ⭐⭐⭐⭐ |
| CI/CD | 4/5 | ⭐⭐⭐⭐ |
| Bug Reporting | 5/5 | ⭐⭐⭐⭐⭐ |
| Exploratory Testing | 4/5 | ⭐⭐⭐⭐ |
| Git | 4/5 | ⭐⭐⭐⭐ |
| Performance Testing | 3/5 | ⭐⭐⭐ |
| Accessibility Testing | 3/5 | ⭐⭐⭐ |
| Security Testing Basics | 3/5 | ⭐⭐⭐ |

### Nice to Have

| Skill | Nivel | Importancia |
|-------|-------|-------------|
| Load Testing | 3/5 | ⭐⭐⭐ |
| Visual Testing | 3/5 | ⭐⭐⭐ |
| Mobile Testing | 3/5 | ⭐⭐⭐ |
| Security Testing Deep | 2/5 | ⭐⭐ |
| Kubernetes | 2/5 | ⭐⭐ |

## 📚 Learning Path

### Foundational (Months 1-4)

```yaml
Month 1: QA Fundamentals
  - Testing types (unit, integration, E2E)
  - Bug lifecycle
  - Test case writing
  - Bug reporting best practices
  - Basic HTTP/APIs
  
Month 2: Manual Testing Proficiency
  - Exploratory testing
  - Test planning
  - Requirements analysis
  - UAT coordination
  - SQL basics
  
Month 3: Programming Basics
  - JavaScript/TypeScript fundamentals
  - Git workflows
  - Understanding code structure
  - Reading developer code
  
Month 4: Automation Introduction
  - Choose framework (Playwright recommended)
  - First automated tests
  - Page Object Model pattern
  - Assertions & verifications
```

### Intermediate (Months 5-10)

```yaml
Month 5-6: Test Automation
  - E2E testing (Playwright/Cypress)
  - Test framework structure
  - Data-driven tests
  - CI/CD integration
  
Month 7-8: API Testing
  - REST API testing
  - Postman advanced
  - API automation (SuperTest/REST Assured)
  - Contract testing (Pact)
  
Month 9-10: Advanced Automation
  - Test framework architecture
  - Custom utilities
  - Parallel execution
  - Flaky test handling
  - Reporting & metrics
```

### Advanced (Months 11-18)

```yaml
Month 11-12: Performance Testing
  - Load testing (K6)
  - Performance metrics
  - Bottleneck identification
  - Web vitals (Core Web Vitals)
  
Month 13-14: Specialization
  - Visual regression testing
  - Accessibility testing (axe-core)
  - Security testing basics
  - Mobile testing
  
Month 15-16: Quality Engineering
  - Quality metrics & KPIs
  - Test strategy development
  - Risk-based testing
  - Process improvement
  
Month 17-18: Leadership & Strategy
  - Mentorship
  - Cross-team collaboration
  - Tool evaluation
  - Industry best practices
```

## 🎯 KPIs y Métricas

### Quality Metrics

```yaml
Test Coverage:
  - Code coverage > 80%
  - E2E coverage of critical paths: 100%
  - API coverage > 90%
  
Defect Metrics:
  - Defect detection rate (before production) > 95%
  - Production bugs < 5/month
  - Critical bugs escaped: 0
  - Bug fix time (average) < 2 days
  
Test Automation:
  - Automated test coverage > 70%
  - Test execution time < 15 min
  - Flaky test rate < 5%
  - Test maintenance time < 20% of automation time
```

### Process Metrics

```yaml
CI/CD:
  - Green build rate > 95%
  - Test execution in CI/CD: 100%
  - Time to feedback < 10 min
  
Efficiency:
  - Test planning time per story
  - Automation ROI (time saved)
  - Bug find rate in testing vs production
```

### Team Collaboration

```yaml
Engagement:
  - Participation in sprint planning: 100%
  - Quality advocacy in design reviews
  - Pair testing sessions > 3/week
  - Documentation contributions
```

## 🔧 Herramientas del Día a Día

```yaml
IDE & Code:
  - VS Code
  - Extensions: ESLint, Prettier, GitLens
  - Postman / Insomnia
  
Test Automation:
  - Playwright / Cypress
  - Playwright Test (test runner)
  - Vitest / Jest (unit tests)
  
API Testing:
  - Postman
  - Newman (CLI)
  - REST Client (VS Code)
  
Performance:
  - K6
  - Lighthouse
  - Application Insights
  
Bug Tracking:
  - Azure DevOps
  - Jira
  - GitHub Issues
  
CI/CD:
  - GitHub Actions
  - Azure Pipelines
  
Database:
  - Azure Data Studio
  - SQL Server Management Studio
  
Browsers & DevTools:
  - Chrome DevTools
  - Firefox Developer Tools
  - Edge DevTools
  - Browser extensions (axe, WAVE for accessibility)
  
Collaboration:
  - Slack / Teams
  - Notion / Confluence (documentation)
  - Miro (test planning)
```

## 🏗️ Test Automation Examples

### Playwright E2E Test Example

```typescript
// tests/checkout.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Checkout Flow', () => {
  test.beforeEach(async ({ page }) => {
    await page.goto('/products');
  });

  test('user can complete purchase with credit card', async ({ page }) => {
    // Add product to cart
    await page.click('[data-testid="product-1"]');
    await page.click('button:has-text("Add to Cart")');
    
    // Verify cart
    await expect(page.locator('[data-testid="cart-count"]')).toHaveText('1');
    
    // Go to checkout
    await page.click('[data-testid="cart-icon"]');
    await page.click('button:has-text("Checkout")');
    
    // Fill shipping info
    await page.fill('[name="fullName"]', 'John Doe');
    await page.fill('[name="address"]', '123 Main St');
    await page.fill('[name="city"]', 'Seattle');
    await page.selectOption('[name="state"]', 'WA');
    await page.fill('[name="zip"]', '98101');
    
    // Fill payment info
    await page.fill('[name="cardNumber"]', '4242424242424242');
    await page.fill('[name="expiry"]', '12/25');
    await page.fill('[name="cvv"]', '123');
    
    // Submit order
    await page.click('button:has-text("Place Order")');
    
    // Verify success
    await expect(page.locator('h1')).toContainText('Order Confirmed');
    await expect(page.locator('[data-testid="order-number"]')).toBeVisible();
  });

  test('shows validation errors for invalid payment', async ({ page }) => {
    // ... navigate to checkout
    
    // Invalid card number
    await page.fill('[name="cardNumber"]', '1111111111111111');
    await page.click('button:has-text("Place Order")');
    
    await expect(page.locator('.error')).toContainText('Invalid card number');
  });
});
```

### API Testing Example (SuperTest)

```typescript
// tests/api/orders.test.ts
import request from 'supertest';
import { expect } from 'chai';

const API_URL = 'https://api.example.com';

describe('Orders API', () => {
  let authToken: string;
  
  before(async () => {
    // Get auth token
    const response = await request(API_URL)
      .post('/auth/login')
      .send({ email: 'test@example.com', password: 'password123' });
    
    authToken = response.body.token;
  });

  it('should create a new order', async () => {
    const order = {
      items: [
        { productId: 1, quantity: 2 },
        { productId: 3, quantity: 1 }
      ],
      shippingAddress: {
        street: '123 Main St',
        city: 'Seattle',
        state: 'WA',
        zip: '98101'
      }
    };

    const response = await request(API_URL)
      .post('/api/orders')
      .set('Authorization', `Bearer ${authToken}`)
      .send(order)
      .expect(201);

    expect(response.body).to.have.property('orderId');
    expect(response.body.total).to.be.a('number');
    expect(response.body.status).to.equal('pending');
  });

  it('should validate required fields', async () => {
    const invalidOrder = {
      items: [] // empty items - should fail
    };

    const response = await request(API_URL)
      .post('/api/orders')
      .set('Authorization', `Bearer ${authToken}`)
      .send(invalidOrder)
      .expect(400);

    expect(response.body.error).to.include('items');
  });
});
```

### Performance Test Example (K6)

```javascript
// tests/performance/checkout-load.js
import http from 'k6/http';
import { check, sleep } from 'k6';

export const options = {
  stages: [
    { duration: '1m', target: 50 },  // Ramp up to 50 users
    { duration: '3m', target: 50 },  // Stay at 50 users
    { duration: '1m', target: 0 },   // Ramp down
  ],
  thresholds: {
    http_req_duration: ['p(95)<500'], // 95% requests < 500ms
    http_req_failed: ['rate<0.01'],   // Error rate < 1%
  },
};

export default function () {
  // Homepage
  let res = http.get('https://example.com');
  check(res, {
    'homepage status 200': (r) => r.status === 200,
    'homepage load time < 500ms': (r) => r.timings.duration < 500,
  });

  sleep(1);

  // Product page
  res = http.get('https://example.com/products/123');
  check(res, {
    'product status 200': (r) => r.status === 200,
  });

  sleep(2);

  // Add to cart (API)
  res = http.post('https://api.example.com/cart', JSON.stringify({
    productId: 123,
    quantity: 1,
  }), {
    headers: { 'Content-Type': 'application/json' },
  });
  
  check(res, {
    'add to cart success': (r) => r.status === 200,
    'add to cart fast': (r) => r.timings.duration < 300,
  });

  sleep(1);
}
```

## 🚀 Career Progression

### From Junior to Mid (2-3 años)

```yaml
Focus Areas:
  - Master test automation
  - Programming proficiency
  - API testing
  - CI/CD integration
  
Milestones:
  ✓ Own automated test suites
  ✓ Contribute to framework
  ✓ Independent feature testing
  ✓ Mentor juniors
  ✓ Quality advocacy
```

### From Mid to Senior (3-5 años)

```yaml
Focus Areas:
  - Test strategy & architecture
  - Performance testing
  - Cross-team collaboration
  - Process improvement
  
Milestones:
  ✓ Design test frameworks
  ✓ Quality roadmap ownership
  ✓ Performance engineering
  ✓ Team mentorship
  ✓ Influence engineering practices
```

### From Senior to Staff / QA Lead (5+ años)

```yaml
Focus Areas:
  - Organization-wide quality
  - Platform engineering
  - Strategic initiatives
  - Industry leadership
  
Milestones:
  ✓ Company quality strategy
  ✓ Test platform development
  ✓ Multi-team initiatives
  ✓ Tool adoption strategy
  ✓ Industry thought leadership
```

## 💡 Modern QA Principles

### Shift-Left Testing
```yaml
Concept:
  - Test early in SDLC
  - QA involved from requirements
  - Prevention over detection
  
Practices:
  ✓ Participate in sprint planning
  ✓ Review designs for testability
  ✓ Pair with developers
  ✓ Unit test collaboration
  ✓ Early automation
```

### Test Pyramid
```yaml
Structure:
  Unit Tests (70%):
    - Fast, isolated
    - Developer-owned (QA collaborates)
    - Run on every commit
  
  Integration Tests (20%):
    - API testing
    - Component integration
    - Database testing
  
  E2E Tests (10%):
    - Critical user journeys
    - Cross-browser
    - Slower, more brittle
    - Focus on happy paths + critical edges
```

### Quality Ownership
```yaml
Mindset:
  - Quality is team responsibility, not just QA
  - QA enables quality, doesn't own it
  - Developers write tests, QA guides strategy
  
QA Role:
  ✓ Quality advocate
  ✓ Testing expert
  ✓ Framework builder
  ✓ Mentor & enabler
  ✗ Not "gatekeeper"
```

---

**Reporta a**: Engineering Manager / QA Lead  
**Colabora con**: Developers (todos), Product, Design, DevOps  
**Última actualización**: Diciembre 2025
