
# 🧾 Airbnb Clone Backend Requirements

## ✅ Feature 1: User Authentication

### 📌 Functional Description
This feature allows users (Guests, Hosts, Admins) to securely register, log in, and manage their sessions using token-based authentication (JWT).

---

### 🔗 API Endpoints

#### 1. `POST /api/v1/auth/register`
- **Description:** Register a new user
- **Request Body (JSON):**
  ```json
  {
    "first_name": "Jane",
    "last_name": "Doe",
    "email": "jane@example.com",
    "password": "SecurePass123",
    "role": "guest"
  }
````

* **Validations:**

  * `email` must be unique and valid format
  * `password` must be at least 8 characters
  * `role` must be one of `guest`, `host`
* **Success Response (201):**

  ```json
  {
    "message": "User registered successfully",
    "token": "<JWT_TOKEN>"
  }
  ```
* **Error Response (400/409):**

  ```json
  { "error": "Email already exists" }
  ```

---

#### 2. `POST /api/v1/auth/login`

* **Description:** Authenticate user and return access token
* **Request Body:**

  ```json
  {
    "email": "jane@example.com",
    "password": "SecurePass123"
  }
  ```
* **Validations:**

  * Must match stored email/password
* **Success Response (200):**

  ```json
  {
    "message": "Login successful",
    "token": "<JWT_TOKEN>"
  }
  ```
* **Error Response (401):**

  ```json
  { "error": "Invalid credentials" }
  ```

---

#### 3. `GET /api/v1/auth/me`

* **Description:** Fetch current authenticated user's profile
* **Headers:**

  * `Authorization: Bearer <JWT_TOKEN>`
* **Response (200):**

  ```json
  {
    "user_id": "uuid",
    "first_name": "Jane",
    "last_name": "Doe",
    "email": "jane@example.com",
    "role": "guest",
    "created_at": "2025-07-09T14:55:32Z"
  }
  ```

---

### 🧪 Validation Rules

* Email must follow standard email format.
* Password must be hashed using bcrypt or similar before storage.
* Role must be either `guest` or `host`.
* Duplicate accounts by email are not allowed.

---

### 🚀 Performance Criteria

* Response time for authentication endpoints should be **<200ms** under normal load.
* Registration and login must scale to handle **100+ concurrent requests/sec**.
* Token expiry and refresh logic should be implemented for session security.

---

More features to be added:

* [ ] Property Management
* [ ] Booking System
* [ ] Payments
* [ ] Reviews

````

