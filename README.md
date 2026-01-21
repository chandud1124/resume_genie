# Resume Genie

An AI-powered resume builder that helps users craft, save, and export professional resumes. Built as a mini academic project (3rd semester) by two contributors.

## Overview
- AI assistance via Google Generative AI (Gemini) to generate resume sections from prompts.
- User authentication using JWT with protected routes and cookies.
- Create, list, and delete saved resumes in MongoDB.
- Modern React frontend with Vite and Tailwind CSS.

## Tech Stack
- Backend: Node.js, Express, Mongoose, MongoDB, JSON Web Tokens
- AI: Google Generative AI (gemini-1.5-flash)
- Frontend: React, Vite, Tailwind CSS

## Repository Structure
- Backend API: [Backend/](Backend)
- Frontend app: [Frontend/](Frontend)

## Prerequisites
- Node.js 18+ and npm
- A MongoDB connection string
- Google Generative AI API key

## Environment Variables
Create a `.env` file in each side as shown.

Backend [.env] (in [Backend/](Backend))
- `PORT` — server port (e.g., 8000)
- `DB_CONNECT` — MongoDB connection URI
- `JWT_KEY` — JWT signing secret
- `GOOGLE_AI_API_KEY` — Google Generative AI API key

Frontend [.env] (in [Frontend/](Frontend))
- `VITE_BASE_URL` — Backend base URL (e.g., http://localhost:8000)

## Setup & Run

Clone the repository:

```bash
git clone https://github.com/Shoaib232002/Resume-Genie.git
cd Resume-Genie
```

Install and run the Backend:

```bash
cd Backend
npm install
echo "PORT=8000" >> .env
echo "DB_CONNECT=YOUR_MONGODB_URI" >> .env
echo "JWT_KEY=YOUR_JWT_SECRET" >> .env
echo "GOOGLE_AI_API_KEY=YOUR_GOOGLE_KEY" >> .env
node server.js
```

Install and run the Frontend (Vite dev server):

```bash
cd Frontend
npm install
echo 'VITE_BASE_URL="http://localhost:8000"' >> .env
npm run dev
```

By default, the backend CORS is configured for `http://localhost:5173` (Vite). Adjust origin in [Backend/app.js](Backend/app.js#L14-L23) if needed.

## API Reference

Base URL: `http://localhost:<PORT>`

Users
- POST `/users/register` — Register user (expects `fullname`, `email`, `password`).
- POST `/users/login` — Login and receive JWT cookie/token.
- GET `/users/profile` — Get user details and all resumes (requires auth).
- POST `/users/create/resume` — Create a resume (requires auth).
- DELETE `/users/:resumeId` — Delete a resume by id (requires auth).
- GET `/users/logout` — Clear auth cookie and logout.

AI
- GET `/ai/get-result?prompt=...` — Get AI-generated text for the provided prompt.

## Frontend Integration
The frontend calls the backend using `import.meta.env.VITE_BASE_URL`. Ensure cookies are enabled for requests that need authentication.

## Development Notes
- CORS is restricted to `http://localhost:5173` in development. Update `origin` in [Backend/app.js](Backend/app.js#L16) for other hosts.
- JWT verification uses `process.env.JWT_KEY` as seen in [Backend/middleware/isLoggedIn.js](Backend/middleware/isLoggedIn.js#L9).
- MongoDB connection reads `process.env.DB_CONNECT` via [Backend/config/mongoose.connection.js](Backend/config/mongoose.connection.js#L4).
- Gemini API key is loaded from `process.env.GOOGLE_AI_API_KEY` in [Backend/services/ai.service.js](Backend/services/ai.service.js#L3).

## License
This project is licensed under the MIT License — see [LICENSE](LICENSE).

