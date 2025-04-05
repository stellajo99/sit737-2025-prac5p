# Calculator Microservice (Dockerised with Health Check)

## Overview

This is a Dockerised calculator microservice developed for SIT737 – Cloud Native Application Development.  
Built with **Node.js** and **Express**, the app supports both **basic arithmetic operations** and **advanced mathematical functions** via HTTP GET endpoints.  
It includes structured **logging** using the `winston` library and is containerised using **Docker** and **Docker Compose**, with integrated container **health checks**.

---

## 🚀 Features

- Arithmetic operations: add, subtract, multiply, divide
- Advanced operations: power, square root, modulo
- RESTful API using GET requests
- Request and error logging to console and files
- Docker containerisation with healthcheck support

---

## 🐳 Docker Setup

### 1. Build the Docker Image

```bash
docker build -t sit737-2025-prac5p .
```

### 2. Run the Application with Docker Compose

```bash
docker-compose up -d
```

The application will run at:  
📍 `http://localhost:3000`

---

## ❤️ Health Check

Docker Compose includes a built-in healthcheck that pings the root endpoint every 30 seconds to ensure the container is running and responsive.

### Docker Compose Healthcheck Configuration:

```yaml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:3000"]
  interval: 30s
  timeout: 10s
  retries: 3
```

### To inspect health status:

```bash
docker inspect --format="{{json .State.Health}}" sit737-2025-prac5p-web-1
```

---

## 🧮 API Endpoints

### 1. `/add`  
Adds two numbers  
**Example:** `http://localhost:3000/add?num1=5&num2=3`

### 2. `/subtract`  
Subtracts num2 from num1  
**Example:** `http://localhost:3000/subtract?num1=10&num2=4`

### 3. `/multiply`  
Multiplies two numbers  
**Example:** `http://localhost:3000/multiply?num1=6&num2=7`

### 4. `/divide`  
Divides num1 by num2 (error if num2 is 0)  
**Example:** `http://localhost:3000/divide?num1=20&num2=4`

### 5. `/power`  
Exponentiation: num1 raised to the power of num2  
**Example:** `http://localhost:3000/power?num1=2&num2=3`

### 6. `/sqrt`  
Square root of num1 (error if num1 < 0)  
**Example:** `http://localhost:3000/sqrt?num1=25`

### 7. `/modulo`  
Remainder of num1 divided by num2 (error if num2 is 0)  
**Example:** `http://localhost:3000/modulo?num1=10&num2=3`

---

## ❌ Error Handling

The API will return:
- `400 Bad Request` if query params are missing, non-numeric, or invalid
- Descriptive JSON error messages for:
  - Division by zero
  - Square root of a negative number
  - Modulo by zero

---

## 📜 Logging (via Winston)

- Logs are written to:
  - Console (info + error)
  - `logs/combined.log` – all logs
  - `logs/error.log` – errors only
- Each request logs the operation type and input values

### To view logs in real time:

```bash
tail -f logs/combined.log
```

---

## 🐳 DockerHub

The built image is available on DockerHub:

```bash
docker pull stellajo99/sit737-2025-prac5p
docker run -p 3000:3000 stellajo99/sit737-2025-prac5p
```

🔗 [https://hub.docker.com/r/stellajo99/sit737-2025-prac5p](https://hub.docker.com/r/stellajo99/sit737-2025-prac5p)

---

## 👩‍💻 Author

**Stella Jo**  
SIT737 – Cloud Native Application Development  
Deakin University | 2025