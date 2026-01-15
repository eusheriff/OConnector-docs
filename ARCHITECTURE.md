# System Architecture

## 🏗️ Architectural Pattern: Edge-First Static Generation
The OConnector platform uses a **Static Site Generation (SSG)** approach with **Edge Delivery**, prioritizing speed, security, and global availability.

### Tech Stack
- **Core**: Next.js 15 (React 19)
- **Language**: TypeScript 5.x (Strict Mode)
- **Styling**: TailwindCSS 3.4 (Utility-first) + Framer Motion (Animations)
- **Infrastructure**: Cloudflare Pages (Global CDN)

## 🔒 Security Model
We implement a "Security-First" approach for the frontend:

1.  **Strict Content Security Policy (CSP)**:
    - `default-src 'self'` prevents unauthorized scripts.
    - Specific allowlists for `cdn.jsdelivr.net` (UI libs) and `fonts.googleapis.com`.
    - Implemented via both `HTTP Headers` (`_headers` file) and `Meta Tags`.

2.  **Transport Security (HSTS)**:
    - Enforced `max-age=31536000` (1 year) with `includeSubDomains`.
    - `preload` directive included for browser list submission.

3.  **Feature Policies**:
    - Disabling sensitive APIs (`camera`, `microphone`, `geolocation`) by default via `Permissions-Policy`.

## ⚡ Performance Optimization Strategy
To achieve a **98/100 Performance Score**, we utilized:

1.  **Code Splitting via Dynamic Imports**:
    - Critical Path: Only `Navbar` and `Hero` are included in the initial bundle.
    - Lazy Loading: Sections like `Services`, `Projects`, `Team`, and `Footer` are loaded dynamically using `next/dynamic` only when needed.

2.  **Asset Optimization**:
    - Font sub-setting with `next/font`.
    - Image optimization via built-in Next.js `Image` component (WebP conversion).

3.  **Edge Caching**:
    - Static assets are cached at Cloudflare's edge locations globally, resulting in <50ms TTFB (Time to First Byte).

## 🧩 Component Design System
- **Atomic Design Principles**: Reusable atoms (`ShimmerButton`), molecules (`ServiceCard`), and organisms (`Hero`).
- **Accessibility (A11y)**:
    - All interactive elements use `aria-label`.
    - Semantic HTML hierarchy (H1 -> H2 -> H3) strictly enforced.
    - Interactive states (Hover/Focus) clearly defined for keyboard navigation.
