<div align="center">
  <img src="public/img/app-logo.png" alt="Aevum Iter" width="140"/>

  # Panel Aevum Iter APPROD4.1.8_R10_IN

  **Administración de orientación vocacional** — catálogos versionados, resultados en vivo y reportes PDF genéricos.

  [![release](https://img.shields.io/badge/release-APPROD4.1.8__R10__IN-0262FC?style=for-the-badge)](README_VERSION_4.1.8.md)
  [![node](https://img.shields.io/badge/Node.js-Express_4-339933?style=for-the-badge&logo=node.js&logoColor=white)](src/server.js)
  [![mysql](https://img.shields.io/badge/MySQL_MariaDB-utf8mb4-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](sql/schema.sql)
  [![realtime](https://img.shields.io/badge/Tiempo_real-Socket.IO-010101?style=for-the-badge&logo=socket.io&logoColor=white)](src/server.js)
  [![pwa](https://img.shields.io/badge/PWA-instalable-5A0FC8?style=for-the-badge)](public/manifest.json)
</div>

---

## Qué hace

| Área | Función |
|---|---|
| 📊 Dashboard | KPIs, gráficas (carreras, Holland, afinidad, procedencia, escuelas, lenguas), tabla de evaluaciones con respuestas abiertas |
| 🗂️ Catálogos | CRUD de estados, municipios, escuelas, lenguas, carreras, preguntas y pregunta por departamento |
| 🔌 API app | `/health`, `/api/catalogs`, `/api/catalog-version`, `/api/evaluations` (Bearer `API_INGEST_KEY`) |
| 📄 Reportes | PDF genérico Aevum Iter con KPIs, gráficas de barras y tabla de evaluaciones |
| ⚡ Vivo | Socket.IO: nuevas evaluaciones y cambios de catálogo sin recargar |

## Instalación

```bash
mysql -u root -p < sql/schema.sql
cp .env.example .env   # edita credenciales (nunca subir .env)
npm install
npm start
```

Panel en `http://localhost:8080` · Salud en `GET /health`.
La key de ingesta debe coincidir con `AEVUM_ITER_API_KEY` al compilar la app.

## 🔢 Versionado

Esquema estilo ZZZ: siglas+canal pegados, versión y revisiones con guion bajo — `APPROD4.1.8_R10_IN`:

| Parte | Significado |
|---|---|
| `AP` | Admin Panel (fijo, pegado) |
| `PROD` | Canal presentación comercial / producción |
| `4` | Número de versión |
| `1` | Actualizaciones mayores |
| `8` | Actualizaciones medianas |
| `_R9` | Revisión |
| `_IN` | Rama Innovatec |

## 📜 Historial de versiones

| Versión | Cambios (general) | Detalle |
|---|---|---|
| [APPROD4.1.8_R10_IN](README_VERSION_4.1.8.md) | Rebrand total + pesos y códigos del rebalanceo RIASEC | [Ver detalle](README_VERSION_4.1.8.md) |

---

<div align="center">
  <sub>Panel Aevum Iter APPROD4.1.8_R10_IN · Rama Innovatec</sub>
</div>
