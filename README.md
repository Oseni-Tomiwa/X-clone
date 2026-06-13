# X Clone

A full-stack Twitter/X-style social media application built with a modern TypeScript stack. The project includes authentication, user profiles, posts, feeds, follows, notifications, messaging, bookmarks, search, media uploads, admin features, API documentation, tests, and Docker deployment support.

## Features

- Register, login, logout, email verification, password reset, JWT access tokens, and refresh-token rotation
- Editable user profiles with avatar, cover image, bio, location, website, follower counts, and following counts
- Create, edit, delete, like, repost, quote, reply, and thread posts
- Image and video upload support with local development storage
- Home, following, and trending feeds with cursor pagination
- Follow and unfollow users, search users, and user recommendations
- Real-time notifications for likes, replies, follows, reposts, messages, and quotes
- Direct messages, conversation list, and read receipts
- Search for users, posts, and hashtags
- Save and remove bookmarks
- Admin user management, moderation actions, and analytics dashboard data
- Swagger/OpenAPI documentation
- Docker Compose setup for local deployment

## Tech Stack

**Frontend**

- React
- TypeScript
- Vite
- Tailwind CSS
- Zustand
- React Router
- Socket.IO Client
- React Testing Library
- Vitest

**Backend**

- Node.js
- Express.js
- TypeScript
- PostgreSQL
- Prisma ORM
- JWT authentication
- Socket.IO
- Swagger/OpenAPI
- Jest

**DevOps**

- Docker
- Docker Compose
- Local file storage for development
- S3-ready storage abstraction for production

## Project Structure

```text
x-clone/
  apps/
    api/
      prisma/
        schema.prisma
      src/
        config/
        middleware/
        modules/
        realtime/
        storage/
        utils/
      Dockerfile
    web/
      src/
        api/
        components/
        pages/
        store/
      Dockerfile
  docs/
    ARCHITECTURE.md
    openapi.yaml
  docker-compose.yml
  package.json
  README.md
```

## Getting Started

### Prerequisites

- Node.js 22+
- npm
- Docker and Docker Compose
- PostgreSQL, if running without Docker

### 1. Clone and install dependencies

```bash
git clone <your-repo-url>
cd x-clone
npm install
```

### 2. Configure environment variables

```bash
cp apps/api/.env.example apps/api/.env
cp apps/web/.env.example apps/web/.env
```

Update `apps/api/.env` with secure JWT secrets before using the app outside local development.

### 3. Generate Prisma Client

```bash
npm run prisma:generate
```

### 4. Run database migrations

If PostgreSQL is running locally:

```bash
npm run prisma:migrate
```

If using Docker Compose, start the database first:

```bash
docker compose up db
```

Then run:

```bash
npm run prisma:migrate
```

### 5. Start development servers

```bash
npm run dev
```

The app runs at:

- Web: `http://localhost:5173`
- API: `http://localhost:4000`
- API docs: `http://localhost:4000/docs`

## Docker

Run the full stack:

```bash
docker compose up --build
```

Docker Compose starts:

- PostgreSQL
- Express API
- React web app

## Available Scripts

```bash
npm run dev
```

Starts the API and web development servers.

```bash
npm run build
```

Builds both workspaces for production.

```bash
npm test
```

Runs backend and frontend tests.

```bash
npm run prisma:generate
```

Generates Prisma Client.

```bash
npm run prisma:migrate
```

Runs Prisma migrations in development.

## API Documentation

The OpenAPI contract is stored at:

```text
docs/openapi.yaml
```

When the API is running, Swagger UI is available at:

```text
http://localhost:4000/docs
```

## Security Notes

- Passwords are hashed with bcrypt.
- Access tokens are short-lived JWTs.
- Refresh tokens are opaque, hashed, stored in the database, and rotated.
- Auth routes are rate limited.
- Request bodies are validated with Zod.
- Helmet is enabled for HTTP security headers.
- CORS is restricted through environment configuration.
- Production deployments should use HTTPS, managed PostgreSQL backups, secure secrets, and S3-compatible media storage.

## Testing

The project includes backend tests with Jest and frontend tests with Vitest and React Testing Library.

```bash
npm test
```

## Deployment Notes

For production:

- Use strong JWT secrets.
- Run Prisma migrations before starting the API.
- Use managed PostgreSQL with backups and connection pooling.
- Replace local uploads with S3-compatible object storage.
- Put the API behind HTTPS.
- Configure `WEB_ORIGIN` to the deployed frontend URL.
- Monitor API logs and database performance.

## Documentation

More implementation details are available in:

- `docs/ARCHITECTURE.md`
- `docs/openapi.yaml`

## License

MIT
