# create-pbx

A CLI tool that scaffolds a backend project with Prisma, Better Auth, and Express already wired together.

---

## What it is

Setting up auth on the backend is repetitive. You install packages, configure the database adapter, register routes, handle CORS, wire up sessions. It is the same work every time.

`create-pbx` does that work for you. Run one command and you get a working Express server with Better Auth and Prisma set up, PostgreSQL schema included.

---

## What you get

- Express 5 server
- Better Auth with GitHub OAuth
- Prisma ORM with a PostgreSQL schema (User, Session, Account, Verification)
- CORS configured for local frontend development
- A `/api/me` endpoint that returns the current session
- TypeScript and nodemon for development

---

## Requirements

- Node.js 18 or higher
- npm
- A PostgreSQL database

---

## Usage

```bash
npm init pbx
```
Or

```bash
npx create-pbx my-app
```

Or without a name, and it will ask:

```bash
npx create-pbx
```

It will copy the template files, update `package.json` with your project name, and optionally run `npm install`.

---

## Configuration

After scaffolding, copy `.env.example` to `.env` and fill in the values:

```env
BETTER_AUTH_SECRET=your_secret_here
BETTER_AUTH_URL=http://localhost:3005
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
PORT=3005
DATABASE_URL=your_postgresql_connection_string
```

To get GitHub OAuth credentials, create an OAuth App at github.com/settings/developers. Set the callback URL to `http://localhost:3005/api/auth/callback/github`.

---

## Running the project

```bash
# Generate Prisma client
npm run generate

# Push schema to your database
npx prisma db push

# Start the dev server
npm run dev
```

The server starts on the port you set in `.env`.

---

## Project structure

```
my-app/
  prisma/
    schema.prisma       # Database schema
  src/
    lib/
      auth.ts           # Better Auth setup
    server.ts           # Express server
  .env.example
  prisma.config.ts
  tsconfig.json
```

---

## Adding more providers

Open `src/lib/auth.ts` and add providers under `socialProviders`. Better Auth supports Google, Discord, Twitter, and others. The setup is the same pattern as the existing GitHub config.

---

## Changing the frontend origin

The CORS origin is set to `http://localhost:3000` in both `src/server.ts` and `src/lib/auth.ts`. Change both when you deploy.

---

## Stack versions

| Package      | Version |
|--------------|---------|
| Express      | 5       |
| Better Auth  | 1.5.x   |
| Prisma       | 6.x     |
| TypeScript   | 5.x     |

**Note:** this template is built for Prisma 6 only. Prisma 7 and above are not supported and will likely break the setup.