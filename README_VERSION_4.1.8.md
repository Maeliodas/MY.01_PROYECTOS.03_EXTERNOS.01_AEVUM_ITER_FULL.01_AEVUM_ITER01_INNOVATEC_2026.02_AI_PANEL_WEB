# Panel Aevum Iter · Versión APPROD4.1.8

> **Versión completa actual: `APPROD4.1.8_R16_IN`** — siglas **AP** (Admin Panel, pegadas), canal **PROD**,
> versión **4**, actualizaciones mayores **1**, actualizaciones medianas **8**,
> revisión **16**, rama **IN** (Innovatec).

Origen: copia de `admin_panel` de App Vocacional ITTUX (sin historial git) adaptada a Aevum Iter.

## Revisión R16 (actual): filtro de perfiles dinámico

- El filtro `Perfil` traía 8 códigos fijos viejos que no coincidían con la tabla. Ahora lista los códigos distintos reales (`profileCodes` desde el servidor) sin tocar el refresco en vivo. Render EJS verificado.

## Revisión R15: JS versionado anti-caché

- `dashboard.ejs`: `/admin.js?v=<panelVersion>` para que cada versión jale su JS fresco aunque el navegador conserve caché.
- `package.json` → `4.1.8-15`. Render EJS verificado.

## Revisión R14: caché del navegador

- `sw.js`: caché `aevum-admin-v1` → `v2` para expulsar el `admin.js` viejo. El HTML fresco traía 4 columnas pero el JS en caché repintaba 9 celdas (valores corridos). Con recarga dura (`Ctrl+Shift+R`) se corrige.
- `package.json` → `4.1.8-14`.

## Revisión R13: fuera pregunta abierta

- Eliminado endpoint `PUT department-questions`, tarjeta por departamento, query de abiertas, columna `Respuestas` y `departmentQuestions` del payload admin. Tablas e ingesta intactas.
- Sintaxis y render EJS verificados.

## Revisión R12: fuera procedencia y lenguas

- Dashboard sin filtros estado/municipio/escuela, sin gráficas de procedencia/escuelas/lenguas/idiomas, registros con 5 columnas y KPI de 3 tarjetas; fuera 4 tabs/parciales de esos catálogos.
- Servidor sin agregados de procedencia/lenguas, totales sin escuelas y PDF sin secciones 6–7 ni columnas de lugar/escuela.
- Ingesta (`evaluations`, `students`) y esquema intactos a propósito. Sintaxis y render EJS verificados.

## Revisión R11: corrección de sintaxis en pesos

- `sql/schema.sql`: el reemplazo de los 66 pesos dejó sintaxis rota (`('isc','R',6.5)5.8` por índice de grupo erróneo en mi script). Reparado y validado: 66 tuplas bien formadas (6 por carrera), 11 códigos únicos, paréntesis y comillas balanceados, sin restos corruptos.

## Revisión R10 (actual): pesos y códigos del rebalanceo

- `sql/schema.sql`: mismos 66 pesos y 5 códigos Holland de `AIPROD2.4.0_R1_IN` para instalaciones frescas del panel (el sync los propaga a la app).

## Rebrand a Aevum Iter

- `package.json`: `aevum-iter-admin-panel`, `4.1.8-10`. `panelVersion`: `APPROD4.1.8_R16_IN`.
- Textos: servicio `aevum-iter-panel`, cookie `aevum_iter_admin`, login, dashboard, manifiesto PWA, SW (`aevum-admin-v1`), `db.js` y `schema.sql` (BD `aevum_iter`, URLs de carreras a `NULL`).
- Iconos: `icon-192/512.png`, `apple-touch-icon.png` y `public/img/app-logo.png` generados del logo brújula; `assets/aevum_logo.png` para el PDF.
- Eliminados assets institucionales (`tecnm_*`, `sep_*`, `escudo_*`, `cert_*`, `app_logo.png` anterior).
- `.env` con secretos heredados neutralizado (valores vacíos); `.env.example` con `AEVUM_ITER_API_KEY` y `DB_NAME=aevum_iter`.

## Paleta azul

- `public/styles.css` (60 reemplazos), gráficas Chart.js y toasts en `public/admin.js` (12), login y manifiesto: `#0262FC` / `#024AB8` / navy `#0A1F44`.

## Funciones retiradas (la app ya no las usa)

- `POST /api/catalog-suggestions`, `POST /api/admin/suggestions/:id/:action` y `GET /api/admin/suggestions`.
- Vista `Sugerencias` del dashboard + lógica JS (`bindSuggestionButtons`, `refreshSuggestions`, badge, handlers de socket).
- Payload `suggestions` fuera de `catalogAdminData` y `pendingSuggestions` fuera de `live-state`.
- Se conserva dormida la ruta de auto-registro de escuela en `POST /api/evaluations` y sus JOINs (sin UI; quitarla exigiría migración).

## Reporte PDF genérico (desde cero en forma)

- Nuevo encabezado (logo + `AEVUM ITER` + folio `AI-AAAAMMDD`) y pie (filete azul + paginación); fuera membretes TecNM/SEP, domicilios y certificaciones.
- Paleta azul, nombre `reporte-aevum-iter-*.pdf`, metadatos `Aevum Iter`.
- Se conserva la ingeniería: buffer en memoria, secciones por página, gráficas de barras, KPIs y tabla con rejilla.

## Verificación

- `node --check` en `src/server.js` y `src/db.js`.
- Arranque con BD de prueba (falla solo la conexión MySQL si no hay servidor, lo esperado).
- `/health` blindado: sin BD responde 503 JSON en vez de tumbar el proceso.
- Render EJS de `dashboard` y `login` probado con datos falsos.
- `flutter analyze` de la app: sin issues.

## ⏳ Pendiente próxima sesión (al indicar `continúa`)

Enfocarse en el panel web y verificar punto por punto:
- Misma paleta de la app Aevum Iter en todo lo visible (estilos, gráficas, login, PDF).
- Quitar gráfica e internamente lo que la app ya no usa (sugerencias fuera de UI; restan solo JOINs dormidos de ingesta en `server.js`).
- Reportes sin formato del Tec: encabezado y pie genéricos solo con el logo oficial de la app (`assets/aevum_logo.png`).
- Re-test completo con MySQL (schema listo) antes de físicos.
