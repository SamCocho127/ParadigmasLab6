# Memoria persistente de Samir

> **TL;DR:** Al iniciar una sesión, lee `daily-log/status.md`, el diario de hoy, `INDEX.md` y solo las notas pertinentes; durante la sesión registra avances reales y, al cerrar, actualiza los hallazgos duraderos y reemplaza el estado vigente.

Created 2026-10-28.

## Inicio de cada sesión

1. Leer [[daily-log/status]] y luego `daily-log/YYYY-MM-DD.md` si existe para la fecha actual en `America/Costa_Rica`.
2. Leer [[INDEX]] y abrir únicamente las notas relacionadas con la tarea.
3. Aplicar las preferencias de [[Working/How I work]].
4. Para trabajar en UNA Chat, leer además [Repos/AGENTS.md](../../Repos/AGENTS.md) y [Repos/Lab5/agent.md](../../Repos/Lab5/agent.md).

## Durante la sesión

- Añadir al diario de hoy una viñeta con hora `CST` después de cada avance, decisión, hallazgo o bloqueo significativo.
- El diario es acumulativo: anexar sin reordenar ni reescribir entradas anteriores.
- Registrar correcciones o preferencias nuevas de Samir en [[Working/How I work]] con fecha.
- Usar la ruta absoluta de esta memoria al escribir el diario para evitar confundir otro checkout o subdirectorio.

## Cierre de cada sesión

1. Incorporar cada hallazgo duradero en la nota temática correspondiente.
2. Reescribir [[daily-log/status]] para reflejar el estado actual; no acumular historia allí.
3. Si se crea una nota, añadirla a [[INDEX]] y enlazarla desde [[Home]].
4. Dejar claro qué se completó, qué sigue y de quién se espera una acción.

## Convenciones

- Usar notas cortas, wikilinks y divulgación progresiva; enlazar en vez de duplicar.
- Distinguir hechos confirmados, decisiones, inferencias y pendientes.
- Fechar lo confirmado o actualizado.
- Corregir hechos falsos en su lugar, sin conservar la versión errónea como vigente.
- No guardar contraseñas, tokens, cookies, claves, cadenas de conexión ni valores reales de `.env`.
- No hacer commit, pull, push ni cambios de rama sin solicitud expresa.
