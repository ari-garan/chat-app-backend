
# Realtime Chat App 💬

A **real-time one-to-one chat application** built with **Node.js, TypeScript, Express, MongoDB, and Socket.IO**.  
Supports **online/offline status**, **typing indicators**, **read receipts**, and secure JWT-based authentication.

---

## **Tech Stack**

- **Backend**: Node.js + TypeScript + Express  
- **Database**: MongoDB (Mongoose)  
- **Realtime Engine**: Socket.IO  
- **Authentication**: JWT (JSON Web Token)  

---

## **Features**

- User registration & login with JWT  
- One-to-one real-time messaging  
- Typing indicators & read receipts  
- Online/offline user tracking  
- Admin and user analytics  

---

## **Folder Structure**

```
realtime-chat-app/
│
├── node_modules/
│
├── src/
│   ├── common/
│   │   ├── constants.ts
│   │   ├── helpers.ts
│   │   └── interfaces.ts
│   │
│   ├── connections/
│   │   └── connectDB.ts
│   │
│   ├── controllers/
│   │   ├── analytics.controller.ts
│   │   ├── auth.controller.ts
│   │   └── chat.controller.ts
│   │
│   ├── middlewares/
│   │   ├── admin.middleware.ts
│   │   └── auth.middleware.ts
│   │
│   ├── models/
│   │   ├── message.model.ts
│   │   └── user.model.ts
│   │
│   ├── routes/
│   │   └── routes.ts
│   │
│   ├── services/
│   │   ├── analytics.service.ts
│   │   ├── auth.service.ts
│   │   └── chat.service.ts
│   │
│   ├── sockets/
│   │   └── chatSocket.ts
│   │
│   └── validators/
│       └── validator.ts
│
├── .env
├── chatClient.ts          <-- ✅ Local CLI chat test client
├── index.ts               <-- ✅ Main server entry (rename from server.ts if needed)
├── package.json
├── package-lock.json
└── tsconfig.json
└── README.md
```

---

## **Installation**

```bash
# Clone the repository
git clone https://github.com/yourusername/realtime-chat-app.git
cd realtime-chat-app

# Install dependencies
npm install

# Start MongoDB locally

# Start the server
npm run start

# Start the client
npm run client
```

> `npm run dev` uses **ts-node-dev** to run TypeScript in development mode.

---

## **Environment Variables**

Create a `.env` file in the root:

```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/chat-app
JWT_SECRET=yourStrongSecretKey
```

---

## **API Endpoints**

| Method | Endpoint                         | Description                      | Role  |
|--------|---------------------------------|----------------------------------|-------|
| POST   | /api/auth/register               | Register a new user              | Public|
| POST   | /api/auth/login                  | Login and get JWT                | Public|
| GET    | /api/chat/history/:userId        | Get chat history with a user     | Auth  |
| POST   | /api/chat/send                   | Send a message                   | Auth  |
| GET    | /api/analytics/user              | Get logged-in user analytics     | User  |
| GET    | /api/analytics/admin             | Get system-wide analytics        | Admin |

> Replace `:userId` in `/api/chat/history/:userId` with the ID of the user you want to fetch chat history for.

---

## **Socket.IO Events**

### Client → Server

| Event          | Payload                                           |
|----------------|-------------------------------------------------|
| `send_message` | `{ senderId, receiverId, message }`            |
| `user_online`  | `{ userId }`                                   |
| `typing`       | `{ senderId, receiverId }`                     |
| `message_read` | `{ messageId, readerId, senderId }`           |

### Server → Client

| Event             | Payload                                           |
|------------------|-------------------------------------------------|
| `receive_message` | `{ senderId, receiverId, message, _id }`       |
| `update_online_users` | `[userId, ...]`                             |
| `typing`          | `{ senderId }`                                 |
| `message_read`    | `{ messageId, readerId, senderId }`           |
