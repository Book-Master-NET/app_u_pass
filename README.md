# Screaming Architecture con Next.js 15 + shadcn/ui

Este repositorio sigue **Screaming Architecture**, donde la estructura de carpetas está organizada por dominio (features) en lugar del framework.

---

## 📂 Estructura de carpetas

```
src/
  app/                       # Rutas Next.js (App Router, RSC)
    (public)/                # Segmentos paralelos públicos (marketing, landing)
      page.tsx
    (app)/                   # App autenticada u operativa
      layout.tsx
      clasess/              # Página protegida de productos
        page.tsx
        api/                 # API Routes específicas del feature (opcional)
          route.ts

  features/                  # Slices que gritan dominio (modular por feature)
    clasess/
      ui/                    # Componentes de UI específicos del feature (pueden usar shadcn/ui)
        ProductCard.tsx
        ProductTable.tsx
      actions/               # Server Actions compatibles con RSC (Next.js)
        createProduct.ts
        listClases.ts
      services/              # Orquestación de lógica del dominio (validación, persistencia, etc.)
        clasesService.ts
      schemas/               # Esquemas de validación (Zod), DTOs
        product.ts
      model/                 # Tipos/entidades simples del dominio (TS types)
        Product.ts
      index.ts               # Barrel export del feature

  infrastructure/            # Integraciones externas
    supabase/                # Cliente Supabase y helpers relacionados
      client.ts
    http/                    # Helpers genéricos para fetch
      fetcher.ts

  shared/                    # Código reutilizable y transversal a features
    ui/                      # Componentes genéricos (shadcn/ui + wrappers propios)
      button.tsx
      input.tsx
      data-table/
        DataTable.tsx
    lib/                     # Utilidades compartidas (env, logging, auth, etc.)
      env.ts                 # Validador de variables de entorno (Zod)
      logger.ts              # Logger compartido (puede ser consola o externalizado)
      auth.ts                # Helpers de autenticación (NextAuth u otro)
    hooks/                   # Custom React hooks compartidos
      useDebounce.ts
    styles/                  # Estilos globales y tokens
      globals.css

  config/                    # Configuración del proyecto
    eslint/                  # Reglas ESLint personalizadas (si aplica)
    tsconfig/                # Configuración de TypeScript

public/                      # Archivos públicos (imágenes, fuentes, etc.)
```

---

## 🚀 Cómo correr el proyecto

### 1) Instalar dependencias

```bash
npm install
```

### 2) Variables de entorno

Crea un archivo `.env.local` en la raíz del proyecto con tus claves:

```env
NEXT_PUBLIC_SUPABASE_URL=...
NEXT_PUBLIC_SUPABASE_ANON_KEY=...
```

### 3) Servidor de desarrollo

```bash
npm run dev
```

### 4) Build de producción

```bash
npm run build
npm run start
```

---

## 🧩 Notas

* `app/` solo orquesta rutas y usa features.
* `features/*` encapsula dominio, UI, acciones y servicios.
* `shared/ui` contiene componentes base generados con shadcn/ui.
* `infrastructure/` implementa integraciones externas (Supabase, fetcher, etc.).
* No es necesario lo de los loggers y supabase, aun no se decide
