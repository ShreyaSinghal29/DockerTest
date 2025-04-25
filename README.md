Here’s a clean and professional `README.md` you can copy-paste directly into your project folder:

---

```markdown
# 🐳 Streamlit + PostgreSQL Multi-Container App

This project is a beginner-friendly example of building a **multi-container application** using **Docker**, **Streamlit**, and **PostgreSQL**. The application connects to a PostgreSQL database container and displays data using a custom Streamlit frontend.

---

## 📦 Tech Stack

- **Python** (Streamlit)
- **PostgreSQL** (as database)
- **Docker** (to containerize both services)
- **Docker Network** (for communication between containers)

---

## 🛠️ Setup Instructions

### 1️⃣ Pull PostgreSQL Image

```bash
docker pull postgres
```

---

### 2️⃣ Create Docker Network

```bash
docker network create my_postgres_network
```

---

### 3️⃣ Run PostgreSQL Container

```bash
docker run --name my_postgres_container --network my_postgres_network \
  -e POSTGRES_USER=shreya \
  -e POSTGRES_PASSWORD=secret \
  -e POSTGRES_DB=testdb \
  -p 5432:5432 -d postgres
```

---

### 4️⃣ Add Data to Database

```bash
docker exec -it my_postgres_container psql -U shreya -d testdb
```

Inside the psql shell:

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  age INT
);

INSERT INTO users (name, age) VALUES ('Alice', 28), ('Bob', 34);
```

---

### 5️⃣ Streamlit Dockerfile Setup

Inside your `streamlit-app/` folder:

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY main.py .
RUN pip install streamlit psycopg2

CMD ["streamlit", "run", "main.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

---

### 6️⃣ Build and Run Streamlit Container

```bash
docker build -t streamlit-app ./streamlit-app
docker run --name my_streamlit_container --network my_postgres_network -p 8501:8501 -d streamlit-app
```

---

## 💻 Access the Application

Open your browser and go to:

```
http://localhost:8501
```

You’ll see a stylish Streamlit dashboard that fetches and displays data from the PostgreSQL container.

---

## 📂 Folder Structure

```
docker-streamlit-postgres/
│
├── streamlit-app/
│   ├── Dockerfile
│   ├── main.py
│
├── docker-compose.yml (optional)
└── README.md
```


## 👩‍💻 Author

**Shreya Singhal**

_Thanks for checking out this project! If you found it helpful, feel free to ⭐ the repo._

---

```

