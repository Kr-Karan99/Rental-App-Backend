# 🚗 Vehicle Rental Backend API

A comprehensive, production-ready backend API for a vehicle rental platform built with **Node.js**, **Express**, **TypeScript**, and **PostgreSQL**. This application enables customers to rent vehicles from stores and allows owners to manage their stores and vehicle inventory.

![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)

---

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Architecture](#-project-architecture)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Database Schema](#-database-schema)
- [API Endpoints](#-api-endpoints)
- [Authentication](#-authentication)
- [Testing](#-testing)
- [Production Deployment](#-production-deployment)
- [API Documentation](#-api-documentation)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

### 🔐 Authentication & Authorization
- **JWT-based authentication** with access and refresh tokens
- **Role-based access control** (Customer & Owner roles)
- Secure password hashing using bcrypt
- Password reset functionality with email notifications
- Token refresh mechanism for seamless user experience

### 👥 User Management
- User registration and login
- Profile management (view & update)
- Role-based user types (Customer & Owner)

### 🏪 Store Management (Owner Features)
- Create and manage multiple stores
- Update store information (name, location, coordinates)
- View all stores owned by the authenticated user
- Delete stores
- Geographic location support (latitude/longitude)

### 🚙 Vehicle Management (Owner Features)
- Add vehicles to stores
- Update vehicle details (title, description, pricing, availability)
- Upload multiple images per vehicle
- Delete vehicle images
- Set daily and monthly rental rates
- Mark vehicles as available/unavailable

### 📝 Rental System
- **Customer Features:**
  - Browse available vehicles by store
  - Create rental requests with date range
  - View rental history
  - Renew active rentals
  
- **Owner Features:**
  - View rental requests for their vehicles
  - Approve or reject rental requests
  - Track rental status (Pending, Approved, Cancelled, Completed)

### 💳 Payment Processing
- Multiple payment methods (Card, UPI, Cash, Mock)
- Payment status tracking
- Automatic PDF receipt generation
- Receipt download in PDF and JSON formats
- Payment history

### 🛡️ Security Features
- Helmet.js for security headers
- CORS protection
- Rate limiting on authentication endpoints
- Input validation using Zod schemas
- Error handling middleware with detailed logging

### 📊 Additional Features
- Pagination support for list endpoints
- Structured logging with Pino
- Request/response logging
- Swagger API documentation
- Docker support
- Database migrations with Prisma
- Comprehensive error handling

---

## 🛠️ Tech Stack

### Core Technologies
| Technology | Version | Purpose |
|-----------|---------|---------|
| **Node.js** | ≥18.0.0 | Runtime environment |
| **TypeScript** | ^5.3.3 | Type-safe JavaScript |
| **Express** | ^4.18.2 | Web framework |
| **PostgreSQL** | Latest | Relational database |
| **Prisma** | ^5.7.1 | ORM and database toolkit |

### Key Dependencies

#### Authentication & Security
- **jsonwebtoken** (^9.0.2) - JWT token generation and verification
- **bcrypt** (^5.1.1) - Password hashing
- **helmet** (^7.1.0) - Security headers
- **cors** (^2.8.5) - Cross-Origin Resource Sharing
- **express-rate-limit** (^7.1.5) - Rate limiting

#### Validation & Schema
- **zod** (^3.22.4) - Schema validation and type inference

#### File Handling
- **multer** (^1.4.5-lts.1) - Multipart form data and file uploads

#### Email & PDF
- **nodemailer** (^6.9.7) - Email sending
- **pdfkit** (^0.14.0) - PDF generation

#### Logging
- **pino** (^8.17.2) - High-performance logging
- **pino-http** (^8.5.0) - HTTP request logging
- **pino-pretty** (^10.3.1) - Pretty logging for development

#### Documentation
- **swagger-jsdoc** (^6.2.8) - Swagger documentation generation
- **swagger-ui-express** (^5.0.0) - Swagger UI

#### Development Tools
- **ts-node-dev** (^2.0.0) - TypeScript development server
- **eslint** (^8.56.0) - Code linting
- **prettier** (^3.2.4) - Code formatting
- **jest** (^29.7.0) - Testing framework
- **husky** (^8.0.3) - Git hooks

---

## 🏗️ Project Architecture

```
Vehicle-Rent---Backend/
├── prisma/
│   ├── schema.prisma          # Database schema
│   ├── migrations/            # Database migrations
│   └── seed.ts                # Database seeding
├── src/
│   ├── config/
│   │   ├── env.ts             # Environment configuration
│   │   ├── logger.ts          # Logger configuration
│   │   └── prismaClient.ts    # Prisma client setup
│   ├── controllers/           # Request handlers
│   │   ├── auth.controller.ts
│   │   ├── user.controller.ts
│   │   ├── store.controller.ts
│   │   ├── vehicle.controller.ts
│   │   ├── rental.controller.ts
│   │   └── payment.controller.ts
│   ├── services/              # Business logic
│   │   ├── auth.service.ts
│   │   ├── user.service.ts
│   │   ├── store.service.ts
│   │   ├── vehicle.service.ts
│   │   ├── rental.service.ts
│   │   └── payment.service.ts
│   ├── repositories/          # Database operations
│   │   ├── user.repository.ts
│   │   ├── store.repository.ts
│   │   ├── vehicle.repository.ts
│   │   ├── rental.repository.ts
│   │   └── payment.repository.ts
│   ├── routes/                # API routes
│   │   ├── index.ts
│   │   ├── auth.routes.ts
│   │   ├── user.routes.ts
│   │   ├── store.routes.ts
│   │   ├── vehicle.routes.ts
│   │   ├── rental.routes.ts
│   │   └── payment.routes.ts
│   ├── middlewares/           # Express middlewares
│   │   ├── auth.middleware.ts
│   │   ├── role.middleware.ts
│   │   ├── validation.middleware.ts
│   │   ├── error.middleware.ts
│   │   └── requestLogger.middleware.ts
│   ├── schemas/               # Zod validation schemas
│   │   ├── auth.schema.ts
│   │   ├── user.schema.ts
│   │   ├── store.schema.ts
│   │   ├── vehicle.schema.ts
│   │   ├── rental.schema.ts
│   │   └── payment.schema.ts
│   ├── utils/                 # Utility functions
│   │   ├── jwt.util.ts
│   │   ├── password.util.ts
│   │   ├── email.util.ts
│   │   ├── errors.ts
│   │   └── pagination.util.ts
│   ├── types/                 # TypeScript type definitions
│   ├── app.ts                 # Express app setup
│   └── server.ts              # Server entry point
├── tests/                     # Test files
├── .env.example               # Environment variables template
├── docker-compose.yml         # Docker configuration
├── tsconfig.json              # TypeScript configuration
├── package.json               # Dependencies
└── README.md                  # Project documentation
```

### Design Pattern: Repository Pattern
The application follows the **Repository Pattern** with clear separation of concerns:
- **Controllers**: Handle HTTP requests/responses
- **Services**: Contain business logic
- **Repositories**: Manage data access and database operations
- **Middlewares**: Handle cross-cutting concerns (auth, validation, logging)

---

## 🚀 Getting Started

### Prerequisites
- **Node.js** ≥ 18.0.0
- **PostgreSQL** database
- **npm** or **yarn**

### Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd Vehicle-Rent---Backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```
   Then edit `.env` file with your configuration (see [Environment Variables](#-environment-variables))

4. **Set up the database**
   
   Create a PostgreSQL database:
   ```bash
   createdb vehicle_rental
   ```

5. **Run database migrations**
   ```bash
   npm run prisma:migrate
   ```

6. **Generate Prisma Client**
   ```bash
   npm run prisma:generate
   ```

7. **Seed the database** (optional - adds test data)
   ```bash
   npm run seed
   ```

8. **Start the development server**
   ```bash
   npm run dev
   ```

The server will start at `http://localhost:3000`

---

## 🔑 Environment Variables

Create a `.env` file in the root directory with the following variables:

```env
# Server Configuration
NODE_ENV=development
PORT=3000
API_PREFIX=/api/v1

# Database
DATABASE_URL=postgresql://username:password@localhost:5432/vehicle_rental

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
JWT_EXPIRES_IN=15m
REFRESH_TOKEN_SECRET=your-super-secret-refresh-token-key-change-this
REFRESH_TOKEN_EXPIRES_IN=7d

# Email Configuration (SMTP)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_SECURE=false
SMTP_USER=your-email@gmail.com
SMTP_PASSWORD=your-app-password
EMAIL_FROM=noreply@vehiclerental.com

# File Upload
UPLOAD_DIR=uploads
MAX_FILE_SIZE=5242880

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=5

# CORS
CORS_ORIGIN=http://localhost:3000

# Logging
LOG_LEVEL=info
```

### Environment Variables Explanation

| Variable | Description | Default |
|----------|-------------|---------|
| `NODE_ENV` | Environment (development/production) | development |
| `PORT` | Server port | 3000 |
| `API_PREFIX` | API route prefix | /api/v1 |
| `DATABASE_URL` | PostgreSQL connection string | - |
| `JWT_SECRET` | Secret key for access tokens | - |
| `JWT_EXPIRES_IN` | Access token expiration | 15m |
| `REFRESH_TOKEN_SECRET` | Secret key for refresh tokens | - |
| `REFRESH_TOKEN_EXPIRES_IN` | Refresh token expiration | 7d |
| `SMTP_HOST` | Email SMTP host | smtp.gmail.com |
| `SMTP_PORT` | Email SMTP port | 587 |
| `SMTP_USER` | SMTP username | - |
| `SMTP_PASSWORD` | SMTP password | - |
| `EMAIL_FROM` | From email address | - |

---

## 🗄️ Database Schema

The application uses **Prisma ORM** with PostgreSQL. Here's an overview of the main entities:

### Models

#### 👤 User
- **id**: UUID (Primary Key)
- **name**: String
- **email**: String (Unique)
- **passwordHash**: String
- **role**: Enum (CUSTOMER, OWNER)
- **createdAt**, **updatedAt**: DateTime

#### 🏪 Store
- **id**: UUID (Primary Key)
- **ownerId**: UUID (Foreign Key → User)
- **name**: String
- **location**: String
- **latitude**, **longitude**: Float (Optional)
- **createdAt**, **updatedAt**: DateTime

#### 🚗 Vehicle
- **id**: UUID (Primary Key)
- **storeId**: UUID (Foreign Key → Store)
- **title**: String
- **description**: String (Optional)
- **rentPerDay**: Decimal(10,2)
- **rentPerMonth**: Decimal(10,2)
- **isAvailable**: Boolean
- **createdAt**, **updatedAt**: DateTime

#### 🖼️ VehicleImage
- **id**: UUID (Primary Key)
- **vehicleId**: UUID (Foreign Key → Vehicle)
- **imageUrl**: String
- **createdAt**: DateTime

#### 📝 RentalRequest
- **id**: UUID (Primary Key)
- **vehicleId**: UUID (Foreign Key → Vehicle)
- **customerId**: UUID (Foreign Key → User)
- **startDate**, **endDate**: DateTime
- **totalAmount**: Decimal(10,2)
- **status**: Enum (PENDING, APPROVED, CANCELLED, COMPLETED)
- **createdAt**, **updatedAt**: DateTime

#### 💳 Payment
- **id**: UUID (Primary Key)
- **rentalRequestId**: UUID (Foreign Key → RentalRequest)
- **amount**: Decimal(10,2)
- **method**: Enum (CARD, UPI, CASH, MOCK)
- **receiptUrl**: String (Optional)
- **status**: Enum (PENDING, SUCCESS, FAILED)
- **createdAt**, **updatedAt**: DateTime

#### 🔄 RefreshToken
- **id**: UUID (Primary Key)
- **userId**: UUID (Foreign Key → User)
- **token**: String (Unique)
- **expiresAt**: DateTime
- **createdAt**: DateTime


## 📡 API Endpoints

Base URL: `http://localhost:3000/api/v1`

### 🔐 Authentication (`/auth`)

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/auth/signup` | Register new user | ❌ |
| POST | `/auth/login` | Login user | ❌ |
| POST | `/auth/refresh` | Refresh access token | ❌ |
| POST | `/auth/logout` | Logout user | ❌ |
| POST | `/auth/forgot-password` | Request password reset | ❌ |
| POST | `/auth/reset-password` | Reset password with token | ❌ |

### 👥 Users (`/users`)

| Method | Endpoint | Description | Auth Required | Role |
|--------|----------|-------------|---------------|------|
| GET | `/users/profile` | Get user profile | ✅ | Any |
| PUT | `/users/profile` | Update user profile | ✅ | Any |

### 🏪 Stores (`/stores`)

| Method | Endpoint | Description | Auth Required | Role |
|--------|----------|-------------|---------------|------|
| GET | `/stores` | Get all stores (with filters) | ❌ | - |
| GET | `/stores/:id` | Get store by ID | ❌ | - |
| POST | `/stores` | Create new store | ✅ | Owner |
| GET | `/stores/owner/my-stores` | Get owner's stores | ✅ | Owner |
| PUT | `/stores/:id` | Update store | ✅ | Owner |
| DELETE | `/stores/:id` | Delete store | ✅ | Owner |

### 🚗 Vehicles (`/vehicles`)

| Method | Endpoint | Description | Auth Required | Role |
|--------|----------|-------------|---------------|------|
| GET | `/vehicles/store/:storeId` | Get vehicles by store | ❌ | - |
| GET | `/vehicles/:id` | Get vehicle by ID | ❌ | - |
| POST | `/vehicles` | Create new vehicle | ✅ | Owner |
| PUT | `/vehicles/:id` | Update vehicle | ✅ | Owner |
| DELETE | `/vehicles/:id` | Delete vehicle | ✅ | Owner |
| POST | `/vehicles/:id/images` | Upload vehicle image | ✅ | Owner |
| DELETE | `/vehicles/:vehicleId/images/:imageId` | Delete vehicle image | ✅ | Owner |

### 📝 Rentals (`/rentals`)

| Method | Endpoint | Description | Auth Required | Role |
|--------|----------|-------------|---------------|------|
| POST | `/rentals` | Create rental request | ✅ | Customer |
| GET | `/rentals/customer/my-rentals` | Get customer's rentals | ✅ | Customer |
| GET | `/rentals/owner/my-rentals` | Get owner's rentals | ✅ | Owner |
| GET | `/rentals/:id` | Get rental by ID | ✅ | Any |
| POST | `/rentals/:id/approve` | Approve rental | ✅ | Owner |
| POST | `/rentals/:id/reject` | Reject rental | ✅ | Owner |
| POST | `/rentals/:id/renew` | Renew rental | ✅ | Customer |

### 💳 Payments (`/payments`)

| Method | Endpoint | Description | Auth Required | Role |
|--------|----------|-------------|---------------|------|
| POST | `/payments/rental/:rentalId` | Process payment | ✅ | Any |
| GET | `/payments/:id` | Get payment by ID | ✅ | Any |
| GET | `/payments/:id/receipt` | Download receipt (PDF/JSON) | ✅ | Any |


---

## 🔐 Authentication

The API uses **JWT (JSON Web Tokens)** for authentication with a dual-token strategy:

### Token Types
1. **Access Token**: Short-lived (15 minutes), used for API requests
2. **Refresh Token**: Long-lived (7 days), used to obtain new access tokens

### Authentication Flow

1. **Sign up or Login**
   ```bash
   POST /api/v1/auth/signup
   POST /api/v1/auth/login
   ```
   Returns both access and refresh tokens.

2. **Use Access Token**
   Include in the Authorization header:
   ```
   Authorization: Bearer <access_token>
   ```

3. **Refresh Token When Expired**
   ```bash
   POST /api/v1/auth/refresh
   Body: { "refreshToken": "<refresh_token>" }
   ```

### Role-Based Access Control

- **CUSTOMER**: Can browse stores/vehicles, create rentals, make payments
- **OWNER**: Can manage stores, vehicles, and approve/reject rentals

### Example: Making an Authenticated Request

```bash
curl -X GET http://localhost:3000/api/v1/users/profile \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
```

---

## 📚 API Documentation

### Swagger UI
Interactive API documentation is available at:
```
http://localhost:3000/docs
```

---

h ❤️ using TypeScript, Node.js, and PostgreSQL**
