# Lab 2 - Token Authentication with JWT
This repository is part of LAB 6 - Security in NodeJS. It demonstrates Token-Based Authentication using JWT (JSON Web Token) with MongoDB.
## How to Run
### Install Dependencies
Run the following in the project directory:
npm install
### Start Server
Run the server using:
node app.js
The server will start at http://localhost:3000.
## Routes
### Auth Routes (/api/auth)
Available routes are:
- POST /api/auth/register → register a new user  
  Body JSON:
  {
    "username": "user1",
    "email": "user1@example.com",
    "password": "123456"
  }
- POST /api/auth/login → login with email and password, returns JWT token  
  Body JSON:
  {
    "email": "user1@example.com",
    "password": "123456"
  }
- GET /api/auth/profile → protected route, requires valid JWT token in header  
  Header:
  Authorization: Bearer <JWT_TOKEN>
- POST /api/auth/logout → logout, simply returns a success message (JWT is stateless)  
  Header:
  Authorization: Bearer <JWT_TOKEN>
## Testing with Postman
### Import Postman Collection
You can import the ready-to-use Postman collection JSON provided in this repo: Open Postman → Import → File → select TokenAuth.postman_collection.json. The collection includes requests for register, login, profile (protected), and logout (protected). The Login request will return a JWT token which you can save as an Environment Variable in Postman: Key: authToken, Value: <JWT_TOKEN from login response>. For Profile and Logout, the header uses Authorization: Bearer {{authToken}} so it automatically uses the saved token.
### Manual Testing (Optional)
#### Register
POST http://localhost:3000/api/auth/register Body (raw JSON):
{
  "username": "user1",
  "email": "user1@example.com",
  "password": "123456"
}
#### Login
POST http://localhost:3000/api/auth/login Body (raw JSON):
{
  "email": "user1@example.com",
  "password": "123456"
}
#### Profile
GET http://localhost:3000/api/auth/profile Header:
Authorization: Bearer <JWT_TOKEN>
#### Logout
POST http://localhost:3000/api/auth/logout Header:
Authorization: Bearer <JWT_TOKEN>
## Notes
JWT is stateless, so logout does not invalidate the token on the server side. Client should remove the token after logout. Ensure MongoDB is running locally at mongodb://127.0.0.1:27017/tokenAuthApp. Passwords are hashed with bcrypt before storing in the database.
