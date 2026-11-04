# Cómo actualizar la página de GimliForge

La URL `gimli.adriansr.com` redirige a `https://adriansr.com/gimli`. Esa página se sirve desde este repositorio mediante GitHub Pages. El dominio principal está indicado en `CNAME` (`adriansr.com`). No cambies `CNAME` para modificar la página de GimliForge.

## Archivos de la página

- `gimli.html`: textos, secciones, enlaces y metadatos.
- `gimli.css`: colores, tipografía y presentación adaptable a móvil.
- `gimli.js`: selector de comandos para Windows, macOS y Linux.
- `gimli.js` contiene también `VIDEO_FILE`. Cuando el vídeo final esté listo, sube su MP4 a la raíz del repositorio y sustituye la cadena vacía por su ruta, por ejemplo `'/GimliForge_2.0_demo.mp4'`. Se reproducirá en la sección Vídeo sin YouTube.
- Por ahora `VIDEO_FILE` está vacío a propósito: la página muestra un espacio reservado y no necesita un vídeo para publicarse.
- `gimli-bg.jpg`: imagen de portada ya existente en el repositorio.
- `fonts/`: tipografías locales de la página y sus licencias. Mantén esta carpeta junto a `gimli.css` para evitar peticiones a Google Fonts.
- `gimli-v1.html` y `gimli-v1-assets/`: copia estática de la página original 1.0. La página nueva enlaza a ese archivo para conservar su historia.
- `GimliForge-2.0.zip`: paquete enlazado desde la página.
- `SEGURIDAD_GIMLI.md`: revisión de seguridad, controles preparados y tareas pendientes antes de publicar.

## Actualizar desde cualquier ordenador

La página 2.0 se prepara en la rama `feature/gimli-2.0-site`. Para publicarla, incorpora esa rama a `main`. GitHub Pages sirve los archivos de la raíz. El archivo local `GimliForge-web-preview.zip` sirve para revisar o trasladar los archivos, pero GitHub no despliega el contenido de un ZIP subido como un único archivo.

1. Entra en `https://github.com/GalicianHat/galicianhat.github.io` con tu cuenta.
2. Abre el archivo que quieras modificar. Pulsa el icono del lápiz (**Edit this file**). Para sustituir una imagen o el ZIP, usa **Add file → Upload files**.
3. Revisa los cambios y guarda un commit descriptivo. Si trabajas en una rama, crea una pull request y fusiónala a la rama que publique GitHub Pages.
4. En **Settings → Pages**, comprueba que la fuente de publicación es la rama y carpeta que contiene `gimli.html` (en esta copia, `main` y la raíz). Comprueba el estado en **Actions**.
5. Abre `https://adriansr.com/gimli` y `https://gimli.adriansr.com` en una ventana privada. La segunda debe redirigir a la primera. Puede haber un retraso de caché antes de ver cambios.

El repositorio contiene la exportación estática de un antiguo sitio Next.js. Editar `gimli.html` cambia la página `/gimli`, pero una futura exportación completa de Next.js podría sobrescribirla. Antes de hacer una exportación completa, incorpore estos cambios al proyecto fuente de Next.js o conserve una copia de los archivos de la página 2.0 y del archivo 1.0. Los documentos y el vídeo originales siguen en la raíz del repositorio y se enlazan desde `gimli-v1.html`.

La página pública **no ejecuta** GimliForge. La aplicación Python se inicia en el ordenador de cada auditor y abre una interfaz en `127.0.0.1`; los proyectos de auditoría se guardan localmente. No subas la carpeta `projects/` ni informes reales a este repositorio público.
