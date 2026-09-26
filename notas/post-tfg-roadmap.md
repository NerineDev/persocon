# Post-TFG Roadmap

> Estado: roadmap vivo de evolución del producto después del TFG.
>
> Este documento define el orden de trabajo provisional. Puede cambiar cuando la implementación, investigación, cumplimiento normativo o pruebas revelen una ruta mejor. Su objetivo es impedir que el proyecto vuelva a dispersarse entre mejoras aisladas.
>
> Para el alcance y las decisiones de producto, consultar también `producto-post-tfg.md`. Los documentos `roadmap.md`, `backlog.md` y `decisiones.md` conservan el contexto histórico del TFG/MVP.

## Objetivo

Convertir el MVP académico existente en un producto comercializable para profesionales autónomos y pequeños negocios de servicios, conservando la lógica funcional útil y evolucionando la experiencia hacia una herramienta ligera CRM/ERP-ish que conecte:

**clientes -> calendario/citas -> servicios -> comunicación -> pagos -> facturación -> automatización administrativa**

El objetivo no es construir un ERP completo ni rehacer desde cero una aplicación que ya funciona.

---

## Fase 0 — Proteger y documentar el baseline

**Objetivo:** asegurar que el TFG/MVP funcional permanezca recuperable antes de iniciar cambios amplios.

### Tareas

- Identificar el commit exacto actualmente desplegado.
- Verificar rama y estado actual del repositorio de aplicación.
- Crear un punto de recuperación claro del estado TFG/MVP conocido como funcional, mediante tag/branch según convenga.
- Crear una rama de evolución post-TFG cuando se decida la estrategia de ramas.
- Documentar las dependencias principales del despliegue actual: frontend, backend, PostgreSQL, Railway, variables/configuración y servicios externos relevantes.
- Verificar que el baseline puede arrancar y desplegarse sin depender de cambios posteriores.

### Criterio de salida

Existe un estado conocido y recuperable del MVP y se puede comenzar la evolución sin riesgo de perder la referencia funcional.

---

## Fase 1 — Rebranding e identidad de producto

**Objetivo:** definir la identidad del producto antes de reconstruir extensamente su interfaz.

### Tareas

- Decidir si `Sesvia` continúa como nombre o se sustituye.
- Definir posicionamiento y mensaje principal.
- Definir personalidad de marca.
- Definir dirección visual.
- Sustituir la dependencia de la estética terapéutica/terracota original por una identidad más generalista.
- Priorizar una interfaz predominantemente blanca, limpia y profesional, manteniendo calidez.
- Definir paleta, tipografía, iconografía y principios visuales.
- Preparar los primeros tokens del futuro sistema de diseño.

### Criterio de salida

Existe una identidad suficientemente definida para diseñar pantallas sin tomar decisiones visuales contradictorias en cada iteración.

---

## Fase 2 — Arquitectura UX e información

**Objetivo:** fijar cómo se organiza el producto antes de pedir a Bolt o a cualquier otra herramienta que reconstruya pantallas.

### Área profesional propuesta

- Inicio
- Calendario
- Clientes
- Servicios
- Facturación
- Mensajes
- Configuración

### Área cliente propuesta

- Inicio
- Explorar
- Citas
- Pagos y facturas
- Mensajes
- Configuración

### Tareas

- Crear mapa de pantallas y navegación.
- Definir relaciones entre cita, cliente, pago, factura y conversación.
- Aplicar el principio de **sin callejones sin salida**.
- Permitir varias rutas naturales hacia la misma información sin duplicar la lógica subyacente.
- Definir drawers/modales para consulta contextual sin abandonar tareas, especialmente desde Mensajes.
- Definir comportamiento responsive de navegación, paneles y detalles.
- Definir claramente el cambio de contexto para usuarios con rol cliente + profesional.

### Criterio de salida

La navegación y relaciones principales pueden explicarse sin depender del diseño visual de una pantalla concreta.

---

## Fase 3 — Fundación frontend y sistema de diseño

**Objetivo:** establecer el nuevo lenguaje visual y técnico sin intentar reconstruir toda la aplicación de una sola vez.

### Primer vertical slice recomendado

1. Shell/navegación profesional.
2. Inicio profesional.
3. Calendario.
4. Un drawer/modal de detalle contextual.

Este conjunto permite validar navegación, dashboard, datos densos, calendario, responsive y patrones de detalle antes de propagarlos.

### Tareas

- Implementar tokens de diseño.
- Crear componentes reutilizables para botones, inputs, filtros, tablas/listas, cards, badges, modales/drawers, navegación y estados.
- Definir loading, empty, error y success states.
- Validar escritorio grande, portátil, tablet y móvil.
- Mantener la lógica existente cuando sea correcta; no reescribir backend por motivos puramente estéticos.

### Criterio de salida

Existe un sistema visual reutilizable y un pequeño conjunto de pantallas representativas que funciona correctamente antes de migrar el resto.

---

## Fase 4 — Migración y pulido de áreas existentes

**Objetivo:** trasladar al nuevo sistema las funciones ya útiles antes de añadir grandes bloques nuevos.

### Prioridades

- Calendario existente y corrección de problemas responsive/scroll/contexto.
- Servicios.
- Facturación existente.
- Mensajes.
- Configuración profesional y cliente.
- Detalles de citas.

### Mejoras incluidas

- Acciones contextuales claras en citas.
- Navegación cruzada entre objetos relacionados.
- Mejor presentación de estados.
- Reorganización de settings.
- Carga real de logo/medios en lugar de URL manual cuando corresponda.
- Contexto de cita/cliente desde Mensajes.

### Criterio de salida

Las principales funciones heredadas pueden utilizarse dentro del nuevo producto sin depender de las pantallas TFG antiguas.

---

## Fase 5 — Rework de descubrimiento

**Objetivo:** sustituir el área más débil del MVP por una búsqueda útil para un catálogo generalista de profesionales y servicios.

### Tareas

- Búsqueda textual por necesidad, servicio y profesional.
- Mejorar relevancia para consultas no idénticas a categorías/filtros.
- Hacer que los filtros refinen la búsqueda en lugar de sustituirla.
- Filtro y ranking por idiomas de atención del profesional.
- Modalidad presencial / online / cualquiera.
- Geolocalización opcional con permiso explícito.
- Distancia/radio para servicios presenciales.
- Fallback manual estructurado por país/región/provincia/municipio cuando no se conceda ubicación.
- Considerar disponibilidad como señal/filtro útil.
- Mejorar cards de resultados para mostrar qué ofrece el profesional, modalidad, ubicación/distancia, precio cuando proceda y otra información necesaria para decidir.
- Diseñar estados sin resultados con alternativas útiles en lugar de dead ends.
- Investigar patrones de Booksy, Groupon y Wallapop como inspiración, sin copiar sus modelos o UI.

### Criterio de salida

Un cliente puede expresar razonablemente lo que busca y encontrar profesionales relevantes sin conocer previamente la taxonomía interna del producto.

---

## Fase 6 — CRM ligero: Clientes

**Objetivo:** convertir la relación con clientes en un objeto de primer nivel para el profesional.

### Tareas

- Crear sección `Clientes`.
- Búsqueda por nombre/email/teléfono y filtros útiles.
- Crear perfil de cliente.
- Mostrar historial de citas.
- Mostrar próxima/última cita.
- Mostrar servicios contratados.
- Mostrar pagos y facturas relacionadas.
- Acceso a mensajes.
- Acciones rápidas: nueva cita, mensaje y documentación relacionada.
- Mantener acceso al mismo cliente desde calendario, citas, facturación y mensajes.

### Criterio de salida

El profesional puede responder a preguntas como “¿qué pasó con María?” sin buscar primero a María dentro del calendario.

---

## Fase 7 — Calendario profesional ampliado

**Objetivo:** convertir el calendario en la vista operativa completa del tiempo profesional.

### Tareas

- Mantener reservas/citas.
- Mejorar bloques existentes.
- Añadir eventos personales/no reservables cuando corresponda.
- Añadir vacaciones/ausencias.
- Añadir controles para mostrar/ocultar citas, eventos personales, bloques y festivos.
- Renombrar la configuración recurrente a `Horario laboral y disponibilidad` o equivalente para evitar ambigüedad con Calendario.
- Diseñar infraestructura geográfica reutilizable para festivos.
- Evolucionar festivos nacionales hacia regionales/locales y overrides del profesional.

### Criterio de salida

El calendario representa de forma fiable cuándo puede y no puede trabajar el profesional, sin obligar a convertir todo compromiso en una reserva.

---

## Fase 8 — Servicios como oferta comercial

**Objetivo:** convertir los servicios existentes en listings atractivos y útiles para descubrimiento y conversión.

### Tareas

- Imagen de portada por servicio.
- Diseñar soporte para galería futura sin convertirla necesariamente en requisito inicial.
- Cards de gestión más compactas.
- Mejor vista pública del servicio.
- Mantener nombre, descripción, duración, precio, modalidad, ubicación y políticas.
- Separar visualmente configuración fiscal de la edición cotidiana cuando sea posible.
- Añadir traducción automática de contenido público.
- Conservar siempre el original.
- Permitir revisar/editar traducciones.
- Mantener separación estricta entre idioma del contenido e idioma en que el profesional puede prestar el servicio.

### Criterio de salida

Los servicios funcionan como ofertas comerciales presentables, no únicamente como registros administrativos.

---

## Fase 9 — Ciclo de vida completo de la cita

**Objetivo:** completar las operaciones que faltan para que una reserva sea gestionable de principio a fin.

### Tareas

- Implementar reprogramación real.
- Validar nueva disponibilidad y conflictos.
- Mantener historial de cambios.
- Integrar consecuencias sobre pagos/facturas cuando proceda.
- Pulir cancelación existente.
- Pulir reembolsos y políticas.
- Añadir notificaciones de cambios relevantes.
- Añadir acciones `Reprogramar`, `Mensaje`, `Ver cliente/profesional`, `Ver pago/factura` según estado y rol.

### Criterio de salida

Cliente y profesional pueden gestionar cambios normales de una cita sin soluciones manuales fuera del producto.

---

## Fase 10 — Reserva para otra persona / regalo

**Objetivo:** convertir la función existente de reservar para otra persona en un flujo completo de delegación/regalo.

### Tareas

- Diferenciar claramente `Para mí` y `Para otra persona`.
- Crear flujo de destinatario/invitación.
- Enviar acceso para reclamar/confirmar la reserva.
- No generar ni enviar contraseñas por email.
- Permitir reclamar mediante cuenta existente o creación/confirmación segura según diseño final.
- Mantener el email del destinatario como dato pendiente hasta confirmación de identidad.
- Definir quién recibe recordatorios de cita.
- Definir quién recibe factura/documentación financiera en caso de regalo.
- Añadir función de reenvío cuando corresponda.

### Criterio de salida

Una reserva para otra persona deja de ser solo un nombre/email alternativo y se convierte en una transferencia de contexto comprensible y segura.

---

## Fase 11 — Facturación operativa

**Objetivo:** hacer que el área financiera sea manejable con volumen real antes de añadir la capa final de cumplimiento.

### Tareas

- Buscar por cliente.
- Buscar por número/identificador de factura.
- Filtrar por fecha/rango.
- Presets: mes actual, mes anterior, trimestre y personalizado.
- Añadir filtros de estado/tipo cuando aporten valor.
- Enlazar factura -> cliente -> cita.
- Enlazar cliente -> facturas.
- Separar `Citas` de `Pagos y facturas` en cliente manteniendo enlaces cruzados.
- Revisar presentación de pagos manuales, pendientes, reembolsos y estados.

### Criterio de salida

La facturación deja de ser una lista creciente y se convierte en una herramienta de trabajo diaria.

---

## Fase 12 — Automatización de cobro

**Objetivo:** completar una de las propuestas de valor originales del producto: que el profesional no tenga que perseguir manualmente cada pago.

### Tareas

- Formalizar reglas de vencimiento por reserva/servicio/política.
- Recordatorios automáticos de pago pendiente.
- Configurar cadencia y evitar spam/repeticiones incorrectas.
- Definir la regla de cancelación por impago; dirección inicial: cancelación automática 24 horas antes cuando siga impagada, salvo reglas configuradas que indiquen otra cosa.
- Notificar al cliente y profesional cuando se acerque/aplique la cancelación.
- Liberar disponibilidad correctamente tras cancelación.
- Mantener coherencia reserva/pago/factura.
- Registrar auditoría/historial de automatizaciones relevantes.

### Criterio de salida

Una reserva impagada sigue un ciclo automático y visible sin que el profesional tenga que recordarlo manualmente.

---

## Fase 13 — VERI*FACTU y cumplimiento de facturación

**Objetivo:** convertir la facturación en una base comercial válida para el mercado español objetivo.

### Antes de implementar

- Realizar investigación específica con fuentes oficiales vigentes.
- Documentar requisitos técnicos y obligaciones aplicables.
- Determinar qué elementos del modelo de facturas existente pueden conservarse.
- Definir registros, trazabilidad, rectificación, QR/envío y demás requisitos aplicables según normativa vigente.
- Separar claramente cumplimiento verificado de supuestos de diseño.

### Implementación

Se realizará solo después de contar con una especificación técnica de cumplimiento suficientemente sólida. Bolt u otras herramientas generativas no deben improvisar esta arquitectura.

### Criterio de salida

La capa de facturación ha sido diseñada e implementada contra requisitos oficiales vigentes y validada antes de presentarse como compatible/conforme.

---

## Fase 14 — Dashboards y métricas finales de V1

**Objetivo:** completar el dashboard profesional CRM/business con datos ya estabilizados por las fases anteriores.

El diseño base de Inicio se trabaja desde las primeras fases; aquí se conectan y refinan métricas que dependan de Clientes, Billing y nuevos estados.

### Profesional

- Ingresos por periodo y evolución visual.
- Reservas/citas por periodo.
- Clientes activos/nuevos.
- Rendimiento por servicio.
- Pendientes de cobro.
- Acciones que requieren atención.
- Mensajes pendientes.
- Agenda del día.

### Cliente

- Próxima cita.
- Pagos/confirmaciones pendientes.
- Próximas y recientes citas.
- Mensajes relevantes.
- Acceso a descubrimiento.
- Evitar dashboards dominados por contadores vacíos cuando no existe actividad.

### Criterio de salida

El inicio profesional muestra salud del negocio + atención + agenda, y el inicio cliente prioriza contexto personal y acciones relevantes.

---

## Fase 15 — Administración mínima para operación real

**Objetivo:** ampliar admin únicamente hasta el punto necesario para operar los primeros usuarios reales.

### Tareas orientativas

- Verificación/gestión necesaria de profesionales.
- Soporte e incidencias.
- Consulta suficiente de usuarios/reservas/pagos cuando sea necesaria para asistencia.
- Herramientas mínimas para resolver estados anómalos de forma segura.
- Auditoría básica de acciones administrativas sensibles.

No convertir esta fase en un back-office empresarial completo.

---

## Fase 16 — Privacidad, seguridad y producción

**Objetivo:** pasar de producto funcional a producto en el que se puede confiar con datos, agenda, pagos y facturas reales.

### Tareas

- Revisión GDPR/privacidad.
- Revisión de cookies/almacenamiento y consentimiento cuando corresponda.
- Permisos de geolocalización y fallback manual.
- Seguridad de autenticación/autorización.
- Protección de datos entre roles.
- Revisión de subida de archivos/medios.
- Accesibilidad.
- Responsive completo.
- Emails transaccionales y fallos de entrega.
- Edge cases de pagos/reembolsos.
- Estados de error/reintento/idempotencia donde corresponda.
- Tests end-to-end de flujos críticos.
- Backup/restore.
- Logs, observabilidad y alertas suficientes para beta.
- Configuración de producción de proveedores externos.

### Criterio de salida

Los flujos críticos han sido probados de extremo a extremo y existen mecanismos razonables para detectar, diagnosticar y recuperar fallos.

---

## Fase 17 — Beta controlada y lanzamiento

**Objetivo:** validar el producto con usuarios reales antes de ampliar exposición.

### Tareas

- Seleccionar pequeño grupo de profesionales/pymes de servicios.
- Preparar onboarding y soporte.
- Medir fricción real en configuración, descubrimiento, reservas, cobros y facturación.
- Registrar incidencias y solicitudes sin convertir automáticamente cada petición en roadmap.
- Corregir bloqueantes y problemas de confianza/usabilidad.
- Validar costes de infraestructura y servicios externos.
- Definir condiciones para ampliar la beta o lanzar públicamente.

---

# Orden resumido

1. Proteger baseline.
2. Rebranding.
3. Arquitectura UX/IA.
4. Fundación frontend/design system.
5. Migrar y pulir funcionalidad existente.
6. Rehacer descubrimiento.
7. Crear CRM de Clientes.
8. Ampliar Calendario.
9. Mejorar Servicios.
10. Completar ciclo de cita.
11. Completar reserva para terceros/regalo.
12. Hacer Facturación operativa.
13. Automatizar cobros e impagos.
14. Implementar VERI*FACTU con especificación dedicada.
15. Completar métricas/dashboard V1.
16. Admin mínimo.
17. Hardening de producción.
18. Beta controlada/lanzamiento.

---

# Reglas para mantener este roadmap útil

- Este roadmap es **provisional, no sagrado**.
- Cambiar el orden está permitido cuando exista una razón técnica o de producto documentable.
- No iniciar una reconstrucción completa si una capa existente puede evolucionarse con seguridad.
- No añadir grandes features nuevas a V1 sin identificar qué problema comercial o de lanzamiento resuelven.
- Las mejoras visuales pueden avanzar junto a fases funcionales cuando reduzcan retrabajo.
- Las dependencias legales/fiscales se verifican con fuentes oficiales antes de implementación.
- Cada fase debe terminar con software comprobable o documentación accionable, no solo con ideas.
- `producto-post-tfg.md` define principalmente **qué** queremos construir; este archivo define principalmente **en qué orden** intentaremos hacerlo.
