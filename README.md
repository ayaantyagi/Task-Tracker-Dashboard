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


