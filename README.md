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

# File Contents
1. 'requirements.txt'             
    Django==4.2.7                       

2. 'manage.py'                          
     #!/usr/bin/env python                                    
 """Django's command-line utility for administrative tasks."""                                    
 import os                                 
 import sys
                                                                 
 def main():                                      
     """Run administrative tasks."""                                           
     os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'task_tracker.settings')                                     
     try:                                                
         from django.core.management import execute_from_command_line                                     
     except ImportError as exc:                                             
         raise ImportError(                                               
             "Couldn't import Django. Are you sure it's installed and "                                                 
             "available on your PYTHONPATH environment variable? Did you "                                                     
             "forget to activate a virtual environment?"                                              
         ) from exc                                                      
     execute_from_command_line(sys.argv)                                                                   
            
                                    
 if __name__ == '__main__':                                     
     main()                                                           
   
