# Jarvis Arena

Jarvis Arena is a Django-based web app that offers:
- A gaming homepage with interactive UI
- User authentication (register, login, forgot password)
- Developer and services pages
- Multiple browser games and game detail/play screens
- Downloadable game documentation/PDFs

## Tech Stack
- Python
- Django
- django-allauth
- HTML/CSS/JavaScript

## Project Structure
```text
jarvis-arena/
├── jarvis/                # Django project settings and root URLs
├── jarvisapp/             # App views, models, routes
├── templates/             # HTML templates
├── static/                # CSS, JS, images, audio
├── requirements.txt
├── manage.py
└── Dockerfile
```

## Prerequisites
- Python 3.10+ recommended
- pip

## Quick Start (Local)

1. Clone and enter project
```bash
git clone <your-repo-url>
cd jarvis-arena
```

2. Create and activate virtual environment
```bash
python -m venv .venv
source .venv/bin/activate
```
On Windows (PowerShell):
```powershell
.venv\Scripts\Activate.ps1
```

3. Install dependencies
```bash
pip install -r requirements.txt
```

4. Run migrations
```bash
python manage.py migrate
```

5. Start server
```bash
python manage.py runserver --insecure 127.0.0.1:8000
```

6. Open in browser
```text
http://127.0.0.1:8000/
```

## Why `--insecure`?
This project currently has `DEBUG = False` in `jarvis/settings.py`, so static files may not load in normal `runserver` mode.  
Using `--insecure` is the easiest local workaround.

## Important Routes
- Home: `/`
- Login: `/authrization/login/`
- Register: `/authrization/register/`
- Contact: `/services/contact_us`
- Games dashboard: `/Games/allgames/` (login required)

## Authentication Notes
- Most game pages are protected with `@login_required`.
- Register and login first to access game dashboards and downloads.
- Forgot password flow is available at `/authrization/forget_password/`.

## Email Configuration (Optional but Recommended)
Password reset and some account flows use email.

In `jarvis/settings.py`, configure:
- `EMAIL_HOST_USER`
- `EMAIL_HOST_PASSWORD` (or app password)

Without valid email setup, email-based features may fail.

## Docker (Optional)
Build image:
```bash
docker build -t jarvis-arena .
```

Run container:
```bash
docker run --rm -p 8000:8000 jarvis-arena python manage.py runserver --insecure 0.0.0.0:8000
```

Open:
```text
http://127.0.0.1:8000/
```

## Common Issues

1. `ModuleNotFoundError: No module named 'django'`
- Activate virtualenv and install requirements again.

2. HTML loads but no CSS/images
- Use:
```bash
python manage.py runserver --insecure 127.0.0.1:8000
```

3. Migration warning on startup
- Run:
```bash
python manage.py migrate
```

4. Social login/site issues with allauth
- Verify `SITE_ID` in `jarvis/settings.py` matches an existing Site record in DB.

## Contributing
1. Create a branch
2. Make changes
3. Test locally
4. Open a pull request

---
If you want, I can also add a one-command setup script (`setup.sh`) so anyone can install + run the project automatically.
