# UI Designer

## 📋 Visión General

El UI Designer es responsable del **diseño visual** de interfaces de usuario, creando experiencias estéticamente atractivas, consistentes, y que refuercen la identidad de marca. Trabaja sobre wireframes de UX para añadir color, tipografía, iconografía, y micro-interacciones que dan vida al producto.

## 🎯 Responsabilidades

### Visual Design

**Principales tareas**:
- Diseñar interfaces high-fidelity (mockups finales)
- Aplicar branding y visual identity
- Crear paletas de colores accesibles
- Seleccionar tipografías apropiadas
- Diseñar layouts responsive (mobile, tablet, desktop)

**Entregables**:
- High-fidelity mockups (Figma, Sketch)
- Visual design specs (color codes, spacing, typography)
- Responsive layouts (breakpoints para mobile, tablet, desktop)
- Style tiles (exploración de estilos visuales)

**Principios de visual design**:
- **Contrast**: Crear jerarquía visual (headings vs body text)
- **Alignment**: Todo alineado a una grid invisible
- **Repetition**: Consistencia de estilos
- **Proximity**: Elementos relacionados agrupados
- **White space**: Espacio negativo, breathing room
- **Color theory**: Armonía de colores, psicología

---

### Design Systems & Component Libraries

**Principales tareas**:
- Crear y mantener design system (biblioteca de componentes reutilizables)
- Diseñar components: buttons, inputs, cards, modals, etc.
- Documentar usage guidelines (cuándo usar qué component)
- Tokens de diseño (colors, spacing, typography)
- Handoff de design system a Frontend (Figma → código)

**Componentes típicos en design system**:
```yaml
Foundations:
  - Colors (primary, secondary, semantic, neutrals)
  - Typography (font families, sizes, weights, line heights)
  - Spacing (4px, 8px, 16px, 24px, 32px grid)
  - Iconography (icon library, sizes)
  - Elevation (shadows, z-index)

Components:
  - Buttons (primary, secondary, tertiary, icon buttons)
  - Inputs (text, textarea, select, checkbox, radio, toggle)
  - Cards (product card, info card, media card)
  - Navigation (header, sidebar, breadcrumbs, tabs)
  - Modals & Dialogs
  - Toasts & Alerts
  - Tables & Lists
  - Forms (layouts, validation states)
```

**Tools**:
- **Figma** (design system master file + component library)
- **Storybook** (frontend component library documentation)
- **Zeroheight / Supernova**: Design system documentation platforms

---

### Iconography

**Principales tareas**:
- Diseñar icon sets consistentes
- Curate icon libraries (Material Icons, Feather, Font Awesome)
- Customizar icons para branding
- Asegurar accesibilidad (tamaño mínimo 24x24px para tap targets)

**Estilos de iconos**:
- **Outlined**: Lineal, moderno (e.g., Material Outlined)
- **Filled**: Sólido, más visual (e.g., Material Filled)
- **Flat**: Minimalista, sin profundidad
- **Duo-tone**: Dos colores, más expresivo

**Best practices**:
- Consistencia de stroke width (2px típico)
- Grid alignment (diseñar sobre 24x24px grid)
- SVG format (escalable, performance)
- Naming conventions claras (`icon-arrow-right.svg`)

---

### Typography

**Principales tareas**:
- Seleccionar font families apropiadas
- Definir type scale (tamaños de texto jerárquicos)
- Line heights, letter spacing
- Responsive typography (tamaños por breakpoint)
- Web font optimization (performance)

**Type scale ejemplo** (Tailwind-inspired):
```yaml
Headings:
  - H1: 48px / 3rem (font-weight: 700)
  - H2: 36px / 2.25rem (font-weight: 700)
  - H3: 30px / 1.875rem (font-weight: 600)
  - H4: 24px / 1.5rem (font-weight: 600)
  - H5: 20px / 1.25rem (font-weight: 600)
  - H6: 18px / 1.125rem (font-weight: 600)

Body:
  - Large: 18px / 1.125rem
  - Base: 16px / 1rem (default)
  - Small: 14px / 0.875rem
  - XSmall: 12px / 0.75rem (captions, labels)
```

**Font pairing**:
- **Serif + Sans-serif**: Clásico (e.g., Playfair + Inter)
- **Geometric + Humanist**: Moderno (e.g., Futura + Open Sans)
- **Monospace**: Código, datos (e.g., Fira Code)

**Web fonts**:
- Google Fonts (gratis, CDN rápido)
- Adobe Fonts (calidad premium, requiere Creative Cloud)
- Self-hosted fonts (control total, privacy)

---

### Color Systems

**Principales tareas**:
- Diseñar paletas de colores (primary, secondary, semantic)
- Asegurar accesibilidad (WCAG contrast ratios)
- Dark mode design
- Color tokens para design system
- Semantic colors (success, error, warning, info)

**Paleta típica**:
```yaml
Primary: #3B82F6 (brand color, CTAs)
  - Shades: 50, 100, 200, 300, 400, 500 (base), 600, 700, 800, 900

Secondary: #8B5CF6 (complementario)

Neutrals (Grays):
  - 50 (lightest) → 900 (darkest)
  - Uso: text, backgrounds, borders

Semantic:
  - Success: #10B981 (green)
  - Error: #EF4444 (red)
  - Warning: #F59E0B (amber)
  - Info: #3B82F6 (blue)
```

**Accesibilidad de color**:
- **WCAG AA**: Contrast ratio ≥4.5:1 (text normal), ≥3:1 (text grande)
- **WCAG AAA**: Contrast ratio ≥7:1 (text normal), ≥4.5:1 (text grande)
- **Tools**: WebAIM Contrast Checker, Stark plugin (Figma)

**Dark mode**:
- No invertir colores simplemente
- Background: No pure black (#000), usar dark gray (#121212 a #1E1E1E)
- Elevar surfaces con subtle shadows o borders
- Reducir contrast en texto (no pure white #FFF, usar #E0E0E0)

---

### Micro-interactions & Animations

**Principales tareas**:
- Diseñar transiciones entre estados
- Hover, focus, active states
- Loading states (spinners, skeletons)
- Animations para delight (celebratory animations)
- Prototipar interactions en Figma / Principle / Framer

**Tipos de micro-interactions**:
- **Feedback**: Confirmar acción (e.g., button click, form submit)
- **State change**: Mostrar cambio (e.g., toggle on/off, favorite)
- **Affordance**: Indicar interactividad (e.g., hover states)
- **Progressive disclosure**: Revelar información gradualmente

**Principios de animation**:
- **Duration**: 200-300ms típico (no muy lento ni rápido)
- **Easing**: Ease-out (natural, no linear)
- **Purposeful**: Animación debe comunicar algo, no ser decorativa
- **Performance**: 60fps, usar CSS transforms (no margin/width)

**Tools**:
- **Figma**: Smart Animate (basic interactions)
- **Principle**: Animation prototyping
- **Framer**: Code-based interactions
- **Lottie**: JSON animations (After Effects → Lottie → Web)

---

## 💼 Perfil del Rol

### Seniority

**Nivel**: Junior a Senior (1-8 años de experiencia)

**Progresión típica**:
```
Junior UI Designer (0-2 años)
    - Tareas: Mockups básicos, component design, design system contribution
    ↓
UI Designer (2-5 años)
    - Tareas: Ownership de visual design, design system, iconography
    ↓
Senior UI Designer (5-8 años)
    - Tareas: Design system lead, branding, mentoring
    ↓
Lead UI Designer / Design Systems Lead (8+ años)
    - Tareas: Design system strategy, cross-product consistency
```

---

### Skills Requeridas

#### Visual Design (Critical)

**Must have**:
- ✅ **Color theory**: Paletas armoniosas, accesibilidad
- ✅ **Typography**: Font pairing, type scale, hierarchy
- ✅ **Layout design**: Grid systems, alignment, spacing
- ✅ **Composition**: Balance, contrast, proximity
- ✅ **Iconography**: Icon design, consistency
- ✅ **Design systems**: Component libraries, tokens

**Nice to have**:
- 🔶 **Illustration**: Crear custom illustrations
- 🔶 **Motion design**: Animations complejas (After Effects)
- 🔶 **3D design**: Spline, Blender (emerging trend)

---

#### Tools & Software

**Must have**:
- ✅ **Figma** (industry standard, collaborative)
- ✅ **Design systems knowledge** (Atomic Design, Tokens)
- ✅ **Prototyping** (Figma Smart Animate, Principle)
- ✅ **Hand-off tools** (Figma Dev Mode, Zeplin)

**Nice to have**:
- 🔶 **Sketch** (legacy, aún usado)
- 🔶 **Adobe Creative Suite**: Photoshop, Illustrator (assets)
- 🔶 **Framer**: Code-based design (trending)
- 🔶 **Spline**: 3D design
- 🔶 **After Effects + Lottie**: Animations

---

#### Technical Skills (Basic)

**Nice to have** (no requerido, pero muy útil):
- 🔶 **HTML/CSS basics**: Entender cómo se implementa
- 🔶 **Responsive design**: Breakpoints, flexible layouts
- 🔶 **Accessibility**: WCAG, ARIA, keyboard navigation
- 🔶 **Performance**: Image optimization, web fonts

---

#### Soft Skills

**Must have**:
- ✅ **Atención al detalle**: Pixel-perfect designs
- ✅ **Creatividad**: Explorar soluciones visuales
- ✅ **Colaboración**: Trabajar con UX, PM, Engineering
- ✅ **Comunicación**: Defender decisiones de diseño
- ✅ **Feedback receptivity**: Iterar basado en critique

---

### Stack Tecnológico

El UI Designer usa principalmente **design tools**:

#### Design & Prototyping
```yaml
Primary: Figma (mockups, design systems, prototypes)
Alternatives: Sketch, Adobe XD
Animation: Principle, Framer, Figma Smart Animate
3D: Spline, Blender (emerging)
```

#### Design Systems
```yaml
Documentation: Zeroheight, Supernova, Storybook
Tokens: Style Dictionary (design tokens → code)
Version control: Git (design system changes)
```

#### Assets & Graphics
```yaml
Icons: Figma (custom), Heroicons, Feather, Material Icons
Illustrations: Figma, Adobe Illustrator
Photos: Unsplash, Pexels (stock), Photoshop (editing)
Animations: After Effects + Lottie
```

#### Hand-off to Development
```yaml
Figma Dev Mode (specs, code snippets)
Zeplin (legacy, design hand-off)
Avocode (design inspection)
```

---

## 📊 Métricas de Éxito

### Design Quality Metrics

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Design Consistency Score** | >90% (design system adoption) | Mensual |
| **Accessibility Compliance** | 100% WCAG AA | Pre-launch |
| **Design Hand-off Time** | <2 días | Por feature |
| **Design QA Pass Rate** | >95% (implementación fiel) | Por sprint |

### Design System Metrics

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Component Coverage** | >80% UI con design system components | Trimestral |
| **Component Reusability** | >70% components reusados en 2+ lugares | Trimestral |
| **Design Debt Ratio** | <10% (inconsistencias visuales) | Mensual |
| **Design System Adoption** | >90% engineering usando library | Trimestral |

### Collaboration Metrics

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Design Critique Participation** | 100% mockups reviewed | Semanal |
| **Engineering Satisfaction** | >4/5 (hand-off clarity) | Trimestral |
| **Design Iteration Cycles** | <3 iterations por feature | Por feature |

### Business Impact Metrics (indirect)

| Métrica | Target | Influencia UI |
|---------|--------|---------------|
| **Brand Perception** | Positive sentiment | Media |
| **User Engagement** | +10% (attractive UI) | Baja-Media |
| **Design Awards** | Industry recognition (Awwwards, etc.) | Branding |

---

## 🔄 Interacciones con Otros Equipos

### Con UX Designer

**Frecuencia**: Daily  
**Modo**: **Collaboration** (workflow secuencial UX → UI)

**Actividades**:
- Recibir wireframes de UX
- Iterar juntos en prototipos
- Design critique sessions
- Design system co-creation (UX patterns + visual design)

**División típica**:
- **UX**: Research, IA, wireframes, user flows
- **UI**: Visual design, branding, components, iconography

**Tools**: Figma (shared files), Slack, Daily syncs

---

### Con Frontend Developers

**Frecuencia**: Weekly  
**Modo**: **X-as-a-Service** (handoff) + **Collaboration**

**Actividades**:
- Design hand-off (mockups finales, specs)
- Design system implementation (Figma → code)
- Design QA (revisar implementación fiel)
- Accessibility review
- Performance discussions (image optimization)

**Handoff incluye**:
- High-fidelity mockups (Figma)
- Design specs (spacing, colors, typography) via Figma Dev Mode
- Assets export (icons SVG, images optimizadas)
- Responsive breakpoints (mobile, tablet, desktop)
- Interaction specs (animations, transitions)

**Tools**: Figma Dev Mode, Zeplin, Slack

---

### Con Product Manager

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Feature kickoffs (entender requirements)
- Design iterations basadas en feedback
- Priorización de design system work
- Design validation con stakeholders

**Tools**: Jira, Figma, Bi-weekly planning

---

### Con Product Designer (si hay overlap)

**Frecuencia**: Daily  
**Modo**: **Collaboration** o **Same person**

**Nota**: En startups/small teams, **Product Designer = UX + UI** (mismo rol). En empresas grandes, están separados.

---

### Con Marketing / Brand Team

**Frecuencia**: Monthly a Quarterly  
**Modo**: **Collaboration**

**Actividades**:
- Alineación de branding (colores, tipografía, tono visual)
- Campaign visuals (landing pages, marketing sites)
- Brand guidelines adherence
- Marketing assets creation (banners, social media)

**Tools**: Figma, Adobe Creative Suite, Slack

---

### Con Design Lead / Manager

**Frecuencia**: Weekly (1:1s)  
**Modo**: **Mentoring** + **Feedback**

**Actividades**:
- Career development discussions
- Design critique
- Portfolio reviews
- Skill development planning

---

## 🎓 Desarrollo Profesional

### Path de Carrera

#### Opción 1: Specialist (IC Track)

```
UI Designer (2-5 años)
    ↓
Senior UI Designer (5-8 años)
    - Features complejos, design system ownership
    ↓
Staff UI Designer / Design Systems Lead (8-12 años)
    - Cross-product design systems, strategy
    ↓
Principal UI Designer (12+ años)
    - Design vision, thought leadership
```

#### Opción 2: Generalist (Product Designer)

```
UI Designer (2-5 años)
    ↓
Product Designer (UX + UI combined) (5-8 años)
    - End-to-end ownership (research + visual)
```

#### Opción 3: Brand / Visual Specialist

```
UI Designer (2-5 años)
    ↓
Brand Designer (5-8 años)
    - Focus: Branding, marketing, illustrations
    ↓
Creative Director (10+ años)
    - Lead creative vision, campaigns
```

#### Opción 4: Management

```
Senior UI Designer (5-8 años)
    ↓
Lead UI Designer (8-10 años)
    - Manage 2-4 designers
    ↓
Design Manager (10-12 años)
    - Manage 5-10 designers (UX+UI)
    ↓
Director of Design (12-15 años)
    - Manage design org
```

---

### Skills a Desarrollar

**Próximos 6-12 meses**:
- [ ] Dominar Figma (components, variants, auto-layout)
- [ ] Crear design system from scratch
- [ ] Aprender accessibility (WCAG AA compliance)
- [ ] Portfolio con 3-5 case studies (antes/después, process)
- [ ] Animation fundamentals (Principle, Lottie)

**Próximos 1-2 años**:
- [ ] Contribuir a open-source design system
- [ ] Aprender UX basics (para product designer path)
- [ ] Motion design avanzado (After Effects)
- [ ] Frontend basics (HTML/CSS, para mejor colaboración)
- [ ] Mentoring de junior UI designer

**Próximos 3-5 años** (hacia Senior/Lead):
- [ ] Design system strategy (cross-product)
- [ ] Thought leadership (conferencias, blogs)
- [ ] Brand design expertise
- [ ] Team management (si management track)
- [ ] Industry recognition (Dribbble, Behance influence)

---

### Recursos de Aprendizaje

#### Libros Esenciales

- 📚 **"Refactoring UI"** - Adam Wathan & Steve Schoger (practical UI tips)
- 📚 **"The Design of Everyday Things"** - Don Norman (design principles)
- 📚 **"Atomic Design"** - Brad Frost (design systems methodology)
- 📚 **"Design Systems Handbook"** - DesignBetter.co (free online)
- 📚 **"UI is Communication"** - Everett McKay

#### Cursos

- **Refactoring UI** (Adam Wathan): Paid course, highly practical
- **Figma Official Tutorials**: Free, comprehensive
- **Awwwards Courses**: Advanced UI/UX courses
- **Skillshare**: Typography, color theory courses

#### Comunidades

- **Dribbble**: Design showcase, inspiration
- **Behance**: Portfolio hosting, case studies
- **Designer News**: Design news, discussions
- **Figma Community**: Plugins, templates, resources
- **Twitter**: Follow @steveschoger, @adamwathan, @jessicahische

---

## 📝 Herramientas del Día a Día

### Design & Prototyping

| Tool | Uso | Nivel |
|------|-----|-------|
| **Figma** | Primary design tool (mockups, design systems, prototypes) | Advanced |
| **Sketch** | Alternative (macOS only, legacy projects) | Intermediate |
| **Adobe XD** | Alternative (Adobe ecosystem) | Basic |
| **Framer** | Code-based design, interactions | Intermediate |

### Design Systems

| Tool | Uso |
|------|-----|
| **Figma Libraries** | Shared component libraries |
| **Zeroheight** | Design system documentation |
| **Storybook** | Frontend component library (collaboration with devs) |
| **Style Dictionary** | Design tokens → code |

### Assets & Graphics

| Tool | Uso |
|------|-----|
| **Adobe Illustrator** | Vector graphics, custom icons |
| **Adobe Photoshop** | Image editing, mockups |
| **Spline** | 3D graphics (emerging trend) |
| **Unsplash / Pexels** | Stock photography |

### Animation

| Tool | Uso |
|------|-----|
| **Principle** | Animation prototyping |
| **After Effects + Lottie** | JSON animations para web |
| **Figma Smart Animate** | Basic transitions |

### Handoff & Collaboration

| Tool | Uso |
|------|-----|
| **Figma Dev Mode** | Design specs, code snippets |
| **Zeplin** | Design handoff (legacy) |
| **Slack** | Team communication |

---

## 🚀 Ejemplo de Semana Típica

### Lunes
- **9:00-10:00**: Sprint planning (feature kickoff)
- **10:00-12:00**: Recibir wireframes de UX, explorar visual directions (mood boards)
- **14:00-16:00**: Design system work: Crear nuevo component (data table)
- **16:00-17:00**: Design critique session con team

### Martes
- **9:00-12:00**: Deep work: High-fidelity mockups para nueva feature (desktop)
- **14:00-15:00**: Sync con Frontend dev (design system implementation)
- **15:00-17:00**: Responsive design: Mobile y tablet layouts

### Miércoles
- **9:00-10:00**: 1:1 con Design Manager
- **10:00-12:00**: Iconography: Diseñar 10 custom icons para feature
- **14:00-16:00**: Color palette exploration (dark mode)
- **16:00-17:00**: Design QA: Revisar implementación en staging

### Jueves
- **9:00-12:00**: Deep work: Animations (micro-interactions en Figma Smart Animate)
- **14:00-15:00**: Accessibility review (contrast checker, WCAG compliance)
- **15:00-16:30**: Design handoff meeting con Frontend team (specs, assets export)
- **16:30-17:00**: Update design system documentation (Zeroheight)

### Viernes
- **9:00-10:00**: Team design review (share work, feedback)
- **10:00-12:00**: Portfolio work: Document case study de proyecto reciente
- **14:00-16:00**: Learning time: Tutorial de Spline (3D design), Dribbble inspiration
- **16:00-17:00**: Week wrap-up, backlog planning

**Deep work** (designing mockups): ~40%  
**Design systems**: ~20%  
**Meetings & Collaboration**: ~25%  
**QA & Handoff**: ~10%  
**Learning**: ~5%

---

## 🎯 Señales de que estás listo para este rol

✅ **Tienes**:
- Portfolio con 5-10 proyectos mostrando visual design skills
- Dominio de Figma (components, auto-layout, variants)
- Strong understanding de color theory, typography, layout
- Experiencia creando design systems
- Eye for detail (pixel-perfect designs)

✅ **Puedes**:
- Crear high-fidelity mockups desde wireframes
- Diseñar component libraries consistentes
- Asegurar accesibilidad (WCAG AA contrast ratios)
- Handoff designs a developers con claridad
- Recibir y aplicar feedback constructivamente

✅ **Te gusta**:
- Visual aesthetics (hacer cosas bonitas y funcionales)
- Craftsmanship (atención al detalle)
- Sistemas (design systems, consistency)
- Colaborar con developers para implementación fiel
- Mantenerte actualizado con design trends

---

## 🔗 Links Relacionados

- [UX Designer](ux-designer.md) - Investigación y wireframes
- [Product Designer](product-designer.md) - UX + UI combinado
- [UX Researcher](ux-researcher.md) - Investigación de usuarios
- [Equipo de Diseño](README.md) - Visión general del equipo

---

**Última actualización**: Diciembre 2025  
**Mantenido por**: Lead UI Designer