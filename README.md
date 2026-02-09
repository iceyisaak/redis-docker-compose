Here is the comprehensive, polished `README.md`. I’ve consolidated the setup instructions, the updated Docker Compose configuration with the **auto-restart** policies, and the essential management commands into one file.

---

```markdown
# Redis + Redis Insight Docker Environment

A production-ready Docker Compose setup providing a high-performance Redis instance paired with the Redis Insight GUI for easy data management.

## 🚀 Features
* **Redis 7.2 (Alpine):** Lightweight and secure database core.
* **Redis Insight:** Web-based GUI for real-time key browsing and profiling.
* **Data Persistence:** Automatic data saving via Docker volumes.
* **Auto-Recovery:** Configured to restart automatically unless manually stopped.

---

## 🛠 Setup & Deployment

### 1. Prerequisites
Ensure you have [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) installed.

### 2. Configuration (`docker-compose.yaml`)
Save the following as `docker-compose.yaml` in your project folder:

```yaml
services:
  redis:
    image: redis:7.2-alpine
    container_name: redis_server
    restart: unless-stopped
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    command: ["redis-server", "--appendonly", "yes"]

  redis-insight:
    image: redis/redisinsight:latest
    container_name: redis_insight
    restart: unless-stopped
    ports:
      - "5540:5540"
    depends_on:
      - redis

volumes:
  redis_data:

```

### 3. Launching the Services

Run the following command in your terminal:

```bash
docker-compose up -d

```

---

## 🔗 Access Details

| Service | Host | Port | URL / Link |
| --- | --- | --- | --- |
| **Redis Server** | `localhost` | `6379` | `redis://localhost:6379` |
| **Redis Insight (GUI)** | `localhost` | `5540` | [http://localhost:5540](https://www.google.com/search?q=http://localhost:5540) |

**Note on Connection:** When adding a database in Redis Insight, use the hostname `redis` (the service name) if you are connecting via the internal Docker network.

---

## 💻 Essential Docker Commands

### Lifecycle Management

* **Start Services:** `docker-compose up -d`
* **Stop Services:** `docker-compose stop` (Pauses containers)
* **Remove Containers:** `docker-compose down` (Removes network/containers)
* **Full Reset:** `docker-compose down -v` (⚠️ Deletes all saved Redis data)

### Monitoring & Interaction

* **View Logs:** `docker-compose logs -f`
* **Check Status:** `docker-compose ps`
* **Redis CLI Access:**
```bash
docker exec -it redis_server redis-cli

```



---

## ⚙️ Persistence & Reliability

* **Restart Policy:** Both services use `unless-stopped`. They will automatically restart after a system reboot or a crash, unless you manually ran `docker-compose stop`.
* **Storage:** Data is stored in the `redis_data` volume. Even if the container is destroyed, your data persists until the volume is explicitly deleted.

```


