# Medición de Kozmic Pearls

## Instalación

Sitio estático, sin framework ni proceso de compilación. `index.html` contiene la única página; sus secciones se enlazan con fragmentos (`#contacto`, `#fechas`, etc.).

- Contenedor: `GTM-TBM9DFNT`.
- Propiedad de destino confirmada por la usuaria: `G-FE8XPMTY05`.
- El script asíncrono de GTM está al principio de `<head>`, después del charset.
- El respaldo `noscript` está inmediatamente después de `<body>`.
- GA4 se configura dentro de GTM. No agregar `gtag.js`, otra instalación de GTM ni eventos manuales de `page_view` sin revisar duplicación.

El contenedor público consultado el 19 de noviembre de 2026 contiene el destino GA4 indicado y su inicialización. Las modificaciones futuras del contenedor se administran en Google Tag Manager.

## Despliegue en Vercel

Publicar `index.html` en la rama `main` del repositorio `arenaspatt/kozmicpearls`, que activa el despliegue existente. No se requieren paquetes, secretos ni variables de entorno. Este cambio por sí solo no publica el sitio.

## Verificación tras desplegar

1. Esperar el estado correcto del despliegue en Vercel.
2. Abrir Google Tag Manager → Vista previa y conectar `https://www.kozmicpearls.com/` con Tag Assistant.
3eien+. Comprobar que solo se carga el contenedor `GTM-TBM9DFNT` y que la etiqueta de Google tiene como destino `G-FE8XPMTY05`.
4. En las herramientas de desarrollo del navegador → Network, filtrar `collect`. Revisar una solicitud GA4 con `tid=G-FE8XPMTY05` y `en=page_view`. Una carga normal debe generar un solo `page_view`; comprobar también la configuración de etiquetas en Tag Assistant.
5. En la propiedad correcta de Google Analytics → Informes → Tiempo real, abrir la web en otra pestaña y comprobar la visita. Para investigar eventos, usar Administrar → DebugView con la sesión de depuración de Tag Assistant.

Si no aparecen solicitudes, comprobar bloqueadores, consentimiento, filtros de tráfico interno y que el contenedor esté publicado. No enviar el formulario de contacto para probar visitas. El respaldo `noscript` no garantiza la medición GA4 sin JavaScript.

## Alcance de las comprobaciones locales

Se comprobó que hay una única instalación del contenedor, que el código JavaScript es válido y que el cargador inserta una sola petición asíncrona al contenedor correcto e inicializa `dataLayer`. Esto no prueba recepción en la propiedad: esa comprobación requiere la versión desplegada y los informes de GA4/Tag Assistant.
