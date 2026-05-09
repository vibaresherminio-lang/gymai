# School Clinic EMR System (IPO-Based)

Fully functional thesis-ready Web-Based School Clinic Management System using the IPO model:

- **Input:** Student registration, patient forms, visit forms, feedback forms
- **Process:** Validation, CRUD processing, AI decision tree inference, auth/token verification
- **Output:** EMR records, visit history, AI classification, analytics dashboard, health insights
- **Feedback:** Rating + comment collection, stored in DB, visible to admin

## Tech Stack

- Frontend: React + TypeScript + Vite + Tailwind CSS + Recharts
- Backend: Flask + Flask-CORS + PyJWT + bcrypt
- AI Engine: scikit-learn DecisionTreeClassifier + joblib
- Database: SQLite (`clinic_v2.db`)

## User Roles (Strict)

- **Admin** (default seeded account)
- **Student** (registers via UI)

## Project Structure

```text
CLINIC/
  frontend/
    src/
      components/ProtectedRoute.tsx
      contexts/AuthContext.tsx
      pages/
        LoginPage.tsx
        RegisterPage.tsx
        AdminDashboardPage.tsx
        StudentDashboardPage.tsx
      api.ts
      App.tsx
      main.tsx
      types.ts
  backend/
    app.py
    db.py
    ai_model.py
    schema.sql
    requirements.txt
  ai-engine/
    train.py
    model.pkl
    metrics.pkl
```

## API Endpoints

- AUTH: `POST /login`, `POST /register`, `GET /me`
- PATIENTS: `POST /patients`, `GET /patients`, `GET /patients/<id>`, `PUT /patients/<id>`, `DELETE /patients/<id>`
- VISITS: `POST /visits`, `GET /visits`, `PUT /visits/<id>`, `DELETE /visits/<id>`
- AI: `POST /classify`
- REPORTS: `GET /reports`
- FEEDBACK: `POST /feedback`, `GET /feedback`

## Database Schema

- `users(id, username, password, role, patient_id)`
- `patients(id, name, age, gender, grade_level, medical_history, allergies)`
- `visits(id, patient_id, symptoms, temperature, notes, diagnosis, classification, date)`
- `feedback(id, user_id, rating, comment, created_at)`

See `backend/schema.sql`.

## Setup Guide (Step-by-Step)

### 1) Train AI model

```bash
cd ai-engine
python train.py
```

### 2) Run backend API

```bash
cd backend
pip install -r requirements.txt
python app.py
```

Backend URL: `http://127.0.0.1:5051`

### 3) Run frontend UI

```bash
cd frontend
npm install
npm run dev
```

Frontend URL: `http://localhost:5188`

## Login Credentials

- Admin: `admin / admin123`
- Student: register via `/register`, then login

## Implemented Analytics

- Total patients
- Total visits
- Most common illness
- Condition distribution (bar chart)
- Mean visits per patient
- AI accuracy rate
- Peak visits day
- Health insight sentence
