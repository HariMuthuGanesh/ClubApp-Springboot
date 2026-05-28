# Club Management System (ClubApp-Springboot)

A premium, modern REST API backend built with **Spring Boot 3.x** and **Java 21/25** designed to streamline managing college clubs, event organization, attendance tracking, member join requests, and roles within an educational institution.

---

## 🌟 Key Features

*   **Role-Based Access Control (RBAC):** Distinct roles (`ADMIN`, `COORDINATOR`, `STUDENT`) secured via stateless **JWT Authentication**.
*   **Club Administration:** Complete management of club details, active members, and assigning coordinators.
*   **Event Planning & Tracking:** Publish upcoming and past events, track attendance in real-time, and manage attendee registration.
*   **Club Join Requests:** Smooth workflow for students requesting to join clubs and coordinators approving/rejecting requests.
*   **Excel Export Reports:** Export club event attendance reports directly to Excel format using Apache POI.
*   **Real-time Notifications:** Real-time event updates and alerts powered by WebSockets.
*   **Interactive API Docs:** Fully documented REST endpoints via Swagger UI / Springdoc OpenAPI.

---

## 🛠️ Technology Stack

*   **Language:** Java 21 / 25
*   **Framework:** Spring Boot 3.2.4
*   **Security:** Spring Security & JJWT (JSON Web Token)
*   **Database:** MySQL (Object-relational mapping via Spring Data JPA & Hibernate)
*   **WebSockets:** Spring WebSocket messaging
*   **Report Generation:** Apache POI (Excel spreadsheets)
*   **Interactive Docs:** Springdoc OpenAPI / Swagger UI
*   **Utilities:** Lombok, Spring Dotenv

---

## ⚙️ Configuration & Credentials Setup

The application uses the `spring-dotenv` library to securely load configuration variables at runtime without hardcoding them in the source code or properties files.

### Where to Replace Credentials

You need to define your credentials in a **`.env`** file. Follow these steps:

1. Create a file named **`.env`** in the root directory of the project (`d:\ClubApp-Springboot\.env`).
2. Add the following lines and replace the values with your local configurations:

```env
# -------------------------------------------------------------
# 1. DATABASE CREDENTIALS
# The password for your local MySQL server (User: root)
# -------------------------------------------------------------
DB_PASSWORD=your_mysql_password_here

# -------------------------------------------------------------
# 2. SECURITY CREDENTIALS
# A secret key used to sign and verify JSON Web Tokens.
# IMPORTANT: Must be at least 32 characters (256 bits) long to satisfy HMAC-SHA256 requirements.
# -------------------------------------------------------------
JWT_SECRET=your_super_secret_jwt_key_that_is_at_least_32_characters_long_12345

# -------------------------------------------------------------
# 3. ADMIN PRIVILEGES
# A secure token string used to verify and allow registering new ADMIN users.
# Pass this in the 'X-Admin-Secret' header when creating admins.
# -------------------------------------------------------------
ADMIN_SECRET=your_admin_setup_secret_token_here
```

> [!WARNING]
> Do not commit this `.env` file to your Git repository (it is automatically ignored via `.gitignore` to keep credentials secure).

---

## 🚀 Running the Project

### Prerequisites
*   **Java Development Kit (JDK 21 or later)**
*   **Apache Maven (3.x or later)**
*   **MySQL Server** (running on `localhost:3306`)

### Step 1: Initialize Database
Ensure your MySQL service is running. You do not need to create the database schema manually. The JDBC URL configuration:
`jdbc:mysql://localhost:3306/ClubApp?createDatabaseIfNotExist=true`
will automatically create the `ClubApp` database schema on your MySQL instance when the application bootstraps.

### Step 2: Build & Start
To build the application and start the dev server, execute:
```powershell
mvn spring-boot:run
```

Alternatively, package the app into a runnable JAR:
```powershell
# Compile & Package
mvn clean package

# Run Executable Jar
java -jar target/ClubApp-Spring-1.0-SNAPSHOT.jar
```

---

## 📖 API Documentation & Endpoints

Once the application runs, it starts on port **`9090`** (defined in [application.properties](file:///d:/ClubApp-Springboot/src/main/resources/application.properties)).

*   **Swagger API Documentation UI:** [http://localhost:9090/swagger-ui.html](http://localhost:9090/swagger-ui.html)
*   **OpenAPI JSON Specification:** [http://localhost:9090/v3/api-docs](http://localhost:9090/v3/api-docs)

### Core Authentication Endpoints
*   `POST /api/auth/register` — Registers a new student account.
*   `POST /api/auth/register/admin` — Registers a new administrator (requires `X-Admin-Secret` header).
*   `POST /api/auth/login` — Authenticates a user and returns a JWT token.
