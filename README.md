# JobPulse — Job & Industry News Intelligence Platform

JobPulse is an intelligent job discovery and tech industry news aggregator. It automatically crawls, cleans, and normalizes remote developer job postings and tech news, providing rich search, filtering, bookmarking, and verified application links.

---

## Features

- **Automated Scraping**: Crawls live jobs from the Remotive API and tech news from TechCrunch RSS.
- **Data Normalization & Cleaning**: Deterministic skill extraction, salary formatting, and robust fallback handling for missing data.
- **Duplicate Prevention & Run Logging**: Fingerprinting prevents duplicate rows; every scraper execution is recorded in SQLite.
- **Search & Filtering**: Multi-dimensional filtering by keyword, level, job type, category, and remote status.
- **Job Details & Safe Apply**: Full job overview, structured descriptions, and validated external application links.
- **Saved Jobs**: Local bookmarking with optimistic UI updates and persistent database storage.
- **Responsive Dashboard**: Dark-mode interface tailored for desktop, tablet, and mobile devices.

---

## Installation & Setup

### 1. Prerequisites
- Node.js 18+ (tested on Node.js 20+)
- npm or pnpm

### 2. Install Dependencies
```bash
npm install
```

### 3. Environment Variables
Copy `.env.example` to create your local environment file:
```bash
cp .env.example .env.local
```

Configurable variables:
- `DATABASE_URL`: Path to SQLite database file (default: `sqlite.db`)
- `SCRAPER_INTERVAL_MINUTES`: Frequency in minutes for automatic background scraper runs (default: `60`)
- `REMOTIVE_API_URL` (optional override): Remotive public jobs endpoint
- `TECHCRUNCH_RSS_URL` (optional override): TechCrunch RSS feed endpoint

---

## Database Management

JobPulse uses **SQLite** powered by **Drizzle ORM**.

### Apply Migrations
Create all database tables (`jobs`, `news`, `saved_jobs`, `scrape_runs`):
```bash
npm run db:migrate
```

### Seed Initial Mock Data
Populate the database with initial verified seed jobs, news, and saved bookmarks:
```bash
npm run db:seed
```

---

## Running Scrapers

### Run Remotive Job Scraper
Fetches real remote job listings, normalizes fields, skips duplicates, and records run metrics:
```bash
npm run scrape:jobs
```

### Run TechCrunch News Scraper
Fetches latest technology news articles and updates the news catalog:
```bash
npm run scrape:news
```

### Run Scheduled Ingestion
Starts the background scheduler which periodically refreshes jobs and news according to `SCRAPER_INTERVAL_MINUTES`:
```bash
npm run scrape:schedule
```

---

## Running the Application

### Development Server
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) to view the application.

### Production Build & Start
```bash
npm run build
npm run start
```
