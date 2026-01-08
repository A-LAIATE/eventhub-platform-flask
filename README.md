# EventHub — Hobby Event Platform (Flask)

EventHub is a Flask web application for discovering and hosting hobby-based events. Users can create events, explore what others have posted, and interact through “Join” and “Like” actions without page reloads. A lightweight recommendation feature suggests an event based on a user’s activity.

---

## Key features

- **Authentication & accounts**
  - Sign up / log in / log out
  - Password hashing
  - Admin access
- **Event lifecycle**
  - Create, edit, and delete events (creator controls)
  - Explore all events in one place
  - “My Events” view for created and joined events
- **Real-time interaction (AJAX)**
  - Like / Unlike events
  - Join / Unjoin events
  - Counts update instantly (no page refresh)
- **Personalized recommendation**
  - Recommends a single event based on the user’s engagement patterns and event popularity
- **Responsive UI + accessibility**
  - Bootstrap-based layout
  - ARIA labels used for interactive groups and navigation elements

---

## Tech stack

- **Backend:** Python, Flask (app factory pattern + Blueprints)
- **Database:** SQLite + SQLAlchemy ORM
- **Auth:** Flask-Login + password hashing
- **Forms:** Flask-WTF / WTForms
- **API:** Flask-RESTful (AJAX endpoints)
- **Frontend:** Jinja templates, Bootstrap, jQuery/AJAX


---

## Data model (high-level)

- `User`
  - username, email, password_hash
  - relationships:
    - created events (one-to-many)
    - liked events (many-to-many)
    - joined events (many-to-many)
- `Event`
  - title, category, description, date, start/end time, location, creator_id
- Association tables
  - `likes` (user ↔ event)
  - `registrations` (user ↔ event)

---

## Setup & run locally

### 1) Create and activate a virtual environment

**Windows (PowerShell)**
```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

macOS / Linux
```
python3 -m venv .venv
source .venv/bin/activate
```

---

### 2) Install dependencies
```
pip install -r requirements.txt
```


### 3) Create the database

This project includes a simple database creation script:
```
python db_create.py
```
This will create `app.db` in the project root (SQLite).

### 4) Start the app
```
python run.py
```
Open: `http://127.0.0.1:5000/`

---


## How to use 

1. Visit the homepage `/`
2. Create an account at `/signup` and log in at `/login`
3. Create an event at `/create_event`
4. Browse events at `/explore_event`
5. Use Join and Like buttons (updates happen instantly via AJAX)
6. View `created/joined` events and a recommendation at `/my_events`
7. Update profile at `/update_profile`

---

## API endpoints used by the UI (AJAX)

These endpoints are called by the frontend JavaScript:

`POST /like-event/<event_id>`

`POST /join-event/<event_id>`

They return JSON responses that the UI uses to update button states and counters.

---

## Notes / known improvement areas

- Admin hardening: an admin interface exists, but role-based authorization should be hardened before any real-world use.
- Feature ideas: comments, messaging, profile pictures, event images, richer profiles.
- Engineering improvements: stricter validation, clearer separation of concerns, and more automated tests.

