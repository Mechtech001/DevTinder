# DevTinder

A developer networking backend that helps developers discover profiles, express interest, manage connections, and communicate in real time.

## Features

- User registration, login, and logout
- Profile viewing and editing
- Developer feed with pagination
- Connection requests with interested, ignored, accepted, and rejected states
- Connection and received-request management
- Real-time messaging using Socket.IO
- Premium membership and payment integration with Razorpay
- MongoDB persistence using Mongoose

## Tech Stack

- Node.js
- Express.js
- MongoDB and Mongoose
- JSON Web Tokens (JWT) and bcrypt
- Socket.IO
- Razorpay
- dotenv

## Prerequisites

- Node.js and npm
- A MongoDB database
- Razorpay API credentials if you intend to test payment functionality

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/Mechtech001/DevTinder.git
cd DevTinder
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env` file in the project root:

```env
PORT=7777
DB_CONNECTION_SECRET=your_mongodb_connection_string
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
RAZORPAY_WEBHOOK_SECRET=your_razorpay_webhook_secret
```

Use your own credentials. Never commit your real secrets or the `.env` file.

**Security note:** Before production use, move the JWT signing secret into environment configuration and remove any logging of database connection credentials.

### 4. Start the server

```bash
npm start
```

The backend uses the configured `PORT` and requires a working MongoDB connection before it starts listening.

The current CORS configuration allows `http://localhost:5173`. Update it if your frontend runs on a different origin.

## API Reference

The server exposes these routes:

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/signup` | Register a user |
| POST | `/login` | Authenticate a user |
| POST | `/logout` | Log out |
| GET | `/profile/view` | View the authenticated profile |
| PATCH | `/profile/edit` | Update the profile |
| POST | `/request/send/:status/:toUserId` | Send a connection request |
| POST | `/request/review/:status/:requestId` | Accept or reject a request |
| GET | `/user/requests/received` | List received requests |
| GET | `/user/connections` | List accepted connections |
| GET | `/feed` | Retrieve developer profiles |
| GET | `/chat/:targetUserId` | Retrieve or create a conversation |
| POST | `/payment/create` | Create a premium payment order |
| POST | `/payment/webhook` | Process a Razorpay webhook |
| GET | `/premium/verify` | Check premium membership |

Most profile, connection, chat, and payment endpoints require authentication. The payment webhook uses signature verification.

See [apiList.md](apiList.md) for the existing API notes.

## Real-Time Messaging

The Socket.IO server supports the `joinChat` and `sendMessage` client events and emits `messageReceived` to the conversation room.

## Development

The project is under active development. Review the source code and configure credentials before exposing the server publicly.

## License

See the repository for license information.
