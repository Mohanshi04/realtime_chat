# Real-Time Chat Application

This is a simple real-time chat application built using FastAPI, WebSockets, Redis Pub/Sub, and Docker. It allows multiple clients to connect to a chat room and exchange messages in real-time.

## Features

- WebSocket-based chat using FastAPI
- Redis Pub/Sub for broadcasting messages between clients
- Scalable architecture with decoupled message handling
- Dockerized for easy development and deployment
- Basic test suite using pytest

---

## Project Structure

```
realtime_chat/
├── app/
│   ├── main.py             # FastAPI app with WebSocket endpoint
│   ├── chat_manager.py     # Manages client connections and broadcasting
│   ├── models.py           # SQLAlchemy models or data schemas
│   ├── redis_pubsub.py     # Redis Pub/Sub interface
│   └── database.py         # Redis connection setup
├── tests/
│   └── test_chat.py        # Sample test for chat manager
├── Dockerfile              # Docker image for FastAPI app
├── docker-compose.yml      # Docker Compose setup for app + Redis
└── requirements.txt        # Python dependencies
```

---

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/Mohanshi04/realtime_chat.git
cd realtime_chat
```

### 2. Start the Application using Docker Compose

```bash
docker-compose up --build
```

This command starts two services:
- `app`: The FastAPI server
- `redis`: Redis instance for Pub/Sub

FastAPI will be accessible at: `http://localhost:8000`

### 3. WebSocket Endpoint

You can connect to a WebSocket room at:

```
ws://localhost:8000/ws/{room}
```

Replace `{room}` with any room name you wish to join.

Example using JavaScript WebSocket client:

```javascript
const socket = new WebSocket("ws://localhost:8000/ws/general");
socket.onmessage = (event) => {
    console.log("Received:", event.data);
};
socket.send("Hello from client!");
```

---

## Running Tests

To run the test suite using `pytest`, use the following command:

```bash
docker-compose exec app pytest tests/test_chat.py
```

Make sure Docker Compose is running before executing this.

---

## Tech Stack

- Python 3.11
- FastAPI
- WebSockets
- Redis (via `aioredis`)
- Docker
- Pytest

---

## Notes

- Redis is used as a central Pub/Sub broker to broadcast messages between clients.
- FastAPI handles WebSocket connections and routes incoming messages to Redis.
- When a message is received from Redis, it is pushed to all subscribed WebSocket clients in that room.

---
