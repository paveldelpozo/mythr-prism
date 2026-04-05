# Mythr Prism Monorepo

Este repositorio usa un monorepo PNPM para separar el frontend operativo actual y el backend realtime de sincronizacion remota.

## Estructura

- `mythr-prism-front/`: app frontend Vue 3 + TypeScript (operador master + runtime slave).
- `mythr-prism-back/`: backend realtime (Socket.io + Redis) para pairing/senalizacion de monitores remotos.

## Requisitos

- Node.js `>=20.19.0`.
- pnpm `>=8.15.9`.

## Instalacion

```bash
pnpm install
```

## Comandos de workspace (raiz)

- `pnpm run dev`: arranca el frontend actual.
- `pnpm run dev:front`: arranca solo `mythr-prism-front`.
- `pnpm run dev:back`: ejecuta placeholder de backend scaffold.
- `pnpm run dev:all`: preparado para ejecutar front y back en paralelo.
- `pnpm run dev:all:lan`: arranca front+back en paralelo accesibles en red LAN (ideal para pruebas desde movil).

## Pruebas remotas en móvil (HTTPS)

`getScreenDetails` (Window Management API) requiere un **secure context**.
En desarrollo, `localhost` se considera secure context, pero una IP LAN en `http://<ip>` no siempre mantiene el mismo nivel de compatibilidad.
Por eso, el flujo recomendado es mantener el operador en `localhost` y exponer solo la URL que usan los clientes moviles via HTTPS.

### Flujo recomendado

1. El host operador abre la app en local (`http://localhost:<puerto>`).
2. El QR de pairing se genera con `VITE_REMOTE_PUBLIC_URL` (URL publica HTTPS).
3. El cliente movil abre esa URL HTTPS publica y completa el pairing.

### Ejemplo de `.env` (frontend)

Archivo: `mythr-prism-front/.env`

```dotenv
# URL publica HTTPS para el QR remoto (cliente movil)
VITE_REMOTE_PUBLIC_URL=https://mythr-prism-demo.trycloudflare.com

# URL del backend Socket.IO remoto (opcional, segun tu setup)
VITE_REMOTE_BACKEND_URL=https://mythr-prism-back-demo.trycloudflare.com
```

Notas:
- Si `VITE_REMOTE_PUBLIC_URL` no esta definida, el QR usa `window.location.origin`.
- `VITE_REMOTE_BACKEND_URL` mantiene su comportamiento actual (sin cambios): si no se define en dev, usa `http://localhost:3000`.

### Tunel HTTPS rapido (Cloudflare Tunnel o ngrok)

#### Opcion A: Cloudflare Tunnel

1. Arranca frontend y backend en local.
2. Expone el frontend:

```bash
cloudflared tunnel --url http://localhost:5173
```

3. (Opcional) expone backend Socket.IO:

```bash
cloudflared tunnel --url http://localhost:3000
```

4. Copia las URLs `https://...trycloudflare.com` al `.env` del front (`VITE_REMOTE_PUBLIC_URL` y, si aplica, `VITE_REMOTE_BACKEND_URL`).

#### Opcion B: ngrok

1. Expone frontend:

```bash
ngrok http 5173
```

2. (Opcional) expone backend:

```bash
ngrok http 3000
```

3. Usa las URLs HTTPS de ngrok en `mythr-prism-front/.env`.

### Nota de seguridad

No uses tuneles publicos sin controles en produccion. Para entornos reales, agrega autenticacion, restricciones de red/origen y rotacion de credenciales/tokens.

## Comandos de validacion frontend

- `pnpm --filter mythr-prism-front run typecheck`
- `pnpm --filter mythr-prism-front run build`
- `pnpm --filter mythr-prism-front run test`

## Notas de ruta

- El backlog operativo del frontend ahora vive en `mythr-prism-front/docs/backlog.md`.

## Estado de roadmap

- MVP: completado al 100% (cierre formal registrado el 2026-03-31).
- Siguiente fase activa: V1.

## Arranque V1 (checklist corto)

- [ ] Crear rama `feature/<nombre>` desde `development` para la primera entrega V1.
- [ ] Seleccionar un objetivo V1 acotado del backlog (recomendado: `Flash ID monitores`).
- [ ] Definir criterio de aceptacion y prueba minima antes de implementar.
- [ ] Ejecutar validacion tecnica al cerrar la feature (`typecheck`, `build`, `test` del frontend).

## Flujo de ramas (git-flow simplificado)

- `main`: rama de produccion.
- `development`: rama de integracion y pruebas locales previas a produccion.
- Nuevas features: crear `feature/<nombre>` desde `development`.
- Integracion: merge `feature/<nombre>` -> `development`.
- Publicacion: merge `development` -> `main`.

## Deploy en Dokploy

- Despliegue actual (hoy): solo `frontend` con `docker-compose.yml` de la raiz.
- Si Dokploy clona sin submodulos, habilitar checkout recursivo o ejecutar `git submodule update --init --recursive` antes del deploy.
- Base futura: servicio `backend` ya definido como profile opcional para activarlo sin rehacer la infraestructura.
- Guia paso a paso: `DOKPLOY.md`.

## Licencia

Licencia: Propietaria (All Rights Reserved).
