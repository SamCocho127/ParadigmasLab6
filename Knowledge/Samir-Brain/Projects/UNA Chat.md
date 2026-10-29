# UNA Chat

Contexto durable y verificable del proyecto de chat en tiempo real. Created 2026-10-28. Last reinforced 2026-10-28.

## Hechos confirmados

- ParadigmasLab6 es el espacio de trabajo principal; `Repos/` contiene repositorios independientes y `Repos/AGENTS.md` es su índice.
- Ruta local: `Repos/Lab5` desde la raíz del espacio de trabajo.
- Remoto: https://github.com/SamCocho127/Lab5.git.
- Lab5 conserva su propio `.git`, historial, rama `main` y remoto. Su contenido no se versiona desde ParadigmasLab6.
- Tecnologías: Node.js, Express, Socket.IO, Mocha, Jest, Playwright y OpenSpec.
- Propósito: chat web en tiempo real que publica texto y muestra URLs completas compatibles como imágenes o reproductores de video.

## Arquitectura y contrato

- `server.js`: punto de entrada; sirve `index.html`, crea HTTP/Express/Socket.IO, usa `PORT` o `3000`, valida mensajes y los difunde.
- `index.html`: interfaz y cliente; toma nombre, mensaje y color, rechaza texto vacío, usa `Anónimo` sin nombre y pinta lo recibido.
- `libs/unalib.js`: clasifica el campo `mensaje`, bloquea patrones de script y genera HTML para medios aceptados.
- Evento principal: `Evento-Mensaje-Server`, usado tanto para recibir como para reemitir.
- JSON del mensaje: `{ nombre, mensaje, color }`.
- El cliente analiza el JSON recibido y agrega `Nombre: mensaje` a `#messages` con `.html(mensajeDisplay)`.

## Mensajes y medios

- Texto: se conserva cuando no es exclusivamente una URL de medio; una URL dentro de una frase sigue siendo texto.
- Imágenes: URL `http`/`https` completa con extensión `jpg`, `jpeg`, `png`, `gif`, `bmp` o `webp`.
- YouTube: formas `watch`, `youtu.be` y `embed`, usando solo un identificador válido de 11 caracteres.
- Archivos de video: `mp4`, `webm`, `ogg`, `ogv` o `mov`, con controles.
- Para clasificar, se recortan espacios externos; el texto normal se conserva tal como fue enviado.

## Seguridad y validación actuales

- Los mensajes vacíos se detienen en el navegador.
- La detección de inyección vacía mensajes con etiqueta `script`, esquema `javascript:` o atributos de evento.
- Las URLs aceptadas para medios requieren HTTP(S); los atributos generados se escapan y YouTube usa solo el identificador extraído.
- Consideración pendiente: el nombre, el color y el texto ordinario no reciben un escape HTML general antes de insertarse con `.html`; cualquier endurecimiento debe especificarse y probarse antes de cambiar el comportamiento.
- No existen credenciales, variables ni dependencias de Auth0 confirmadas en el repositorio al 2026-10-28.

## Ejecución y pruebas

- `npm start`: inicia `node server.js`.
- `npm test`: Mocha, unidad sobre `libs/unalib.js`.
- `npm run test:integration`: Jest y Socket.IO con puerto efímero.
- `npm run test:e2e`: Playwright contra el servidor en puerto `3010`, navegador visible y `slowMo: 1000`.
- `npm run test:all`: ejecuta Mocha y Jest; no incluye Playwright.

## Convenciones que deben preservarse

- Leer [Repos/Lab5/agent.md](../../../Repos/Lab5/agent.md) antes de modificar Lab5.
- Especificar cambios de comportamiento con OpenSpec antes de implementar.
- Mantener `#nombre`, `#m`, `#messages`, el botón `Send`, el texto `pegue una URL` y el evento principal mientras las pruebas dependan de ellos.
- Mantener la validación y transformación de medios en el servidor.
- Proteger texto, imágenes, videos y bloqueo de scripts con pruebas apropiadas.

## Estado del Laboratorio 8

- Paso 1: completado.
- Paso 2: completado el 2026-10-28 con esta memoria.
- Paso 3: excluido; no usar `rsc-harness`.
- Paso 4: pendiente.
- Historia pendiente: US-01, autenticación social con Auth0 para ejecución local y despliegue en Vercel.

Consulta también [[Working/Tickets and recent work]], [[Working/Environments]] y [[Working/Gaps]].
