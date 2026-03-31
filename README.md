# Mythr Prism Monorepo

Este repositorio usa un monorepo PNPM para separar el frontend operativo actual y el backend scaffold para evoluciones futuras.

## Estructura

- `mythr-prism-front/`: app frontend Vue 3 + TypeScript (operador master + runtime slave).
- `mythr-prism-back/`: scaffold inicial del backend (sin implementacion funcional todavia).

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

## Comandos de validacion frontend

- `pnpm --filter mythr-prism-front run typecheck`
- `pnpm --filter mythr-prism-front run build`
- `pnpm --filter mythr-prism-front run test`

## Notas de ruta

- El backlog operativo del frontend ahora vive en `mythr-prism-front/docs/backlog.md`.

## Deploy en Dokploy

- Despliegue actual (hoy): solo `frontend` con `docker-compose.yml` de la raiz.
- Base futura: servicio `backend` ya definido como profile opcional para activarlo sin rehacer la infraestructura.
- Guia paso a paso: `DOKPLOY.md`.

## Licencia

Licencia: Propietaria (All Rights Reserved).
