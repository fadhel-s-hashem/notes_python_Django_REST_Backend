# notes_python_Django_REST_Backend


## 📚 Project Setup & Architecture Overview

### Virtual Environment & Project Initialization

- Create and activate virtual environment
- Windows Git Bash:
```bash
python -m venv .venv
source .venv/Scripts/activate
```
- Add project dependencies
- Create `requirements.txt`
- add these to install the core packege
``` bash
Django>=5.2,<5.3
djangorestframework>=3.16,<4
django-cors-headers>=4,<5
djangorestframework-simplejwt>=5.5,<6
psycopg[binary]>=3.2,<4
python-dotenv>=1,<2

```
- Install core packages
```bash
pip install -r requirements.txt
```
- some times it may needed to write `python -m ` if its denied
```bash
 python -m pip install -r requirements.txt
```
- Create the PostgreSQL database
```bash
createdb students_api
```
- Initialize Django project and application
```bash
django-admin startproject student_api .
python manage.py startapp api
```
### 🎞️ The project structure 
<details>
<summary>Press here to check how it look</summary>

> Request ➡️ Main URLs (student_api/urls.py) ➡️ App URLs (api/urls.py) ➡️ View = Controllers (api/views.py) ➡️ Database Model (api/models.py)
>>the Serializer file goona add later inside the api folder == ➡️ Serializer (api/serializers.py)
>>
**This almost how it will look like**
```
hoot-backend/
├── .venv/
├── api/
│   ├── migrations/
│   ├── admin.py
│   ├── apps.py
│   ├── models.py 
│   └── views.py 
├── student_api/
│   ├── settings.py 
│   ├── urls.py 
│   ├── asgi.py
│   └── wsgi.py 
├── manage.py 
└── requirements.txt 
```
</details>

- Create `.env` beside `manage.py`
- and add these , fill needed info
```
# generate secret key may use in terminal= node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
SECRET_KEY=  📌☝️
DATABASE_ENGINE=django.db.backends.postgresql
DATABASE_NAME=students_api #📌 Here put same created database name (createdb students_api)
DATABASE_USER=  #📌 user name 
DATABASE_PASSWORD= #📌 password
DATABASE_HOST=localhost
DATABASE_PORT=5432
```
---
### Load the environment in settings 
***In side `settings.py` that part of the created api `student_api`***
-  add the new imports `path` and `dotenv`:
```
import os
from pathlib import Path

from dotenv import load_dotenv
```
- In `BASE_DIR`, load `.env`:
- just add `load ` at the end
```
BASE_DIR = Path(__file__).resolve().parent.parent
# ☝️ after this add the load_dotenv
load_dotenv(BASE_DIR / ".env")
```
- Chanfe the `SECRET_KEY`
```
SECRET_KEY = os.getenv(
    "SECRET_KEY",
    "django-insecure-classroom-only-not-for-production-12345",
)
```
- add the `INSTALLED_APPS` at the end of array
```
# new INSTALLED_APPS
    "corsheaders",
    "rest_framework",
    "api",
```
- add the `MIDDLEWARE` at the beginig of the array
```
 # the added middleware must be before the original
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.security.SecurityMiddleware",
    "django.contrib.sessions.middleware.SessionMiddleware",
    "django.middleware.common.CommonMiddleware",
```
- Replace the generated DATABASES setting:
```
DATABASES = {
    "default": {
        "ENGINE": os.getenv(
            "DATABASE_ENGINE", "django.db.backends.postgresql"
        ),
        "NAME": os.getenv("DATABASE_NAME", "hoot_api"),
        "USER": os.getenv("DATABASE_USER", ""),
        "PASSWORD": os.getenv("DATABASE_PASSWORD", ""),
        "HOST": os.getenv("DATABASE_HOST", "localhost"),
        "PORT": os.getenv("DATABASE_PORT", "5432"),
    }
}
```
### Create Django built-in tables
- First create tabel the first `migrate` commant is to create tabel
```
python manage.py migrate
```
- You can use the `check` command before running the server to catch setup bugs
```
python manage.py check
```
- finally start the server with `runserver`
```
python manage.py runserver
```
| Command | Action | When to Use |
| :--- | :--- | :--- |
| **`python manage.py migrate`** | Builds/updates database tables | First setup, or after running `makemigrations` |
| **`python manage.py check`** | Scans project for code errors | Before running the server to catch setup bugs |
| **`python manage.py runserver`** | Starts local HTTP dev server | Every time you want to test your API (` http://localhost:8000`) |
### 🛑 Important Django built-in tables rules
Whenever you change your schema in `models.py`, always run:

1. **`python manage.py makemigrations`** → Creates the blueprint file.
2. **`python manage.py migrate`** → Executes the blueprint to build actual SQL tables.

> **Note:** Forgetting to run `migrate` causes an `OperationalError: no such table` error when hitting your API endpoints.

**Main URL Routing Configuration `(student_api/urls.py)`**
- Includes all API app routes at root/path
```
from django.contrib import admin
from django.urls import path , include # remeber to add the include

urlpatterns = [
    path('admin/', admin.site.urls),
    path("", include("api.urls")),
]
```
---
For more info --> [the hoot backend lesson](https://seb-bh.github.io/django-rest-hoots-backend/)




