# AKTan V25 PostgreSQL Persistent Build

This build keeps the V25 HTML as the UI and adds PostgreSQL-backed persistence to the public tournament server.

## Render setup
1. Keep the PostgreSQL database available on Render.
2. In the Web Service Environment, set `DATABASE_URL` to the database's **Internal Database URL**.
3. Push/replace ALL files from this package in the GitHub repository used by the Render Web Service.
4. Deploy the latest commit.
5. Open `/health`. A correct setup returns `persistentStore: true` and version `25.2.0-postgres`.

The server automatically creates the `aktan_publications` table. If a local `public-data.json` exists and the PostgreSQL table is empty, it migrates those publications once.

Never commit `DATABASE_URL` or database passwords to GitHub.


## V26 Public Contest Rooms
Unlimited public rooms/contests with independent category, format, map, slot capacity, entry-fee display, prize pool, start time, status and rules. Public registration selects a room and the server enforces capacity including pending registrations. Entry fee is display/information only; payment collection, verification and refunds remain outside the app. Admin PIN can be changed from the Admin/Teams area.
