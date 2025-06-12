# CI/CD Pipeline for n8n Workflows

## 1. Descripción
Este workflow de GitHub Actions automatiza la importación de tus archivos JSON de `workflows/` a tu instancia de n8n.  
Cada vez que se hace push a la rama `main` o se lanza manualmente, se ejecuta y actualiza tus workflows en el entorno de n8n.

## 2. Triggers
- **on.push.branches: [main]**  
- **on.workflow_dispatch** (ejecución manual)

## 3. Secrets Requeridos
Los siguientes **GitHub Secrets** deben estar configurados en **Settings → Secrets → Actions**:

- `N8N_HOST`  
  - Valor: `http://localhost:5678`  
- `N8N_AUTH_TOKEN`  
  - Tu API Key generada en la UI de n8n (no la pegues aquí; solo menciona el nombre del secret).  
- `N8N_BASIC_AUTH_USER`  
  - Usuario HTTP Basic definido en tu `.env`.  
- `N8N_BASIC_AUTH_PASSWORD`  
  - Contraseña HTTP Basic definida en tu `.env`.  
- `N8N_RUNNERS_ENABLED`  
  - Valor: `true`  
- `N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS`  
  - Valor: `true`

> **Nota:** Nunca incluyas valores reales de secretos en la documentación; siempre usa placeholders o el nombre del secret.

## 4. Estructura del Workflow (`.github/workflows/deploy-n8n.yml`)
```yaml
name: Deploy n8n Workflows

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  deploy-n8n:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Ensure n8n_data exists & is writable
        run: |
          mkdir -p ${{ github.workspace }}/n8n_data
          sudo chown -R 1000:1000 ${{ github.workspace }}/n8n_data

      - name: Import exported workflow via n8n CLI
        run: |
          docker run --rm \
            -v ${{ github.workspace }}/n8n_data:/home/node/.n8n \
            -v ${{ github.workspace }}/workflows:/workflows \
            -e N8N_HOST=${{ secrets.N8N_HOST }} \
            -e N8N_AUTH_TOKEN=${{ secrets.N8N_AUTH_TOKEN }} \
            -e N8N_BASIC_AUTH_ACTIVE=true \
            -e N8N_BASIC_AUTH_USER=${{ secrets.N8N_BASIC_AUTH_USER }} \
            -e N8N_BASIC_AUTH_PASSWORD=${{ secrets.N8N_BASIC_AUTH_PASSWORD }} \
            -e N8N_RUNNERS_ENABLED=true \
            -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true \
            n8nio/n8n:latest \
            import:workflow --input=/workflows/J4lle5NxO9yixcDc.json
