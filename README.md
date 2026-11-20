Installation and configuration
1. Open this project folder in Visual Studio Code.
2. Open Terminal → New Terminal.
3. Install dependencies:
   npm install
4. Copy .env.example to a new file named .env.
5. Set the environment variables in .env:
   PORT=3000
   MONGO_URI=mongodb_connection_string
   JWT_SECRET=replace_with_a_long_random_secret
   Replace MONGO_URI with your actual MongoDB connection string. Use
   a strong, private value for JWT_SECRET.
6. Do not upload .env to GitHub. The .gitignore file should exclude
   it.
Both practicals use port 3000 and connect to the MongoDB database
specified by MONGO_URI. Run one practical at a time.
Practical A1 --- Library Book Management API
File: file/A1.js
Technology: Node.js, Express, MongoDB and Mongoose

Start the API:
npm run start:a1
The server starts on http://localhost:3000 after a successful MongoDB
connection.
API endpoints
  Method   Endpoint       Description
  POST     /books       Create a book
GET      /books       List all books
GET      /books/:id   Get a book by its MongoDB ID
PUT      /books/:id   Update a book
DELETE   /books/:id   Delete a book
Example request body --- create a book
Send this JSON body to POST http://localhost:3000/books:
{
  "title": "The Alchemist",
  "author": "Paulo Coelho",
  "price": 250,
  "category": "Fiction",
  "isAvailable": true
}
The API uses 201 for successful creation, 200 for successful
requests, 400 for invalid input or ID, 404 when a book is not found,
and 500 for an unexpected server error. The request logger prints the
HTTP method and URL in the terminal.
Practical A2 --- Student Portal with Login and Protected Routes
File: file/A2.js
Technology: Node.js, Express, MongoDB/Mongoose, Joi, bcrypt, JSON
Web Token, Helmet, CORS and express-rate-limit

Stop A1 with Ctrl + C before starting A2. Then run:
npm run start:a2
The server starts on http://localhost:3000 after a successful MongoDB
connection and environment configuration.
API endpoints
  Method            Endpoint          Access            Description
  POST              /register       Public            Register a
student or admin

  POST              /login          Public            Verify
credentials and
return a JWT

  GET               /profile        Authenticated     Return the
logged-in user's
details without
the password
GET               /students       Admin only        Return the list
of students
without passwords
Example student registration
Send this JSON body to POST http://localhost:3000/register:
{
  "name": "Kanishk Balwani",
  "email": "kanishk@example.com",
  "password": "secret123",
  "role": "student"
}
Example admin registration for practical testing
Use a different email address:
{
  "name": "Admin User",
  "email": "admin@example.com",
  "password": "admin123",
  "role": "admin"
}
The supplied practical explicitly accepts student or admin as the
registration role. In a real production application, public users should
not be allowed to grant themselves an admin role; admin accounts should
be provisioned securely.
Example login
Send the registered email and password to
POST http://localhost:3000/login:
{
  "email": "kanishk@example.com",
  "password": "secret123"
}
The response contains a JWT that expires after one hour. Copy the token
for protected requests.
Testing protected routes in Postman
For GET /profile and GET /students:
1. Open the Authorization tab.
2. Select Bearer Token.
3. Paste the token returned by login.
4. Click Send.
Expected access behavior:

  Test                                                 Expected result
  GET /profile without a token                       401 Unauthorized
GET /profile with a valid student or admin token   200 OK
GET /students with a student token                 403 Forbidden
GET /students with an admin token                  200 OK

Registration validates input using Joi, hashes passwords with bcrypt,
and rejects duplicate email addresses. The application uses Helmet, CORS
and a rate limit of 100 requests per 15 minutes.
Output screenshots
After running and testing the APIs, save clear screenshots in the
outputs/ folder using the required filenames:
- A1.png --- A1 book API tests and MongoDB Compass showing the
  book data.
- A2.png --- A2 registration and login, /profile without and
  with a token, and /students tested as both student and admin.
- A3.png --- only if a third practical is assigned by the
  instructor.
Use genuine screenshots of your own running application and API
responses. Demonstration/mock images are not proof that the APIs were
executed successfully.
Available npm commands
npm install
npm run start:a1
npm run start:a2
npm run start:a3
