# Revisión de seguridad de la página GimliForge

Estado: borrador local, 3 de noviembre de 2026. Los cambios de la versión 2.0 no están publicados.

## Alcance

La página `/gimli` es estática y se sirve desde GitHub Pages. `gimli.adriansr.com` redirige mediante Cloudflare a `https://adriansr.com/gimli`. La aplicación GimliForge se ejecuta en `127.0.0.1` en el ordenador del usuario; la página pública no almacena proyectos ni claves de Gemini.

## Activos y amenazas

| Activo | Riesgo principal | Control y comprobación |
| --- | --- | --- |
| Código y contenido de la página | Alteración de HTML, JS o enlaces | Revisión de cambios antes de publicar; pendiente comprobar MFA y protección de la rama de publicación. |
| Visitantes | Carga de recursos maliciosos si se introduce una inyección | Política de seguridad de contenido en `gimli.html`: scripts, estilos, imágenes y fuentes locales; solo se permite el marco futuro de `youtube-nocookie.com`. |
| Tráfico | Intercepción o modificación en HTTP | El dominio público redirigía de HTTP a HTTPS y enviaba HSTS `max-age=31556952` en la revisión del 3 de noviembre. Volver a comprobar tras publicar. |
| Privacidad | Envío de datos de navegación a servicios externos | Fuentes alojadas en este repositorio y política `no-referrer`. El vídeo no se carga hasta que se configure su ID; cuando se configure, usará `youtube-nocookie.com` y carga diferida. |
| Integridad de la descarga | Sustitución del ZIP por otro contenido | El ZIP será revisado antes de publicar; añadir suma SHA-256 visible y verificar que corresponda al código etiquetado final. |

## Cambios preparados en la página 2.0

- Se han retirado las peticiones a Google Fonts: Inter y Marcellus SC se sirven desde `fonts/`, con sus licencias OFL.
- `gimli.html` declara una política CSP por `meta` que limita scripts, estilos, fuentes, imágenes, conexiones, marcos, objetos, formularios y workers. Los dos estilos en línea del gráfico ilustrativo se sustituyeron por CSS local.
- Se declara `referrer=no-referrer`. El futuro iframe de YouTube solo solicitará los permisos `encrypted-media` y `picture-in-picture` y no enviará la URL de origen como referrer.
- Los enlaces externos que abren una pestaña nueva ya usan `rel="noopener noreferrer"`.
- Comprobación local: la página carga con la CSP activa, las fuentes locales se cargan, el gráfico conserva su ancho y la consola del navegador no muestra errores ni avisos.
- Una búsqueda de patrones de claves privadas, tokens y claves API, así como de nombres de archivo sospechosos, en los cinco commits locales y sus archivos versionados no encontró coincidencias. Este análisis de patrones no detecta todos los tipos posibles de secreto ni inspecciona el contenido de recursos binarios.

## Límites y tareas pendientes

- Una CSP declarada mediante `meta` protege **solo** `gimli.html`. La portada del portfolio y la copia histórica `gimli-v1.html` no heredan esa política.
- `frame-ancestors` (protección frente a que otro sitio incruste la página), CSP en modo de solo informe y otros encabezados HTTP requieren configurarse en el servidor o en una capa de distribución; no se pueden imponer con un archivo `meta` de GitHub Pages. Si se quiere esa protección para todo `adriansr.com`, estudiar una capa de distribución que controle encabezados o una migración de alojamiento, probarla antes de cambiar el dominio y documentar el resultado.
- Revisar MFA de la cuenta GitHub, acceso al repositorio y protección de la rama que publica la web. No se han cambiado configuraciones de cuenta ni DNS.
- Antes de publicar, confirmar manualmente que los documentos, audio, vídeo y demás recursos binarios presentes en el repositorio están destinados a ser públicos; repetir el análisis de secretos sobre la versión definitiva.
- Después de publicar, repetir las pruebas de HTTPS, redirección del subdominio, cabeceras, CSP, recursos cargados y enlaces. El resultado local no demuestra la configuración final de GitHub Pages.

Fuentes: [GitHub Pages y HTTPS](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https), [dominios personalizados de GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site), [CSP en `meta`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CSP), [`frame-ancestors`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Security-Policy/frame-ancestors).
