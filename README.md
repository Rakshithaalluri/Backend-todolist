# Todo List Application

This is a full-stack **Todo List Application** built using **Node.js** and **SQLite**. The backend handles user authentication and allows users to create, retrieve, update, and delete to-do items.

## Features

- **User Registration**: Users can sign up for an account.
- **User Login**: Users can log in using their credentials, and a JWT token is generated for authorization.
- **CRUD Operations on Todos**: 
  - Users can add, retrieve, update, and delete their to-do items.
  - Users can also update the status of a to-do item (e.g., from "incomplete" to "complete").
- **Login Activity**: Tracks and stores login times for users.
- **Protected Routes**: Some routes are protected by JWT-based authentication.

## Tech Stack

- **Node.js** with **Express**: Backend framework.
- **SQLite**: Database to store user data and todo items.
- **JWT**: For user authentication and session management.
- **bcrypt.js**: To hash passwords securely.
- **dotenv**: For environment variable management.
- **CORS**: To allow cross-origin requests.

## Installation and Setup

### Prerequisites
- **Node.js** installed on your machine.
- **SQLite** installed for managing the database.

### Steps

1. Clone the repository:
    ```bash
    git clone <repository-url>
    cd todo-backend
    ```

2. Install dependencies:
    ```bash
    npm install
    ```

3. Set up your environment variables:
    - Create a `.env` file in the root directory.
    - Add the following line to your `.env` file:
      ```
      JWT_SECRET=your_jwt_secret_key
      ```

4. Initialize and run the server:
    ```bash
    node server.js
    ```
    The server will start on `http://localhost:3000`.

## API Endpoints

### User Authentication

- **POST** `/register` – Register a new user:
  - Request Body: 
    ```json
    {
      "username": "your_username",
      "password": "your_password"
    }
    ```
  - Response:
    - `201`: User created successfully.
    - `400`: User already exists.

- **POST** `/login` – User login:
  - Request Body:
    ```json
    {
      "username": "your_username",
      "password": "your_password"
    }
    ```
  - Response: 
    - `200`: JSON Web Token (JWT) for authentication.
    - `400`: Invalid credentials.

### To-Do Operations

- **POST** `/todos` – Create a new to-do item (requires JWT token):
  - Request Body:
    ```json
    {
      "description": "Task description",
      "status": "Task status"
    }
    ```
  - Response:
    - `201`: New to-do item created.

- **GET** `/todos` – Retrieve all to-do items for the authenticated user (requires JWT token):
  - Response: List of to-do items for the authenticated user.

- **GET** `/todos/:id` – Get a specific to-do item by ID (requires JWT token):
  - Response: A specific to-do item.

- **PUT** `/todos/:id` – Update a to-do item by ID (requires JWT token):
  - Request Body:
    ```json
    {
      "description": "Updated task description",
      "status": "Updated task status"
    }
    ```
  - Response: `200` if successful, or `404` if not found.

- **PATCH** `/todos/:id` – Update only the status of a to-do item by ID (requires JWT token):
  - Request Body:
    ```json
    {
      "status": "New status"
    }
    ```
  - Response: `200` if successful, or `404` if not found.

- **DELETE** `/todos/:id` – Delete a to-do item by ID (requires JWT token):
  - Response: `200` if successful, or `404` if not found.

### Protected Routes

- **GET** – Example of a protected route (requires JWT token):
  - Response: `"This is a protected route"`.

## How to Use

- After registering and logging in, the user will receive a JWT token.
- The JWT token should be passed in the `Authorization` header as a Bearer token for all protected routes.
- Example:
  Authorization: Bearer <your_jwt_token>
