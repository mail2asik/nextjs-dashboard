## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

## PostgreSQL Setup (WSL / Local Development)

This project requires PostgreSQL to run locally.

1. Install PostgreSQL (WSL)

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib -y
```

Start the service:

```bash
sudo service postgresql start
```

2. Create Database & User

Switch to postgres user:

```bash
sudo -u postgres psql
```

Run the following:

```bash
-- Create user
CREATE USER nextuser WITH PASSWORD 'password123';

-- Create database with correct ownership (IMPORTANT)
CREATE DATABASE nextjs_dashboard OWNER nextuser;

-- Connect to database
\c nextjs_dashboard

-- Ensure schema ownership (fixes permission issues)
ALTER SCHEMA public OWNER TO nextuser;

-- Enable UUID extension
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
```

Exit:

```bash
\q
```

3. Environment Variables

Create a .env or .env.local file:

```bash
POSTGRES_USER=nextuser
POSTGRES_PASSWORD=password123
POSTGRES_DATABASE=nextjs_dashboard
POSTGRES_HOST=127.0.0.1

POSTGRES_URL=postgresql://nextuser:password123@127.0.0.1:5432/nextjs_dashboard
POSTGRES_URL_NON_POOLING=postgresql://nextuser:password123@127.0.0.1:5432/nextjs_dashboard
POSTGRES_PRISMA_URL=postgresql://nextuser:password123@127.0.0.1:5432/nextjs_dashboard
```
⚠️ Use 127.0.0.1 instead of localhost to avoid WSL networking issues.

4. Verify Connection

```bash
psql -h 127.0.0.1 -U nextuser -d nextjs_dashboard
```

Then:

```bash
SELECT current_user;
```

Expected output:

```bash
nextuser
```

Test table creation:

```bash
CREATE TABLE test_table(id INT);
```