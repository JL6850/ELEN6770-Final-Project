# ELEN6770-Final-Project

A web application where users can register, log in, create blog posts, edit their profiles, and interact with other users. 

## Overall Architecture

This project is built with a three-layer architecture:

### 1. **Frontend Layer**
- Technologies: HTML, CSS, JavaScript, Jinja2
- Role: Provides a responsive user interface for user interactions.
- Examples: User registration, login, profile management, and blog post creation.

### 2. **Backend Layer**
- Framework: Flask (Python)
- Role: Handles API requests, user authentication, session tracking, and business logic.

### 3. **Database Layer**
- Technology: SQLite
- Role: Stores user profiles, posts, comments, and other persistent data.

### Architecture Diagram

The architecture of the project is visualized in the diagram below:

![Optimized Web Application Architecture](./figures/Optimized%20Web%20Application%20Architecture.png)



## Features

### User Services/Interfaces
1. **User Registration and Authentication**
   - Register an account with a username, email, and password.
   - Log in and log out functionality.
   - Password reset option for registered users.

2. **Profile Management**
   - Update profile information, including bio and profile picture.

3. **Blog Posting**
   - Create blog posts.
   - Posts are displayed in a feed visible to all users.

4. **Interaction with Posts**
   - View other users' posts.
   - Leave comments.

5. **User Interface**
   - Fully responsive web interface accessible via any modern browser.
   - Built using HTML, CSS, JavaScript, and Jinja2 for interactivity.

## **Database**

- Tables and Columns

#### 1. **alembic_version**
| Column      | Type        |
| ----------- | ----------- |
| version_num | VARCHAR(32) |

---

#### 2. **followers**
| Type    | Column      |
| ------- | ----------- |
| INTEGER | follower_id |
| INTEGER | followed_id |

---

#### 3. **message**
| Column       | Type         |
| ------------ | ------------ |
| id           | INTEGER      |
| sender_id    | INTEGER      |
| recipient_id | INTEGER      |
| body         | VARCHAR(140) |
| timestamp    | DATETIME     |

---

#### 4. **notification**
| Column       | Type         |
| ------------ | ------------ |
| id           | INTEGER      |
| name         | VARCHAR(128) |
| user_id      | INTEGER      |
| timestamp    | FLOAT        |
| payload_json | TEXT         |

---

#### 5. **post**
| Column    | Type         |
| --------- | ------------ |
| id        | INTEGER      |
| body      | VARCHAR(140) |
| timestamp | DATETIME     |
| user_id   | INTEGER      |
| language  | VARCHAR(5)   |

---

#### 6. **user**
| Column                 | Type         |
| :--------------------- | ------------ |
| id                     | INTEGER      |
| username               | VARCHAR(64)  |
| email                  | VARCHAR(120) |
| password_hash          | VARCHAR(256) |
| about_me               | VARCHAR(140) |
| last_seen              | DATETIME     |
| last_message_read_time | DATETIME     |

---

### Usage

#### Database Configuration
- The database consists of 6 primary tables: `alembic_version`, `followers`, `message`, `notification`, `post`, and `user`.
- These tables support the main functionalities of the project, such as user management, notifications, messaging, and post creation.

#### Relationships
- **followers**: Manages the many-to-many relationship between users (follower and followed).
- **message**: Stores messages exchanged between users, including sender and recipient.
- **notification**: Handles user-specific notifications with associated payloads.
- **post**: Stores user-generated posts, including content, timestamps, and language.
- **user**: Maintains user profiles, login credentials, and activity metadata.

#### Notes
- For efficient querying, indices are defined for key columns such as `username` and `email` in the `user` table.

---



###  **Cloud**
- **Platform**: Hosted on AWS EC2.
- **Translation**: Uses **Microsoft Azure Translate API** for translating posts or comments to English.

---


## Project Setup

### Prerequisites
- Python 3.8+
- Flask Framework
- AWS EC2 Instance (for deployment)
- SQLite (for local testing) or MySQL/PostgreSQL (for production)

## 1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```
---

## 2. Configure Environment Variables

Create a `.flaskenv` file in the root directory of the project with the following content:

```plaintext
FLASK_APP=microblog.py
FLASK_ENV=development
SECRET_KEY=<your-secret-key>
DATABASE_URL=sqlite:///app.db
```

- Replace `<your-secret-key>` with a strong secret key.

---

## 3. Initialize the Database

Run the following commands to set up the database:

```bash
flask db init
flask db migrate -m "Initial migration"
flask db upgrade
```

---

## 4. Run the Application Locally

Start the Flask development server:

```bash
flask run
```

The application will be accessible at `http://127.0.0.1:5000`.

or you can use
```bash
flask run --host=0.0.0.0
```

---

## 5. Troubleshooting

### 5.1 Missing Dependencies
Ensure all dependencies in `requirements.txt` are installed:
```bash
pip install -r requirements.txt
```

### 5.2 Database Issues
Ensure the database URL in `.flaskenv` is correct, and check if database migrations were successfully applied.

### 5.3 Environment Variables Not Set
Ensure the `.flaskenv` file is correctly configured. Activate the virtual environment before running Flask commands:
```bash
source venv/bin/activate
```

---

# Project Directory Structure

```plaintext
.
├── README.md
├── app
│   ├── __init__.py
│   ├── auth
│   │   ├── __init__.py
│   │   ├── email.py
│   │   ├── forms.py
│   │   └── routes.py
│   ├── cli.py
│   ├── email.py
│   ├── errors
│   │   ├── __init__.py
│   │   └── handlers.py
│   ├── errors.py
│   ├── main
│   │   ├── __init__.py
│   │   ├── forms.py
│   │   └── routes.py
│   ├── models.py
│   ├── search.py
│   ├── static
│   │   └── loading.gif
│   ├── templates
│   │   ├── _post.html
│   │   ├── auth
│   │   │   ├── login.html
│   │   │   ├── register.html
│   │   │   ├── reset_password.html
│   │   │   └── reset_password_request.html
│   │   ├── base.html
│   │   ├── bootstrap_wtf.html
│   │   ├── edit_profile.html
│   │   ├── email
│   │   │   ├── reset_password.html
│   │   │   └── reset_password.txt
│   │   ├── errors
│   │   │   ├── 404.html
│   │   │   └── 500.html
│   │   ├── index.html
│   │   ├── messages.html
│   │   ├── search.html
│   │   ├── send_message.html
│   │   ├── user.html
│   │   └── user_popup.html
│   ├── translate.py
│   └── translations
│       └── es
│           └── LC_MESSAGES
│               ├── messages.mo
│               └── messages.po
├── app.db
├── babel.cfg
├── config.py
├── logs
│   └── microblog.log
├── microblog.py
├── migrations
├── requirements.txt
├── test2.py
└── tests.py

22 directories, 86 files
```


## Notes

- This setup is for local development purposes. For production deployment, additional steps such as setting up a production database, securing the application, and configuring a WSGI server (e.g., Gunicorn) will be necessary.
- Reference [Miguel Grinberg's Flask Mega-Tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world) for additional insights.

---

