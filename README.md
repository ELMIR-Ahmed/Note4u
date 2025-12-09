## 📝 Note4u

---

### **Project Overview**

**Note4u** is a simple, web-based application developed using **PHP** that allows users to **manage personal notes**. It provides a secure space where authenticated users can create an account and then log in to view, create, and read their notes. Each note consists of a title and a body.

---

### **✨ Features**

* **User Registration:** Users can create a new, secure account.
* **User Authentication:** Secure login for existing users.
* **Note Creation:** Authenticated users can create new notes with a **title** and **body**.
* **Note Viewing:** Users can access and read all their personal notes.
* **User Space:** A dedicated, personalized dashboard for managing notes.

---

### **🛠️ Technologies Used**

* **Backend:** **PHP** (Core logic and server-side processing)
* **Database:** **MySQL/MariaDB** (For storing user and note data)
* **Frontend:** **HTML5, CSS3, JavaScript** (For user interface and interactivity)
* **Web Server:** **Apache** or **Nginx**

---

### **🚀 Getting Started**

Follow these steps to get a copy of the project up and running on your local machine for development and testing purposes.

#### **Prerequisites**

You'll need a local environment that can run PHP and a MySQL database. **XAMPP**, **WAMP**, or **MAMP** are highly recommended.

* **PHP** (version 7.4 or later recommended)
* **MySQL/MariaDB**
* A Web Server (Apache/Nginx)

#### **Installation**

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/ELMIR-Ahmed/Note4u.git](https://github.com/ELMIR-Ahmed/Note4u.git)
    cd Note4u
    ```
    *(Replace the URL with your actual repository link)*

2.  **Set up the Database:**
    * Create a new database (e.g., `note4u_db`) in your MySQL server.
    * The database structure is defined in: `sql/note4u_db.sql`. Import this file into your new database.

3.  **Configure Database Connection:**
    * Locate the connection file (e.g., `php/connexion_DB.php`).
    * Update the database credentials to match your local setup:

    ```php
    // php/connexion_DB.php
    <?php
    define('DB_SERVER', 'localhost');
    define('DB_USERNAME', 'root');
    define('DB_PASSWORD', 'your_password'); // Use actual password
    define('DB_NAME', 'note4u_db');

    // Attempt to connect to MySQL database
    $conn = new mysqli(DB_SERVER, DB_USERNAME, DB_PASSWORD, DB_NAME);

    // Check connection
    if($conn === false){
        die("ERROR: Could not connect. " . $conn->connect_error);
    }
    ?>
    ```

4.  **Run the application:**
    * Place the project files into your web server's document root (e.g., `/htdocs` or `/www`).
    * Open your web browser and navigate to the project's URL (e.g., `http://localhost/Note4u`).

---

### **🗄️ Database Schema (`sql/note4u_db.sql` Example)**

This file contains the SQL necessary to create the required tables:

```sql
-- sql/note4u_db.sql

-- -----------------------------------------------------
-- Schema note4u
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `note4u` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci ;
USE `note4u` ;

-- -----------------------------------------------------
-- Table `note4u`.`users`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `note4u`.`users` (
  `id_users` INT NOT NULL AUTO_INCREMENT,
  `username` VARCHAR(45) NOT NULL,
  `phone_number` VARCHAR(25) NULL DEFAULT NULL UNIQUE,
  `email` VARCHAR(100) NOT NULL,
  `pass` VARCHAR(30) NOT NULL,
  PRIMARY KEY (`id_users`),
  UNIQUE INDEX `id_users_UNIQUE` (`id_users` ASC) VISIBLE,
  UNIQUE INDEX `email_UNIQUE` (`email` ASC) VISIBLE)
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `note4u`.`notes`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `note4u`.`notes` (
  `id_note` INT NOT NULL AUTO_INCREMENT,
  `title_note` VARCHAR(100) NOT NULL,
  `context_note` VARCHAR(10000) NOT NULL,
  `date_note` DATE NULL DEFAULT NULL,
  `id_users` INT NULL DEFAULT NULL,
  PRIMARY KEY (`id_note`),
  INDEX `id_users_idx` (`id_users` ASC) VISIBLE,
  CONSTRAINT `id_users`
    FOREIGN KEY (`id_users`)
    REFERENCES `note4u`.`users` (`id_users`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;
```

---

### **Usage**

* **Register:** Click on the "Register" link on the homepage
* **Login:** Use your new credentials to access your note space.
* **Create Note:** Click "New Note" and input a Title and the note Body.
* **View Notes:** All your notes will be listed on your dashboard.
