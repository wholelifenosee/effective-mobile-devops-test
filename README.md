# Effective Mobile DevOps Test Assignment

Simple web application with Python backend and Nginx reverse proxy in Docker containers.

## Architecture

```
[User] → [Nginx:80] → [Backend:8080 (internal)]
```

- **Nginx** receives HTTP requests on port 80 and proxies them to backend
- **Backend** is a Python HTTP server that responds with "Hello from Effective Mobile!"
- Backend is only accessible through nginx (not exposed to host)

## Technologies

- Python 3.11 (http.server)
- Nginx 1.25 (Alpine)
- Docker & Docker Compose

## Project Structure

```
.
├── backend/
│   ├── Dockerfile
│   └── app.py
├── nginx/
│   └── nginx.conf
├── docker-compose.yml
└── README.md
```

## How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/wholelifenosee/effective-mobile-devops-test#
   cd effective-mobile-devops-test
   ```

2. **Start the application**
   ```bash
   docker-compose up --build
   ```

3. **Wait for:** `Server running on port 8080...`

## How to Test

Open a new terminal and run:

```bash
curl http://localhost
```

**Expected response:**
```
Hello from Effective Mobile!
```

Or open browser: `http://localhost`

## How to Stop

Press `Ctrl+C`, then:

```bash
docker-compose down
```

## How It Works

1. User sends request to `http://localhost` (port 80)
2. Nginx receives the request
3. Nginx proxies to `backend:8080` (using Docker internal DNS)
4. Backend returns "Hello from Effective Mobile!"
5. Nginx forwards response to user

Backend port 8080 is NOT exposed to host - only accessible via nginx through Docker network.

## Requirements Met

-  Python HTTP server on port 8080
-  Backend not exposed to host (no port published)
-  Nginx as reverse proxy on port 80
-  Separate nginx.conf with upstream and proxy_pass
-  Backend Dockerfile with CMD to start app
-  Nginx uses official image with volume-mounted config
-  Docker Compose with 2 services on isolated network
-  Only port 80 exposed to host

