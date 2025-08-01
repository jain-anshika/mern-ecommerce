# 🚀 MERN Ecommerce Setup Instructions

This document provides step-by-step instructions to set up and run the MERN Ecommerce application on your local machine.

## 📋 Prerequisites

Before starting, ensure you have the following installed:

- **Node.js** (version v21.1.0 or later) - [Download here](https://nodejs.org/)
- **MongoDB** installed and running locally - [Installation Guide](https://docs.mongodb.com/manual/installation/)
- **Git** - [Download here](https://git-scm.com/downloads)

## 📥 Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/jain-anshika/mern-ecommerce.git
cd mern-ecommerce
```

### 2. Install Dependencies

**Important:** Install dependencies for both frontend and backend separately. Use split terminals for efficiency.

#### Install Frontend Dependencies
```bash
cd frontend
npm install
```

#### Install Backend Dependencies
```bash
cd backend
npm install
```

## ⚙️ Environment Configuration

### Backend Environment Variables

1. **Create a `.env` file** in the `backend` directory
2. **Copy the contents** from `backend/.env.example`
3. **Update the values** as described below:

```bash
# Database connection string
# For local MongoDB:
MONGO_URI=mongodb://localhost:27017/mern-ecommerce
# For MongoDB Atlas (cloud):
MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/mern-ecommerce

# Frontend URL (adjust if needed)
ORIGIN=http://localhost:3000

# Email credentials for sending password resets and OTPs
# IMPORTANT: Use Gmail App Password, not your regular Gmail password
# Steps to get App Password:
# 1. Enable 2-Factor Authentication on your Gmail
# 2. Go to Google Account Settings > Security > App Passwords
# 3. Generate password for "Mail" application
EMAIL=your-email@gmail.com
PASSWORD=your-16-digit-app-password

# Token and cookie expiration settings
LOGIN_TOKEN_EXPIRATION=30d  # Days
OTP_EXPIRATION_TIME=120000  # Milliseconds (2 minutes)
PASSWORD_RESET_TOKEN_EXPIRATION=2m  # Minutes
COOKIE_EXPIRATION_DAYS=30    # Days

# Secret key for JWT security
# Generate a strong random key using: require('crypto').randomBytes(64).toString('hex')
SECRET_KEY=your-super-secure-random-jwt-secret-key-here

# Environment (production/development)
PRODUCTION=false # Set to true for production
```

### Frontend Environment Variables

1. **Create a `.env` file** in the `frontend` directory
2. **Copy the contents** from `frontend/.env.example`
3. **Update the values**:

```bash
# Backend API URL
# For development:
REACT_APP_BASE_URL=http://localhost:8000/
# For production:
# REACT_APP_BASE_URL=https://your-api-domain.com/
```

### 🔒 Security Guidelines for Environment Variables

#### Gmail App Password Setup:
1. **Enable 2-Factor Authentication** on your Gmail account
2. **Go to Google Account Settings**: https://myaccount.google.com/security
3. **Navigate to "App passwords"**
4. **Generate a password** for "Mail" application
5. **Use the 16-digit code** as your PASSWORD in the .env file

#### JWT Secret Key Generation:
```javascript
// Run this in Node.js console to generate a secure key:
require('crypto').randomBytes(64).toString('hex')
```

#### Important Security Notes:
- ❌ **Never commit `.env` files** to version control
- ✅ **Use strong, unique passwords** for all services
- ✅ **Keep your secret keys secure** and rotate them regularly
- ✅ **Use different credentials** for development and production

## 🗄️ Database Setup

### Option 1: Local MongoDB
1. **Install MongoDB** on your local machine
2. **Start MongoDB service**:
   ```bash
   # On Windows
   net start MongoDB
   
   # On macOS
   brew services start mongodb/brew/mongodb-community
   
   # On Linux
   sudo systemctl start mongod
   ```
3. **Use local connection string** in your `.env` file:
   ```
   MONGO_URI=mongodb://localhost:27017/mern-ecommerce
   ```

### Option 2: MongoDB Atlas (Cloud)
1. **Create account** at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. **Create a free cluster**
3. **Set up database access** (create database user)
4. **Configure network access** (add your IP or allow all for development)
5. **Get connection string** and update your `.env` file

## 🌱 Database Seeding (Optional but Recommended)

Populate your database with sample data for testing:

1. **Navigate to backend directory**:
   ```bash
   cd backend
   ```

2. **Run the seeding script**:
   ```bash
   npm run seed
   ```

This will create:
- Sample users (including demo accounts)
- Product catalog
- Categories and brands
- Sample reviews and orders

## 🏃‍♂️ Running the Application

### Important Notes:
- **Use separate terminals** for frontend and backend
- **Install nodemon globally** for backend development: `npm install -g nodemon`

### 1. Start the Backend Server

```bash
cd backend
npm run dev
# or
npm start
```

**Expected output:**
```
[nodemon] starting `node index.js`
server [STARTED] ~ http://localhost:8000
connected to DB
```

### 2. Start the Frontend Server

```bash
cd frontend
npm start
```

**Expected output:**
```
Compiled successfully!

You can now view frontend in the browser.

Local:            http://localhost:3000
On Your Network:  http://192.168.x.x:3000
```

## 🌐 Accessing the Application

Once both servers are running:

- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8000

## 👤 Demo Account (After Seeding)

Use these credentials to explore the application:

```
Email: demo@gmail.com
Password: demo
```

**Note**: The demo account has limitations:
- Password reset and OTP verification are not available (uses non-real email)
- To test these features, create a personal account with a valid email

## 🛠️ Development Tools

### Useful Commands

#### Backend:
```bash
# Development mode with auto-restart
npm run dev

# Production mode
npm start

# Database seeding
npm run seed
```

#### Frontend:
```bash
# Development server
npm start

# Build for production
npm run build

# Run tests
npm test
```

## 🐛 Troubleshooting

### Common Issues:

#### Port Already in Use:
```bash
# Check what's using port 8000
netstat -ano | findstr :8000

# Kill the process (Windows)
taskkill /PID <process_id> /F
```

#### MongoDB Connection Issues:
- Ensure MongoDB service is running
- Check connection string format
- Verify network access (for Atlas)
- Check username/password encoding

#### Environment Variable Issues:
- Ensure no quotes around values in `.env` files
- Restart servers after changing `.env` files
- Check for typos in variable names

#### Email/OTP Issues:
- Verify Gmail App Password setup
- Check email credentials in `.env`
- Ensure 2FA is enabled on Gmail

### Getting Help:
- Check the browser console for frontend errors
- Check terminal output for backend errors
- Verify all environment variables are set correctly

## 📁 Project Structure

```
mern-ecommerce/
├── backend/
│   ├── controllers/     # Business logic
│   ├── models/         # Database schemas
│   ├── routes/         # API endpoints
│   ├── middleware/     # Custom middleware
│   ├── utils/          # Utility functions
│   ├── seed/           # Database seeding
│   ├── .env.example    # Environment template
│   └── index.js        # Entry point
├── frontend/
│   ├── src/
│   │   ├── components/ # React components
│   │   ├── pages/      # Page components
│   │   ├── features/   # Feature modules
│   │   └── assets/     # Static assets
│   ├── .env.example    # Environment template
│   └── package.json
└── README.md
```

## 🎯 Next Steps

After successful setup:

1. **Explore the application** using the demo account
2. **Create your own account** to test all features
3. **Customize the application** to your needs
4. **Deploy to production** when ready

## 🔐 Production Deployment Checklist

Before deploying to production:

- [ ] Set `PRODUCTION=true` in backend `.env`
- [ ] Use strong, unique passwords for all services
- [ ] Set up proper CORS configuration
- [ ] Enable HTTPS
- [ ] Use environment-specific database
- [ ] Set up proper logging and monitoring
- [ ] Enable rate limiting
- [ ] Review and update security settings

---

## 📞 Support

If you encounter any issues:

1. Check this instructions file
2. Review the main README.md
3. Check the GitHub issues page
4. Create a new issue if needed

Happy coding! 🚀
