

# ITKANNADIGARU Web Application

A Java-based web application with user authentication, displaying ITKANNADIGARU homepage with a link to the YouTube channel. Users must register and login to access the application.

## Project Structure

```
.
├── pom.xml
├── itkannadigaru.db (SQLite database - created automatically)
└── src
    └── main
        ├── java
        │   └── com
        │       └── itkannadigaru
        │           ├── HomeServlet.java
        │           ├── database
        │           │   └── DatabaseManager.java
        │           ├── model
        │           │   └── User.java
        │           └── servlet
        │               ├── LoginServlet.java
        │               ├── LogoutServlet.java
        │               └── RegisterServlet.java
        └── webapp
            ├── WEB-INF
            │   └── web.xml
            ├── index.jsp
            ├── login.jsp
            └── register.jsp
```

## Prerequisites

- Java Development Kit (JDK) 11 or higher
- Apache Maven 3.6 or higher

## How to Build

Build the application using Maven:

```bash
mvn clean package
```

This will create a WAR file in the `target` directory: `itkannadigaru.war`

## How to Run

### Option 1: Using Embedded Tomcat (Recommended for Development)

Run the application directly using the Tomcat Maven plugin:

```bash
mvn tomcat7:run
```

Then open your browser and navigate to:
```
http://localhost:8080
```

### Option 2: Deploy to External Tomcat Server

1. Build the WAR file:
   ```bash
   mvn clean package
   ```

2. Copy the WAR file to your Tomcat webapps directory:
   ```bash
   cp target/itkannadigaru.war $TOMCAT_HOME/webapps/
   ```

3. Start Tomcat:
   ```bash
   $TOMCAT_HOME/bin/startup.sh  # On Linux/Mac
   $TOMCAT_HOME/bin/startup.bat # On Windows
   ```

4. Access the application at:
   ```
   http://localhost:8080/itkannadigaru
   ```

## Application Features

### Authentication System
- **User Registration**: New users can create an account with username, email, and password
- **User Login**: Registered users must login to access the application
- **Secure Password Storage**: Passwords are hashed using SHA-256 before storage
- **SQLite Database**: User credentials stored in a local SQLite database
- **Session Management**: User sessions with 30-minute timeout
- **Form Validation**: Server-side validation for all input fields

### Homepage Features
- Clean and modern homepage design (accessible only after login)
- Displays "ITKANNADIGARU" as the main heading
- Shows logged-in username with welcome message
- Logout button to end session
- Provides a clickable link to the YouTube channel: https://www.youtube.com/@Manojdevops-z7s
- Responsive design that works on mobile and desktop
- Smooth animations and hover effects

## Technology Stack

- Java Servlet API 4.0
- JSP (JavaServer Pages)
- SQLite JDBC Driver for database operations
- JSTL (JSP Standard Tag Library)
- Maven for build management
- HTML5 & CSS3 for frontend

## Database

The application uses SQLite for storing user credentials. The database file `itkannadigaru.db` is created automatically in the project root directory when you first run the application.

### Database Schema

**users table:**
- `id` - INTEGER PRIMARY KEY AUTOINCREMENT
- `username` - TEXT NOT NULL UNIQUE
- `email` - TEXT NOT NULL UNIQUE
- `password` - TEXT NOT NULL (SHA-256 hashed)
- `created_at` - TIMESTAMP DEFAULT CURRENT_TIMESTAMP

## Usage Flow

1. **First Time Users:**
   - Navigate to http://localhost:8080
   - Click "Register here" on the login page
   - Fill in username, email, and password
   - Submit registration form
   - After successful registration, you'll be redirected to login

2. **Returning Users:**
   - Navigate to http://localhost:8080
   - Enter username and password
   - Click "Login"
   - Access the main homepage with YouTube link

3. **Logging Out:**
   - Click the "Logout" button in the top-right corner
   - You'll be redirected to the login page

## Security Features

- Password hashing using SHA-256
- Session-based authentication
- Protected routes (home page accessible only after login)
- Input validation on both client and server side
- Unique username and email constraints
- SQL injection prevention using prepared statements

## Stopping the Application

If running with `mvn tomcat7:run`, press `Ctrl+C` in the terminal to stop the server.

## Troubleshooting

### Port Already in Use

If port 8080 is already in use, you can change it by editing the `pom.xml` file:

```xml
<configuration>
    <port>9090</port>  <!-- Change to your desired port -->
    <path>/</path>
</configuration>
```

### Database Issues

If you encounter database issues:
1. Delete the `itkannadigaru.db` file
2. Restart the application - the database will be recreated automatically

### Login Issues

- Make sure you've registered first
- Username and password are case-sensitive
- Check that there are no spaces before or after your credentials

## License

This is a simple demonstration application for educational purposes.
