# 🏥 NovaCare 3D — Premium Hospital Appointment System

An ultra-modern, full-stack Hospital Appointment and Clinical Management platform built with **React 19, TypeScript, Vite, Tailwind CSS, Three.js, React Three Fiber, Framer Motion, Recharts, Node.js, Express, and MySQL 8**.

---

## ✨ Features & Architecture

### 1. Cinematic 3D Medical Hero Section
- **Genuinely rendered 3D Medical Cross & Holographic Core** built with Three.js & `@react-three/fiber`.
- Frosted physical glass transmission (`meshPhysicalMaterial`) with glowing internal heartbeat pulse core.
- Dynamic mouse-responsive parallax rotation and scientific counter-rotating orbital data rings.
- Shimmering floating particle dust field (`@react-three/drei Sparkles`).
- Orbiting 3D molecular capsules and DNA double helix visualization.
- Respects `prefers-reduced-motion` for accessibility.

### 2. Full 11-Page Healthcare Application
1. **Home (`/`)**: Cinematic 3D hero, animated statistics counters, medical departments showcase, top doctor cards, robotic surgery innovation section, and high-impact CTA.
2. **Find Doctors (`/doctors`)**: Real-time doctor search, specialty filter pills, fee & experience sorting, availability badges, and interactive 3D card tilt effects.
3. **Doctor Profile (`/doctors/:id`)**: Comprehensive physician biography, credentials, weekly consultation schedules, patient reviews, and direct booking trigger.
4. **Book Appointment (`/book`)**: 5-step guided booking wizard:
   - *Step 1*: Select doctor
   - *Step 2*: Date selection
   - *Step 3*: Dynamic time slot grid (with live booked slots marked and disabled)
   - *Step 4*: Chief complaints, symptoms, and clinical notes
   - *Step 5*: Review and confirmation with celebratory confetti animation
5. **Patient Login (`/login`)**: JWT authentication with instant 1-click Demo credentials switchers (*Patient*, *Admin*, *Doctor*).
6. **Patient Registration (`/register`)**: Account creation saving directly to MySQL `users` and `patients` tables.
7. **Patient Dashboard (`/dashboard`)**: Welcome greeting, upcoming appointments, past visit records, status badges (*Confirmed*, *Pending*, *Completed*, *Cancelled*), appointment cancellation modal, and profile editor.
8. **Admin Dashboard (`/admin`)**: Role-based access control, Recharts visual analytics (Specialty distribution bar charts, appointment status breakdown pie charts), doctor management (toggle availability, add doctor), and patient overview.
9. **About Us (`/about`)**: Clinical mission, robotic surgical suites, interactive 3D DNA Double Helix model, and hospital infrastructure metrics.
10. **Contact Us (`/contact`)**: Emergency 24/7 hotline numbers, clinic hours, interactive campus map preview, and contact inquiry form saving to MySQL `contact_messages`.
11. **Custom 404 (`*`)**: Futuristic 404 diagnostic failure screen with direct navigation back to directory.

### 3. MySQL 8 Database Architecture
Normalized relational database schema with foreign keys, indexes, and double-booking prevention:
- `users`: Core authentication and role-based access control (`patient`, `doctor`, `admin`).
- `specialties`: Medical departments (`Cardiology`, `Neurology`, `Orthopedics`, `Pediatrics`, `Dermatology`, `Oncology`).
- `doctors`: Clinical faculty, qualifications, experience, fees, ratings, and room numbers.
- `patients`: Patient profiles, blood group, date of birth, emergency contacts.
- `doctor_availability`: Weekly consultation schedules with slot durations.
- `appointments`: Scheduled consultations with **atomic double-booking prevention** via `UNIQUE KEY (doctor_id, appointment_date, appointment_time)`.
- `contact_messages`: Inpatient and outpatient inquiries.

---

## 🚀 Running the Project Locally

### Prerequisites
- **Node.js** v18+ or v20+ / v24+
- **MySQL 8** (Optional: backend includes automated smart store fallback if MySQL is offline during quick previews)

### 1. Start the Express Backend
```bash
cd backend
npm install
node src/server.js
```
The backend will run at **`http://localhost:5000`**.
- Health check: `http://localhost:5000/api/health`
- Doctors API: `http://localhost:5000/api/doctors`

#### Database Setup (When MySQL is running):
To initialize or re-seed the MySQL database:
```bash
cd backend
npm run seed
```

### 2. Start the Frontend Vite Application
```bash
cd frontend
npm install
npm run dev
```
The frontend will launch at **`http://localhost:5173`**.

---

## 🔑 Demo Login Credentials

For quick evaluation without registering a new account, the login screen provides 1-click demo buttons:

| Role | Email | Password |
|---|---|---|
| **Patient** | `patient@novacare.com` | `Password123!` |
| **Admin** | `admin@novacare.com` | `Password123!` |
| **Doctor** | `dr.elena.vance@novacare.com` | `Password123!` |

---

## 🛡️ Double-Booking Prevention

Double bookings are strictly prevented on two layers:
1. **Application Layer**: In `appointmentController.js`, a transactional query checks for existing non-cancelled bookings for the selected doctor at that exact date and time.
2. **Database Layer**: The MySQL table `appointments` enforces a unique composite constraint:
   ```sql
   UNIQUE KEY uq_doctor_slot (doctor_id, appointment_date, appointment_time)
   ```
If a conflicting booking is attempted, an HTTP `409 Conflict` error is returned with a friendly message advising the user to select another slot.

---

## 🎨 Color Palette & Typography
- **Pale Lavender**: `#f0eefa`
- **Dark Navy**: `#0a0f1d`, `#0b1329`
- **Electric Purple**: `#7c3aed`, `#8b5cf6`, `#6366f1`
- **Cyan & Emerald Accents**: `#06b6d4`, `#10b981`
- **Typography**: `Plus Jakarta Sans` for clean UI body text, `Outfit` for bold modern headings.
