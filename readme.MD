<div align="center">

# QueryHub — Discuss Q&A Forum

[![Made with PHP](https://img.shields.io/badge/Made%20with-PHP-777bb3?logo=php&logoColor=white)](https://www.php.net/)  
[![Database-MySQL](https://img.shields.io/badge/Database-MySQL-00618a?logo=mysql&logoColor=white)](https://www.mysql.com/)  
[![UI-Bootstrap](https://img.shields.io/badge/UI-Bootstrap%205-7952B3?logo=bootstrap&logoColor=white)](https://getbootstrap.com/)

<img src="public/logo.png" alt="QueryHub" width="140" />

<br/>
<br/>

Simple, clean Q&A web app where users can sign up, ask questions, answer peers, and browse by category or search.

</div>

---

### Features

- *Auth*: Sign up, log in, log out  
- *Questions*: Ask, list, view details, see related by category  
- *Answers*: Post answers on question pages  
- *Browse*: Latest feed, category filter, user’s questions  
- *Search*: Query questions by title  

### Tech Stack

- *PHP* (vanilla)  
- *MySQL* database  
- *Bootstrap 5* for styling  

### Project Structure

QueryHub/
client/ # UI pages and partials
common/ # Shared utilities (DB connection)
public/ # Static assets (CSS, images)
server/ # Request handlers
index.php # App entry/router
README.md



### Prerequisites

- PHP 7.4+ (or PHP 8+)  
- MySQL 5.7+ / MariaDB  
- Apache/Nginx (or PHP built-in server)  

### Quick Start

1) Clone this repository into your web root as a folder named **queryhub** (recommended to match redirects in code):

```bash
# Example (XAMPP on Windows)
# Place the folder at: C:\xampp\htdocs\queryhub


Create the database and tables (use name queryhub or update common/db.php).

You can start with this minimal schema:

CREATE DATABASE IF NOT EXISTS queryhub DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE queryhub;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  username VARCHAR(100) NOT NULL,
  email VARCHAR(150) NOT NULL UNIQUE,
  password VARCHAR(255) NOT NULL,
  address VARCHAR(255) NULL
);

CREATE TABLE category (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL
);

CREATE TABLE questions (
  id INT AUTO_INCREMENT PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  category_id INT NOT NULL,
  user_id INT NOT NULL,
  INDEX (category_id),
  INDEX (user_id),
  CONSTRAINT fk_questions_category FOREIGN KEY (category_id) REFERENCES category(id) ON DELETE CASCADE,
  CONSTRAINT fk_questions_user FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

CREATE TABLE answers (
  id INT AUTO_INCREMENT PRIMARY KEY,
  answer TEXT NOT NULL,
  question_id INT NOT NULL,
  user_id INT NOT NULL,
  INDEX (question_id),
  INDEX (user_id),
  CONSTRAINT fk_answers_question FOREIGN KEY (question_id) REFERENCES questions(id) ON DELETE CASCADE,
  CONSTRAINT fk_answers_user FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

Configure database connection in common/db.php:

$host = "localhost";
$username = "root";
$password = null; // or your password
$database = "queryhub"; // must match your DB name



Run the app

Via Apache: navigate to http://localhost/queryhub (folder name should be queryhub)

Via PHP built-in server (for quick preview):


cd QueryHub
php -S localhost:8000
# then open http://localhost:8000


cd QueryHub
php -S localhost:8000
# then open http://localhost:8000


Usage Tips

Use the navbar to Sign Up, Log In, search, and access Latest Questions

After login, you can Ask a Question and see My Questions

On a question page, post answers and explore related by category


Notes & Caveats

This project is intentionally simple for learning/demo purposes

Server code currently builds SQL using raw input; for production, migrate to prepared statements with bound parameters and hashing for passwords

Redirects assume the app lives under /queryhub; either keep that folder name or update redirect paths in server/requests.php

ontributing

Fork + clone

Create a feature branch

Commit with clear messages

Open a Pull Request