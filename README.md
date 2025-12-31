# 💰 AUTH-SERVICE CORE (Monorepo)

[![pnpm](https://img.shields.io/badge/pnpm-9.0.0-blue.svg)](https://pnpm.io/)
[![Powered by Turborepo](https://img.shields.io/badge/powered%20by-turborepo-blue.svg)](https://turbo.build/repo)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An advanced, secure, and production-ready **authentication service boilerplate**. This project is built on a **Monorepo architecture** using Turborepo.

**Current status:** The project has implemented a comprehensive **user authentication flow**, including **Registration, Login, Token Refresh, and Forgot/Reset Password**.

---

## ✨ Key Features (Completed)

- **Dual Token System (JWT)**
  - Utilizes short-lived Access Tokens and long-lived Refresh Tokens to optimize security
- **Refresh Token Rotation**
  - The previous Refresh Token is immediately revoked (isRevoked) whenever a new token is issued to prevent session hijacking
- **Security with Redis Blacklisting**
  - Integrates Redis to blacklist Access Tokens upon user logout or password changes
- **Secure Password Reset Mechanism**
  - Uses hashed tokens (`SHA-256`) and delivers reset links via an Email Service (`Nodemailer`)
- **Cookie Security**
  - Refresh Tokens are stored securely in HttpOnly Cookies to mitigate XSS (Cross-Site Scripting) attacks
- **Duplicate Management**
  - Real-time availability checks for Email and Username

---

## 🛠️ Tech Stack

| Category     | Technology      | Description |
|--------------|----------------|-------------|
| **Monorepo** | Turborepo & pnpm | Efficient multi-project management |
| **Backend**  | NestJS v10     | Main backend framework (`apps/api`) |
|              | TypeORM        | ORM for database interaction |
|              | PostgreSQL     | Relational database (`pg`) |
|              | Passport-JWT   | Authentication strategy for NestJS |
|              | Swagger (OpenAPI) | Auto API docs |
| **Caching**  | Redis          | Blacklisting and authentication acceleration via CacheManager |
| **Frontend** | Next.js v15    | Modern UI powered by React v19 (`apps/web`) |
|              | TypeScript     | Main language |
| **UX/UI**    | Chakra UI      | UI component library |
|              | Tailwind CSS   | Utility-first CSS styling |

---

## 📂 Project Structure

The project is managed by Turborepo and consists of the following core components:
- `apps/api`: The NestJS Backend handling authentication logic and APIs.

- `apps/web`: The Next.js Frontend integrating the user interface.

- `packages/`: Contains shared configurations for ESLint, TypeScript, and database schemas.

---

## 🔑 Environment Variables

The backend (`apps/api`) requires environment variables to run.

First, copy the example file:

```bash
cp apps/api/.env.example apps/api/.env
```

---

## 🚀 Quick Start

### Prerequisites

- **Node.js** (v18+)
- **pnpm** (v9.0.0+)
- **PostgreSQL** instance (running locally or remotely)
- **Docker & Docker Compose** (optional, for Option 2)

### Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Wltung/auth-service.git
    cd auth-service
    ```

2.  **Configure Environment:**
    Copy the backend environment file and fill in your database/JWT details (as described in the section above).
    ```bash
    cp apps/api/.env.example apps/api/.env
    ```

3.  **Run Database Migrations:**
    This command applies the latest schema to the database you configured in step 2.
    ```bash
    pnpm --filter api migration:run
    ```

---

## 🚦 Running the Application

You can run the project in two ways:

### ✅ Option 1 — Local Development (Manual)

**Install dependencies:**
Run from the root directory
```bash
pnpm install
```

**Development Mode (Recommended for development):**
Run the API and Web services directly on your machine in "watch" mode.
```bash
pnpm dev
```

**Production Mode (Run built version):**
Build the entire project
```bash
pnpm build
```

Start the production server
```bash
pnpm start
```

### ✅ Option 2 — Docker Compose
Run the entire stack (API, Web, DB) in containers.
```bash
docker compose up --build -d
```

