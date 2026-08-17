# 💰 ExpenseX.

A full-stack Expense Tracker application built with **Java Spring Boot 3.5.4**, **MySQL**, **Spring Security**, **JWT authentication**, **Thymeleaf**, and **Docker**.

The application allows users to securely manage income and expenses, create budgets and categories, view dashboards and analytics, generate PDF/Excel reports, and perform authentication using OTP and JWT-based security.

---

## 🚀 Features

### 🔐 Authentication & Security
- User registration
- Email OTP verification
- Login with OTP verification
- JWT-based authentication
- Access token and refresh token support
- Forgot password functionality
- Password reset
- Change password
- Account activation/deactivation
- Spring Security integration
- CORS configuration

### 💸 Expense Management
- Add expenses
- View expenses
- Edit expenses
- Delete expenses
- Search expenses by category
- Filter expenses by date range
- Calculate total expenses
- Calculate monthly expenses
- Expense categorization

### 💰 Budget Management
- Create budgets
- View budgets
- Update budgets
- Delete budgets
- View budgets by user
- Monthly budget management

### 🏷️ Category Management
- Create categories
- View categories
- Update categories
- Delete categories

### 📊 Dashboard & Analytics
- Expense dashboard
- Monthly expense summary
- Financial summary
- Category-wise expense analysis
- Analytics page
- User-specific dashboard

### 📄 Reports
Generate financial reports in multiple formats:
- PDF reports
- Excel reports
- Analytics reports
- Monthly summary
- Yearly summary
- Category-wise summary

### 📧 Email & OTP
The application supports email communication using Gmail SMTP. Features include:
- Registration OTP
- Login OTP
- Password reset email
- OTP verification
- OTP resend

> **Security:** Never commit your Gmail password, Google App Password, JWT secret, database password, or other secrets to GitHub.

### 📱 SMS Expense Integration
The project contains an SMS expense parser and webhook endpoint designed to receive bank transaction information.

```
POST /api/webhook/sms/{webhookToken}
```

This provides the backend integration point for a future Android application that can read transaction SMS messages and send relevant transaction information to the Expense Tracker backend.

---

## 🛠️ Technology Stack

**Backend**
- Java 21
- Spring Boot 3.5.4
- Spring Web
- Spring Security
- Spring Data JPA
- Hibernate
- Spring Validation
- Spring Mail
- Thymeleaf

**Database**
- MySQL 8.0

**Authentication**
- JWT
- Spring Security
- Refresh Tokens
- OTP verification

**Libraries**
- Lombok
- ModelMapper
- JJWT
- Jackson Java 8 Date/Time
- iText PDF
- Apache POI

**API Documentation**
- Springdoc OpenAPI
- Swagger UI

**DevOps**
- Docker
- Docker Compose
- Maven

---

## 📁 Project Structure

```
ExpenseTracker/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/expensetracker/
│   │   │       ├── config/
│   │   │       ├── controller/
│   │   │       ├── model/
│   │   │       ├── repository/
│   │   │       ├── security/
│   │   │       ├── service/
│   │   │       └── util/
│   │   │
│   │   └── resources/
│   │       ├── templates/
│   │       ├── static/
│   │       └── application.properties
│   │
│   └── test/
│
├── Dockerfile
├── docker-compose.yaml
├── pom.xml
├── mvnw
├── mvnw.cmd
├── .gitignore
└── README.md
```

---

## ⚙️ Requirements

Before running the application, install:

- Java 21
- Maven
- MySQL 8.0
- Git
- Docker Desktop (optional)

Check versions:

```bash
java -version
mvn -version
docker --version
```

---

## 🗄️ Database Setup

Create the MySQL database:

```sql
CREATE DATABASE expense_tracker;
```

The application uses:

| Setting | Value |
|---|---|
| Database Name | `expense_tracker` |
| Database Port | `3306` |

The project uses:

```properties
spring.jpa.hibernate.ddl-auto=update
```

Hibernate can therefore automatically create/update the required tables when the application starts.

---

## 🔑 Environment Variables

For security, use environment variables instead of storing credentials directly in the project.

```env
DB_URL=jdbc:mysql://localhost:3306/expense_tracker
DB_USERNAME=root
DB_PASSWORD=YOUR_DATABASE_PASSWORD

JWT_SECRET=YOUR_LONG_RANDOM_JWT_SECRET
JWT_EXPIRATION=86400000
JWT_REFRESH_EXPIRATION=604800000

MAIL_USERNAME=your-email@gmail.com
MAIL_APP_PASSWORD=YOUR_GOOGLE_APP_PASSWORD
```

> **Important:** Do not upload the following to GitHub:
> - `.env`
> - `application.properties` containing passwords
> - JWT secrets
> - Database passwords
> - Gmail App Passwords
> - API keys
> - Webhook secrets
>
> If credentials were previously committed to GitHub, rotate them immediately.

---

## ▶️ Running Locally

**1. Clone the repository**

```bash
git clone https://github.com/Lokesh-github07/ExpenseTracker.git
cd ExpenseTracker
```

**2. Configure MySQL**

Make sure MySQL is running and create the database:

```sql
CREATE DATABASE expense_tracker;
```

**3. Configure Environment Variables**

Set your database, JWT, and email credentials.

**4. Build the Project**

Using Maven:

```bash
mvn clean install
```

On Windows:

```bash
mvnw.cmd clean install
```

**5. Start the Application**

```bash
mvn spring-boot:run
```

Or on Windows:

```bash
mvnw.cmd spring-boot:run
```

The application will start on:

```
http://localhost:8080
```

---

## 🌐 Web Application

Open:

```
http://localhost:8080
```

Typical application pages include:

- `/`
- `/login`
- `/register`
- `/terms`
- `/forgot-password`
- `/dashboard`
- `/add-expense`
- `/edit-expense`
- `/profile`
- `/analytics`

---

## 🐳 Running with Docker

The project includes:

- `Dockerfile`
- `docker-compose.yaml`
- MySQL 8 Docker container
- Spring Boot Docker container

The Docker setup contains two services:

- `expense-tracker-app`
- `expense-tracker-mysql`

**1. Configure Environment Variables**

Create a `.env` file in the project root:

```env
DB_PASSWORD=YOUR_DATABASE_PASSWORD
JWT_SECRET=YOUR_LONG_RANDOM_SECRET
JWT_EXPIRATION=86400000
JWT_REFRESH_EXPIRATION=604800000

MAIL_USERNAME=your-email@gmail.com
MAIL_APP_PASSWORD=YOUR_GOOGLE_APP_PASSWORD
```

**2. Start Docker**

```bash
docker compose up --build
```

Run in background:

```bash
docker compose up --build -d
```

**3. Check Containers**

```bash
docker ps
```

You should see containers similar to:

```
expense-tracker-app
expense-tracker-mysql
```

**4. Open Application**

```
http://localhost:8080
```

MySQL is exposed to the host on:

```
localhost:3307
```

Inside Docker, the application connects to MySQL using:

```
mysql:3306
```

**5. Stop Docker**

```bash
docker compose down
```

To remove the database volume as well:

```bash
docker compose down -v
```

> **Warning:** Removing the volume deletes the MySQL container data.

---

## 🔐 Authentication API

Base URL: `http://localhost:8080/api/auth`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/register` | Register a new user |
| POST | `/verify-otp` | Verify registration OTP |
| POST | `/resend-otp` | Resend OTP |
| POST | `/login` | Login |
| POST | `/login/verify-otp` | Verify login OTP |
| POST | `/refresh-token` | Generate a new access token |
| POST | `/forgot-password` | Request password reset |
| POST | `/reset-password` | Reset password |
| GET | `/health` | Authentication service health check |

---

## 💸 Expense API

Base URL: `http://localhost:8080/api/expenses`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/` | Create expense |
| GET | `/` | Get expenses |
| GET | `/{id}` | Get expense |
| PUT | `/{id}` | Update expense |
| DELETE | `/{id}` | Delete expense |
| GET | `/category/{categoryId}` | Get expenses by category |
| GET | `/date-range` | Get expenses by date range |
| GET | `/total` | Get total expenses |
| GET | `/monthly-total` | Get monthly total |

---

## 💰 Budget API

Base URL: `http://localhost:8080/api/budgets`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/` | Create budget |
| GET | `/` | Get budgets |
| GET | `/{id}` | Get budget |
| PUT | `/{id}` | Update budget |
| DELETE | `/{id}` | Delete budget |
| GET | `/user/{userId}` | Get user budgets |
| GET | `/month` | Get monthly budget |

---

## 🏷️ Category API

Base URL: `http://localhost:8080/api/categories`

| Method | Endpoint | Description |
|---|---|---|
| POST | `/` | Create category |
| GET | `/` | Get categories |
| GET | `/{id}` | Get category |
| PUT | `/{id}` | Update category |
| DELETE | `/{id}` | Delete category |

---

## 📊 Dashboard API

Base URL: `http://localhost:8080/api/dashboard`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Dashboard data |
| GET | `/user/{userId}` | User dashboard |
| GET | `/monthly` | Monthly dashboard |
| GET | `/summary` | Financial summary |

---

## 📄 Reports API

Base URL: `http://localhost:8080/api/reports`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/analytics` | Analytics report |
| GET | `/pdf` | Generate PDF report |
| GET | `/excel` | Generate Excel report |
| GET | `/monthly-summary` | Monthly summary |
| GET | `/yearly-summary` | Yearly summary |
| GET | `/category-summary` | Category summary |

---

## 👤 User API

Base URL: `http://localhost:8080/api/users`

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Get users |
| GET | `/{id}` | Get user |
| GET | `/email/{email}` | Find user by email |
| PUT | `/{id}/profile` | Update profile |
| PUT | `/change-password` | Change password |
| DELETE | `/account` | Delete current account |
| DELETE | `/{id}` | Delete user |
| PUT | `/{id}/activate` | Activate account |
| PUT | `/{id}/deactivate` | Deactivate account |

---

## 📱 SMS Webhook

The application includes an endpoint for receiving transaction information from an external application such as a future Android SMS integration.

```
POST /api/webhook/sms/{webhookToken}
```

**Possible architecture:**

```
Bank SMS
   ↓
Android Application
   ↓
SMS Parser
   ↓
Expense Tracker REST API
   ↓
Spring Boot
   ↓
MySQL
   ↓
Dashboard / Reports
```

This allows the project to be extended into a mobile expense-tracking system that automatically detects bank debit and credit SMS messages.

---

## 📚 Swagger API Documentation

The project includes Springdoc OpenAPI configuration.

After starting the application, Swagger UI can normally be accessed at:

```
http://localhost:8080/swagger-ui/index.html
```

OpenAPI specification:

```
http://localhost:8080/v3/api-docs
```

Swagger can be used to:

- View API endpoints
- Test APIs
- Send GET/POST/PUT/DELETE requests
- Inspect request parameters
- Inspect API responses
- Test authentication-protected endpoints

---

## 🧪 API Testing with Postman

You can test the application using Postman.

Base URL:

```
http://localhost:8080
```

Example registration:

```
POST /api/auth/register
```

Example login:

```
POST /api/auth/login
```

After obtaining the JWT access token, use:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

for protected API requests.

---

## 🔄 Application Flow

```
                 ┌──────────────────┐
                 │      User        │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │  Web Interface   │
                 │    Thymeleaf     │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Spring Security  │
                 │   + JWT + OTP    │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ REST Controllers │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │    Services      │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │ Spring Data JPA  │
                 └────────┬─────────┘
                          │
                          ▼
                 ┌──────────────────┐
                 │      MySQL       │
                 └──────────────────┘
```

---

## 🐳 Docker Architecture

```
                 Docker Compose
                       │
          ┌────────────┴────────────┐
          │                         │
          ▼                         ▼
 ┌─────────────────┐       ┌─────────────────┐
 │ Spring Boot App │──────▶│   MySQL 8.0     │
 │     :8080       │       │   :3306         │
 └─────────────────┘       └────────┬────────┘
                                    │
                                    ▼
                              mysql-data
                                volume
```

---

## 🔒 Security Considerations

This project uses several security mechanisms:

- Spring Security
- JWT authentication
- Refresh tokens
- OTP verification
- Password reset
- Account activation/deactivation
- SMTP authentication
- Environment-based secrets

**For production deployment:**

- Use HTTPS.
- Generate a strong random JWT secret.
- Never expose database credentials.
- Never commit `.env`.
- Use a Google App Password instead of a Gmail account password.
- Use secure database credentials.
- Configure proper CORS rules.
- Protect the SMS webhook token.
- Disable unnecessary debug logging.
- Use a production database backup strategy.

---

## 📦 Build JAR

Build the application:

```bash
mvn clean package -DskipTests
```

The generated JAR will be located in:

```
target/expense-tracker-0.0.1-SNAPSHOT.jar
```

Run it using:

```bash
java -jar target/expense-tracker-0.0.1-SNAPSHOT.jar
```

---

## 🧹 Useful Docker Commands

| Command | Description |
|---|---|
| `docker ps` | View running containers |
| `docker logs expense-tracker-app` | View application logs |
| `docker logs -f expense-tracker-app` | Follow application logs |
| `docker logs expense-tracker-mysql` | View MySQL logs |
| `docker compose down` | Stop containers |
| `docker compose up --build` | Rebuild |
| `docker compose down -v` | Remove containers and database volume |

---

## 📈 Future Improvements

- Android mobile application
- Automatic bank SMS transaction detection
- Automatic debit/credit classification
- UPI transaction detection
- Push notifications
- Recurring expenses
- Savings goals
- Investment tracking
- Multiple currencies
- Advanced financial analytics
- Spending predictions
- AI-powered expense categorization
- Cloud deployment
- CI/CD pipeline
- Automated unit and integration testing
- Automated Postman API testing
- Jira-based QA workflow
- Role-based admin dashboard

---

## 🧪 Testing

**Recommended testing tools:**

- JUnit
- Mockito
- Postman
- Swagger UI
- Selenium
- Playwright
- Jira
- Docker

**Testing can cover:**

```
Unit Testing
     ↓
Integration Testing
     ↓
API Testing
     ↓
Manual Testing
     ↓
Automation Testing
     ↓
Docker Testing
     ↓
Deployment Testing
```

---

## 🌐 Deployment

The application can be deployed using:

- Docker
- Oracle Cloud
- VPS
- AWS
- Azure
- Google Cloud
- Cloudflare Tunnel for exposing a locally hosted application

For production deployment, use a managed MySQL database or a properly secured MySQL server rather than exposing a local development database.

---

## 👨‍💻 Author

**Lokesh Pande**

Java Full Stack Developer | Spring Boot | REST APIs | MySQL | Docker | Manual & Automation Testing

---

## ⭐ Project Highlights

This project demonstrates practical experience with:

Java 21 · Spring Boot · Spring Security · JWT · REST API · MySQL · JPA / Hibernate · Thymeleaf · OTP Authentication · Email Integration · PDF Generation · Excel Generation · Docker · Docker Compose · Swagger / OpenAPI · API Testing · SMS Integration

---

## 📜 License

This project is intended for educational, portfolio, and development purposes.

You may modify and extend the project according to your requirements.
