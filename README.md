# AR-OS

AR-OS es el sistema operativo interno de AR-CHILE para gestionar el ciclo completo de investigación financiera documental y recuperación de acreencias:

**hallazgo → identidad → investigación → scoring → contacto → contrato → autorización → R3 → recuperación → honorarios → cierre**

## Stack inicial
- Frontend: React + Vite + TypeScript.
- Backend: Python + FastAPI.
- ORM: SQLAlchemy.
- Desarrollo local: SQLite.
- Producción objetivo: PostgreSQL.
- Documentos objetivo: Cloudflare R2.
- Correo objetivo: Zoho.
- Firma: proveedor externo por API.
- IA objetivo: OpenAI API.

## Seguridad
Este repositorio es público. No incluir datos reales de prospectos/clientes, claves, tokens, contratos firmados, correos privados ni documentos confidenciales.

## Desarrollo
La primera versión funcional está preparada como ZIP para ejecutarse localmente en Windows. El plan detallado está en `docs/ROADMAP.md`.

El prompt maestro para continuar con Codex está en `docs/CODEX_MASTER_PROMPT.md`.
