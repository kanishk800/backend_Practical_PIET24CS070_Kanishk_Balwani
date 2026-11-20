# Backend Practical Exam Submission

> Rename the two folders to include your registration number and name, as required by the submission guideline.

## Included practicals
- **A1.js — Task 1:** Library Book Management API (Express + MongoDB/Mongoose).
- **A2.js — Task 2:** Student Portal API with registration, login, JWT authentication, protected routes, Joi validation, bcrypt password hashing, Helmet, CORS and rate limiting.
- **A3.js:** Placeholder only. A third practical question was not present in the supplied task documents. Replace it if your instructor assigned an A3.

## Setup
1. Install Node.js and start MongoDB locally, or obtain a MongoDB connection string.
2. Open a terminal in this project folder and run:
   ```bash
   npm install
   ```
3. Copy `.env.example` to `.env` and set `MONGO_URI` and a strong `JWT_SECRET`.
4. Run one practical at a time:
   ```bash
   npm run start:a1
   # or
   npm run start:a2
   ```
   Both examples use port 3000, so stop one before starting the other.

## A1 endpoints
| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/books` | Add a book |
| GET | `/books` | List all books |
| GET | `/books/:id` | Get one book |
| PUT | `/books/:id` | Update a book |
| DELETE | `/books/:id` | Delete a book |

Example POST body:
```json
{"title":"The Alchemist","author":"Paulo Coelho","price":250,"category":"Fiction","isAvailable":true}
```

## A2 endpoints
| Method | Endpoint | Access |
|---|---|---|
| POST | `/register` | Public |
| POST | `/login` | Public |
| GET | `/profile` | Logged-in user; send `Authorization: Bearer <token>` |
| GET | `/students` | Admin only; send `Authorization: Bearer <token>` |

Example register body:
```json
{"name":"Demo Student","email":"student@example.com","password":"secret123","role":"student"}
```
For an admin test account, use `"role":"admin"` in the registration body, as specified in the practical task. In a real production system, public registration should not allow users to assign themselves the admin role.

## Output screenshots
Save genuine Postman/Thunder Client and MongoDB Compass screenshots in `outputs/` with these exact names:
- `A1.png` — A1 endpoint tests and MongoDB Compass data.
- `A2.png` — A2 registration/login, `/profile` with and without token, and `/students` as admin and student.
- `A3.png` — only if a third practical is assigned.

The `outputs/` folder is initially empty; screenshots must be captured after running and testing the APIs. Do not submit placeholder images as test evidence.

## GitHub submission
Create a **Public** GitHub repository, upload this project folder (including `file/`, `outputs/`, and `README.md`), commit, and submit the repository URL using your instructor's Google Form.
