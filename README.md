# AbsenYuk

> Platform manajemen acara dan absensi berbasis web dengan QR code terintegrasi.

AbsenYuk memungkinkan penyelenggara acara mengelola peserta, membuat sesi absensi dengan QR code, dan memantau kehadiran secara real-time — semuanya paperless.

---

## Tech Stack

| Layer | Teknologi |
|-------|-----------|
| **Frontend** | Vanilla HTML/CSS/JS, DM Sans |
| **Backend** | Express.js, JWT, bcrypt |
| **Database** | MySQL / MariaDB |
| **QR** | `qrcode` (SVG) |
| **Export** | ExcelJS (XLSX) + pdfmake (PDF) |
| **Upload** | Multer (avatar) |

---

## Struktur Proyek

```
AbsenYuk/
├── backend/           # Express API server
│   ├── src/api/       Route definitions
│   ├── src/database/  SQL queries & business logic
│   ├── src/middleware/ JWT auth + role guards
│   └── src/utils/     QR, export generators
├── frontend/
│   ├── pages/         13 HTML pages (homepage, login, dashboard, etc.)
│   ├── scripts/       16 JS modules (api, shared, per-page logic)
│   └── styles/        7 CSS files
└── package.json       Root orchestration
```

---

## Role System

| Role | Akses |
|------|-------|
| **User** | Ikut acara, isi absensi via QR/link, forum diskusi |
| **Organizer** | Buat/kelola acara, sesi absensi, QR, log kehadiran |
| **Admin** | Kelola semua user/acara/absensi, export, preview role |

---

## Cara Menjalankan

```bash
# Backend
cd backend
npm install
npm run dev            

# Frontend (development — static serve)
cd frontend
npx serve . -l 5000

# Production (Express serve frontend + API)
cd backend
npm start
```

Backend `.env`:
```
APP_PORT=3000
APP_BASE_URL=http://localhost:3000
JWT_SECRET=your-secret
DB_HOST=localhost
DB_USER=root
DB_PASS=your-password
DB_NAME=your-db-name
```

---

## Fitur Utama

- **QR Code Absensi** — Generate QR per sesi, peserta scan atau buka link
- **Forum Diskusi** — Tiap acara punya forum post + komentar
- **Role-based Dashboard** — Admin/Organizer/User masing-masing punya tampilan sendiri
- **Export Data** — Excel/PDF untuk user, acara, absensi, log (admin only)
- **Server-side Pagination** — Semua tabel admin ter-paginate
- **Avatar Upload** — Foto profil via multer (JPEG/PNG/WebP, max 2MB)

---

## API Overview

Base URL: `http://localhost:{PORT}/api`

| Domain | Endpoints | Auth |
|--------|-----------|------|
| `/user` | Register, login, CRUD, profile, avatar | Public + JWT |
| `/acara` | CRUD, browse, status | JWT (org/admin) |
| `/acara-ikuti` | Join/leave events | JWT |
| `/acara-post` | Forum CRUD, komentar | JWT |
| `/absensi` | Sesi, QR, submit, logs | JWT |
| `/dashboard` | Summary stats | JWT (admin) |
| `/export` | Export XLSX/PDF | JWT (admin only) |

---

## Tim Pengembang

| Role | Nama |
|------|------|
| **Frontend** | Rahmat Ramadhan, Azahari Faisal |
| **Backend** | Muhammad Putra Ramadhan, Fahrizal Pratama |
