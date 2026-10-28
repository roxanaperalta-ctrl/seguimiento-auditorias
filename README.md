# Seguimiento de auditorías de cartera

Tablero privado de seguimiento. Lee tu Gmail de forma automática, compara cada correo de decisión (APROBADO u OBSERVADO) con el aviso original "Auditoría ejecutada" y guarda el resultado en tu Google Drive.

## Cómo funciona

| Pieza | Dónde vive | Qué hace |
|---|---|---|
| `apps-script/` | Tu cuenta de Google (script.google.com) | Lee Gmail de lunes a viernes a la 1 p. m. y a las 6 p. m. (hora de Lima), analiza y guarda `datos.json` en la carpeta de Drive **Seguimiento auditorías cartera**. Publica el tablero como aplicación web con acceso **Solo yo**. |
| `notas.json` (Drive) | Tu Drive | Estado y notas que escribes en el tablero. |
| `index.html` | GitHub Pages | Página de entrada **sin datos**: abre el tablero privado. Aunque alguien vea esta página, sin tu cuenta de Google no ve nada. |

Los datos (lotes, montos, correos) nunca se suben a GitHub.

## Instalación

1. **Apps Script**: entra a script.google.com con tu cuenta y crea un proyecto nuevo llamado "Seguimiento auditorías".
   - Pega `apps-script/Code.gs` en `Code.gs`.
   - Crea un archivo de secuencia de comandos llamado `Analisis` y pega `apps-script/Analisis.gs`.
   - Crea un archivo HTML llamado `Pagina` y pega `apps-script/Pagina.html`.
2. Elige la función `instalar` y pulsa **Ejecutar**. Acepta los permisos (lectura de Gmail, Drive y activadores). Así se crea la carpeta en Drive, se programan las dos lecturas diarias y se hace la primera lectura.
3. **Implementar → Nueva implementación → Aplicación web**: Ejecutar como **Yo**, Quién tiene acceso **Solo yo**. Copia la URL que termina en `/exec`.
4. **GitHub**: en este repositorio, edita `index.html` y reemplaza `PEGA_AQUI_LA_URL_DE_APPS_SCRIPT` por esa URL.
5. **Settings → Pages**: Source **Deploy from a branch**, rama `main`, carpeta `/ (root)`. GitHub te da la dirección web (por ejemplo, `https://<usuario>.github.io/seguimiento-auditorias/`).

## Para cambiar algo

- Horarios o días a leer: `CFG.HORAS` y `CFG.DIAS` en `Code.gs`. Después vuelve a ejecutar `instalar`.
- Si cambias el código de la página, crea una **nueva versión** en Implementar → Gestionar implementaciones, para que la URL `/exec` la muestre.

## Límites

- Solo revisa tu bandeja: no ve copias ocultas (CCO) ni reenvíos que no te lleguen.
- Para detectar lotes sin auditoría, tu cuenta debe ir en copia de los correos de lote.
- Si el navegador bloquea las cookies de terceros, el tablero no se ve dentro de la página de GitHub. En ese caso usa el botón **Abrir tablero**.
