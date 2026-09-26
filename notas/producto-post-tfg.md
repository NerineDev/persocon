# Producto post-TFG: visión y alcance

> Estado: documento de consolidación posterior al TFG.
>
> Este documento no reescribe el alcance académico ni afirma que las mejoras descritas estuvieran implementadas durante la entrega. Resume la dirección de producto decidida después del TFG a partir del MVP existente y de la revisión funcional/UX posterior.

## 1. Qué es el producto

La plataforma evoluciona desde un gestor de citas nacido de un caso terapéutico hacia una herramienta ligera de gestión de negocio para profesionales autónomos y pequeños negocios de servicios.

El objetivo no es competir como ERP completo ni limitarse a ser un marketplace de reservas. El producto combina una capa CRM y una capa operativa/administrativa acotada alrededor del ciclo de vida de un servicio:

**descubrimiento -> reserva -> pago -> seguimiento -> prestación/cita -> facturación -> relación con el cliente**

La propuesta para el profesional es reducir el trabajo administrativo alrededor de sus servicios y centralizar calendario, clientes, cobros, facturas y comunicación. Para el cliente, la propuesta es facilitar el descubrimiento de profesionales, la reserva, el pago, la comunicación y la gestión posterior de sus citas y documentos.

### 1.1 Público objetivo

- Profesionales autónomos que venden tiempo o servicios reservables.
- Pequeños negocios de servicios con operativa similar.
- No se limita a salud o terapia.
- No pretende cubrir inventario, compras, proveedores, nóminas, RR. HH., contabilidad general, fabricación u otras áreas propias de un ERP completo.

### 1.2 Principios de producto

1. **Menos administración para el profesional.** La reserva es el inicio del flujo, no el producto completo.
2. **CRM-ERP ligero.** Clientes, agenda, servicios, pagos y facturación conectados sin complejidad empresarial innecesaria.
3. **Sin callejones sin salida.** Un mismo objeto debe ser accesible desde los contextos donde resulte natural: cita, cliente, factura, pago o conversación.
4. **Redundancia útil.** Se permiten varias rutas hacia la misma información para evitar que el usuario tenga que memorizar una única navegación correcta.
5. **Mantener la lógica que ya funciona.** El MVP existente sirve como base; el objetivo es evolucionarlo, no reconstruirlo por defecto.
6. **Automatizar sin ocultar el estado.** El sistema puede recordar, cobrar, cancelar o generar documentación según reglas, pero debe mostrar claramente qué está ocurriendo y por qué.
7. **Diseño para pequeños negocios.** La interfaz debe ser comprensible sin formación especializada.

## 2. Estado heredado del TFG

El MVP ya dispone de una base funcional importante: autenticación y roles, perfil profesional, servicios, disponibilidad, exploración pública, reservas, pagos, facturación, mensajería, soporte y frontend SPA.

La revisión post-TFG concluye que la principal debilidad general no es la ausencia del producto base, sino una interfaz funcional pero poco pulida, una arquitectura de información demasiado centrada en reservas y varias operaciones incompletas para uso comercial real.

### 2.1 Áreas a conservar como base

- Autenticación, identidad y roles.
- Perfil profesional y datos privados de facturación separados.
- Servicios y modalidades de servicio.
- Agenda recurrente, reservas y cálculo de disponibilidad.
- Pagos y relación pago-reserva-factura.
- Facturación existente como base, manteniendo trazabilidad.
- Mensajería cliente-profesional y soporte.
- Cancelación/reembolso existente como base para ampliar y pulir.
- Idiomas del profesional.
- Modalidades `online`, `in_person` e híbrida.
- Festivos nacionales y bloques de disponibilidad como base del calendario ampliado.

## 3. Arquitectura de información objetivo

### 3.1 Área profesional

Navegación principal propuesta:

- **Inicio**
- **Calendario**
- **Clientes**
- **Servicios**
- **Facturación**
- **Mensajes**
- **Configuración**

`Calendario` representa todo lo que ocupa o condiciona el tiempo profesional. La configuración de horarios recurrentes debe denominarse de forma más explícita, por ejemplo **Horario laboral y disponibilidad**, para evitar confundirla con el calendario operativo.

### 3.2 Área cliente

Navegación conceptual:

- **Inicio**
- **Explorar**
- **Citas**
- **Pagos y facturas**
- **Mensajes**
- **Configuración**

Citas y documentos financieros se separan como espacios propios, pero mantienen enlaces bidireccionales para que el usuario pueda pasar de una cita a su pago/factura y de una factura a la cita relacionada.

### 3.3 Usuarios con doble rol

Una misma identidad puede actuar como cliente y profesional. Debe existir un cambio de contexto claro sin crear dos identidades independientes ni duplicar datos de cuenta innecesariamente.

## 4. Inicio profesional: enfoque CRM y pulso de negocio

El inicio profesional debe evolucionar desde contadores de estados hacia un dashboard operativo y comercial ligero.

Debe responder rápidamente a tres preguntas:

1. **¿Cómo va mi negocio?**
2. **¿Qué necesita mi atención?**
3. **¿Qué tengo hoy/próximamente?**

### 4.1 Información deseada

- Ingresos por periodo y evolución visual.
- Reservas/citas por periodo y estado.
- Clientes activos y clientes nuevos.
- Rendimiento básico por servicio: reservas e ingresos.
- Pagos pendientes o vencidos.
- Mensajes sin leer o asuntos pendientes.
- Agenda del día.

Las analíticas avanzadas pueden evolucionar posteriormente; V1 debe priorizar indicadores accionables y comprensibles para pequeños negocios.

## 5. Clientes como área de primer nivel

El profesional debe poder buscar clientes directamente sin tener que localizarlos primero en un calendario o una reserva.

### 5.1 Directorio de clientes

Búsqueda por datos relevantes como nombre, email o teléfono y filtros útiles a medida que aumente el volumen.

### 5.2 Perfil de cliente

Debe reunir, según permisos y datos disponibles:

- Datos básicos de contacto.
- Próxima cita y última cita.
- Historial de citas y cancelaciones.
- Servicios contratados.
- Pagos y estado de cobro.
- Facturas asociadas.
- Acceso a conversación/mensajes.
- Notas internas del profesional cuando se implemente.
- Acciones directas: nueva cita, mensaje y acceso a documentación financiera.

La información no se duplica conceptualmente: el perfil de cliente ofrece otra entrada a reservas, pagos, facturas y mensajes existentes.

## 6. Calendario y disponibilidad

El calendario debe mantener citas de clientes y ampliar la gestión de tiempo profesional.

### 6.1 Tipos de elementos

- Citas/reservas.
- Bloques de indisponibilidad.
- Eventos personales u otros compromisos no asociados a reservas.
- Vacaciones/ausencias.
- Festivos y cierres.

La vista debe permitir mostrar u ocultar categorías, especialmente elementos personales.

### 6.2 Comportamiento responsive

La revisión detectó una experiencia incómoda en resoluciones de portátil: determinadas acciones del calendario desplazan la vista mientras el resultado aparece fuera del área visible. El rediseño debe garantizar que el feedback de una acción quede visible y que paneles/detalles se adapten correctamente a anchos inferiores a escritorio grande.

### 6.3 Festivos

La implementación actual de festivos nacionales debe evolucionar para contemplar calendarios regionales y locales cuando proceda.

No se recomienda convertir la base principal en un catálogo manual gigantesco de festivos. La arquitectura deberá permitir asociar calendarios oficiales a niveles geográficos y aplicar excepciones/overrides del profesional, incluyendo la posibilidad de trabajar un festivo concreto.

## 7. Reservas, reprogramación y cancelación

La reserva actual es una base funcional, pero la gestión comercial debe completarse.

### 7.1 Detalle de cita

Además de la información de estado, debe ofrecer acciones contextuales claras, por ejemplo:

- Reprogramar.
- Cancelar según política.
- Ver cliente/profesional.
- Enviar mensaje.
- Ver pago.
- Ver factura/documentación relacionada.

### 7.2 Reprogramación

La reprogramación completa es requisito de producto antes de comercialización. Debe respetar disponibilidad, historial, pagos, políticas y notificaciones relacionadas.

### 7.3 Cancelaciones y reembolsos

La base existente debe conservarse y ampliarse/pulirse. El objetivo es que las reglas, consecuencias financieras y notificaciones sean comprensibles para ambas partes.

## 8. Pagos y automatización de cobro

El producto debe gestionar el ciclo de cobro alrededor de la reserva, no limitarse a registrar un pago.

### 8.1 Objetivo V1 comercial

- Estado de pago claramente visible.
- Solicitud/cobro según el flujo elegido.
- Recordatorios automáticos a clientes con pagos pendientes.
- Reglas de vencimiento.
- Cancelación automática de reservas que sigan impagadas antes del límite configurado; la dirección actual contempla especialmente la cancelación 24 horas antes cuando siga pendiente.
- Notificaciones claras a las partes afectadas.
- Coherencia entre estado de reserva, pago y factura.

Las reglas exactas deberán formalizarse antes de implementación para evitar ambigüedades entre servicios, políticas y métodos de pago.

## 9. Facturación y cumplimiento

La facturación deja de considerarse una función secundaria. Es parte central de la propuesta para autónomos y pequeños negocios.

### 9.1 Mejoras de uso

La vista profesional debe permitir como mínimo:

- Buscar por cliente.
- Buscar por número/identificador de factura.
- Filtrar por fecha o rango.
- Presets temporales útiles, por ejemplo mes actual, mes anterior, trimestre y rango personalizado.
- Filtros adicionales cuando los estados/tipos lo justifiquen.
- Acceder al perfil del cliente desde la factura.
- Acceder a facturas desde el perfil del cliente.

La vista cliente debe separar **Citas** de **Pagos y facturas**, manteniendo enlaces cruzados entre ambos.

### 9.2 VERI*FACTU

La evolución comercial para España debe diseñar la facturación con cumplimiento VERI*FACTU desde el principio de esta nueva etapa, en lugar de añadirlo como parche posterior.

La implementación existente de facturas y trazabilidad es una base, pero no debe darse por equivalente a cumplimiento VERI*FACTU. Antes de implementar esta capa se requiere una especificación técnica y de cumplimiento dedicada y verificada contra requisitos oficiales vigentes.

## 10. Servicios profesionales

Los servicios deben evolucionar de registros funcionales a presentaciones comerciales útiles tanto para gestión como para descubrimiento.

### 10.1 Contenido

- Imagen de portada por servicio como requisito de evolución.
- Posible galería en evolución posterior.
- Nombre.
- Resumen y descripción completa.
- Precio.
- Duración.
- Modalidad.
- Ubicación cuando corresponda.
- Condiciones/política de cancelación.
- Estado activo/inactivo.
- Configuración fiscal, presentada de forma comprensible y sin dominar la edición ordinaria del servicio.

### 10.2 Traducción

Se desea traducción automática del contenido público de los servicios, conservando siempre el texto original y permitiendo al profesional revisar/editar las traducciones.

La traducción de contenido **no implica** que el profesional pueda prestar el servicio en ese idioma.

## 11. Idiomas del profesional

Los idiomas del perfil profesional representan idiomas en los que el profesional puede atender al cliente y deben convertirse en un criterio real de descubrimiento.

- El onboarding/configuración debe preguntar claramente en qué idiomas puede prestar sus servicios.
- El perfil público debe mostrarlos de forma visible.
- El cliente debe poder filtrar profesionales por idioma.
- El idioma preferido del cliente puede ayudar a priorizar resultados, pero no debe ocultar silenciosamente otras opciones salvo que el cliente aplique un filtro excluyente.

## 12. Descubrimiento y búsqueda

La exploración pública requiere un rediseño importante. Los filtros actuales no deben ser la única forma de encontrar un profesional.

### 12.1 Objetivo de búsqueda

El usuario debe poder escribir lo que necesita en lenguaje natural o términos habituales y obtener resultados relevantes por profesional o servicio.

La búsqueda podrá combinar señales como:

- Relevancia del texto/intención.
- Servicio y contenido del servicio.
- Ubicación/distancia para servicios presenciales.
- Idioma del profesional.
- Modalidad online/presencial/híbrida.
- Disponibilidad.

Los filtros refinan los resultados; no sustituyen a la búsqueda.

### 12.2 Modalidad

El cliente debe poder buscar:

- Presencial.
- Online.
- Cualquiera.

Para servicios online la distancia pierde importancia; para servicios presenciales puede convertirse en señal y filtro principal.

### 12.3 Ubicación y permisos

Con permiso explícito de geolocalización, la búsqueda presencial podrá usar distancia y radio.

Si el usuario no concede ubicación, el producto debe seguir siendo plenamente utilizable mediante selección manual estructurada, por ejemplo:

**país -> comunidad/región -> provincia -> municipio/ciudad**

La geografía debe diseñarse como infraestructura reutilizable para búsqueda, ubicación profesional y calendarios de festivos, evitando sistemas incompatibles para cada función.

### 12.4 Inspiración de producto

En una fase posterior de diseño se estudiarán patrones de productos como Booksy, Groupon y Wallapop para comprender buenas prácticas de descubrimiento, categorías, ubicación, filtros y presentación de resultados. El objetivo es inspirarse en patrones útiles, no replicar sus modelos de negocio ni interfaces.

## 13. Reservar para otra persona / regalo

La opción actual de reservar para otra persona debe convertirse en un flujo explícito y cuidado.

Dirección conceptual:

1. El comprador/reservante elige reservar para sí o para otra persona.
2. Si es para otra persona, se registran los datos necesarios del destinatario.
3. El destinatario recibe una invitación para reclamar/confirmar el acceso.
4. No se envían contraseñas generadas por email; el destinatario establece sus propias credenciales o usa un mecanismo de autenticación permitido.
5. El email introducido para el destinatario se trata inicialmente como dato de invitación/reserva y no como identidad canónica plenamente confirmada hasta la aceptación.
6. Debe definirse expresamente quién recibe comunicaciones de cita y quién recibe documentación financiera, especialmente en casos de regalo.

## 14. Mensajería y contexto

La mensajería existente se conserva como base. No se exige chat de tiempo real estricto para V1 si la experiencia actual sigue siendo suficientemente rápida y fiable.

Debe mejorarse el contexto:

- Mostrar quién es la persona y permitir acceder a su perfil cuando proceda.
- Mostrar el servicio/cita relacionada de forma comprensible, no solo un ID técnico.
- Permitir previsualizar la cita en modal/drawer sin abandonar la conversación.
- Mantener enlace a la vista completa.
- Aplicar un patrón equivalente a tickets de soporte cuando exista contexto relacionado.

## 15. Configuración

La configuración requiere un rediseño antes de comercialización aunque la lógica actual permita operar el MVP.

### 15.1 Profesional

Agrupación conceptual posible:

- Perfil público.
- Negocio.
- Horario laboral y disponibilidad.
- Pagos.
- Facturación e impuestos.
- Notificaciones.
- Cuenta y seguridad.

Los archivos visuales como logotipo deben subirse mediante una experiencia de carga de archivo, no exigir al usuario una URL externa.

### 15.2 Cliente

La configuración cliente puede ser más sencilla, centrada en:

- Perfil y datos personales.
- Idioma/preferencias.
- Notificaciones.
- Cuenta y seguridad.

## 16. Inicio cliente

No se busca convertir el inicio cliente en un dashboard analítico. Debe ser un panel personal sencillo y útil.

Prioridades:

- Próxima cita cuando exista.
- Acciones pendientes, especialmente pagos o confirmaciones.
- Próximas/recientes citas.
- Mensajes relevantes.
- Acceso claro a explorar profesionales.

Cuando no exista actividad, el espacio puede favorecer descubrimiento en lugar de mostrar contadores vacíos.

## 17. Administración

El panel administrativo actual es limitado. Su ampliación completa no es prioridad inmediata.

Antes de comercialización debe cubrir suficientemente las tareas necesarias para operar, verificar, asistir y resolver incidencias de los primeros usuarios. Las funciones avanzadas pueden quedar posteriores al V1 comercial.

## 18. Rebranding y diseño

Toda la interfaz requiere al menos un pase de pulido visual. La dirección preliminar es abandonar la dependencia de la paleta tierra/terapéutica original y evolucionar hacia una interfaz más blanca, limpia y generalista, manteniendo calidez y confianza.

El nombre `Sesvia` no se considera definitivo ni descartado en este documento. El naming y la identidad visual se decidirán en una fase específica antes de una reconstrucción extensa del frontend.

La reimplementación visual debe preservar funcionalidad probada y no utilizar el rebranding como excusa para reescribir lógica estable sin necesidad.

## 19. Privacidad, ubicación y almacenamiento

La futura búsqueda geolocalizada requiere consentimiento de ubicación cuando se use ubicación del dispositivo. Debe existir alternativa manual completa.

Antes de producción se realizará una revisión específica de privacidad/GDPR, cookies/almacenamiento, permisos de ubicación, comunicaciones y tratamiento de datos. No se debe asumir que todos los mecanismos de almacenamiento requieren el mismo tratamiento ni diseñar el consentimiento mediante suposiciones no verificadas.

## 20. Fuera de alcance inmediato

Salvo nueva decisión, no son requisito del primer V1 comercial:

- ERP completo.
- Inventario/proveedores/compras.
- Nóminas y RR. HH.
- Contabilidad general completa.
- Analítica empresarial avanzada.
- App móvil nativa.
- Asistente conversacional completo.
- Secretaria virtual/inteligencia avanzada de agenda.
- Reseñas completas, salvo que se reprioricen.
- Panel administrativo empresarial avanzado.

Estas exclusiones sirven para proteger el alcance y evitar que la evolución post-TFG se convierta en una reconstrucción infinita.
