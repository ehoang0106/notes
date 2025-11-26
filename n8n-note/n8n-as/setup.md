`docker-compose.yml`:

```yml
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n:latest
    container_name: n8n
    ports:
      - "5678:5678"
    environment:
      - N8N_HOST=n8n.awakenservices.net
      - N8N_PROTOCOL=https
      - WEBHOOK_URL=https://n8n.awakenservices.net/
      - N8N_EDITOR_BASE_URL=https://n8n.awakenservices.net/
      - N8N_SECURE_COOKIE=true
      - N8N_PROXY_HOPS=1
    volumes:
      - n8n_data:/home/node/.n8n
    restart: unless-stopped
    networks:
      - npm

volumes:
  n8n_data:

networks:
  npm:
    external: true

```

create a npm network:
```bash
docker network create npm
```

deploy:

```bash
 docker compose up -d
```