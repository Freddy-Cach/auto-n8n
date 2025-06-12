## Variables de entorno

- N8N_BASIC_AUTH_ACTIVE  
- N8N_BASIC_AUTH_USER  
- N8N_BASIC_AUTH_PASSWORD  
- N8N_HOST

## docker-compose.yml

```yaml

services:
  n8n:
    image: n8nio/n8n:latest
    restart: unless-stopped
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=${N8N_BASIC_AUTH_ACTIVE}
      - N8N_BASIC_AUTH_USER=${N8N_BASIC_AUTH_USER}
      - N8N_BASIC_AUTH_PASSWORD=${N8N_BASIC_AUTH_PASSWORD}
      - N8N_HOST=${N8N_HOST}
    volumes:
      - ./n8n_data:/home/node/.n8n```

## Verificación

![docker-compose ps](./images/ps.png)

![Health check](./images/healthz.png)

## Acceso a la UI de n8n

1. Abre tu navegador en:
   http://localhost:5678

2. Inicia sesión con las credenciales definidas en tu `.env`:
   - **Usuario**: `freddy-cach`
   - **Contraseña**: la que elegiste en `N8N_BASIC_AUTH_PASSWORD`

3. Tras el login verás el dashboard de **Overview** con tus workflows.

