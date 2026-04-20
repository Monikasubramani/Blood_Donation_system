# Social Welfare Connect - MongoDB Integration

This project now uses MongoDB database to store user data instead of localStorage.

## Features Added

### User Authentication with MongoDB
- **User Registration**: Store user data (name, phone, password, profile photo) in MongoDB
- **User Login**: Authenticate users with phone number and password
- **Password Security**: Passwords are hashed using bcryptjs
- **Profile Management**: Update user profile information
- **Admin Dashboard**: View all registered users

### API Endpoints

#### User Authentication
- `POST /api/register` - Register new user
- `POST /api/login` - User login
- `GET /api/user/:id` - Get user profile
- `PUT /api/user/:id` - Update user profile
- `GET /api/users` - Get all users (admin)

#### Existing Donation Endpoints
- Blood donation/receiver APIs
- Organ donation/receiver APIs
- Money donation/receiver APIs

## Setup Instructions

### 1. Install Dependencies
```bash
npm install
```

### 2. MongoDB Setup
You need to have MongoDB running. You can either:

#### Option A: Local MongoDB
1. Install MongoDB locally
2. Start MongoDB service
3. Create a database named `social_welfare_connect`

#### Option B: MongoDB Atlas (Cloud)
1. Create a free account at [MongoDB Atlas](https://www.mongodb.com/atlas)
2. Create a new cluster
3. Get your connection string

### 3. Environment Configuration
Create a `.env` file in the root directory:

```env
# MongoDB Connection String
MONGO_URI=mongodb://localhost:27017/social_welfare_connect
# OR for MongoDB Atlas:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/social_welfare_connect

# Server Port (optional, defaults to 3000)
PORT=3000
```

### 4. Start the Server
```bash
npm start
```

### 5. Access the Application
- **Home Page**: http://localhost:3000
- **Signup**: http://localhost:3000/signup.html
- **Login**: http://localhost:3000/login.html
- **Profile**: http://localhost:3000/profile.html
- **Admin Dashboard**: http://localhost:3000/admin.html

## User Data Structure

### MongoDB User Schema
```javascript
{
  name: String,           // User's full name
  phone: String,          // 10-digit phone number (unique)
  password: String,       // Hashed password
  profilePhoto: String,   // Base64 encoded image
  createdAt: Date,        // Registration timestamp
  donations: Array        // User's donation history
}
```

## Security Features

- **Password Hashing**: All passwords are hashed using bcryptjs
- **Input Validation**: Server-side validation for all inputs
- **Unique Phone Numbers**: Phone numbers must be unique
- **File Size Limits**: Profile photos limited to 5MB
- **Error Handling**: Comprehensive error handling and user feedback

## Admin Features

The admin dashboard (`/admin.html`) provides:
- **User Statistics**: Total users, active users, new users this month
- **User List**: Complete list of all registered users
- **User Details**: Profile photos, names, phone numbers, join dates
- **Real-time Data**: Refresh button to get latest data

## Testing the System

1. **Register a new user** at `/signup.html`
2. **Login** with the registered credentials at `/login.html`
3. **View profile** and update information at `/profile.html`
4. **Check admin dashboard** at `/admin.html` to see registered users

## Troubleshooting

### Common Issues

1. **MongoDB Connection Error**
   - Ensure MongoDB is running
   - Check your connection string in `.env`
   - Verify network connectivity for cloud MongoDB

2. **Port Already in Use**
   - Change the PORT in `.env` file
   - Or kill the process using the current port

3. **Module Not Found Errors**
   - Run `npm install` to install all dependencies
   - Check if `bcryptjs` is installed

### Database Reset
To reset the database, simply delete the database and restart the server. All data will be cleared.

## API Testing

You can test the APIs using tools like Postman or curl:

```bash
# Register a new user
curl -X POST http://localhost:3000/api/register \
  -H "Content-Type: application/json" \
  -d '{"name":"Test User","phone":"1234567890","password":"test123","profilePhoto":"data:image/png;base64,..."}'

# Login
curl -X POST http://localhost:3000/api/login \
  -H "Content-Type: application/json" \
  -d '{"phone":"1234567890","password":"test123"}'

# Get all users
curl http://localhost:3000/api/users
```
