# NHL Fan Rankings

This is an independent NHL player-ranking site with no CapWages or PuckPedia branding.

## What is already built

- Overall NHL rankings
- Position-specific rankings
- Top 10, Top 15, and Top 20 boards
- Drag-and-drop ordering
- Local browser saving
- Copy and JSON export
- A "Submit completed ranking" button
- Central database submission through Supabase
- Anonymous public inserts with no public database-reading permission

## Connect the central database

### 1. Create a free Supabase project

Go to Supabase and create a new project.

### 2. Create the rankings table

Open:

**SQL Editor -> New query**

Paste everything from `supabase-setup.sql`, then run it.

### 3. Copy two public project values

Open:

**Project Settings -> API**

Copy:

- Project URL
- anon public key

Do **not** use or publish the service-role key.

### 4. Add them to the website

Open `index.html` and find:

```js
const DATABASE_CONFIG = {
  supabaseUrl: "PASTE_YOUR_SUPABASE_PROJECT_URL_HERE",
  supabaseAnonKey: "PASTE_YOUR_SUPABASE_ANON_KEY_HERE"
};
```

Replace those two placeholder values and save the file.

### 5. Upload the new files to GitHub

Replace the old `index.html` in your GitHub repository with this one.

The website can remain on GitHub Pages. Supabase receives the completed rankings.

## Accessing submissions

In Supabase, open:

**Table Editor -> ranking_submissions**

You can:

- inspect every completed ranking
- filter by overall or position
- export the table as CSV
- use the `ranking_rows` JSON column to calculate consensus rankings

Visitors can insert rows, but the included row-level security policy does not allow anonymous users to read the database.

## Important limitation

A public website cannot completely prevent spam or coordinated manipulation. This build includes:

- completed-board validation
- a one-minute browser cooldown
- unique submission IDs
- anonymous browser session IDs
- database-side length validation

For a public launch with significant traffic, add CAPTCHA or move submissions through a serverless function with stricter rate limiting.
