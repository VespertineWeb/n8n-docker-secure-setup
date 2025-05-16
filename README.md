# n8n Docker Secure Setup

This repository contains a production-ready Docker Compose configuration to self-host [n8n](https://n8n.io), an open-source workflow automation tool.
It includes:

* **Traefik reverse proxy with automatic SSL via Let's Encrypt**
* **Persistent storage for workflows and credentials**
* **Easy customization using `.env` file**

---

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/Kartik240803/n8n-docker-secure-setup.git
cd n8n-docker-secure-setup
```

### 2. Configure Environment Variables

Update the `.env` file with your domain and email:

```ini
DOMAIN_NAME=yourdomain.com
SUBDOMAIN=n8n
SSL_EMAIL=your@email.com
GENERIC_TIMEZONE=America/Sao_Paulo
```

This will make n8n accessible at `https://n8n.yourdomain.com`.

### 3. Create Local Files Directory (Optional)

```bash
mkdir local-files
```

This folder will be mounted inside the container at `/files`.

### 4. Start the Services

```bash
docker-compose up -d
```

### 5. Access n8n

Open your browser:

```
https://n8n.yourdomain.com
```

---

## 📂 Files Included

| File                 | Description                                   |
| -------------------- | --------------------------------------------- |
| `docker-compose.yml` | Docker Compose setup for n8n and Traefik      |
| `.env`               | Environment variables template for easy setup |

---

## 💾 Persistent Storage

* **Workflows & Credentials:** Stored in `n8n_data` Docker volume.
* **Certificates:** Stored in `traefik_data` Docker volume.
* **Custom Files:** From `local-files/` (mounted inside the container).

---

## 🔒 Security Best Practices

* Enable basic auth for n8n by adding these to the `n8n` service in `docker-compose.yml`:

```yaml
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=youruser
      - N8N_BASIC_AUTH_PASSWORD=yourpassword
```

* Keep Traefik dashboard (`:8080`) disabled or properly secured.
* Only expose ports `80` and `443` to the public internet.

---

## 🛑 Stop the Stack

```bash
docker-compose down
```

---

## 📚 References

* [n8n Documentation](https://docs.n8n.io/)
* [Traefik Documentation](https://doc.traefik.io/traefik/)
