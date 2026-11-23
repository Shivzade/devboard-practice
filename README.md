This is the same DevBoard UI as the master branch, but now the data comes from a real backend instead of fake in-memory data.

Three pieces talk to each other:

browser  →  frontend (React)  →  backend (Go API)  →  database (Postgres)
frontend — the React app. It also forwards anything starting with /api to the backend.
backend — a small Go program that reads and writes the database.
database — Postgres, with some example projects and tasks loaded on first start.
There's no login and no AI here on purpose. The whole point is to see how the pieces connect.
