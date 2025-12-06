# Mobile Developer

## 📋 Descripción del Rol

El Mobile Developer se especializa en crear aplicaciones nativas o cross-platform para iOS y Android. Trabaja con tecnologías móviles específicas, considerando constraints únicos de dispositivos móviles como batería, conectividad intermitente, diferentes tamaños de pantalla, y capacidades del hardware.

## 🎯 Responsabilidades Principales

### Desarrollo de Aplicaciones Móviles
- Implementar interfaces nativas o cross-platform
- Optimizar performance en dispositivos móviles
- Manejar diferentes tamaños de pantalla y orientaciones
- Implementar gestures y navegación móvil
- Publicar en App Store y Google Play

### Integración con Backend
- Consumir RESTful APIs o GraphQL
- Implementar sincronización de datos
- Manejar offline-first scenarios
- Caching y persistencia local
- Push notifications

### Performance y Optimización
- Optimizar tiempo de inicio (cold start)
- Reducir tamaño de bundle/APK
- Gestión eficiente de memoria
- Optimización de batería
- Animaciones a 60 FPS

### Platform-Specific Features
- Acceso a cámara, GPS, sensores
- Biometrics (Face ID, Touch ID)
- In-app purchases
- Deep linking
- Platform guidelines (iOS HIG, Material Design)

## 🛠️ Stack Tecnológico

### Cross-Platform (Recomendado para la mayoría)

#### React Native
```yaml
Framework: React Native 0.73+
Language: TypeScript
State: Redux Toolkit, Zustand, Jotai
Navigation: React Navigation 6
UI: React Native Paper, NativeBase
Testing: Jest, Detox

Pros:
  ✓ Código compartido iOS + Android (95%+)
  ✓ Ecosistema React
  ✓ Hot reload
  ✓ Large community
  ✓ Expo para rapid development
  
Cons:
  ✗ Performance en apps muy complejas
  ✗ Bridge overhead
  ✗ Depende de native modules

Example Stack:
  - React Native + TypeScript
  - React Navigation
  - React Query (data fetching)
  - Zustand (state)
  - React Native MMKV (storage)
```

#### Flutter
```yaml
Framework: Flutter 3.16+
Language: Dart 3
State: Riverpod, Bloc, Provider
Navigation: Navigator 2.0, go_router
UI: Material 3, Cupertino widgets
Testing: flutter_test, integration_test

Pros:
  ✓ Performance (compilado a native)
  ✓ Hermoso UI out-of-the-box
  ✓ Single codebase
  ✓ Hot reload excelente
  ✓ Google backing
  
Cons:
  ✗ Dart no es mainstream
  ✗ App size mayor
  ✗ Menos third-party packages que RN

Example Stack:
  - Flutter + Dart 3
  - Riverpod (state)
  - Dio (HTTP)
  - Hive (local storage)
  - Firebase (backend)
```

### Native (Para apps complejas o específicas)

#### iOS Native
```yaml
Language: Swift 5.9+
UI: SwiftUI + UIKit
Architecture: MVVM, TCA (The Composable Architecture)
Networking: URLSession, Alamofire
Storage: Core Data, Realm, SQLite
Testing: XCTest, Quick/Nimble

When to use:
  - iOS-only app
  - Maximum performance needed
  - Heavy use of iOS-specific features
  - Games (con SpriteKit/SceneKit)
```

#### Android Native
```yaml
Language: Kotlin 1.9+
UI: Jetpack Compose + XML Views
Architecture: MVVM + Clean Architecture
Networking: Retrofit, OkHttp
Storage: Room, DataStore
Testing: JUnit, Espresso, Robolectric

When to use:
  - Android-only app
  - Maximum performance needed
  - Heavy use of Android-specific features
  - Wearables (Wear OS)
```

### Backend & Services

```yaml
APIs:
  - REST (JSON)
  - GraphQL (Apollo Client)
  - gRPC (móvil a backend)
  
Backend Services:
  - Firebase (auth, firestore, analytics, crashlytics)
  - Azure Mobile Apps
  - AWS Amplify
  
Analytics:
  - Firebase Analytics
  - App Center Analytics
  - Mixpanel
  
Crash Reporting:
  - Firebase Crashlytics
  - Sentry
```

## 📈 Niveles de Seniority

### Junior Mobile Developer (0-2 años)

```yaml
Habilidades Técnicas:
  ✓ React Native o Flutter basics
  ✓ UI component development
  ✓ API integration basics
  ✓ Git basics
  ✓ Debugging tools

Responsabilidades:
  - Implementar screens simples
  - Bug fixes
  - UI adjustments
  - Basic API integration

Autonomía:
  - Requiere supervisión frecuente
  - Pair programming regular
  - Tareas bien especificadas
```

### Mid-level Mobile Developer (2-5 años)

```yaml
Habilidades Técnicas:
  ✓ React Native/Flutter proficiency
  ✓ State management
  ✓ Performance optimization
  ✓ Platform-specific code
  ✓ App store deployment
  ✓ Testing

Responsabilidades:
  - Implementar features complejas
  - Offline-first functionality
  - Push notifications
  - In-app purchases
  - Performance tuning
  - Code reviews

Autonomía:
  - Trabaja independientemente
  - Technical decision making
  - Mentoría a juniors
```

### Senior Mobile Developer (5-8 años)

```yaml
Habilidades Técnicas:
  ✓ Multiple platforms (React Native + Native)
  ✓ Architecture patterns
  ✓ Performance expert
  ✓ CI/CD para mobile
  ✓ App store optimization
  ✓ Security best practices

Responsabilidades:
  - Mobile architecture
  - Technical leadership
  - App optimization
  - Release management
  - Team mentorship
  - Technical debt management

Liderazgo:
  - Define mobile strategy
  - Establish best practices
  - Cross-platform decisions
```

### Staff Mobile Engineer (8+ años)

```yaml
Habilidades Técnicas:
  ✓ Todas las anteriores
  ✓ Mobile platform strategy
  ✓ Multi-app architecture
  ✓ Developer tooling
  ✓ Strategic thinking

Responsabilidades:
  - Mobile platform vision
  - Cross-team architecture
  - Developer experience
  - Organization-wide impact
  - Industry thought leadership

Scope:
  - Multiple apps/teams
  - Company mobile strategy
  - Industry influence
```

## 💼 Día Típico

### Morning (9:00 - 12:00)
```
09:00 - Daily standup (15 min)
09:15 - Code review de 2 PRs mobile (30 min)
09:45 - Implementar pantalla de Product Details (2 horas)
       - Diseñar layout responsive
       - Image carousel con gestures
       - Add to cart functionality
       - API integration
       - Loading states
       - Error handling
       - Unit tests
```

### Afternoon (13:00 - 18:00)
```
13:00 - Lunch
14:00 - Fix crash reportado en Crashlytics (1 hora)
       - Analizar stack trace
       - Reproducir issue
       - Fix + test
       - Deploy hotfix
       
15:00 - Performance optimization (1.5 horas)
       - Reducir app size (code splitting)
       - Optimize images
       - Lazy loading
       - Memoization
       
16:30 - Pair programming: Push Notifications setup (1 hora)
       - Firebase Cloud Messaging
       - iOS/Android config
       - Deep linking
       
17:30 - Preparar build para TestFlight/Play Console (30 min)
```

## 🎓 Skills Matrix

### Must Have (Senior Level)

| Skill | Nivel | Importancia |
|-------|-------|-------------|
| React Native / Flutter | 5/5 | ⭐⭐⭐⭐⭐ |
| JavaScript/TypeScript (RN) o Dart (Flutter) | 5/5 | ⭐⭐⭐⭐⭐ |
| Mobile UI/UX | 5/5 | ⭐⭐⭐⭐⭐ |
| State Management | 4/5 | ⭐⭐⭐⭐ |
| API Integration | 4/5 | ⭐⭐⭐⭐ |
| Platform-specific code (iOS/Android) | 4/5 | ⭐⭐⭐⭐ |
| Performance Optimization | 4/5 | ⭐⭐⭐⭐ |
| Testing | 4/5 | ⭐⭐⭐⭐ |
| App Store Deployment | 4/5 | ⭐⭐⭐⭐ |
| Git | 4/5 | ⭐⭐⭐⭐ |
| Firebase / Mobile Backend | 3/5 | ⭐⭐⭐ |
| CI/CD Mobile | 3/5 | ⭐⭐⭐ |

### Nice to Have

| Skill | Nivel | Importancia |
|-------|-------|-------------|
| Native iOS (Swift) | 3/5 | ⭐⭐⭐ |
| Native Android (Kotlin) | 3/5 | ⭐⭐⭐ |
| GraphQL | 3/5 | ⭐⭐⭐ |
| Animations | 3/5 | ⭐⭐⭐ |
| Offline-first | 3/5 | ⭐⭐⭐ |
| AR/VR | 2/5 | ⭐⭐ |

## 📚 Learning Path

### Foundational (Months 1-4)

```yaml
Month 1: Mobile Development Basics
  - Choose platform (React Native vs Flutter)
  - Setup dev environment
  - Basic components/widgets
  - Layouts & styling
  - Navigation basics
  
Month 2: State & Data
  - State management (Redux/Riverpod)
  - API integration (fetch/dio)
  - Local storage
  - Forms & validation
  
Month 3: Platform Features
  - Camera access
  - Location services
  - Push notifications
  - Permissions handling
  
Month 4: First App
  - Build complete app (Todo + Auth)
  - Deploy to TestFlight/Play Console
  - Analytics integration
  - Crash reporting
```

### Intermediate (Months 5-10)

```yaml
Month 5-6: Advanced UI
  - Custom animations
  - Gestures
  - Complex layouts
  - Accessibility
  - Dark mode
  
Month 7-8: Performance
  - App size optimization
  - Startup time reduction
  - Memory management
  - 60 FPS animations
  - Network optimization
  
Month 9-10: Platform-Specific
  - iOS: Write Swift modules
  - Android: Write Kotlin modules
  - Bridge native code
  - Platform channels
```

### Advanced (Months 11-18)

```yaml
Month 11-12: Architecture
  - Clean Architecture
  - MVVM / BLoC patterns
  - Modular apps
  - Code sharing strategies
  
Month 13-14: Advanced Features
  - Offline-first architecture
  - Background tasks
  - In-app purchases
  - Deep linking
  - Universal links
  
Month 15-16: DevOps & Release
  - Fastlane automation
  - CI/CD (App Center, Bitrise)
  - Beta testing workflows
  - App Store Optimization (ASO)
  
Month 17-18: Specialization
  - Choose: Native (Swift/Kotlin) OR
  - Advanced cross-platform patterns
  - Micro-frontends mobile
  - Performance at scale
```

## 🎯 KPIs y Métricas

### Individual Performance

```yaml
Code Quality:
  - Code review approval > 95%
  - Crash-free rate > 99.5%
  - Test coverage > 80%
  - Zero critical bugs in production
  
Delivery:
  - Feature delivery on time > 90%
  - Sprint commitment > 90%
  - Time to PR review < 4 hours
  
Technical:
  - App startup time < 3 seconds
  - App size < 50MB (Android), < 30MB (iOS)
  - 60 FPS animations
  - API response handling < 300ms
  
User Experience:
  - App Store rating > 4.5
  - User retention (Day 7) > 40%
  - Session length growth
```

### Team Contribution

```yaml
Collaboration:
  - Code reviews > 10/week
  - Pair programming > 4h/week
  - Knowledge sharing sessions
  
Release Management:
  - Successful releases > 95%
  - Hotfix rate < 5%
  - Release notes documentation
  
Innovation:
  - New feature proposals
  - Performance improvements
  - Developer tooling contributions
```

## 🔧 Herramientas del Día a Día

```yaml
IDE:
  - VS Code (React Native, Flutter)
  - Xcode (iOS)
  - Android Studio (Android)
  
Extensions:
  - ESLint / Dart analyzer
  - React Native Tools
  - Flutter extensions
  - GitLens
  
Emulators & Devices:
  - iOS Simulator
  - Android Emulator
  - Physical devices (testing real performance)
  
Design Handoff:
  - Figma
  - Zeplin
  
Debugging:
  - Flipper (React Native)
  - Chrome DevTools
  - Xcode Instruments
  - Android Profiler
  
Release & Distribution:
  - App Store Connect
  - Google Play Console
  - TestFlight
  - Firebase App Distribution
  
Analytics & Monitoring:
  - Firebase Crashlytics
  - Firebase Analytics
  - App Center
  - Sentry
  
Productivity:
  - GitHub Copilot
  - Postman (API testing)
  - Draw.io (architecture)
```

## 🏗️ Common Patterns & Examples

### React Native Example: Offline-First List

```typescript
// hooks/useOfflineList.ts
export function useOfflineList<T>(
  queryKey: string,
  fetchFn: () => Promise<T[]>
) {
  const netInfo = useNetInfo();
  
  const query = useQuery({
    queryKey: [queryKey],
    queryFn: fetchFn,
    enabled: netInfo.isConnected,
    staleTime: 5 * 60 * 1000, // 5 minutes
  });
  
  // Persist to local storage
  useEffect(() => {
    if (query.data) {
      MMKV.set(queryKey, JSON.stringify(query.data));
    }
  }, [query.data]);
  
  // Load from cache if offline
  const cachedData = netInfo.isConnected 
    ? null 
    : JSON.parse(MMKV.getString(queryKey) || '[]');
  
  return {
    data: query.data ?? cachedData,
    isLoading: query.isLoading,
    isOffline: !netInfo.isConnected,
  };
}

// screens/ProductList.tsx
export function ProductListScreen() {
  const { data, isLoading, isOffline } = useOfflineList(
    'products',
    fetchProducts
  );
  
  return (
    <View>
      {isOffline && <OfflineBanner />}
      <FlatList
        data={data}
        renderItem={({ item }) => <ProductCard product={item} />}
        refreshing={isLoading}
      />
    </View>
  );
}
```

### Flutter Example: Platform-Specific UI

```dart
// widgets/platform_button.dart
class PlatformButton extends StatelessWidget {
  final String text;
  final VoidCallback onPressed;
  
  @override
  Widget build(BuildContext context) {
    if (Platform.isIOS) {
      return CupertinoButton(
        onPressed: onPressed,
        child: Text(text),
      );
    }
    
    return ElevatedButton(
      onPressed: onPressed,
      child: Text(text),
    );
  }
}

// Platform-specific code
class CameraService {
  Future<String> capturePhoto() async {
    if (Platform.isIOS) {
      return await _capturePhotoIOS();
    } else {
      return await _capturePhotoAndroid();
    }
  }
  
  Future<String> _capturePhotoIOS() async {
    // iOS-specific camera implementation
  }
  
  Future<String> _capturePhotoAndroid() async {
    // Android-specific camera implementation
  }
}
```

## 🚀 Career Progression

### From Junior to Mid (2-3 años)

```yaml
Focus Areas:
  - Framework mastery (RN/Flutter)
  - State management proficiency
  - Platform-specific features
  - Performance awareness
  
Milestones:
  ✓ Ship features end-to-end
  ✓ Handle app releases independently
  ✓ Integrate complex native modules
  ✓ Debug platform-specific issues
  ✓ Mentor junior developers
```

### From Mid to Senior (3-5 años)

```yaml
Focus Areas:
  - Mobile architecture
  - Performance optimization
  - Cross-platform strategies
  - Technical leadership
  
Milestones:
  ✓ Design app architecture
  ✓ Optimize app for App Store
  ✓ Lead mobile initiatives
  ✓ Establish mobile best practices
  ✓ CI/CD automation
```

### From Senior to Staff (5+ años)

```yaml
Focus Areas:
  - Mobile platform strategy
  - Multi-app architecture
  - Developer experience
  - Strategic vision
  
Milestones:
  ✓ Define mobile technology strategy
  ✓ Cross-platform architecture decisions
  ✓ Organization-wide mobile standards
  ✓ Mobile team enablement
  ✓ Industry thought leadership
```

## 📱 Platform Comparison

### React Native vs Flutter vs Native

```yaml
React Native:
  Pros:
    ✓ JavaScript/TypeScript (familiar)
    ✓ Large ecosystem
    ✓ Expo for rapid development
    ✓ Hot reload
    ✓ Web code sharing possible
  
  Cons:
    ✗ Performance overhead (bridge)
    ✗ Larger app size
    ✗ Native code sometimes needed
  
  Best For:
    - Teams with React experience
    - Rapid prototyping
    - Content-heavy apps
    - Startups (speed to market)

Flutter:
  Pros:
    ✓ Excellent performance
    ✓ Beautiful UI out-of-box
    ✓ Hot reload
    ✓ Single codebase
    ✓ Growing ecosystem
  
  Cons:
    ✗ Dart learning curve
    ✗ Larger app size
    ✗ Less mature than RN
  
  Best For:
    - UI-heavy apps
    - High performance needs
    - Teams starting fresh
    - Cross-platform consistency

Native (Swift/Kotlin):
  Pros:
    ✓ Maximum performance
    ✓ Full platform access
    ✓ Best user experience
    ✓ Latest features first
  
  Cons:
    ✗ Two codebases
    ✗ Slower development
    ✗ Higher cost
  
  Best For:
    - Platform-specific apps
    - Complex apps
    - Games
    - Enterprise apps with budget
```

---

**Reporta a**: Tech Lead / Engineering Manager  
**Colabora con**: Backend Developers, Diseño, QA, Product  
**Última actualización**: Diciembre 2025
