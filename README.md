# QVerse — Real-Time Messaging Platform
[![React](https://img.shields.io/badge/React-19-blue?style=for-the-badge)]()
[![Node.js](https://img.shields.io/badge/Node.js-Express-green?style=for-the-badge)]()
[![Socket.IO](https://img.shields.io/badge/Socket.IO-Real_Time-black?style=for-the-badge)]()
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-green?style=for-the-badge)]()

QVerse is a modern **full-stack real-time messaging platform** built using the **MERN stack**. It enables users to communicate instantly through a responsive chat interface powered by **Socket.IO**, while providing secure authentication, live online presence, profile management, and persistent message storage using **MongoDB Atlas**.

The project demonstrates the architecture behind production-grade messaging applications by combining **REST APIs**, **WebSockets**, **JWT authentication**, and cloud-based media storage into a single scalable application.

---

# Table of Contents

1. [Project Overview](#project-overview)
2. [Key Features](#key-features)
3. [System Architecture](#system-architecture)
4. [Project Structure](#project-structure)
5. [Quick Start](#quick-start)
6. [Project Walkthrough](#project-walkthrough)
7. [Authentication Flow](#authentication-flow)
8. [Real-Time Messaging](#real-time-messaging)
9. [REST API](#rest-api)

---

# Project Overview

Modern messaging platforms rely on much more than simply storing chat messages. They require secure authentication, persistent databases, bidirectional communication, online user tracking, media management, and responsive user interfaces.

QVerse was built to explore how these systems work together by implementing a complete full-stack chat application using the MERN stack.

The application combines:

- React for the frontend
- Express.js REST APIs
- MongoDB Atlas for persistent storage
- Socket.IO for real-time communication
- JWT authentication
- Cloudinary image hosting
- Vercel deployment

Unlike traditional chat applications that require refreshing the page to receive new data, QVerse uses WebSockets to instantly synchronize messages and online user status across connected clients.

---

# Key Features

| Feature | Description |
|---|---|
| **Real-Time Messaging** | Instant message delivery using Socket.IO without refreshing the page |
| **JWT Authentication** | Secure login and signup using JSON Web Tokens |
| **Password Encryption** | User passwords securely hashed with bcrypt |
| **Profile Management** | Update profile picture, display name, and bio |
| **Cloudinary Integration** | Store profile images in the cloud |
| **Online Presence** | Track currently connected users in real time |
| **Responsive UI** | Desktop and mobile-friendly interface built with Tailwind CSS |
| **Persistent Chat Storage** | Messages and user profiles stored in MongoDB Atlas |
| **RESTful Backend** | Express.js API for authentication, users, and messaging |
| **Production Deployment** | Frontend deployed on Vercel with cloud backend services |

---

# System Architecture

```
                Browser
                   │
                   ▼
           React + Tailwind CSS
                   │
        Axios REST Requests
                   │
                   ▼
           Express.js Backend
          JWT Authentication
                   │
       ┌───────────┴───────────┐
       │                       │
       ▼                       ▼
 MongoDB Atlas          Socket.IO Server
       │                       │
       └───────────┬───────────┘
                   │
                   ▼
          Real-Time Communication
```

---

# Project Structure

```
QVerse/
│
├── client/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   ├── context/
│   │   ├── pages/
│   │   ├── App.jsx
│   │   └── main.jsx
│   │
│   └── package.json
│
├── server/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── lib/
│   ├── server.js
│   └── package.json
│
└── README.md
```

---

# Quick Start

## Prerequisites

- Node.js
- MongoDB Atlas
- Cloudinary Account
- Git

---

## Installation

```bash
git clone https://github.com/saoirseros/QVerse.git

cd QVerse
```

---

## Install Dependencies

### Client

```bash
cd client

npm install
```

### Server

```bash
cd ../server

npm install
```

---

## Configure Environment Variables

### Client (.env)

```env
VITE_BACKEND_URL=http://localhost:5000
```

### Server (.env)

```env
PORT=5000

MONGODB_URI=YOUR_MONGODB_URI

JWT_SECRET=YOUR_SECRET_KEY

CLOUDINARY_CLOUD_NAME=YOUR_CLOUD_NAME

CLOUDINARY_API_KEY=YOUR_API_KEY

CLOUDINARY_API_SECRET=YOUR_API_SECRET
```

---

## Run the Application

### Backend

```bash
cd server

nodemon server.js
```

### Frontend

```bash
cd client

npm run dev
```

---

# Project Walkthrough

## User Authentication

Users can securely create accounts and log into the application.

The authentication system includes:

- JWT-based authentication
- Password hashing with bcrypt
- Protected routes
- Persistent login sessions
- Secure API communication

---

## Real-Time Messaging

QVerse enables live communication between users using Socket.IO.

Every connected user establishes a persistent WebSocket connection with the server.

```
User A
   │
   ▼
Socket.IO
   │
   ▼
Express Server
   │
   ▼
MongoDB
   │
   ▼
Socket.IO
   │
   ▼
User B
```

Messages are delivered instantly without requiring page refreshes.

---

## Online User Tracking

Whenever users connect or disconnect, Socket.IO broadcasts the updated online user list.

The application maintains:

- Connected users
- Live online indicators
- Automatic updates on disconnect

---

## Profile Management

Users can personalize their accounts by:

- Uploading profile pictures
- Editing display names
- Updating personal bios

Profile images are uploaded to Cloudinary while user information is stored in MongoDB Atlas.

---

## Database

MongoDB Atlas stores:

- User accounts
- Password hashes
- Profile information
- Chat messages
- Message metadata

---

# Authentication Flow

```
Signup/Login
      │
      ▼
Express API
      │
      ▼
Validate Credentials
      │
      ▼
Generate JWT
      │
      ▼
Client Stores Token
      │
      ▼
Authenticated Requests
```

Protected routes verify the JWT before granting access to user-specific resources.

---

# Real-Time Messaging

Socket.IO establishes a persistent connection between the client and server.

Whenever a message is sent:

```
Sender
   │
   ▼
Socket.IO Client
   │
   ▼
Express + Socket.IO Server
   │
   ▼
Store Message in MongoDB
   │
   ▼
Emit Message Event
   │
   ▼
Receiver
```

This enables instant synchronization of conversations without polling or refreshing.

---

# REST API

## Authentication

| Method | Endpoint | Description |
| :----: | :------- | :---------- |
| `POST` | `/api/auth/signup` | Register a new user |
| `POST` | `/api/auth/login` | Authenticate existing user |
| `GET` | `/api/auth/check` | Verify authentication token |
| `PUT` | `/api/auth/update-profile` | Update profile information |

## Messages

| Method | Endpoint | Description |
| :----: | :------- | :---------- |
| `GET` | `/api/messages/users` | Retrieve sidebar users |
| `GET` | `/api/messages/:id` | Retrieve conversation with a user |
| `POST` | `/api/messages/send/:id` | Send a new message |
| `PUT` | `/api/messages/mark/:id` | Mark message as seen |

## Server Status

| Method | Endpoint | Description |
| :----: | :------- | :---------- |
| `GET` | `/api/status` | Verify backend status |

---

# Tech Stack

### Frontend

- React
- React Router
- Tailwind CSS
- Axios
- React Hot Toast

### Backend

- Node.js
- Express.js
- Socket.IO
- JWT
- bcryptjs

### Database

- MongoDB Atlas
- Mongoose

### Cloud Services

- Cloudinary
- Vercel

---

# Future Improvements

- Typing indicators
- Read receipts
- Image and file sharing
- Voice messages
- Group chats
- Push notifications
- Message reactions
- Emoji picker
- Search conversations
- Message editing and deletion
- End-to-end encryption

---

# License

This project is intended for educational purposes and portfolio demonstration.
