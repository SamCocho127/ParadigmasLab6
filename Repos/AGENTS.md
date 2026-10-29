# Repositorios locales

> **TL;DR:** `Repos` contiene repositorios clonados e independientes; solo este archivo de índice pertenece al control de versiones de ParadigmasLab6.

## Propósito

La carpeta `Repos` reúne repositorios clonados que se usan desde este espacio de trabajo, pero que son proyectos independientes. El repositorio padre no debe versionar el contenido de esos proyectos ni convertirlos en submódulos.

Cada repositorio interno conserva su propio historial Git, configuración y remoto.

## Repositorios

### UNA Chat / Lab5

- **Nombre:** UNA Chat / Lab5
- **Ruta local:** `Repos/Lab5`
- **Repositorio remoto:** https://github.com/SamCocho127/Lab5.git
- **Tecnologías principales:** Node.js, Express, Socket.IO, Mocha, Jest y Playwright.
- **Propósito:** Chat web en tiempo real que publica texto y convierte URLs completas compatibles en imágenes o reproductores de video. La autenticación social con Auth0 corresponde al Laboratorio 8 y aún no está implementada.
- **Arquitectura:** `server.js` sirve `index.html` y gestiona Socket.IO; `libs/unalib.js` valida y transforma mensajes; `test/`, `integration/` y `e2e/` cubren unidad, sockets y navegador; `openspec/` conserva las especificaciones.
- **Contrato principal:** El servidor inicia con `server.js` y recibe/reemite el evento `Evento-Mensaje-Server`.
- **Comandos:** `npm start`, `npm test`, `npm run test:integration`, `npm run test:e2e` y `npm run test:all`.
- **Instrucciones:** Leer completamente `Repos/Lab5/agent.md` antes de modificar ese proyecto.
- **Git:** Es un repositorio independiente con su propio `.git`, historial y remoto; su contenido no se versiona desde ParadigmasLab6.
