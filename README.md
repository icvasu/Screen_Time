# Screen Time Tracking Backend

This project provides a real-time screen time tracking backend using [ActivityWatch](https://activitywatch.net/) and FastAPI with WebSocket streaming.

## 🚀 Features

- **Tracks active applications and window titles**
- **Detects AFK (away-from-keyboard) status**
- **Streams data in real-time via WebSockets**
- **REST API and WebSocket endpoints for integration**
- **Easy integration with custom frontends or analytics**

## 🏗️ Architecture

```
[ActivityWatch] → [FastAPI WebSocket Server] → [Your Clients/Analytics]
```

- **ActivityWatch** collects raw activity data (apps, windows, AFK).
- **FastAPI backend** polls ActivityWatch and streams data to clients via WebSockets.

## ⚡ Quickstart

### 1. **Install Dependencies**

```sh
pip install fastapi uvicorn websockets requests
```

### 2. **Start ActivityWatch**

Install and run ActivityWatch from [activitywatch.net](https://activitywatch.net/).

### 3. **Run the Backend**

```sh
cd path/to/your/project
python -m aw_qt.main
```

### 4. **Connect a WebSocket Client**

Example in Python:
```python
import asyncio
import websockets
import json

async def main():
    uri = "ws://localhost:8000/websocket/ws/activity"
    async with websockets.connect(uri) as ws:
        await ws.send(json.dumps({"type": "request_data"}))
        async for msg in ws:
            print(msg)

asyncio.run(main())
```

## 🔌 Endpoints

- **WebSocket (activity):** `ws://localhost:8000/websocket/ws/activity`
- **WebSocket (status):** `ws://localhost:8000/websocket/ws/status`
- **HTTP (connections):** `http://localhost:8000/websocket/ws/connections`

## 📊 Data Example

```json
{
  "current_app": "chrome.exe",
  "window_title": "Google - Chrome",
  "is_afk": false,
  "timestamp": "2025-01-20T10:30:00Z"
}
```

## 🛠️ Customization

- Edit `aw-qt/aw_qt/websocket.py` to change polling, data format, or add new endpoints.

## 📝 License

MIT

---

**Happy tracking!** 