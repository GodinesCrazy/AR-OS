# AR-OS · Especificación funcional

AR-OS debe ejecutar y documentar la mayor parte del ciclo operativo de AR-CHILE:

**hallazgo → identidad → investigación → scoring → contacto → contrato → autorización → R3 → recuperación → honorarios → cierre**

## Validación
- R1: publicación/hallazgo confirmado.
- R2: identidad y continuidad verificadas.
- R2.5: revisión pública complementaria sin confirmación actual.
- R3: estado actual confirmado con evidencia suficiente.

## Scoring (100)
- Monto/materialidad: 25.
- Identidad/continuidad: 20.
- Contactabilidad: 15.
- Recencia/revalidabilidad: 15.
- Calidad documental: 10.
- Atractivo comercial: 10.
- Baja complejidad: 5.

Prioridad: A1 >=80; A2 70–79.99; B 55–69.99; C <55.

## Seguridad
- No solicitar claves bancarias, ClaveÚnica ni códigos.
- No custodiar fondos.
- Mantener trazabilidad de fuente.
- No usar datos reales en el repositorio público.
- Exigir MFA/RBAC antes de producción.
