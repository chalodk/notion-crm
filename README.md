# Guía de instalación — Notion CRM

## Requisitos previos

- [Claude Code](https://claude.com/claude-code) instalado
- Node.js (v18+) para el MCP de Google Drive
- Cuenta de Notion con acceso al workspace de Agroanalytics
- Acceso al Shared Drive "Agroanalytics" en Google Drive

## Paso 1 — Clonar el repo

```bash
git clone https://github.com/chalodk/notion-crm.git
cd notion-crm
```

## Paso 2 — Obtener token de Notion

1. Ir a https://www.notion.so/profile/integrations
2. Click **"Nueva integración"** (o "New integration")
3. Nombre: `CRM Agroanalytics`
4. Workspace: elegir el de Agroanalytics
5. Copiar el token (empieza con `ntn_...`)

## Paso 3 — Configurar `.env` y `.mcp.json`

Crear `.env`:

```
NOTION_TOKEN="ntn_tu_token_aqui"
```

Crear `.mcp.json` copiando el template:

```bash
cp .mcp.json.example .mcp.json
```

Editar `.mcp.json` y reemplazar:
- `NOTION_TOKEN` por el token real
- La ruta de `gdrive` → `args` por la ubicación real de `run-mcp.cjs` en su máquina

> `.env` y `.mcp.json` ya están en `.gitignore`. Nunca se commitean.

## Paso 4 — Configurar Google Drive MCP

Seguir la guía en `references/notion-mcp-setup.md` para instalar y autenticar el servidor MCP de Google Drive.

## Paso 5 — Dar permisos a la integración en Notion

1. Ir a la base de datos **"CRM - Agroanalytics"** en Notion
2. Click en `...` (arriba derecha) → **Conexiones** → **Agregar conexión**
3. Seleccionar **"CRM Agroanalytics"** (la integración del Paso 2)
4. Repetir para la base de datos **"Clientes"**

## Paso 6 — Ejecutar setup

Dentro de la carpeta `notion-crm`, abrir Claude Code y escribir:

```
setup
```

Esto ejecuta el cuestionario de onboarding (token, pipeline, moneda) y verifica la conexión MCP.

## Paso 7 — Usar el CRM

Una vez completado el setup, escribir en lenguaje natural. Ejemplos:

- _"Cuántos deals hay en etapa Proposal?"_
- _"Agregá un nuevo deal: Frusan, 120 UF, contacto juan@frusan.cl"_
- _"Pasá el deal de Diagnofruit LIMS a Negotiation"_
- _"Mostrame el pipeline completo"_
- _"Creá una actividad de seguimiento para Granotec mañana"_

## Paso 8 — Mantener actualizado

```bash
git pull origin main
```

Las mejoras al workspace (nuevos patterns, fixes) se publican en el repo.

---

Si algo falla en el Paso 5 o 6, revisar `references/notion-mcp-setup.md` para diagnóstico detallado.
