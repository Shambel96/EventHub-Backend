<div align="center">

# 🎟️ EventHub Backend

### Power Your Events. Connect Your Community.

A modular backend API for **EventHub**, a full-stack event management platform built to support event creation, discovery, user interactions, and event-related data management.

<br/>

[![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=for-the-badge&logo=nestjs&logoColor=white)](https://nestjs.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white)](https://www.prisma.io/)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org/)

<br/>

**Backend Repository:** [EventHub-Backend](https://github.com/Shambel96/EventHub-Backend)

**Frontend Repository:** [EventHub-Frontend](https://github.com/Shambel96/EventHub-Frontend)

</div>

---

## 📌 Overview

**EventHub Backend** is the server-side component of EventHub, a full-stack event management system. It provides a modular foundation for handling user accounts, authentication, event data, categories, event media, and interactions between users and events.

Built with **NestJS, TypeScript, PostgreSQL, and Prisma ORM**, the backend follows a modular architecture that separates application functionality into dedicated modules.

The system is designed to support a maintainable API, structured data relationships, request validation, and role-based access control.

### 🎯 Project Objectives

- Provide backend services for event management.
- Organize application functionality into reusable NestJS modules.
- Manage relational data using PostgreSQL and Prisma.
- Support user authentication and role-based authorization.
- Enable interactions such as liking, bookmarking, commenting on, and rating events.
- Support event images and additional event information.
- Establish a maintainable foundation for future enhancements.

---

## ✨ Features

### 🔐 Authentication and User Management

- User authentication using NestJS authentication modules and JWT-related dependencies.
- Password hashing dependencies for protecting stored credentials.
- User account management.
- Password-reset token data model.
- Role-based authorization infrastructure.
- Account status management.

**Supported user roles:**

| Role | Description |
|---|---|
| `USER` | Standard user role |
| `ADMIN` | Administrative role |
| `OWNER` | Owner-level role |

**Account statuses:**

| Status | Description |
|---|---|
| `ACTIVE` | Active account |
| `SUSPENDED` | Suspended account |
| `BANNED` | Banned account |

Actual access permissions depend on the authorization rules implemented by the application.

### 📅 Event Management

The event data model supports:

- Event titles and descriptions.
- Event duration.
- Physical or virtual event locations.
- Paid and free event configuration.
- Optional event pricing.
- Event start and end dates.
- Event creators.
- Event categories.
- Event ratings and rating totals.
- Additional event information through ordered event steps.

### 🗂️ Categories and Amenities

- Category records associated with events.
- Reusable amenity records.
- Relationships between events and amenities.
- Database constraints to maintain relationship integrity.

### 🖼️ Event Images and Media

- Event image records.
- Image URLs associated with events.
- Featured-image identification.
- Cloudinary integration dependency for media management.

### ❤️ Event Interactions

The database schema supports several user engagement features:

| Feature | Description |
|---|---|
| Likes | Associate users with events they like |
| Bookmarks | Save events for later reference |
| Comments | Store user comments on events |
| Ratings | Associate users' ratings with events |
| Statistics | Dedicated NestJS module for event-related statistics |

The database schema defines these data relationships; the exact available API operations depend on their corresponding service and controller implementations.

### 🛡️ Request Validation

The application configures NestJS's global `ValidationPipe` with:

- `whitelist` to remove properties that are not permitted by validation decorators.
- `forbidNonWhitelisted` to reject requests containing non-whitelisted properties.
- `transform` to enable transformation of incoming request data.

These settings help maintain consistent request validation when DTOs are properly defined.

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| [NestJS](https://nestjs.com/) | Modular backend application framework |
| [TypeScript](https://www.typescriptlang.org/) | Type-safe application development |
| [Node.js](https://nodejs.org/) | JavaScript runtime |
| [PostgreSQL](https://www.postgresql.org/) | Relational database |
| [Prisma ORM](https://www.prisma.io/) | Database access and schema management |
| [JWT](https://jwt.io/) | Token-based authentication infrastructure |
| [Passport](https://www.passportjs.org/) | Authentication strategy integration |
| [Cloudinary](https://cloudinary.com/) | Media management integration |
| [Resend](https://resend.com/) | Email delivery integration |
| [class-validator](https://github.com/typestack/class-validator) | Request DTO validation |
| [class-transformer](https://github.com/typestack/class-transformer) | Object transformation |
| [Jest](https://jestjs.io/) | Testing framework |
| [ESLint](https://eslint.org/) | Code quality and linting |
| [Prettier](https://prettier.io/) | Code formatting |
| [Git](https://git-scm.com/) | Version control |

---

## 🏗️ Architecture

EventHub Backend uses NestJS's modular architecture to organize application functionality.

```text
                        ┌───────────────────────┐
                        │   EventHub Frontend   │
                        │    Nuxt / Vue         │
                        └───────────┬───────────┘
                                    │
                                    │ HTTP Requests
                                    ▼
                        ┌───────────────────────┐
                        │    NestJS Backend     │
                        │                       │
                        │  Controllers & DTOs   │
                        │  Services & Modules   │
                        │  Validation & Guards  │
                        └───────────┬───────────┘
                                    │
                     ┌──────────────┴──────────────┐
                     ▼                             ▼
          ┌────────────────────┐       ┌────────────────────┐
          │   Prisma ORM       │       │ External Services   │
          │                    │       │                    │
          │ Data Access Layer  │       │ Cloudinary / Resend │
          └──────────┬─────────┘       └────────────────────┘
                     │
                     ▼
          ┌────────────────────┐
          │    PostgreSQL      │
          │                    │
          │ Users, Events,     │
          │ Categories, etc.   │
          └────────────────────┘
```

### Architectural Responsibilities

**Controllers**
- Receive HTTP requests.
- Coordinate request handling.
- Return responses to clients.

**Services**
- Contain application logic.
- Coordinate data operations.
- Implement the behavior associated with each module.

**DTOs and Validation**
- Define and validate incoming request data.
- Help enforce expected request structures.

**Prisma**
- Provides database access.
- Defines data models and relationships.
- Supports database queries and migrations.

**PostgreSQL**
- Stores persistent application data.

**External Services**
- Support integrations such as media management and email delivery where configured.

---

## 📂 Project Structure

The repository uses a NestJS project structure with dedicated feature modules.

```text
EventHub-Backend/
│
├── prisma/
│   ├── schema.prisma
│   └── seed.ts
│
├── src/
│   ├── admin/
│   ├── auth/
│   ├── users/
│   ├── events/
│   │   ├── event-images/
│   │   └── event-steps/
│   │
│   ├── uploads/
│   ├── categories/
│   ├── amenities/
│   ├── likes/
│   ├── bookmarks/
│   ├── comments/
│   ├── ratings/
│   ├── stats/
│   ├── common/
│   │   └── guards/
│   │
│   ├── prisma/
│   ├── app.module.ts
│   ├── app.controller.ts
│   ├── app.service.ts
│   └── main.ts
│
├── test/
├── .gitignore
├── .prettierrc
├── eslint.config.mjs
├── nest-cli.json
├── package.json
├── package-lock.json
├── tsconfig.json
└── README.md
```

The structure above highlights the main application modules and configuration files. Individual files and directories may evolve as development progresses.

---

## 🗄️ Database Design

EventHub uses PostgreSQL as its relational database, with Prisma defining the data models and relationships.

### Core Data Models

| Model | Responsibility |
|---|---|
| `User` | User profile, email, password hash, role, and account status |
| `PasswordResetToken` | Password-reset token and expiration |
| `Event` | Event information, dates, pricing, creator, and category |
| `Category` | Event classification |
| `EventStep` | Ordered information associated with an event |
| `Amenity` | Reusable event amenity |
| `EventAmenity` | Relationship between events and amenities |
| `EventImage` | Event image URLs and featured-image status |
| `Like` | User-to-event likes |
| `Bookmark` | User-to-event bookmarks |
| `Comment` | User comments on events |
| `Rating` | User ratings for events |

### Relationship Overview

```text
User
 ├── Created Events
 ├── Likes
 ├── Bookmarks
 ├── Comments
 ├── Ratings
 └── Password Reset Tokens

Event
 ├── Category
 ├── Creator
 ├── Event Steps
 ├── Event Images
 ├── Amenities
 ├── Likes
 ├── Bookmarks
 ├── Comments
 └── Ratings
```

### Data Integrity

The schema includes:

- Unique email addresses for users.
- Unique category and amenity names.
- Foreign-key relationships between related models.
- Composite identifiers for user-event interactions.
- An ordering constraint for event steps.
- Indexes on selected event and interaction fields.
- Cascading deletion rules for selected relationships.

These constraints help maintain data consistency and reduce duplicate relationship records.

---

## 🚀 Getting Started

Follow these instructions to set up the backend locally.

### Prerequisites

Install the following tools:

- **Node.js** — compatible with the project dependencies.
- **npm** — Node.js package manager.
- **PostgreSQL** — database server.
- **Git** — version control.

### 1. Clone the Repository

```bash
git clone https://github.com/Shambel96/EventHub-Backend.git
```

Navigate to the project directory:

```bash
cd EventHub-Backend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the project root:

```bash
touch .env
```

Configure the PostgreSQL connection string:

```dotenv
DATABASE_URL="postgresql://USERNAME:PASSWORD@localhost:5432/eventhub?schema=public"
```

Replace `USERNAME` and `PASSWORD` with your PostgreSQL credentials. Ensure that the `eventhub` database exists before running database commands.

The backend may require additional environment variables for authentication, email, and media integrations. Check the relevant source files and configuration before adding them.

**Security:** Never commit real database credentials, JWT secrets, API keys, or other private configuration values.

### 4. Generate the Prisma Client

```bash
npx prisma generate
```

This generates the Prisma Client based on the configured schema.

### 5. Apply Database Migrations

If the repository contains committed Prisma migrations, apply them to your database:

```bash
npx prisma migrate deploy
```

For local schema development, where appropriate:

```bash
npx prisma migrate dev
```

**Important:** The `prisma/schema.prisma` file defines the database models, but a schema file alone does not establish that migration history exists. Verify the contents of the `prisma/migrations/` directory before choosing the migration workflow.

If you are initializing a fresh development database without existing migrations, follow the project's agreed database setup procedure rather than assuming that migration files are available.

### 6. Start the Development Server

```bash
npm run start:dev
```

The current application bootstrap configures the server to listen on port `3000`.

Once the server starts, the base address is:

```text
http://localhost:3000
```

The exact API routes depend on the implemented controllers and any route prefixes configured in the application.

### 7. Build for Production

```bash
npm run build
```

Start the production build:

```bash
npm run start:prod
```

---

## 📜 Available Scripts

The following commands are defined in `package.json`.

| Command | Description |
|---|---|
| `npm run build` | Compile the NestJS application |
| `npm run start` | Start the application |
| `npm run start:dev` | Start the development server with watch mode |
| `npm run start:debug` | Start the application in debug mode |
| `npm run start:prod` | Run the compiled application |
| `npm run format` | Format TypeScript source and test files |
| `npm run lint` | Run ESLint with automatic fixes |
| `npm run test` | Run unit tests |
| `npm run test:watch` | Run tests in watch mode |
| `npm run test:cov` | Run tests with coverage |
| `npm run test:e2e` | Run end-to-end tests |

---

## 🔌 Frontend Integration

EventHub Backend is designed to work with the separate EventHub frontend.

| Component | Repository |
|---|---|
| 🎨 Frontend | [EventHub-Frontend](https://github.com/Shambel96/EventHub-Frontend) |
| ⚙️ Backend | [EventHub-Backend](https://github.com/Shambel96/EventHub-Backend) |

### Local Development

1. Start PostgreSQL.
2. Configure the backend environment variables.
3. Generate the Prisma Client and apply the appropriate database migrations.
4. Start the backend server.
5. Start the frontend development server.
6. Configure the frontend API client to use the backend's actual address.
7. Verify that CORS permits the frontend's origin.

The backend currently configures CORS for `http://localhost:3001` with credentials and selected request headers. Make sure this matches the origin used by your frontend during local development.

The actual allowed origins should be configured deliberately for production deployment.

---

## 🧪 Testing and Code Quality

The project includes Jest, NestJS testing utilities, ESLint, and Prettier.

Run the test suite:

```bash
npm run test
```

Run tests with coverage:

```bash
npm run test:cov
```

Run end-to-end tests:

```bash
npm run test:e2e
```

Format the source files:

```bash
npm run format
```

Run linting:

```bash
npm run lint
```

These commands are available in the project configuration. Their successful execution and the current level of test coverage should be verified separately.

### Recommended Verification Checklist

- [ ] Application starts successfully.
- [ ] Database connection works.
- [ ] Prisma Client generates successfully.
- [ ] Database migrations apply cleanly.
- [ ] Authentication and authorization behave as expected.
- [ ] DTO validation rejects invalid requests.
- [ ] Event operations work with valid data.
- [ ] User interactions maintain data integrity.
- [ ] External integrations are configured correctly.
- [ ] Unit and end-to-end tests pass.

---

## 🌿 Team Git Workflow

The repository documents a feature-branch and pull-request workflow designed to help team members work independently while reducing merge conflicts.

### Branching Strategy

- `main` — stable integration branch.
- Feature branches — isolated development work.
- Bug-fix branches — targeted fixes.
- Pull requests — reviewed changes before merging.

### Branch Ownership

The team's documented ownership areas are:

| Contributor | Primary Ownership Areas |
|---|---|
| Developer A | Authentication, users, common utilities, Prisma, configuration |
| Developer B | Events, uploads, event images, event steps |
| Developer C | Likes, bookmarks, comments, ratings, statistics |
| Developer D | Categories and amenities |

These are team workflow assignments, not a claim about individual authorship of every file.

### Create a Feature Branch

Update your local `main` branch:

```bash
git checkout main
git pull origin main
```

Create a branch for your work:

```bash
git checkout -b feature/event-management
```

Make your changes and commit them:

```bash
git add .
git commit -m "feat(events): improve event management"
```

Push the branch:

```bash
git push -u origin feature/event-management
```

Open a pull request targeting `main`.

### Pull Request Checklist

Before requesting a review:

- Ensure the branch is up to date with `main`.
- Run relevant tests.
- Update API documentation when endpoints change.
- Include DTO validation for incoming request bodies.
- Include required Prisma migrations when the schema changes.
- Never commit secrets.
- Request review from the relevant module owner.
- Obtain the required approvals before merging.

### Prisma Migration Rules

Database schema changes require particular care in a shared repository.

1. Coordinate migration generation with the team.
2. Commit migration files alongside the corresponding schema changes.
3. Avoid editing previously merged migrations.
4. Verify migrations against a clean development database when appropriate.
5. Regenerate the Prisma Client when the schema changes.
6. Review database changes before merging.

---

## 🔒 Security Considerations

Security is important for a backend handling user accounts and event data.

Recommended practices include:

- Hash passwords before storing them.
- Protect private endpoints with appropriate authentication and authorization.
- Validate incoming request data.
- Keep secrets in environment variables.
- Use secure password-reset token handling and expiration.
- Restrict production CORS origins to trusted applications.
- Avoid exposing sensitive user information in API responses.
- Apply appropriate rate limits to authentication and other sensitive endpoints.
- Use HTTPS in production.
- Keep dependencies updated and review security advisories.

These are security practices for operating the application; they should not be interpreted as confirmation that every listed control is already implemented.

---

## 🚧 Future Improvements

Potential areas for continued development include:

- [ ] Expand automated unit and end-to-end test coverage.
- [ ] Improve API documentation and endpoint examples.
- [ ] Strengthen authentication and authorization testing.
- [ ] Improve structured error handling and logging.
- [ ] Add API rate limiting where appropriate.
- [ ] Improve deployment and environment configuration.
- [ ] Add continuous integration for tests, linting, and builds.
- [ ] Document production deployment and database migration procedures.

---

## 🤝 Contributing

Contributions and constructive feedback are welcome.

To contribute:

1. Fork the repository or create a feature branch if you are a team member.
2. Follow the established module ownership rules.
3. Implement your changes.
4. Run relevant tests and linting.
5. Commit your changes using descriptive commit messages.
6. Push your branch.
7. Open a pull request targeting `main`.
8. Address reviewer feedback before merging.

For database changes or changes that affect shared modules, coordinate with the relevant team members before implementation.

---

## 👨‍💻 Contributors

EventHub is developed collaboratively by:

- **Shambel Dechu**
- **Beata Teka**
- **Moges Sisay**

---

<div align="center">

### 🎟️ EventHub — Making Event Management Simpler

Built with **NestJS, TypeScript, PostgreSQL, and Prisma**.

[Explore the Frontend](https://github.com/Shambel96/EventHub-Frontend) · [Explore the Backend](https://github.com/Shambel96/EventHub-Backend)

⭐ If you find this project interesting, consider starring the repository.

</div>
