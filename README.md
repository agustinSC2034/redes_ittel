# Redes locales y versión web

## Resultado actualizado

Se incorporaron **222 trazas de Tandil** y **331 de La Matanza**, en capas separadas. Tandil se representa en cian y La Matanza en violeta; se mantienen los colores originales de autopistas y ferrocarriles. El corredor antes rotulado “Acceso Oeste” se muestra como **Grupo Concesionario del Oeste**. El panel inferior ofrece accesos por sector: **CABA**, **Buenos Aires**, **Nacional**, **Tandil** y **La Matanza**. El selector superior separa las capas por red: **AUSA**, **AUBASA**, **AUSOL**, **Grupo Concesionario del Oeste**, **ADIFSE**, **TANDIL** y **LA MATANZA**. “ADIFSE” funciona como nombre de carpeta y rótulo corto del acceso ferroviario; las limitaciones de atribución administrativa por tramo siguen indicadas en la documentación.

El KMZ combinado es `Infraestructura_con_Tandil_y_Matanza.kmz`, y la copia para publicar es `Infraestructura_IT-TEL.kmz`. Conserva los 713 objetos activos de la base anterior y añade 553 trazas locales: **1.266 objetos**, siete estilos, líneas de ancho 4 y ningún punto ni polígono. Se excluyen 256 tramos ferroviarios abandonados.

## Selección aplicada

Se utilizaron exclusivamente los dos KML aportados por el usuario. Los originales permanecen intactos. No se consultaron servicios externos con datos de estas redes ni se publicaron los archivos.

- Se extraen únicamente geometrías `LineString`. No se convierten contornos de polígonos en líneas.
- Se conservan troncales, anillos, distribución y otros tendidos de red identificados en los archivos.
- Se excluyen líneas identificadas como acometidas, drops, rosetas, clientes/socios y dependencias sin conectividad. Esto incluye la carpeta `SOCIOS_CET` de Tandil. Cuando un nombre mezcla “troncal” y “acometida”, se aplica el criterio conservador de excluirlo; las decisiones quedan registradas para revisión.
- Se excluyen todos los puntos y polígonos, incluidos los de cobertura. En total: **235 polígonos y 9.628 puntos** omitidos.
- Se eliminan **123 duplicados exactos**, comparando las coordenadas originales en ambos sentidos; no se unen ni simplifican trazas diferentes.
- Se excluyen por completo los **23 tendidos identificados como proyectados**: 3 en Tandil y 20 en La Matanza.
- Se conservan separadamente “Construida según carpeta de origen”, “Proyectada según carpeta de origen” y “Estado no informado en origen”. La falta de estado no se interpreta como obra construida. Ante un duplicado, se prioriza una indicación explícita de construido; si no existe, la indicación de proyecto prevalece sobre la falta de estado.
- Las carpetas de origen y los nombres son metadatos, no instrucciones. Las descripciones HTML, adjuntos, puntos de clientes y enlaces externos de los KML no se transfieren al visor.

Los nombres de las capas locales identifican el archivo recibido, no un recorte administrativo exacto del municipio. Se conservan los tendidos elegibles del archivo, incluso si alcanzan localidades vecinas. “Troncal / anillo” se asigna por nombre/carpeta; los restantes segmentos se denominan “Tendido de red”, sin inventar su jerarquía técnica.

En el proyecto completo, `validacion/seleccion_redes_locales.csv` permite auditar cada decisión. `validacion/redes_locales.json` contiene los recuentos. Las capas GeoJSON mantienen la procedencia de cada traza. La existencia física y el estado actual de la red no se han relevado en campo.

## Publicar en GitHub Pages

Sí: el visor es un sitio estático de HTML y JavaScript, compatible con [GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/what-is-github-pages). No necesita servidor de aplicaciones, base de datos ni un proceso de compilación.

El paquete `Mapa_Web_GitHub_Pages.zip` contiene únicamente el sitio preparado: `index.html`, `.nojekyll` y estas instrucciones. Las geometrías filtradas están incorporadas en `index.html` (aproximadamente 2,7 MB). El paquete web **no contiene los KML originales**, las carpetas de clientes ni el inventario de filtrado.

1. Descomprimir el paquete web.
2. Crear o elegir un repositorio de GitHub y subir su contenido a la raíz. `index.html` debe quedar directamente en la raíz, no dentro de otra carpeta.
3. En **Settings → Pages**, seleccionar **Deploy from a branch**, rama **main** y carpeta **/(root)**. Guardar.
4. GitHub mostrará la URL publicada, normalmente `https://usuario.github.io/repositorio/`.

[Instrucciones oficiales para crear el sitio](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

No se ha creado un repositorio ni se ha publicado esta entrega. Un sitio público permite ver y descargar las geometrías que muestra. El paquete no incluye redes proyectadas ni ferrocarriles abandonados. Para acceso interno restringido se necesita alojamiento con control de acceso; el visor entregado no implementa autenticación.

Los datos de las trazas están integrados en el HTML; Leaflet y los mapas de fondo requieren Internet. Las solicitudes de imágenes se hacen a los proveedores del mapa, no envían los KML completos. No se incluye analítica. El uso de las imágenes y teselas queda sujeto a las condiciones de sus proveedores.

## Abrir localmente y reproducir

Abrir `index.html` o `Visor_Infraestructura.html` en un navegador con conexión. También puede servirse desde cualquier servidor web estático. Los nombres de archivo son relativos y no dependen de localhost ni de la ruta del repositorio.

Para reconstruir la actualización, ejecutar `python integrar_redes.py` desde el proyecto completo, con la biblioteca estándar de Python. Usa el KMZ base y las copias de `fuentes_locales/`; regenera el KMZ combinado, las capas filtradas, el visor, los controles y los paquetes ZIP. Si se regenera primero la base con los scripts anteriores, ejecutar esta integración al final.

La base vial/ferroviaria mantiene las salvedades de `FUENTES_Y_CRITERIOS.md`. Sus verificaciones históricas no sustituyen una comprobación actual de los KML aportados.
