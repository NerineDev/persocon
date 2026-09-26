# Estrategia de ramas post-TFG

> Estado: decisión activa para la evolución post-TFG de Sesvia.
> Repositorio de aplicación: `NerineDev/pi-plataforma-citas-app`.

## Baseline confirmado

El último commit del TFG/MVP en `main` es:

- `28a0b38` — `Fix professional message center refresh badge`

El despliegue histórico de Railway fue utilizado para identificar y comprobar el baseline. La suscripción de Railway ha sido cancelada y Railway deja de ser el entorno de trabajo/despliegue objetivo para la evolución post-TFG. Los recursos existentes no se eliminan todavía, para conservarlos temporalmente como referencia mientras se completa la transición.

## Ramas permanentes

### `prototype`

Snapshot congelado del TFG/MVP en `28a0b38`.

- Conserva la versión académica conocida como funcional.
- Sirve como referencia histórica y punto de recuperación.
- No recibe desarrollo post-TFG.
- No se usa como rama de integración.

### `develop`

Rama activa de integración para la evolución post-TFG.

- Parte del mismo baseline `28a0b38`.
- Recibe el trabajo validado de nuevas funcionalidades, rediseños y correcciones post-TFG.
- Es la base normal para crear ramas de trabajo cuando una tarea justifique una rama separada.
- No implica que su contenido esté listo para producción.

### `main`

Rama destinada al producto estable/publicable.

- Permanece inicialmente en el baseline del TFG mientras se construye la nueva versión en `develop`.
- El trabajo post-TFG solo llega a `main` cuando exista una versión validada que tenga sentido publicar como Sesvia real.
- A partir de ese momento, `main` representa la versión release/production-ready, no el prototipo académico.

## Flujo de trabajo

Flujo normal:

`prototype` (congelada) ← baseline TFG

`main` ← releases validadas

`develop` ← integración post-TFG

Ramas temporales cuando aporten claridad:

- `feat/...`
- `fix/...`
- `redesign/...`

Estas ramas nacen normalmente de `develop` y vuelven a `develop` tras validación. No es necesario crear una rama separada para cada cambio pequeño.

## Reglas

1. No desarrollar directamente sobre `prototype`.
2. Evitar desarrollo cotidiano directamente sobre `main`.
3. No fusionar `develop` en `main` solo para mantener ambas ramas sincronizadas; el merge debe representar una versión realmente publicable.
4. Mantener `prototype` como referencia exacta del estado TFG, aunque `main` avance en el futuro.
5. Antes de una release, validar funcionalidad, migraciones/configuración, responsive y flujos críticos desde `develop`.
6. Los experimentos con Bolt u otras herramientas forman parte del desarrollo post-TFG; no definen por sí mismos la estructura de ramas.

## Relación con el roadmap

Esta decisión completa la parte principal de estrategia de ramas de la Fase 0 de `post-tfg-roadmap.md`:

- baseline identificado;
- snapshot recuperable creado mediante `prototype`;
- rama de evolución creada mediante `develop`;
- `main` reservado para la futura versión estable/publicable.

La Fase 0 no debe darse por totalmente cerrada hasta que las dependencias necesarias del baseline y cualquier dato/configuración que aún deba conservarse fuera de Railway estén suficientemente documentados o migrados.