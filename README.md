# 🏙️ FlatQuest

Welcome to **FlatQuest**, a comprehensive real estate platform that connects property seekers with listings. FlatQuest provides an interactive map view, real-time messaging, and detailed property entries, creating a seamless experience for finding  apartments, houses, and more.

---

## 🚀 Features

- **Interactive Maps:** Explore properties visually using an interactive map built with Leaflet.
- **Real-Time Chat:** Communicate with property owners instantly using WebSockets.
- **Robust Authentication:** Secure JWT-based authentication with bcrypt password hashing.
- **Rich Media & Content:** Upload images via Cloudinary (UploadWidget) and compose rich text property descriptions using React Quill.
- **Advanced Filtering:** Search for properties by specific criteria (price, type, location, etc.).
- **Responsive UI:** A beautifully crafted interface built from the ground up using SCSS.

---

## 🛠️ Technologies Used

FlatQuest's architecture is divided into three main components: a Client Frontend, a Core REST API Server, and a dedicated WebSocket Server.

### 💻 Frontend (Client)
| Technology | Role |
|------------|------|
| **React** | Core UI library |
| **Vite** | Build tool and development server |
| **Zustand** | Lightweight state management |
| **React Router v6** | Client-side routing with loaders/actions |
| **SCSS / Sass** | Styling and responsive design |
| **React Leaflet** | Map integration for property locations |
| **Socket.io-client** | Real-time connection to the chat server |
| **Axios** | Handling API requests |
| **React Quill** | Rich text editor for property descriptions |

### ⚙️ Backend (Server)
| Technology | Role |
|------------|------|
| **Node.js & Express** | RESTful API server |
| **Prisma** | Modern Next-Generation ORM |
| **PostgreSQL / MySQL**| Relational database (configured via Prisma) |
| **JWT & bcrypt** | Security, hashing, and authorization via HTTP-only cookies |
| **cookie-parser** | Parsing auth cookies |

### 📡 Real-Time Server (Socket)
| Technology | Role |
|------------|------|
| **Socket.io** | Bi-directional communication for the chat feature |
| **Node.js** | Runtime environment |

---

## 🧠 Key Concepts & Architecture

1. **Microservice-ish Architecture**: The backend logic is decoupled into a core REST API for CRUD operations (Authentication, Posts, Users) and a dedicated WebSocket server specifically handling real-time chat messages and notifications.
2. **State Management**: Instead of prop drilling, `Zustand` provides elegant global state management alongside the React Context API (`AuthContext`, `SocketContext`). 
3. **Data Fetching with Loaders**: Utilizing React Router v6's `loader` functions to pre-fetch data before navigating to specific routes (e.g., fetching a post before the listing page loads).
4. **Security**: Sensitive routes are protected by robust JWT verification middleware (`verifyToken.js`) that checks HttpOnly cookies, mitigating XSS risks.

---

## 🌐 Deployment Configuration

The application is deployed to cloud platforms for optimal performance and reliability:

- **Frontend:** Hosted on **Vercel** (`vercel.json` provides the required configurations for single-page app routing).
- **Core API Server:** Deployed as a web service on **Render**.
- **WebSocket Server:** Deployed as a web service on **Render**.

---

## 🏃‍♂️ Getting Started (Local Setup)

To run FlatQuest locally, follow these steps.

### Prerequisites
- Node.js (v18+ recommended)
- A relational database (PostgreSQL, MySQL, or MongoDB, depending on your Prisma configuration)

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd flatquest
```

### 2. Setup the API Server (`/server`)
```bash
cd server
npm install
```
- Create a `.env` file in the `server` directory.
- Add your database connection string and JWT secret:
  ```env
  DATABASE_URL="your_database_url_here"
  JWT_SECRET_KEY="your_super_secret_key"
  CLIENT_URL="http://localhost:5173"
  ```
- Push the database schema:
  ```bash
  npx prisma db push
  ```
- Start the server:
  ```bash
  npm run dev # or node index.js depending on scripts
  ```

### 3. Setup the WebSocket Server (`/socket`)
```bash
cd ../socket
npm install
```
- Create a `.env` file (if applicable) and configure origins.
- Start the socket server:
  ```bash
  npm run dev # or node app.js
  ```

### 4. Setup the Frontend (`/client`)
```bash
cd ../client
npm install
```
- Create a `.env` file (or hardcode the development URLs if modifying `lib/apiRequest.js`):
  ```env
  VITE_API_URL="http://localhost:8800/api"
  VITE_SOCKET_URL="http://localhost:4000"
  ```
- Start the development server:
  ```bash
  npm run dev
  ```
- Open [http://localhost:5173](http://localhost:5173) in your browser.
