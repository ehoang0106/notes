create volume for n8n

```bash
docker volume create n8n_data
```

```bash
docker run -d --rm --name n8n -p 5678:5678 -e N8N_SECURE_COOKIE=false -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

```bash
docker run -d \
  --rm \
  --name n8n \
  -p 80:5678 \
  -p 443:5678 \
  -e N8N_SECURE_COOKIE=true \
  -e N8N_HOST=n8n.slimx3.com \
  -e N8N_PROTOCOL=https \
  -e WEBHOOK_URL=https://n8n.slimx3.com \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n


```

`docker-compose.yml`: 

```js
version: '3.8'

services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    container_name: n8n
    ports:
      - "80:5678"
      - "443:5678"
    environment:
      - N8N_SECURE_COOKIE=true
      - N8N_HOST=n8n.khoah.com
      - N8N_PROTOCOL=https
      - WEBHOOK_URL=https://n8n.khoah.com
    volumes:
      - n8n_data:/home/node/.n8n
    restart: unless-stopped

volumes:
  n8n_data:

```