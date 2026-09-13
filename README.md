# Internet Banking Management System

A Java web application for managing banking operations using JSP, Servlets, and JDBC with MySQL database.

## Features

- 🔐 User Authentication (Login/Logout)
- 💳 Account Management (Create & View Accounts)
- 💰 Fund Transfer between accounts
- 📊 Transaction History & Summary
- 👤 User Profile Management
- ✅ Balance Inquiry & Validation

## Tech Stack

- **Backend**: Java (JSP, Servlets)
- **Database**: MySQL with JDBC
- **Frontend**: HTML5, CSS3
- **Server**: Apache Tomcat
- **IDE**: Eclipse

## Quick Start

### Prerequisites
- JDK 8+
- Apache Tomcat 7.0+
- MySQL 5.7+
- Eclipse IDE

### Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   ```

2. **Import in Eclipse**
   - File → Import → Existing Projects into Workspace
   - Select `InternetBanking/bank-example` directory

3. **Add MySQL Driver**
   - Copy `mysql-connector-java-x.x.x-bin.jar` to `WebContent/WEB-INF/lib/`
   - Right-click project → Build Path → Configure Build Path → Add JARs

4. **Create Database**
   ```sql
   CREATE DATABASE banking_system;
   USE banking_system;
   
   CREATE TABLE users (
       user_id INT PRIMARY KEY AUTO_INCREMENT,
       username VARCHAR(50) UNIQUE NOT NULL,
       password VARCHAR(255) NOT NULL,
       email VARCHAR(100),
       phone VARCHAR(20)
   );
   
   CREATE TABLE accounts (
       account_id INT PRIMARY KEY AUTO_INCREMENT,
       user_id INT NOT NULL,
       account_number VARCHAR(20) UNIQUE,
       balance DECIMAL(15, 2),
       FOREIGN KEY (user_id) REFERENCES users(user_id)
   );
   
   CREATE TABLE transactions (
       transaction_id INT PRIMARY KEY AUTO_INCREMENT,
       from_account_id INT NOT NULL,
       to_account_id INT,
       amount DECIMAL(15, 2),
       transaction_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       FOREIGN KEY (from_account_id) REFERENCES accounts(account_id)
   );
   ```

5. **Update Database Credentials**
   - Open `LoginDao.java`
   - Update connection details:
     ```java
     String url = "jdbc:mysql://localhost:3306/banking_system";
     String user = "root";
     String password = "your_password";
     ```

6. **Run the Project**
   - Right-click project → Run As → Run on Server
   - Access at `http://localhost:8080/bank-example/`

## Project Structure

```
├── frontend/                    # HTML pages
│   ├── index.html, login.html, home.html
│   ├── transfer.html, summary.html, profile.html
│   └── images/
│
├── InternetBanking/bank-example/
│   ├── src/net/javaguides/login/
│   │   ├── bean/LoginBean.java         # Data model
│   │   └── database/
│   │       ├── LoginDao.java           # DB operations
│   │       └── Transaction.java        # Transaction handling
│   └── WebContent/
│       ├── *.jsp                       # JSP views
│       └── WEB-INF/web.xml
│
└── Screenshots/                 # App screenshots
```

## Usage

1. **Register**: Create new account on home page
2. **Login**: Enter credentials to access dashboard
3. **View Balance**: Check account summary
4. **Transfer**: Send money to other accounts
5. **History**: View all transactions
6. **Logout**: Exit application

## Architecture

Follows **MVC Pattern**:
- **Model**: LoginBean.java (data objects)
- **View**: JSP pages
- **Controller**: Servlets
- **DAO**: LoginDao.java, Transaction.java

## Common Issues

| Issue | Solution |
|-------|----------|
| Driver not found | Add MySQL JAR to WEB-INF/lib/ and build path |
| DB connection fails | Check MySQL running & credentials in LoginDao.java |
| JSP not loading | Ensure proper Tomcat deployment |
| Port 8080 in use | Change port in Tomcat server config |

## Future Enhancements

- Password encryption & two-factor auth
- Admin dashboard
- Bill payments & scheduled transfers
- Mobile-responsive design
- REST API integration
- Transaction filters & search

## Contact

📧 Email: kundankabra007@gmail.com

## License

MIT License - Open source for educational purposes
