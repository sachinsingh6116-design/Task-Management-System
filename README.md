# Daymark Task Management

A full-stack task manager with account registration, private task lists, status and priority tracking, due dates, and realtime updates across signed-in sessions.

## Requirements

- Node.js 18 or later and npm
- MongoDB running locally or a MongoDB connection string

## Setup

1. Install dependencies from the project root:

   ```sh
   npm run install:all
   ```

2. Copy `server/.env.example` to `server/.env`, then set `MONGODB_URI` and replace `JWT_SECRET` with a long random value. Keep `.env` private.

3. Start MongoDB, then run both applications from the root:

   ```sh
   npm run dev
   ```

The React app runs at `http://localhost:3000`; the API and Socket.IO server run at `http://localhost:5000`. To run separately, use `npm run dev --prefix server` and `npm start --prefix client`.

## API

- `POST /api/auth/register` and `POST /api/auth/login` return a JWT and user profile.
- `GET /api/auth/me` returns the signed-in profile.
- `GET/POST /api/tasks` list and create the current user's tasks.
- `PATCH/DELETE /api/tasks/:id` update or remove a task owned by the current user.
- `GET /api/health` reports API health.

Pass protected requests a `Bearer` token in the `Authorization` header. Task create, update, and delete events are emitted to the authenticated user's Socket.IO room.

Set `CLIENT_URL` in `server/.env` when the client uses a different origin. For a non-default API host, set `REACT_APP_API_URL` and `REACT_APP_SOCKET_URL` in the client environment.