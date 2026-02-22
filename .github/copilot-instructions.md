# Copilot Instructions for webprog_it241_django_w3_schools

## Project Overview
This is a Django 6.0.2 tutorial project for W3Schools, demonstrating web development fundamentals. The project has a single `members` app managing member-related functionality.

**Key Technology Stack:**
- Django 6.0.2 (via venv in `myworld/`)
- SQLite database (`db.sqlite3`)
- Virtual environment: `myworld/` with Python 3.12

## Architecture & Key Components

### Directory Structure
- `my_tennis_club/` - Main Django project with central settings
  - `settings.py` - Project configuration (Django apps, middleware, database)
  - `urls.py` - Root URL router (delegates to `members.urls`)
  - `wsgi.py` - WSGI application entry point
- `members/` - Primary app containing business logic
  - `models.py` - Data models (currently empty, ready for extension)
  - `views.py` - Request handlers (simple function-based views)
  - `urls.py` - App-level URL routing
  - `admin.py` - Django admin interface registration

### Data Flow
1. HTTP request arrives at Django
2. Root URL router (`my_tennis_club/urls.py`) delegates to `members.urls`
3. `members` app views process the request (currently returns HTTP responses)
4. Response returned to client

## Development Workflows

### Running the Development Server
```bash
cd /workspaces/webprog_it241_django_w3_schools/my_tennis_club
python manage.py runserver
```
Server runs on `http://127.0.0.1:8000/` by default.

### Database Migrations
```bash
python manage.py makemigrations  # Create migration files from model changes
python manage.py migrate         # Apply migrations to database
```

### Django Admin Access
- Run the server, then navigate to `http://127.0.0.1:8000/admin/`
- Models must be registered in `members/admin.py` to appear in admin

### Creating Models
Add model classes to `members/models.py`. Remember to:
1. Define fields using Django field types
2. Create and apply migrations: `makemigrations` then `migrate`
3. Register in `members/admin.py` for admin interface access

## Project Patterns & Conventions

### URL Structure
- Root URLs in `my_tennis_club/urls.py` include app URLs
- App-level URLs in `members/urls.py` follow the pattern: `path('members/', views.members, name='members')`
- Always use `name=` parameter for reverse URL lookups (e.g., in templates)

### Views
Currently using function-based views. Pattern in `members/views.py`:
```python
from django.shortcuts import render
from django.http import HttpResponse

def members(request):
    return HttpResponse("Hello WEBPROG IT241!")
```

Extend this as needed:
- Use `HttpResponse` for plain text/JSON
- Use `render()` with templates for HTML
- Access request data via `request.POST`, `request.GET`, or URL parameters

### Django Admin Registration
In `members/admin.py`, register models like:
```python
from django.contrib import admin
from .models import YourModel

admin.site.register(YourModel)
```

## Critical Settings to Know
- **DEBUG = True** in `settings.py` (development only)
- **ALLOWED_HOSTS = []** (empty in dev, add hosts before production)
- **INSTALLED_APPS** - Add new apps here after `startapp`
- **DATABASES** - SQLite backend at `db.sqlite3`

## Common Tasks

### Adding a New App
```bash
python manage.py startapp appname
# Then add 'appname' to INSTALLED_APPS in settings.py
```

### Accessing the Database Shell
```bash
python manage.py shell
```
Useful for testing queries, creating objects: `from members.models import YourModel`

### Creating a Superuser for Admin
```bash
python manage.py createsuperuser
```

## Active Development Notes
- The `members` app is currently minimal with empty models and basic view
- No templates directory yet - add `templates/` in the app to use template rendering
- This is a learning project, so focus on clear structure and conventions
