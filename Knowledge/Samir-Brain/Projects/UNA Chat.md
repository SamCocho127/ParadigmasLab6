# UNA Chat

Contexto durable y verificable del proyecto de chat en tiempo real. Created 2026-10-28. Last reinforced 2026-10-28 19:45 CST.

## Hechos confirmados

- ParadigmasLab6 es el espacio de trabajo principal; `Repos/` contiene repositorios independientes y `Repos/AGENTS.md` es su índice.
- Ruta local: `Repos/Lab5` desde la raíz del espacio de trabajo.
- Remoto: https://github.com/SamCocho127/Lab5.git.
- Lab5 conserva su propio `.git`, historial, rama `main` y remoto. Su contenido no se versiona desde ParadigmasLab6.
- Tecnologías: Node.js, Express, Socket.IO, Mocha, Jest, Playwright y OpenSpec.
- Propósito: chat web en tiempo real que publica texto y muestra URLs completas compatibles como imágenes o reproductores de video.

## Arquitectura y contrato

- `server.js`: punto de entrada y fábrica del servidor; carga la configuración local, aplica Auth0 a HTTP y al handshake de Socket.IO, sirve las rutas y difunde mensajes validados.
- `libs/auth.js`: valida las variables requeridas sin mostrar valores, configura `express-openid-connect` y normaliza la identidad autenticada.
- `login.html`: pantalla pública previa a la autenticación, con reintento genérico ante cancelación o error.
- `index.html`: interfaz protegida; obtiene `/api/me`, muestra perfil y nombre de solo lectura, y conecta el socket después de confirmar la sesión.
- `libs/unalib.js`: clasifica el campo `mensaje`, bloquea patrones de script, escapa contenido visible y genera HTML para medios aceptados.
- Evento principal: `Evento-Mensaje-Server`, usado tanto para recibir como para reemitir.
- JSON del mensaje: `{ nombre, mensaje, color }`; el servidor siempre reemplaza `nombre` con la identidad de la sesión.
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
- Nombre y texto ordinario se escapan antes de mostrarse; el color se restringe a un formato hexadecimal seguro.
- HTTP protegido y Socket.IO comparten la sesión. Un socket anónimo se rechaza y logout desconecta los sockets asociados al sujeto autenticado.
- La configuración real vive solo en `.env` ignorado; `.env.example` contiene marcadores. No guardar valores reales, tokens ni cookies en Git o en esta memoria.
- Dependencias de autenticación: `express-openid-connect` y `dotenv`, fijadas y verificadas con Node 22, Express 4 y CommonJS.

## Ejecución y pruebas

- `npm start`: inicia `node server.js`.
- `npm test`: Mocha, unidad sobre `libs/unalib.js`.
- `npm run test:integration`: Jest y Socket.IO con puerto efímero.
- `npm run test:e2e`: Playwright contra el servidor en puerto `3010`, navegador visible y `slowMo: 1000`.
- `npm run test:all`: ejecuta Mocha y Jest; no incluye Playwright.
- Resultado del 2026-10-28: 40 unitarias, 17 de integración y 16 e2e aprobadas; OpenSpec válido en modo estricto; Snyk sin vulnerabilidades; `npm audit` con 6 hallazgos bajos transitivos de Jest.
- Hallazgo manual corregido: la solicitud inicial de Engine.IO se adapta al prototipo de solicitud Express; la respuesta conserva su prototipo de Engine.IO y recibe únicamente los ayudantes Express de cabeceras y cookies que Auth0 necesita para renovar la sesión.

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
- Paso 4 / US-01: completada para ejecución local con Auth0 y Google; validación manual real aprobada el 2026-10-28.
- Alcance deliberado: sin Vercel, sin Redis y sin `rsc-harness`.
- OpenSpec: cambio archivado como `2026-10-28-us-01-auth0-social-authentication`, con `chat-experience` actualizado y la capacidad `social-authentication` incorporada.

Consulta también [[Working/Tickets and recent work]], [[Working/Environments]] y [[Working/Gaps]].
