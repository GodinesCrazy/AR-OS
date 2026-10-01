# AR-OS — verificación de vigencia y rapidez hasta el cobro

> Este repositorio es público. Esta especificación **no contiene expedientes reales**. Las decisiones sobre fondos de terceros deben fundarse en autorización y respuestas institucionales, nunca en inferencias generadas por IA.

## 1. Regla central de evidencia

- Un hallazgo del Diario Oficial/CMF confirma **publicación histórica** (R1), no dinero vigente. El buscador CMF se actualiza anualmente y advierte que las acreencias pueden haber sido cobradas.
- R2: identidad del beneficiario y poderes documentados. R2.5: investigación pública complementaria posterior; **no** significa saldo confirmado.
- R3: respuesta **individual** del banco, posterior a una solicitud autorizada, con instrumento, identidad, resultado pendiente/cobrado/parcial/caducado, saldo y **fecha de estado**. La respuesta debe conservar referencia y PDF original o registro institucional verificable.
- Distinguir `observed_on` (fecha de descarga) de `effective_on` (fecha a la que se refiere el dato). Descargar hoy una nómina de 2026 no actualiza el saldo a hoy.
- Una negativa por secreto, error de búsqueda, portal caído o ausencia de publicación posterior implica `UNKNOWN`, nunca `PAID` ni `ACTIVE`.
- Cada vale vista se evalúa como activo individual: R3 de uno **no** crea R3 para otros del mismo titular. Evitar unir razón social similar, RUT parcialmente enmascarado y domicilios históricos sin conciliación humana.

Referencias: [Buscador CMF](https://acreencias.cmfchile.cl/); [Secreto bancario CMF](https://www.cmfchile.cl/educa/621/w3-article-27149.html); [Art. 156 LGB](https://nuevo.leychile.cl/navegar?idNorma=83135).

## 2. Máquina de estados y controles

Estados de instrumento: `HISTORICAL` → `R2_IDENTITY` → `R2_5_PUBLIC_CHECK` → `BANK_VERIFIED_PENDING/PARTIAL/COLLECTED/EXPIRED` y `BANK_CONFLICT`. Última respuesta bancaria válida tiene prioridad sobre indicios públicos. Si respuestas bancarias autenticadas contradicen al mismo corte, exigir revisión humana. Parametrizar alerta de revalidación bancaria (por defecto sugerido, siete días para uso operativo; **no es un plazo legal**). Exponer siempre `balance_as_of`, nunca presentar `historical_amount` como `confirmed_amount`.

Dos puertas distintas:

1. **PRECONTACT:** publicación R1 + R2 + persona autorizada identificada + canal corporativo corroborado + no oposición. **No exigir R3**, porque se obtiene tras contratar al cliente/obtener mandato. Primer contacto sin detalles confidenciales ni afirmación de saldo actual.
2. **R3/RECUPERACIÓN:** transparencia de la oferta; acuerdo de prestación y honorarios + confidencialidad, autorización específica del titular para consulta, respuesta bancaria auténtica, mandato/poder que el banco acepte y abono **directo al cliente**. AR-CHILE no custodia fondos; nunca solicita claves bancarias, OTP ni ClaveÚnica.

Si un instrumento se confirma cobrado o extinguido, retirar ese instrumento de la cola comercial de pendientes, sin descartar otros independientes.

BCI tiene procedimiento publicado de revisión de poderes de SpA y estatuto actualizado para Empresa en un Día: [Servicio al cliente Empresas BCI](https://www.bci.cl/empresas/servicio-al-cliente). Los tiempos orientativos de revisión legal del banco no equivalen a confirmación de saldos ni garantía de cobro.

## 3. Métrica adecuada: tiempo hasta comisión efectivamente recibida

Priorizar por **siguiente acción que acerca a recaudar honorarios**, no solo por monto nominal:

`factura de honorarios pendiente de cobro → pago bancario al cliente en curso → expediente R3 positivo y contrato firmado → mandato listo para consulta R3 → contacto corporativo listo para contrato → investigación de identidad/contacto → hallazgo sin identificación`.

Recolectar tiempos reales de transición, costos por caso, comisión contractual y recibo de pago. Hasta tener datos suficientes, mostrar **prioridad heurística**, no porcentaje ficticio de probabilidad de comisión. Cuando existan resultados históricos, evaluar calibración y pruebas fuera de muestra, con segmentación por banco/instrumento.

## 4. Variables, UI y auditoría

- `claims`: `id`, `beneficiary_id`, `bank_id`, `publication_source_id`, `publication_cutoff`, `historical_amount`, `state`, `current_confirmed_amount NULL`, `balance_as_of NULL`.
- `evidences`: `claim_id`, `kind`, `source_id`, `sha256`, `observed_on`, `effective_on`, `authenticated_by`, `authorization_id`, `bank_status`; archivos sensibles en almacenamiento privado.
- `commercial`: `corporate_contact_verified_on`, `contact_opt_out`, `agreement_signed_on`, `nda_signed_on`, `mandate_signed_on`, `bank_fiscalia_approved_on`, `client_settlement_on`, `invoice_issued_on`, `commission_received_on`.
- Vista de casos: columnas separadas *monto histórico* / *saldo confirmado al [fecha]* / *estado desconocido* / *bloqueador* / *próxima acción*.
- Alertas por tarea y por caducidad legal; verificar individualmente fecha de confección de lista y eventuales excepciones del art. 156. Nunca confundir límites del cobro por web con extinción de la acreencia.
- Control de acceso RBAC/MFA; la IA no puede validar por sí misma la autenticidad de una carta bancaria. Los booleanos internos de autenticación/autorización solo los marca un revisor o conector fiable, **nunca** una petición de API del usuario sin verificar.

## 5. Criterios de aceptación

Pruebas sintéticas obligatorias:

1. Publicación anual CMF reconsultada hoy no produce R3.
2. Respuesta de un banco distinto o sin mandato no produce R3.
3. Uno de varios instrumentos confirmado no confirma el resto.
4. Respuesta bancaria cobrados/caducados cierra la oferta de ese instrumento.
5. Respuestas bancarias de igual fecha contradictorias bloquean.
6. Confirmación obsoleta exige revalidación; no se presenta como actual.
7. R2 con contacto verificado permite *oferta inicial*, sin exigir R3.
8. Sin acuerdo firmado no se revelan referencias o montos específicos ni se gestiona la consulta bancaria.
9. Sin abono comprobado del cliente y pago de honorarios comprobado no se marca comisión recibida.
10. Todas las pruebas existentes y migraciones SQLite siguen funcionando.

**Integración pendiente:** el remoto contiene actualmente especificaciones y no el código de la app que corre en `C:\AR-OS`. Integrar en ese proyecto local mediante Codex tras inspeccionar migraciones y modelo real, sin sobreescribir la base de datos de producción. No subir jamás expedientes reales a este repositorio público.
