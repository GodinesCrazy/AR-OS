# Prompt maestro para Codex VS Code

Estás trabajando en el repositorio **AR-OS**.

RUTA LOCAL:
`C:\AR-OS`

REPOSITORIO:
`https://github.com/GodinesCrazy/AR-OS.git`

OBJETIVO:
AR-OS es el sistema operativo interno de AR-CHILE. Debe automatizar y documentar el ciclo:
HALLAZGO → IDENTIDAD → INVESTIGACIÓN → SCORING → CONTACTO → CONTRATO → AUTORIZACIÓN → R3 → RECUPERACIÓN → HONORARIOS → CIERRE.

PRINCIPIOS:
1. Una publicación histórica NO equivale a acreencia vigente.
2. R1 = hallazgo; R2 = identidad/continuidad; R2.5 = revisión pública complementaria; R3 = estado actual confirmado.
3. No presentar R1/R2/R2.5 como vigencia actual.
4. Toda afirmación material debe conservar fuente y fecha.
5. No solicitar ni almacenar claves bancarias, ClaveÚnica ni códigos.
6. AR-CHILE no custodia fondos.
7. Mantener auditoría.
8. Secretos solo por variables de entorno.
9. El repositorio es público: nunca subir datos reales de prospectos/clientes.
10. Para producción, autenticación, MFA y roles son obligatorios.

STACK:
React/Vite/TypeScript + FastAPI/Python + SQLAlchemy + SQLite dev/PostgreSQL prod.

SCORING 100:
monto 25; identidad 20; contacto 15; recencia 15; evidencia 10; atractivo comercial 10; baja complejidad 5.
A1 >=80; A2 70–79.99; B 55–69.99; C <55.
Valor esperado = honorario potencial × probabilidad operativa.

ANTES DE MODIFICAR:
- leer README.md;
- leer docs/PRODUCT_SPEC.md;
- leer docs/ROADMAP.md;
- inspeccionar código;
- preservar compatibilidad Windows;
- crear tests.

PRIMER OBJETIVO:
Implementar Fase 1:
A) importador del Excel AR-CHILE;
B) separar Empresa de Acreencia;
C) tabla Sources/Evidence;
D) Contacts y Tasks;
E) dashboard valor esperado/esfuerzo;
F) ficha expediente con pestañas Investigación | Acreencias | Fuentes | Contactos | Documentos | Comunicaciones | Actividad;
G) tests de scoring/API;
H) usar solo datos demo sintéticos en Git.

No avanzar aún a firma real, envío real de correo u OpenAI hasta probar bien el núcleo.
