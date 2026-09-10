# Coffy Flow — Backend API & WebSockets Service

Servicio backend desacoplado que centraliza las reglas de negocio, persistencia relacional y sincronización en tiempo real para la plataforma Coffy Flow[cite: 3].

---

## 🚀 Tecnologías Principales

- **Framework:** NestJS (Node.js con TypeScript)[cite: 3]
- **Arquitectura:** Modular por Capas (Controllers, Services/Use Cases, Repositories)[cite: 3]
- **Base de Datos:** PostgreSQL[cite: 3]
- **ORM / Query Builder:** Drizzle ORM / Prisma[cite: 3]
- **Tiempo Real:** `@nestjs/websockets` (Socket.io) para sincronización KDS y control de stock[cite: 3]
- **Validación y DTOs:** `class-validator`, `class-transformer`
- **Contenedores:** Docker & Docker Compose[cite: 3]

---

## 🏛️ Estructura del Proyecto

El backend organiza cada recurso del negocio dentro de su propio módulo autónomo:

```text
src/
├── common/                       # Filtros globales, interceptores, guards (RBAC) y decoradores
├── config/                       # Configuración de variables de entorno y base de datos
├── database/                     # Esquemas, migraciones y seeds
└── modules/                      # Módulos de Dominio de Negocio
    ├── auth/                     # Autenticación, JWT, RBAC y recuperación de credenciales
    ├── users/                    # Gestión de personal y roles operativos
    ├── menu/                     # Categorías, productos y disponibilidad inmediata
    ├── tables/                   # Identificadores y estados de mesas físicas
    ├── orders/                   # Comandas y persistencia del flujo POS
    ├── kds/                      # Gateways de WebSockets y eventos de cocina
    ├── transactions/             # Cajas, arqueos y conciliación de tickets
    └── dashboard/                # Agregación de métricas e indicadores de venta
```

## 📦 Flujo de Trabajo y Ramas (GitFlow Adaptado)

El control de versiones replica el modelo estructurado del proyecto:

- **main:** Rama de documentación del servicio, esquemas técnicos y contratos API.
- **prod:** Versión estable desplegada en el entorno de servidor en la nube.
- **qa:** Entorno de homologación, pruebas unitarias y validación con Postman[cite: 3].
- **develop:** Rama activa de integración de servicios.
- **Ramas de Módulo / Feature (`feature/*`):** Ramas que nacen de `develop`:
  - `feature/backend-auth`
  - `feature/backend-kds`
  - `feature/backend-pos`
  - `feature/backend-transactions`
  - `feature/backend-menu`

## 🛠️ Puesta en Marcha

### Prerrequisitos

- Node.js 20 LTS o superior[cite: 3]
- Docker y Docker Compose (para base de datos local)[cite: 3]

### Instalación

1. Clonar el repositorio:

```bash
git clone https://github.com/tu-organizacion/coffy-flow-backend.git
cd coffy-flow-backend
```

2. Instalar dependencias:

```bash
npm install
```

3. Configurar variables de entorno:

```bash
cp .env.example .env
```

Definir `PORT`, `DATABASE_URL`, `JWT_SECRET` y orígenes CORS permitidos.

4. Levantar la base de datos PostgreSQL en Docker[cite: 3]:

```bash
docker compose up -d
```

5. Ejecutar migraciones:

```bash
npm run db:migrate
```

6. Iniciar el servidor en modo desarrollo:

```bash
npm run start:dev
```

La API estará escuchando en [http://localhost:4000](http://localhost:4000) (o el puerto configurado). Documentación Swagger disponible en `/api/docs`.
