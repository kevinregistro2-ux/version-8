# WorkLog Pro — nueva interfaz adaptable (Apple UI, octubre 2026)

## Qué contiene

Una actualización visual creada a partir de **`version 7.zip`**, sin borrar módulos ni sustituir la lógica de Firebase. Compatible con escritorio, tablet y teléfono mediante CSS adaptable. El código fuente de V7 se conserva y se añaden dos nuevas hojas de estilo al final de las cargas existentes para reemplazar las reglas visuales conflictivas.

Se aplica la referencia `apple-ui-skills` proporcionada: fondo blanco, acción principal azul `#155BD0`, tipografía Inter con alternativas del sistema, cuadrícula de espaciado de 4 píxeles, bordes de 1 píxel, radios de 21 píxeles en tarjetas, foco visible de 2 píxeles y tamaños táctiles más amplios. La referencia incluía tonos de texto demasiado claros para alcanzar 4.5:1 sobre blanco, por lo que se ajustaron a colores de mayor contraste. En interfaces de muchos datos se emplea texto de 13–16 px en vez de forzar 27 px en cada celda o botón.

## Archivos modificados o nuevos

| Archivo | Acción | Finalidad |
|---|---|---|
| `css/apple-responsive-2026.css` | Nuevo | Nuevo diseño común, móvil/tablet/escritorio, formularios, modal, navegación y estados. |
| `css/apple-admin-2026.css` | Nuevo | Diseño adaptable del administrador. |
| `index.html` | Modificado | Carga de la nueva hoja, metadatos claros y etiquetas de accesibilidad. |
| `admin.html` | Modificado | Carga de hoja del administrador tras los estilos internos y tema claro. |
| `js/app.js` | Ajuste mínimo | Nuevos usuarios inician con tema claro y acento azul; respeta las preferencias previamente guardadas. |
| `service-worker.js` | Modificado | Nueva clave de caché PWA y precaché de la hoja nueva. |
| `manifest.webmanifest` | Modificado | Colores claros para instalación PWA. |

Los otros archivos de código, incluida toda la integración de Firebase, permanecen iguales a V7. No se han alterado `firebase/firestore.rules`, datos de usuarios, colecciones ni autenticación.

## Instalación recomendada

1. Crea una rama en GitHub, por ejemplo `diseno-apple-responsive-2026`. No sustituyas directamente la versión publicada.
2. Usa `worklog-pro-apple-completo.zip` como copia de V7 con el rediseño, **o** copia desde `worklog-pro-apple-solo-cambios.zip` los siete archivos indicados sobre tu proyecto V7. El ZIP de cambios **no** sirve como proyecto independiente.
3. Abre la app en un servidor local o en un entorno de pruebas con HTTPS (Firebase Auth, PWA y rutas absolutas de `/admin` no deben validarse mediante `file://`).
4. Abre la app y revisa Hoy, Jornada, Lugares, Historial, Calendario, Reportes, Ajustes, panel admin, inicio de sesión y apertura de modales en PC, tablet y teléfono.
5. Al desplegar, comprueba la actualización del Service Worker. Si un usuario sigue viendo la versión anterior, recarga con la actualización aplicada y verifica la caché. Evita limpiar almacenamiento que contenga datos no sincronizados.
6. Solo publica cuando las pruebas de Firebase, guardado, login y flujos críticos se hagan con un entorno de prueba y resulten correctas.

**Nota:** la hoja nueva debe cargarse **después** de `styles.css`, `mobile.css`, `worklog-pro-v3.css` y `loading.css`. No reemplaces las clases ni los identificadores del HTML si quieres conservar sus manejadores de JavaScript.

## Verificaciones realizadas en esta entrega

- Comprobación sintáctica de los 11 JavaScript originales/modificados mediante `node --check`: aprobada.
- Validez JSON de `manifest.webmanifest`, `firebase.json` y `metadata` de las reglas adjuntas: verificable por separado.
- Renderizado **estático** en Chromium con CSS incrustado para seis anchos: **320, 390, 834, 1024, 1366 y 1920 px**. No hubo desbordamiento horizontal del documento al mostrar una a una las siete páginas principales.
- Previsualizaciones del dashboard de escritorio, tablet, teléfono y panel administrativo con HTML existente y sus contadores iniciales. Estas pruebas son visuales/estructurales, no una prueba de carga de datos reales.
- Modal de actividad abierto sin desbordamiento horizontal en 390 px y 1366 px.
- Comprobación CSS del botón azul principal en el renderizado estático: fondo `rgb(21,91,208)` y texto `rgb(255,255,255)`.

## Fuera del alcance de esta entrega

Este rediseño **no corrige** las incidencias previas de persistencia, importación JSON, cálculos monetarios, sincronización o reglas de seguridad. Tampoco se comprobó conexión real con Firebase, autenticación, flujos end-to-end o despliegue PWA en dispositivos físicos. La auditoría y reparación funcional deberán ser una fase independiente.

## Reversión

La nueva hoja puede desactivarse quitando su `<link>`, pero para una reversión limpia restaura los siete archivos desde tu rama anterior. Hazlo tras confirmar que no existen operaciones locales sin sincronizar.
