# Deploy en Dokploy

Esta guia deja el monorepo preparado para desplegar hoy solo el frontend, manteniendo un servicio backend placeholder listo para activarse despues.

## Archivos de despliegue

- `docker-compose.yml`: orquestacion para Dokploy.
- `mythr-prism-front/Dockerfile`: build y runtime de frontend en produccion.
- `mythr-prism-front/nginx.conf`: configuracion de Nginx para servir SPA.
- `mythr-prism-back/Dockerfile`: placeholder backend (profile `backend`).
- `.env.dokploy.example`: variables de entorno para compose.

## Variables de entorno

Copiar y ajustar si hace falta:

```bash
cp .env.dokploy.example .env
```

Variables:

- `FRONTEND_PORT` (default `8080`): puerto publico del frontend.
- `BACKEND_PORT` (default `3000`): puerto reservado para backend futuro.

## Desplegar solo frontend ahora (Dokploy)

1. Crear un proyecto tipo Docker Compose en Dokploy apuntando a este repositorio.
2. Usar `docker-compose.yml` de la raiz.
3. El servicio `frontend` ya usa `build.context: ./mythr-prism-front`; el Dockerfile del front se resuelve de forma autocontenida (sin depender de `pnpm-workspace.yaml` ni otros archivos de la raiz).
4. Definir variables de entorno segun `.env.dokploy.example`.
5. No activar perfiles adicionales; por defecto se levanta solo `frontend`.
6. Deploy.

En local, equivalente:

```bash
docker compose up -d --build frontend
```

## Activar backend mas adelante

Cuando exista backend funcional:

1. Reemplazar `mythr-prism-back/Dockerfile` placeholder por el Dockerfile real del backend.
2. Ajustar `docker-compose.yml` en servicio `backend` (env, healthcheck, volumenes, dependencias).
3. Configurar variables necesarias del backend en Dokploy.
4. Activar profile `backend` y redeploy.

En local, equivalente:

```bash
docker compose --profile backend up -d --build
```
