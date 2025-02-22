# 📘 Spring Boot + MySQL CRUD Application

This project is a simple Spring Boot application that connects to a MySQL database and performs basic CRUD (Create, Read, Update, Delete) operations. Follow this guide to understand and set up your project step by step!

---

## 🛠️ **1. Project Setup**

### ⚙️ **Step 1: Create a Spring Boot Project**

- Go to [start.spring.io](https://start.spring.io)
- Fill in the project details:
  - **Project:** Maven
  - **Language:** Java
  - **Spring Boot Version:** 3.x
  - **Packaging:** Jar
  - **Java Version:** 21

### 📦 **Step 2: Add Dependencies**

Add these dependencies:

- **Spring Web**
- **Spring Boot DevTools**
- **Spring Data JPA**
- **MySQL Driver**

Click **Generate** and download the project ZIP. Extract and open it in your IDE.

---

## 🛢 **2. MySQL Database Setup**

1. Install and start MySQL.
2. Create a new database:

```sql
CREATE DATABASE bookmanagment;
```

3. Add your database credentials in `src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/bookmanagment
spring.datasource.username=root
spring.datasource.password=root

spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
```

> Replace `your_password` with your MySQL password.

---

## 🏗️ **3. Create the User Entity**

Create a class `User.java`:

```java
package com.example.bookmanagment;

import jakarta.persistence.*;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String userName;
    private String userPassword;
    private String userAddress;

    // Getters and Setters
}
```

---

## 🗃️ **4. Create the Repository**

Create `UserRepository.java`:

```java
package com.example.bookmanagment;

import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

---

## 🚀 **5. Create the Controller**

Create `CreateUser.java`:

```java
package com.example.bookmanagment;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;

@Controller
public class CreateUser {

    @Autowired
    private UserRepository userRepository;

    @GetMapping("/createUser")
    public String createUserHomePage() {
        return "createUserHomePage";
    }

    @GetMapping("/createUserDB")
    public String createUserDB(@RequestParam("userName") String userName,
                               @RequestParam("userPassword") String userPassword,
                               @RequestParam("userAddress") String userAddress) {
        
        User user = new User();
        user.setUserName(userName);
        user.setUserPassword(userPassword);
        user.setUserAddress(userAddress);
        
        userRepository.save(user);
        
        return "createUserDB";
    }
}
```

---

## ▶️ **6. Run the Application**

1. Compile and run the project:

```sh
mvn spring-boot:run
```

2. Open the browser and test:

```
http://localhost:8080/createUserDB?userName=JohnDoe&userPassword=secret123&userAddress=NewYork
```

3. Check the data in MySQL:

```sql
USE bookmanagment;
SELECT * FROM user;
```

---

## 📂 **7. Project Structure**

```
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com.example.bookmanagment
│   │   │       ├── BookmanagmentApplication.java
│   │   │       ├── CreateUser.java
│   │   │       ├── User.java
│   │   │       └── UserRepository.java
│   │   └── resources
│   │       ├── application.properties
│   │       └── templates
└── pom.xml
```

---

## ✅ **8. Final Notes**

🎯 You’ve built a complete Spring Boot app with MySQL connectivity! You can now:

- **Create users** via query parameters.
- **Store user details** in MySQL.
- **View stored users** directly from the database.

Want to take it further?
- Add **CRUD operations** (update, delete, fetch by ID).
- Build a simple **HTML form**.
- Implement **password encryption**.

Let me know if you’d like to add these features! 🚀

---

## 📘 **9. Push to GitHub**

1. Initialize a Git repo:

```sh
git init
git add .
git commit -m "Initial commit - Spring Boot MySQL App"
```

2. Create a new repository on GitHub.
3. Add the remote and push:

```sh
git remote add origin https://github.com/your-username/bookmanagment.git
git branch -M main
git push -u origin main
```

🚀 **Done!** Your project is now live on GitHub!

---

Would you like me to help with Git commands or improve your app further? Let me know! 🚀

