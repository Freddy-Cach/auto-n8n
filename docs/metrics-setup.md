# Configuración de métricas con Grafana y Loki

## 1. Añadir servicios al docker-compose
1. Abre `docker-compose.yml`.
2. Añade los servicios **loki**, **promtail** y **grafana** (ver la sección “docker-compose.yml”).
3. Guarda y cierra.

## 2. Crear promtail.yml
1. En la raíz del proyecto, crea `promtail.yml`.
2. Pega la configuración de **scrape_configs** para capturar los logs Docker.
3. Guarda y cierra.

## 3. Levantar toda la pila
```bash
docker-compose down
docker-compose up -d

Grafana: http://localhost:3000 (usuario admin / admin)
Loki API: http://localhost:3100
