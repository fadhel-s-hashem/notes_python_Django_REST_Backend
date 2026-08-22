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
- Request ➡️ Main URLs (student_api/urls.py) ➡️ App URLs (api/urls.py) ➡️ View (api/views.py) ➡️ Database Model (api/models.py)
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
