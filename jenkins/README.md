# Jenkins using Docker Compose

This Docker Compose setup runs [Jenkins](https://www.jenkins.io/) for automating CI/CD pipelines.

##  Service

### 1. **jenkins**
- **Image:** `jenkins/jenkins`
- **Purpose:** Jenkins is an open-source automation server for building, testing, and deploying code.
- **Ports:**
  - `7777:8080` — Jenkins Web UI
  - `50000:50000` — Agent communication port
- **Volumes:**
  - `/home/ubuntu/jenkins_compose/jenkins_configuration:/var/jenkins_home` — Persists Jenkins configuration and job data.
- **User:** `root`
- **Privileged Mode:** Enabled
- **Restart Policy:** `always`

##  Usage

1. **Ensure the configuration directory exists:**
   ```bash
   mkdir -p /home/ubuntu/jenkins_compose/jenkins_configuration
   ```

2. **Start Jenkins:**
   ```bash
   docker compose up -d
   ```

3. **Access Jenkins UI:**
   - Navigate to `http://localhost:7777` in your browser.
   - Unlock Jenkins using the password from:
     ```bash
     cat /home/ubuntu/jenkins_compose/jenkins_configuration/secrets/initialAdminPassword
     ```

4. **Stop the stack:**
   ```bash
   docker compose down
   ```

##  Note:

- This setup runs Jenkins as root in privileged mode, which is convenient for plugin compatibility but not recommended for production without proper security hardening.
- Secure the Jenkins UI with authentication and configure backups for persistent data.
