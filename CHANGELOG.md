# CHANGELOG - Mythr Prism Monorepo

Este documento registra de forma acumulativa los cambios relevantes del monorepo (`raiz`, `mythr-prism-front`, `mythr-prism-back`) para trazar que cambio, para que se cambio y facilitar siguientes iteraciones.

## 2026-04-05

### Monorepo (raiz)

- [Documentacion] Se agrego entrada de estado `Kickoff V2 API foundation (in progress)` para iniciar la iniciativa `API de control total (REST + Realtime)` con plan por fases y guias de arranque local.
- [Infraestructura/Deploy] Se actualizaron punteros de submodulos y sincronizacion de ramas para integrar `remote-monitor-cloud-sync` en `development`, para asegurar coherencia entre front, back y documentacion operativa.
- [Documentacion] Se alinearon notas globales de estado y guias del monorepo tras la entrega Cloud Sync, para dejar trazabilidad unica de release.

### Frontend (mythr-prism-front)

- [Funcionalidad] Se incorporo cliente base versionado para REST `/api/v1` y cliente realtime `/realtime/v1` con API key, junto con panel diagnostico inicial en `Monitores` para validar handshakes V2 sin reemplazar el flujo operativo actual.
- [Funcionalidad] Se completo el flujo de `Monitor Virtual Remoto (Cloud Sync)` en UI de operador y cliente remoto, para sumar monitores virtuales por pairing sin hardware adicional.
- [Funcionalidad] Se implementaron `Filtros en caliente` por monitor (brightness/contrast/saturate/grayscale/blur) con aplicacion en vivo sobre la salida, para ajustar imagen durante reproduccion sin reiniciar ventana esclava.
- [Mejora UX] Se ajusto la experiencia de pairing remoto (QR, codigo, estados de conexion/reconexion) con feedback operativo continuo, para reducir friccion durante pruebas en campo.
- [Mejora UX] Se agrego panel de ajuste rapido de filtros y gestion de presets (guardar/aplicar/eliminar) en el editor de contenido, para operadores que necesitan correcciones visuales inmediatas por escena/monitor.
- [Mejora UX] Se redujo complejidad del dialogo de contenido de pantalla separandolo en tabs (`Transformacion`, `Transiciones`, `Filtros`) y ampliando controles finos (rotar 180, escala numerica, step de movimiento, resets por filtro y reset global), para operacion mas rapida en vivo.
- [Bugfix] Se aplicaron ajustes de estabilidad de conectividad y sincronizacion remota, para disminuir cortes visibles y facilitar recuperacion de sesion.
- [Documentacion] Se cerro el estado de avance V1 y backlog con la entrega remota validada, para mantener roadmap consistente.

### Backend (mythr-prism-back)

- [Funcionalidad] Se habilito foundation API V2 con `/api/v1`, middleware API key + rate limit, envelope de error estandar, OpenAPI 3.1 + Swagger (`/docs`, `/openapi.json`, `/openapi.yaml`) y canal realtime `/realtime/v1` con auth para eventos base de sistema.
- [Testing] Se agregaron contratos iniciales para endpoints REST y eventos realtime foundation, para asegurar consumo externo temprano en la iniciativa V2.
- [Funcionalidad] Se integraron y consolidaron los componentes de senalizacion para Cloud Sync en `development`, para soportar lifecycle de salas remotas en produccion.
- [Infraestructura/Deploy] Se dejo operativo el stack Node + Socket.io + Redis + WebRTC/pairing para sesiones remotas, para habilitar transporte y control host-cliente.
- [Documentacion] Se finalizo el backlog tecnico backend de entrega Cloud Sync, para dejar criterios de cierre y pendientes de hardening explicitados.

## 2026-04-03

### Monorepo (raiz)

- [Infraestructura/Deploy] Se integraron punteros de submodulo de features V1 (`external-app-capture`, `source-modal-tabs`, metrica de progreso), para mantener integracion incremental del monorepo.
- [Documentacion] Se sincronizo estado de backlog global con avances reales de frontend, para evitar desalineacion entre tracking y codigo.

### Frontend (mythr-prism-front)

- [Funcionalidad] Se implemento `Captura y retransmision de aplicaciones externas` hacia monitor esclavo, para compartir ventanas de terceros sin salir de Mythr Prism.
- [Funcionalidad] Se movieron las fuentes del monitor a un modal unico con pestanas (`Imagen local`, `URL externa`, `Aplicacion externa`), para concentrar operaciones por contexto.
- [Mejora UX] Se agregaron ajustes de pruebas remotas (parametros de QR/public URL, orientacion en cliente remoto, auto-hide de toolbar, accion de copiar codigo), para facilitar pairing desde movil en entornos LAN/HTTPS.
- [Bugfix] Se reforzo manejo de errores/cancelaciones de captura externa y continuidad del flujo principal, para evitar bloqueos del monitor.
- [Documentacion] Se actualizaron notas y progreso V1 tras integrar features de alto impacto, para sostener trazabilidad del roadmap.

### Backend (mythr-prism-back)

- [Funcionalidad] Se agrego backend de senalizacion y pairing de monitores remotos, para habilitar alta de clientes cloud en sesiones del host.
- [Infraestructura/Deploy] Se introdujo backlog y base operativa para servicio realtime con Redis, para preparar despliegue con control de estado efimero.
- [Documentacion] Se formalizo backlog tecnico backend inicial, para planificar fases de seguridad, observabilidad y resiliencia.

## 2026-04-02

### Monorepo (raiz)

- [Infraestructura/Deploy] Se actualizaron punteros del submodulo frontend tras merges de `Transiciones`, `URLs externas` y `dropzone unificada`, para mantener versionado consistente en raiz.
- [Documentacion] Se dejo reflejado el avance de integracion V1 en el historial de merges del monorepo, para seguimiento de entregas por lote.

### Frontend (mythr-prism-front)

- [Funcionalidad] Se habilitaron `Transiciones` (cut/fade/wipe) al cambiar contenido, para mejorar continuidad visual entre escenas.
- [Funcionalidad] Se incorporo soporte de `URLs externas` en monitor y playlist con controles seguros, para ampliar fuentes de contenido operativo.
- [Mejora UX] Se unifico la `dropzone` de importacion de imagen entre Monitores y Playlist, para ofrecer un flujo consistente de drag-and-drop/pegado/selector manual.
- [Bugfix] Se ajustaron reglas de dialogos de playlist y persistencia segura en cambios con transicion, para evitar inconsistencias de estado.

### Backend (mythr-prism-back)

- [Infraestructura/Deploy] Sin cambios funcionales relevantes en codigo backend; se mantuvo base preparada para fases de cloud sync.
- [Documentacion] Sin cambios relevantes registrados en esta fecha.

## 2026-03-31

### Monorepo (raiz)

- [Infraestructura/Deploy] Se formalizo cierre de MVP y arranque de V1 a nivel monorepo, para consolidar nueva fase de entrega.
- [Infraestructura/Deploy] Se ajusto `docker-compose`/Dokploy y sincronizacion de submodulos, para facilitar despliegue reproducible del stack.
- [Documentacion] Se publico guia operativa de deploy y flujo de ramas (`development` -> `main`), para estandarizar integracion y release.

### Frontend (mythr-prism-front)

- [Funcionalidad] Se implemento `Flash ID monitores` y controles compactos de accion, para mapear rapidamente monitor logico con monitor fisico.
- [Funcionalidad] Se entrego `Pizarra en vivo` con herramientas de trazo y gestion de overlay, para anotaciones en tiempo real durante proyeccion.
- [Mejora UX] Se mejoro toolbar/distribucion de pizarra y paneles modales, para uso mas estable en viewport dinamico.
- [Bugfix] Se corrigieron validaciones de persistencia y reglas de importacion en contexto fullscreen, para reducir estados invalidos.

### Backend (mythr-prism-back)

- [Infraestructura/Deploy] Se inicializo repositorio backend y configuracion base de entorno (`.gitignore`), para preparar evolucion de servicio realtime.
- [Documentacion] Se establecio base minima de proyecto backend para arrancar backlog tecnico V1.

## 2026-03-30

### Monorepo (raiz)

- [Documentacion] Se consolido seguimiento de iniciativas MVP/V1 en backlog operativo del front, para guiar el cierre de fase.

### Frontend (mythr-prism-front)

- [Funcionalidad] Se cerraron entregables MVP clave: modo espejo, layouts, sincronizacion de video, playlist multi-destino y miniaturas, para estabilizar operacion multi-monitor.
- [Mejora UX] Se mejoraron modales de playlist, accesibilidad de tabs y feedback visual de reordenado drag-and-drop, para reducir carga operativa.
- [Bugfix] Se aplicaron fixes de robustez en fullscreen, cierre de ventanas esclavas y consistencia de estado, para evitar bloqueos en flujos de importacion/cambio de contenido.
- [Documentacion] Se actualizaron notas de progreso y criterios de entrega MVP, para preparar cierre formal y evolucion a V1.

### Backend (mythr-prism-back)

- [Infraestructura/Deploy] Sin cambios funcionales en backend en esta fecha; el foco estuvo en consolidacion MVP frontend.
- [Documentacion] Sin cambios relevantes registrados en esta fecha.

## Como mantener este changelog

- Actualizar este archivo en cada entrega (feature, bugfix, mejora UX, infraestructura/deploy o documentacion) agregando una nueva fecha `YYYY-MM-DD` al inicio con los tres alcances fijos: `Monorepo (raiz)`, `Frontend (mythr-prism-front)` y `Backend (mythr-prism-back)`.
