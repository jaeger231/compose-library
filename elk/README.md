# ELK Stack using Docker Compose

This setup runs the [ELK Stack](https://www.elastic.co/what-is/elk-stack) (Elasticsearch, Logstash, and Kibana) in a single container using Docker Compose.

##  Service

### 1. **elk**
- **Image:** `sebp/elk`
- **Purpose:** Combines Elasticsearch, Logstash, and Kibana in a single container for centralized logging and monitoring.
- **Ports:**
  - `5601:5601` — Kibana Web UI
  - `9200:9200` — Elasticsearch REST API
  - `5044:5044` — Logstash Beats input
- **Restart Policy:** `unless-stopped`

##  Usage

1. **Start the ELK stack:**
   ```bash
   docker compose up -d
   ```

2. **Access Kibana UI:**
   - Open your browser and go to `http://localhost:5601`

3. **Elasticsearch API Access:**
   - Use tools like `curl` or Postman to access `http://localhost:9200`

4. **Logstash Input:**
   - Send logs to `localhost:5044` using Filebeat or other Beats.

5. **Stop the stack:**
   ```bash
   docker compose down
   ```

##  Note:

- This container is suitable for development and testing purposes.
- For production deployments, it's recommended to run Elasticsearch, Logstash, and Kibana in separate containers and with persistent storage.
