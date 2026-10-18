# SmorX Inspection Software

## Folders
- `frontend/` — React + Vite dark UI (Login, Super Admin, Inspection / ballooning)
- `backend/` — FastAPI API (auth, admin, multi-PDF ballooning, report PDF/Excel)

## Default login
- Email: `admin@smorx.ai`
- Password: `admin123`

The Inspection Super Admin and license records use Inspection's own database. In the
production Compose stack, the web app is on port `8464` and the API is on port `19686`.
The API connects only to the `smorx-inspection-db` service; Cost Sheet has a separate
app, login service, and database.

For a fresh database, the initial Super Admin can be set with `SUPERADMIN_EMAIL`,
`SUPERADMIN_USERNAME`, `SUPERADMIN_NAME`, and `SUPERADMIN_PASSWORD` in
`.env.smorx-inspection.production`. These settings only apply when the admin row is
first created.

The former shared Inspection/Cost Sheet auth data is not copied automatically into
the new independent databases. The previous database remains untouched; existing
accounts and licenses need a separate migration if they should remain available.

## Run backend
```bash
cd backend
pip install -r requirements.txt
uvicorn app.main:app --reload --port 9686
```

## Run frontend
```bash
cd frontend
npm install
npm run dev
```

Open http://127.0.0.1:9835 (API proxied to backend on **9686**)

## Features
- Multiple PDF upload at once
- Auto ballooning (vector engine)
- Create / Edit (move) / Delete balloons with auto sequence renumber
- Inspection report with Instr. ID + measured columns
- Tolerance colors: green exact, yellow in-tolerance, red out-of-tolerance
- Add/remove extra measured columns
- Report PDF + Excel download
