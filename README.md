# Land Registration and Transfer System

![PHP Version](https://img.shields.io/badge/PHP-8.3-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Framework](https://img.shields.io/badge/Framework-MVC-orange)
![Status](https://img.shields.io/badge/Status-Active-success)
![Contributors](https://img.shields.io/badge/Contributors-Welcome-brightgreen)

A secure and efficient platform for registering, transferring, and managing land properties. This system leverages advanced technologies including QR codes and blockchain to ensure transparent, secure, and user-friendly property management.

## 📋 Table of Contents
- [Key Features](#-key-features)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Configuration](#-configuration)
- [API Documentation](#-api-documentation)
- [Security Features](#-security-features)
- [Contributing](#-contributing)
- [License](#-license)
- [Authors](#-authors)
- [Support](#-support)

## 🌟 Key Features

### Core System Features
- **Property Registration**: Register and manage land properties with detailed information
  - Property details and specifications
  - Location and boundary information
  - Ownership history
  - Property valuation
- **Ownership Transfer**: Secure and transparent property transfer system
  - Digital transfer process
  - Automated verification
  - Transfer history tracking
- **QR Code Integration**: Quick property verification and information access
  - Instant property details
  - Ownership verification
  - Document access
- **Blockchain Integration**: Immutable record-keeping and transaction history
  - Smart contracts
  - Transaction verification
  - Historical record maintenance
- **User Authentication**: Secure login and role-based access control
  - Multi-factor authentication
  - Role-based permissions
  - Session management
- **Document Management**: Upload and manage property-related documents
  - Digital document storage
  - Document versioning
  - Secure access control
- **Search Functionality**: Advanced property search and filtering
  - Multi-criteria search
  - Advanced filters
  - Export capabilities

### Technical Features
- **AutoLoader**: Automatic class loading for efficient code organization
- **Log System**: Comprehensive error tracking and debugging
- **Request Handler**: Advanced HTTP request processing
- **Response Manager**: Flexible HTTP response handling
- **Router**: Dynamic URL routing and controller mapping
- **View Engine**: Powerful templating system
- **Session Management**: Secure user session handling
- **Hash Utilities**: Advanced security features
- **Data Validation**: Robust input validation system

## 🚀 Getting Started

### Prerequisites
- PHP 8.3 or higher
- Apache 2.4.6 or higher
- MySQL 8.0 or higher
- Composer (for dependency management)
- Git

### System Requirements
- Minimum 4GB RAM
- 10GB free disk space
- Windows 10/11 or Linux/Unix-based system
- Modern web browser (Chrome, Firefox, Safari, Edge)

### Installation

#### Windows Setup

1. **Install PHP**
   ```bash
   # Download PHP 8.3 VS16 X64 Thread Safe
   # Link: https://windows.php.net/download#php-8.3
   # Extract to C:/php
   ```

2. **Install Apache**
   ```bash
   # Download Apache 2.4.6 Win64
   # Link: https://www.apachelounge.com/download/
   # Extract to C:/apache24
   ```

3. **Configure Apache**
   - Navigate to `C:/Apache24/conf/httpd.conf`
   - Update the following configurations:
     ```apache
     DocumentRoot "C:/Apache24/htdocs/LandRegistrysystem/public"
     <Directory "C:/Apache24/htdocs/LandRegistrysystem/public">
         AllowOverride All
         Require all granted
     </Directory>
     DirectoryIndex index.php
     ServerName localhost:80
     ```

4. **Enable PHP in Apache**
   ```apache
   # Add to httpd.conf
     PHPIniDir "C:/php"
     LoadModule php_module "C:/php/php8apache2_4.dll"
     AddType application/x-httpd-php .php
     LoadModule rewrite_module modules/mod_rewrite.so
   ```

5. **Configure PHP**
   - Open `C:/php/php.ini`
   - Enable required extensions:
     ```ini
     extension=pdo_mysql
     extension=mysqli
     extension=openssl
     extension=fileinfo
     extension=gd
     ```

6. **Install MySQL**
   - Download MySQL Installer 8.0
   - Install MySQL Server and MySQL Workbench
   - Configure database connection

7. **Start Services**
   ```bash
   # Install Apache service
     C:/Apache24/bin/httpd.exe -k install
   
   # Start Apache
     C:/Apache24/bin/httpd.exe -k start
     ```

### Project Setup

1. **Clone Repository**
   ```bash
   git clone https://github.com/GhaithAlmomani/LandRegistrysystem.git
   cd LandRegistrysystem
   ```

2. **Install Dependencies**
   ```bash
   composer install
   ```

3. **Configure Permissions**
   ```bash
   # Ensure write permissions for:
   storage/log
   storage/session
   storage/uploads
   ```

4. **Database Setup**
   ```bash
   # Import the database schema
   mysql -u your_username -p your_database < database/schema.sql
   ```

5. **Environment Configuration**
   - Copy `.env.example` to `.env`
   - Update database credentials and other settings

## 📁 Project Structure

```
LandRegistrysystem/
├── public/          # Public entry point
│   ├── index.php    # Front controller
│   ├── assets/      # CSS, JS, images
│   └── .htaccess    # URL rewriting rules
├── src/             # Source code
│   ├── controller/  # Controllers
│   ├── core/        # Core framework
│   ├── model/       # Data models
│   ├── service/     # Business logic
│   └── view/        # Views and templates
├── storage/         # Storage for logs and sessions
│   ├── log/         # Application logs
│   ├── session/     # Session files
│   └── uploads/     # User uploads
├── tests/           # Unit and integration tests
├── vendor/          # Dependencies
└── config/          # Configuration files
```

## 🔧 Configuration

### Environment Variables
Create a `.env` file in the root directory:
```env
# Database Configuration
DB_HOST=localhost
DB_NAME=land_registry
DB_USER=your_username
DB_PASS=your_password

# Application Settings
APP_ENV=development
APP_DEBUG=true
APP_URL=http://localhost
APP_KEY=your-secret-key

# Mail Configuration
MAIL_HOST=smtp.example.com
MAIL_PORT=587
MAIL_USERNAME=your-email
MAIL_PASSWORD=your-password

# Security Settings
SESSION_LIFETIME=120
ENCRYPTION_KEY=your-encryption-key
```

### Apache Configuration
Ensure mod_rewrite is enabled and .htaccess files are allowed:
```apache
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    RewriteRule ^index\.php$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.php [L]
</IfModule>
```

## 📚 API Documentation

### Authentication Endpoints
- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration
- `POST /api/auth/logout` - User logout

### Property Endpoints
- `GET /api/properties` - List properties
- `POST /api/properties` - Create property
- `GET /api/properties/{id}` - Get property details
- `PUT /api/properties/{id}` - Update property
- `DELETE /api/properties/{id}` - Delete property

### Transfer Endpoints
- `POST /api/transfers` - Initiate transfer
- `GET /api/transfers/{id}` - Get transfer status
- `PUT /api/transfers/{id}/approve` - Approve transfer
- `PUT /api/transfers/{id}/reject` - Reject transfer

## 🔒 Security Features

- **Data Encryption**: All sensitive data is encrypted at rest
- **Input Validation**: Comprehensive input sanitization
- **CSRF Protection**: Cross-site request forgery prevention
- **XSS Protection**: Cross-site scripting prevention
- **Rate Limiting**: API request rate limiting
- **Secure Headers**: Security headers implementation
- **Password Hashing**: Bcrypt password hashing
- **Session Security**: Secure session management

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Coding Standards
- Follow PSR-12 coding standards
- Write unit tests for new features
- Update documentation as needed
- Use meaningful commit messages

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **WISE University Team** - *Initial work*

## 🙏 Acknowledgments

- Thanks to all contributors who have helped shape this project
- Special thanks to the open-source community for their invaluable tools and resources
- Inspired by modern land registry systems worldwide

## 📞 Support

For support, please:
1. Check the [documentation](docs/)
2. Search [existing issues](https://github.com/GhaithAlmomani/LandRegistrysystem/issues)
3. Create a new issue if needed
4. Contact the development team at support@landregistry.com

## 🔄 Updates

Stay updated with our latest changes:
- Follow us on [GitHub](https://github.com/GhaithAlmomani/LandRegistrysystem)
- Subscribe to our [newsletter](https://landregistry.com/newsletter)
- Join our [community forum](https://community.landregistry.com)

---

Made with ❤️ by WISE University Team
