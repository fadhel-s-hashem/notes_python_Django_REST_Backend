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
pip install django djangorestframework django-cors-headers
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
### the project structure 
- this almost how it will look like
- Request ➡️ Main URLs (student_api/urls.py) ➡️ App URLs (api/urls.py) ➡️ View = Controllers (api/views.py) ➡️ Database Model (api/models.py)
- the Serializer file goona add later inside the api folder == ➡️ Serializer (api/serializers.py) 
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
- Create `.env` beside `manage.py`
- and add these , fill needed info
```
# generate secret key may use in terminal= node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
SECRET_KEY=  📌
DATABASE_ENGINE=django.db.backends.postgresql
DATABASE_NAME=students_api #📌 Here put same created database name (createdb students_api)
DATABASE_USER=  #📌 user name 
DATABASE_PASSWORD= #📌 password
DATABASE_HOST=localhost
DATABASE_PORT=5432
```
---
### Load the environment in settings 
** in side `settings.py` that part of the created api `student_api` **
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


