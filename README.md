# Task Tracker Dashboard
## Project Overview
Task Tracker Dashboard is a lightweight, full-stack web application built with Django for managing tasks in a collaborative environment. It supports role-based authentication, allowing users to create, read, update, and delete (CRUD) tasks while respecting permissions (e.g., Admins can manage all tasks, while regular Users can only handle their own). The app uses SQLite as a database for simple, file-based storage—ideal for development, prototyping, or small-scale deployment without needing a full database server.

This project emphasizes usability with a responsive Bootstrap frontend, secure backend logic via Django's built-in authentication, and a clean separation of concerns. It's designed for teams or individuals tracking personal/professional tasks, with features like priority levels, status tracking, and user assignments.


## Key Features
Role-Based Authentication:                                     
Two roles: "Admin" (full access to all tasks and users) and "User " (limited to own tasks).                                
Built-in login/logout using Django's auth system. No external libraries needed.                                    
## Task Management:                           
Create tasks with title, description, priority (Low/Medium/High), and status (Pending/In Progress/Completed).                            
Assign tasks to users (Admins can assign to anyone; Users assign to themselves).                              
View dashboard with filtered task lists (all for Admins, personal for Users).                                       
Update or delete tasks with permission checks (only creator or Admin).                                              
Task details view for inspection.          
  
Search and Filtering: Admin interface includes search by title/description and filters by status/priority/date.                                        
Responsive UI: Bootstrap 5 for mobile-friendly design, including navigation, forms, tables, and alerts.                                        
Security: CSRF protection, permission decorators, and hashed passwords out-of-the-box.                                                  
Lightweight Database: SQLite—no setup for external DBs; stores users, tasks, and groups in a single db.sqlite3 file.                                           
Extensibility: Easy to add features like email notifications, file attachments, or switch to PostgreSQL/MySQL.                                         

# Tech Stack
## Backend: Django 4.2.7 (Python 3.8+)                                   
Database: SQLite 3 (default; file-based, no server required)                                          
Frontend: HTML/CSS/JS with Bootstrap 5 (via CDN for simplicity; no build tools needed)                                                     
Authentication: Django's built-in User  model with Groups for roles                                               
Forms/Validation: Django ModelForms with Bootstrap styling                                                           
Dependencies: Minimal—only Django (see requirements.txt)                                                          
Project Structure                                                  
The repository is organized as a standard Django project:  

 # Project Structure
task_tracker_dashboard/                            
├── manage.py                                                   
├── requirements.txt                                                   
├── db.sqlite3                (generated after migrations)                                              
├── task_tracker/             (main project folder)                                  
│   ├── __init__.py                    
│   ├── settings.py                                      
│   ├── urls.py                                    
│   ├── wsgi.py                                         
│   └── asgi.py               (optional, not used here)                
├── tasks/   (Django app)                                 
│   ├── __init__.py                                      
│   ├── admin.py                                                 
│   ├── apps.py                                                        
│   ├── migrations/                                                          
│   │   ├── __init__.py                                                     
│   │   └── 0001_initial.py    (generated; I'll provide a sample)                                             
│   ├── models.py                                       
│   ├── tests.py                                                  
│   ├── urls.py                                                             
│   └── views.py                                                             
└── templates/         (Django templates folder)                                  
    ├── base.html                                           
    ├── registration/                                    
    │   └── login.html                                       
    ├── tasks/                                              
    │   ├── dashboard.html                                         
    │   ├── task_list.html                                               
    │   ├── task_form.html                                           
    │   └── task_detail.html                                                   
└── static/  (optional; Bootstrap via CDN, but you can add if needed)            

Database Details (Tables and Schema)
The app uses Django's ORM to define models, which generate tables in SQLite. After running migrations, the key tables are:                                

auth_user (Built-in Django table):                                                

Stores user accounts: id, username, email, password (hashed), first_name, last_name, is_staff, is_active, date_joined.                                                                         
Example: Admins and Users are standard Django users.                                                                                                
auth_group (Built-in Django table for roles):                                                                                                                      

Stores roles: id, name (e.g., "Admin", "User ").                                                                                                         
Users are assigned to groups via auth_user_groups junction table.                                                                                                  
tasks_task (Custom table from Task model):                                                                                                                            

Primary key: id (auto-incrementing integer).                                                        
Fields:                                       
title: VARCHAR(200) – Task name (required).                                    
description: TEXT – Detailed notes (required).                                             
priority: VARCHAR(10) – Choices: 'low', 'medium', 'high' (default: 'medium').                                                       
status: VARCHAR(15) – Choices: 'pending', 'in_progress', 'completed' (default: 'pending').                                                           
assigned_to_id: INTEGER – Foreign key to auth_user.id (who the task is assigned to).                                              
created_by_id: INTEGER – Foreign key to auth_user.id (who created it).                                         
created_at: DATETIME – Auto-set on creation (timestamp).                                                       
updated_at: DATETIME – Auto-updated on changes.                                                              
Indexes/Ordering: Ordered by -created_at (newest first). No custom indexes beyond Django defaults.                                                                 
Relationships:                                                    
Many-to-one: Task → User (assigned_to, created_by).                                                           
Reverse: User → Tasks (via related_name='assigned_tasks' and 'created_tasks').                                               
Other Built-in Tables (Auto-generated by Django):                                             
                          
django_migrations: Tracks applied migrations.                               
auth_user_groups and auth_user_user_permissions: For role assignments.                                  
django_session: For user sessions.                                              
Total Tables: ~10 (mostly Django internals + 1 custom). Database size starts small (~1-10 MB) and grows with tasks/users. View schema in Django Admin (/admin/) or query SQLite directly (e.g., via sqlite3 db.sqlite3 CLI: .schema tasks_task).                                                         
                                                                                                 
Sample Data Flow:                                        
 
Create User: Via Django Admin or shell (python manage.py createsuperuser).                                       
Assign Role: In Admin, add user to "Admin" or "User " group.                                            
Create Task: Form submits → Model saves to tasks_task → Linked to users via FKs.                                                                  
Query Example (SQL equivalent): SELECT * FROM tasks_task WHERE assigned_to_id = 1 ORDER BY created_at DESC;   

 # Frontend Details
Templates: Jinja2-style Django templates with Bootstrap 5 classes for styling.                                                  
base.html: Shared layout with navbar (login status, links to dashboard/create/logout), message alerts, and content block.                                      
login.html: Simple form for username/password.                                                                                                  
dashboard.html/task_list.html: Table of tasks with columns (Title, Status, Priority, Assigned To, Created At). Buttons for Update/Delete/Detail. Filtered by role.                       
task_form.html: Bootstrap form with inputs (text, textarea, selects). Handles create/update.                                                  
task_detail.html: Read-only view of task + delete confirmation.                                                                 
Styling: Bootstrap CDN for grids, buttons, alerts, modals. Icons via Bootstrap Icons. Responsive (mobile/tablet/desktop).                                
JavaScript: Minimal—Bootstrap's JS for alerts/dismissals. No custom JS needed.                                                     
User Experience: Clean dashboard loads on login. Messages for success/errors. Navbar shows role (e.g., "Welcome, john (Admin)").                                           
# Backend Details       
Views (views.py): Function-based with @login_required decorator.                         
dashboard/task_list: Fetches tasks (all for Admin, own for User) → Renders table.                      
task_create/task_update: Form handling with validation; auto-assigns creator/assigned_to based on role.                          
task_delete/task_detail: Permission checks (e.g., if request.user != task.created_by and not is_admin → redirect with error).                                   
Models (models.py): Single Task model with choices for priority/status. __str__ for readable display.                                   
Forms (forms.py): TaskForm (ModelForm) with Bootstrap attrs for auto-styling.                          
URLs (urls.py): Root includes app URLs (e.g., /tasks/create/, /tasks/update/1/).                                               
Admin (admin.py): Custom TaskAdmin for easy management (list view, filters, search).                         
Middleware/Settings: Standard Django (sessions, CSRF, auth). Templates dir: project-level for shared files.                           
Error Handling: 404 for invalid tasks; messages for permissions; redirects to login if unauthenticated.                             
Security/Performance: Role checks prevent unauthorized access. SQLite is fine for <100 users; for scale, migrate to PostgreSQL.                           
Setup Instructions (Start to End)                               
Prerequisites:                                 
                         
# Python 3.8+ installed.                  
Git (optional, for repo cloning).                        
Clone/Create Repository:                                         
                                                                                
Create a folder: mkdir task_tracker_dashboard && cd task_tracker_dashboard.                             
Copy-paste all files from the provided structure (e.g., via your IDE or file explorer).                                        
Initialize Git: git init (optional). 

# Install Dependencies:                                          
                                                     
Create virtual environment: python -m venv venv.                                    
Activate: Windows (venv\Scripts\activate), macOS/Linux (source venv/bin/activate).                                      
Install: pip install -r requirements.txt.

# Database Setup:                                                                   
                                                                           
Run migrations: python manage.py makemigrations (creates migration files).                                                    
Apply: python manage.py migrate (creates db.sqlite3 and tables).                                                                    
Create superuser (Admin): python manage.py createsuperuser (set username/password).

# Role Setup:                                                                                                                                   
                                                                                              
Access Django Admin: python manage.py runserver → Visit http://127.0.0.1:8000/admin/.                                                                                          
Login with superuser.                                                                                                        
Create Groups: Add "Admin" and "User " under "Groups".                                                                                 
Create Users: Add regular users under "Users", then assign to groups (e.g., superuser to "Admin").

# Run the Server:                                                            
                         
python manage.py runserver.                              
Visit http://127.0.0.1:8000/ (redirects to login).                       
Login: Use created credentials.                                   
Dashboard: /tasks/dashboard/ (auto-redirect after login). 

# Testing:                             
                                 
Create tasks via /tasks/create/.                     
View: /tasks/ or dashboard.                          
Admin full access: /admin/tasks/task/.                               
Tests: python manage.py test tasks (expand tests.py as needed).  

# Deployment (Optional):                                
                                                                                                 
For production: Set DEBUG=False, change SECRET_KEY, use PostgreSQL (update settings.py DATABASES).            
Host on Heroku/Vercel: Add Procfile (web: gunicorn task_tracker.wsgi), push to Git.                        
Static files: python manage.py collectstatic (if adding custom CSS/JS).  

## License

MIT License

Copyright (c) 2023 Ayan Tyagi                                                        
                                                                             
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:                                                      
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS ORIMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Contact

- **Author**: Ayan TYagi  
- **Email**: ayan.tyagi2211@gmail.com  
- **GitHub**: https://github.com/ayaantyagi 
- **LinkedIn**: https://www.linkedin.com/in/ayan-tyagi/ 
- **Project Issues**: Report bugs or request features on the (https://github.com/ayaantyagi/task-tracker-dashboard/issues).

For collaboration, contributions, or customizations, feel free to open an issue or email me directly.
