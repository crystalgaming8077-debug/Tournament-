# AKTan V25.1 — Render Ready

## Deploy
1. Upload these files to a GitHub repository.
2. In Render: New -> Web Service -> connect the repository.
3. Runtime: Node.
4. Build command: `npm install`
5. Start command: `npm start`
6. Health check: `/health`
7. Deploy.

The server listens on `0.0.0.0` and uses Render's `PORT` environment variable.

## Public spectator
Open the deployed URL in the admin browser, create the Public Link, then share only that tokenized URL with spectators.

## Important data note
This version stores shared tournament state in `public-data.json`. Render's free web service filesystem is not a durable database. For a real tournament with important registrations, use a persistent database or persistent disk before relying on it as the sole copy of data. Keep your existing V24/V25.1 local backup.


## V26 Persistent Public Link
This build supports persistent public-link data through Render PostgreSQL. If `DATABASE_URL` is configured, public tokens, tournament state, and registrations are stored in the `aktan_publications` table and survive service restarts/redeploys. Without `DATABASE_URL`, it falls back to `public-data.json`.

### Render setup
1. Create a PostgreSQL database in Render.
2. In the web service Environment settings, add `DATABASE_URL` using the database's internal connection URL.
3. Redeploy the web service.
4. Open `/health`; the response should show `persistentStore: true` and `version: "26.0.0"`.
5. Create/Sync the public link once. Keep that tokenized URL; future restarts use the same database record.
