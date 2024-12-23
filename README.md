# Local AI Stack
## Traefik | Ollama | Open WebUI | n8n

This project provides a Docker-based setup using Traefik as a reverse proxy and load balancer, along with several integrated services including Ollama (AI model serving), Open WebUI (Ollama interface), and n8n (workflow automation).

## Prerequisites

- Docker
- Docker Compose
- A domain name (for SSL/TLS certificates)
- Linode DNS (for automatic SSL certificate management)
- NVIDIA GPU (for Ollama GPU acceleration)
- NVIDIA Container Toolkit installed

## Project Structure

```
.
├── docker-compose.yml      # Main Docker composition file
├── .env                   # Environment variables configuration
├── traefik-config/        # Traefik configuration files
│   └── dynamic.yml        # Dynamic TLS and middleware configuration
├── letsencrypt/          # SSL certificate storage
├── ollama/               # Ollama data directory
├── open-webui/           # Open WebUI data directory
└── n8n/                  # n8n workflow data directory
```

## Services

1. **Traefik**: Reverse proxy and load balancer
   - Handles SSL/TLS termination
   - Provides automatic SSL certificate management via Let's Encrypt
   - Includes a secure dashboard interface

2. **Ollama**: AI model serving platform
   - Runs with NVIDIA GPU support
   - Accessible via API

3. **Open WebUI**: Web interface for Ollama
   - User-friendly interface for interacting with AI models
   - Configurable authentication

4. **n8n**: Workflow automation platform
   - Automated workflow creation and management
   - Secure access with basic authentication

## Setup Instructions

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```

2. Create a `.env` file with the following variables:
   ```
   # Domain Configuration
   DOMAIN=your-domain.com
   TRAEFIK_SUBDOMAIN=traefik
   OLLAMA_SUBDOMAIN=ollama
   OPENWEBUI_SUBDOMAIN=chat
   N8N_SUBDOMAIN=n8n

   # Traefik Configuration
   ACME_EMAIL=your-email@domain.com
   LINODE_TOKEN=your-linode-api-token
   TRAEFIK_BASIC_AUTH=admin:hashed-password

   # Open WebUI Configuration
   WEBUI_AUTH_MODE=password
   WEBUI_USERNAME=your-username
   WEBUI_PASSWORD=your-password

   # n8n Configuration
   N8N_BASIC_AUTH_ACTIVE=true
   N8N_BASIC_AUTH_USER=your-username
   N8N_BASIC_AUTH_PASSWORD=your-password
   N8N_ENCRYPTION_KEY=your-encryption-key
   ```

3. Create required directories:
   ```bash
   mkdir -p traefik-config letsencrypt ollama open-webui n8n
   ```

4. Start the services:
   ```bash
   docker compose up -d
   ```

## Accessing Services

After setup, your services will be available at:

- Traefik Dashboard: `https://traefik.your-domain.com`
- Ollama API: `https://ollama.your-domain.com`
- Open WebUI: `https://chat.your-domain.com`
- n8n: `https://n8n.your-domain.com`

## Security Features

- All services are protected with SSL/TLS encryption
- Traefik dashboard is secured with basic authentication
- Open WebUI includes optional password protection
- n8n can be configured with basic authentication
- Strong TLS configuration with secure headers and cipher suites

## Maintenance

- SSL certificates are automatically renewed through Let's Encrypt
- Service containers are configured to restart automatically unless stopped
- Data persistence is maintained through Docker volumes

## Troubleshooting

1. Check container status:
   ```bash
   docker compose ps
   ```

2. View container logs:
   ```bash
   docker compose logs [service-name]
   ```

3. Common issues:
   - DNS configuration: Ensure your domain points to the correct IP
   - Port conflicts: Verify ports 80 and 443 are available
   - GPU access: Confirm NVIDIA Container Toolkit is properly installed

## Contributing

Feel free to submit issues and enhancement requests!