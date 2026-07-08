# Changelog general - Parche acumulativo OTA

- Generado: 2026-07-08 09:42
- Proyecto: CyC Topografia Suite
- Manifiesto de parche acumulativo: `manifiesto_acumulativo_20260707_2352.json`

## Resumen

- `i18`: base `000000.0000` -> `260422.0728` (2 entrada(s))
- `linderos`: base `260428.1833` -> `260703.1955` (4 entrada(s))
- `postproceso`: base `260623.0600` -> `260707.1610` (7 entrada(s))
- `rinex`: base `260623.0100` -> `260626.0716` (2 entrada(s))
- `Suite_Core`: base `260705.0219` -> `260708.0850` (5 entrada(s))

## i18
Linea base publicada: `000000.0000`
Changelog fuente:
- `C:\00_PROYECTOS\CyC_Suite\V1_(DEV)\i18\CHANGELOG.md`

### v260422.0728

#### Modificado

##### i18

### 🚀 Añadido
- Despliegue de estructura modular: `core.json` para interfaz global y `conversiones.json` para lógica específica.
- Normalización de claves entre idiomas (ES/EN/PT) para asegurar consistencia en el Hub.
- Eliminación de archivos JSON monolíticos en favor de una arquitectura distribuida por carpetas.
- Nueva arquitectura de carpetas por idioma (`/idiomas/{lang}/`).
- Lógica de fusión automática (Merge) en `i18n_servicio.py` que consolida múltiples archivos JSON por idioma en un único mapa de memoria.
- Soporte para carga dinámica de módulos sin necesidad de registro explícito en el código fuente.
- Motor de pre-procesamiento de JSON en `i18n_servicio.py` para admitir comentarios tipo `#`.
- Soporte para diccionarios con clave raíz de idioma (Wrapper Pattern), permitiendo compatibilidad directa con archivos generados por asistentes externos.
- Sanitización de strings mediante RegEx para evitar errores de parseo en archivos con metadatos descriptivos.
### 🐛 Corregido
- Se renombró el directorio principal del módulo de `i18n` a `i18` para simplificar la estructura de paquetes.
- Se actualizaron las importaciones en `i18n_controlador.py` para utilizar referencias locales directas.
- Se ajustó la detección de la ruta de diccionarios en `i18n_servicio.py` para asegurar compatibilidad con la nueva ubicación de la carpeta `idiomas/`.
- Verificado el funcionamiento del empaquetado bajo la nueva ruta relativa en Windows.
- `ModuleNotFoundError`: Se corrigieron las importaciones en `i18n_controlador.py` cambiando el enrutamiento relativo implícito por absoluto (`from i18 import...`) para asegurar la compatibilidad de ejecución desde el `main.py` raíz en Python 3.

### v260422.0709

#### Modificado

##### i18

### 🚀 Añadido
- Módulo `i18n` completamente desacoplado bajo patrón MVC.
- Motor de traducción en `i18n_servicio.py` con soporte para interpolación dinámica de cadenas (`kwargs`).
- Persistencia de configuración en `_cyc.json` gestionada a través de `i18n_estado.py`.
- Patrón Observador en `i18n_controlador.py` (`registrar_vista` / `_notificar_cambio`) para refresco dinámico de la UI en Tkinter sin reinicio de sesión.
- Archivos de idioma base (`es.json`, `en.json`, `pt.json`) con estructura estandarizada de prefijos (`lbl_`, `btn_`, etc.).
- _Fallback_ de seguridad automático a idioma español en caso de claves faltantes en diccionarios extranjeros.

## linderos
Linea base publicada: `260428.1833`
Changelog fuente:
- `C:\00_PROYECTOS\CyC_Suite\V1_(DEV)\linderos\CHANGELOG.md`

### v260703.1955

#### Modificado

##### linderos

### Cambiado
* Eliminación de compuertas funcionales dependientes del estado de licencia en el controlador de Linderos.
* Sustitución de la validación `BASICO`/`Pro` por eventos no bloqueantes enviados a `monetizacion.disparar_donacion(...)`.
* Las acciones de guardar gráfico, exportar reportes TXT/PDF, guardar sesión, guardar como y cargar sesión quedan disponibles para usuarios **Basico** y **Donador** por igual.
* La integración con monetización queda limitada a banners, avisos o reconocimiento de apoyo, sin impedir cálculos, exportaciones, sesiones ni flujos técnicos.

### Política aplicada
* Se alinea el módulo con `README_LICENCIAS_MONETIZACION_USUARIO.md` y `README_INSTALADOR.md`: la licencia reconoce estado y apoyo, pero no bloquea ni desbloquea herramientas.

### v260625.1614

#### Modificado

##### linderos

### Cambiado
* Actualización de la versión central del módulo Linderos en `versiones.py`.
* Adopción de los valores neutros oficiales de la guía visual CyC para fondo, superficies, paneles, bordes, texto, texto secundario y controles deshabilitados.
* Eliminación de variantes oscuras de verde y amarillo en estados hover; los controles conservan el mismo color corporativo y comunican interacción mediante relieve.
* Definición de tres niveles visuales de acción: primario verde, secundario amarillo y terciario neutro con borde verde.
* Clasificación de cálculo, validación y proyección como acciones primarias; exportaciones como acciones secundarias; navegación, edición y sesión como acciones terciarias.
* Incremento de la tipografía monoespaciada de memorias y resultados técnicos a 10 puntos.
* Normalización del padding interno de secciones y filas operativas.
* Reducción del título de vista previa a la escala tipográfica establecida para encabezados de panel.
* Sustitución de colores azul y naranja residuales en los botones de exportación por amarillo corporativo.
* Uniformación de etiquetas de formulario mediante anchos controlados y alineación izquierda, manteniendo variantes compactas en filas con varios controles.
* Simplificación del estado inicial para reducir instrucciones extensas y priorizar la acción operativa.
* Incorporación de una barra de estado corporativa: verde para datos válidos, amarillo para advertencias y borde neutro para espera.
* Protección de la memoria de cálculo y el resumen interactivo como salidas de solo lectura, habilitándolas únicamente durante su actualización programática.
* Ajuste de encabezados técnicos del resumen a Consolas 11 y verde corporativo.
* Extracción de la escritura TXT y construcción PDF a `linderos/reporteador.py`, un servicio sin dependencias de Tkinter.
* Traslado de permisos Pro, selección de rutas, coordinación de exportaciones y mensajes de resultado al controlador.
* Eliminación de la lógica duplicada de licencia y monetización que permanecía dentro de la vista.
* Sustitución de acciones directas de exportación en los botones por eventos delegados al controlador.
* Eliminación completa de las dependencias ReportLab desde `vista.py`; ReportLab queda encapsulado en el servicio de reportes.
* Incorporación de una interfaz pública mínima entre controlador y vista para obtener contenido, configuración, paginación, gráfico temporal y textos visibles sin acceder a implementaciones privadas.
* Traslado de la construcción del editor de códigos topográficos desde el controlador hacia la vista, dejando al controlador únicamente la preparación y actualización de datos.
* Traslado del montaje y ciclo de vida del canvas y la barra de Matplotlib hacia la vista.
* Eliminación de colores visuales aislados y widgets `ttk` creados directamente desde el controlador.
* Corrección de botones azules provocados por la sobrescritura global de estilos `ttk` desde otros módulos de la Suite.
* Sustitución de botones operativos por controles Tk con colores CyC explícitos, inmunes a cambios posteriores del tema global.
* Sustitución de etiquetas, encabezados, filas y marcos de sección sensibles al tema por controles con fondo y texto explícitos.
* Eliminación de los recuadros grises que aparecían detrás de títulos y textos al perderse los estilos locales.
* Conversión de la pestaña Datos completa a un contenedor vertical desplazable para impedir que la sección **Proyecto y Sesión** quede recortada en ventanas de altura limitada.
* Incorporación de desplazamiento local con rueda del ratón sobre paneles y etiquetas, sin enlaces globales y respetando controles editables.
* Conservación de la barra de desplazamiento visible para que todas las acciones inferiores permanezcan localizables y accesibles.
* Corrección definitiva de botones azules bajo `ttkbootstrap`: el tema `litera` interceptaba el constructor de `tk.Button` y reemplazaba los colores declarados por su primario `#4582EC`.
* Desactivación explícita de `autostyle` en botones cuando `ttkbootstrap` está activo y reaplicación posterior de fondo, texto, estado activo y borde.
* Aplicación de la misma protección a la capa `CompatButton`, incluyendo controles compactos de configuración PDF.
* Corrección del ancho efectivo de los selectores basados en `ttk.Combobox` para que el desplegable muestre completas las opciones largas, incluyendo **Integrar en Reporte** y **Referenciar como Anexo**.
* Reorganización de la fila **10. Residuos** en columnas dedicadas para impedir que el selector o la acción lateral se compriman visualmente.

### Decisión de alcance
* La adaptación a una sola columna para pantallas estrechas se pospone como funcionalidad futura; el módulo continuará optimizado para monitores anchos.

### Preparado
* Conservación de la capa i18n existente y de las referencias a widgets para facilitar una internacionalización integral posterior, sin ampliar todavía el catálogo de traducciones.

### v260625.0859

#### Modificado

##### linderos

### Cambiado
* Actualización de la versión central del módulo Linderos en `versiones.py` conforme al esquema `AAMMDD.HHMM`.
* Homologación visual con el módulo de Postproceso mediante paneles equilibrados, superficies blancas, fondo general gris claro y secciones tipo tarjeta.
* Sustitución de acentos azules por verde corporativo `#1A7B3E` y amarillo corporativo `#FFC439`.
* Rediseño de pestañas, botones, encabezados de tablas, estados iniciales y controles compactos para mantener una jerarquía visual uniforme en la Suite.
* Ajuste del panel dividido para permitir crecimiento proporcional de ambos lados y aprovechar mejor resoluciones amplias.
* Limitación de las paletas de exportación corporativas a variantes verde y amarilla de CyC.
* Migración del motor lineal a la ecuación general normalizada `Ax + By + C = 0`, conservando compatibilidad con sesiones que almacenan pendiente e intercepto.
* Sustitución de extremos extendidos artificialmente por extremos físicos obtenidos al proyectar los puntos utilizados sobre la recta ajustada.
* Actualización de OLS, RANSAC y ODR para aceptar cualquier orientación del lindero, incluidas rectas verticales.
* Clasificación de vértices como cruces directos o cruces próximos a extremos; las prolongaciones lejanas ya no se exportan como vértices CAD.
* Sustitución de la selección exclusiva por R² por una puntuación multicriterio basada en R² geométrico, RMSE relativo a tolerancia, proporción de inliers y robustez del método.
* Incorporación de offsets firmados respecto a cada recta ajustada, incluyendo máximo absoluto, promedio, rango positivo/negativo y cantidad de puntos fuera de tolerancia.
* Ampliación del gestor de tramos, resumen interactivo, gráfico y reporte técnico para mostrar score, offsets y excedencias.
* Resaltado gráfico en amarillo corporativo de los puntos cuyo desfase absoluto supera la tolerancia configurada.
* Implementación de la sección 9 de cierre poligonal mediante ordenamiento topológico de tramos y vértices.
* Cálculo de error de cierre X/Y, cierre lineal, perímetro, precisión relativa y brechas entre extremos físicos.
* Validación explícita de cadenas abiertas, ramificaciones, tramos aislados y redes con más de un ciclo, evitando reportar cierres ficticios.
* Implementación de la opción **Integrar en Reporte** para residuos y offsets, con tablas paginables en bloques de veinte puntos.
* Implementación de la opción **Referenciar como Anexo**, incluyendo resumen estadístico y referencia al CSV detallado.
* Ampliación del anexo CSV con offset firmado, residuo ortogonal, tramo asignado y estado del punto.
* Implementación matemática del modelo circular mediante mínimos cuadrados no lineales con estabilización en coordenadas locales para datos UTM.
* Competencia automática entre polinomio de segundo grado y círculo cuando se selecciona geometría curva.
* Determinación del centro, radio, amplitud angular, extremos observados y longitud del arco.
* Integración de residuos radiales firmados, RMSE circular y puntos fuera de tolerancia.
* Representación gráfica del arco o círculo completo, incluyendo marcador del centro.
* Ampliación de la calculadora para devolver las dos soluciones posibles de X o Y sobre un círculo.
* Inclusión de parámetros circulares y geometría del arco en el resumen interactivo y el reporte técnico.
* Configuración de mínimo de puntos por tramo y máximo de tramos para los modos automáticos.
* Selección automática del número de grupos Auto Z mediante índice Silhouette, con opción de fijar manualmente entre 2 y 10 niveles.
* Incorporación de centros Z detectados, confianza de agrupación y diagnóstico de puntos remanentes o grupos omitidos.
* Eliminación del límite fijo de cinco tramos en Auto XY y soporte configurable de hasta veinte detecciones.
* Sustitución del formato de sesión basado en `pickle` por un contenedor ZIP con manifiesto JSON validado y versionado.
* Persistencia completa de entrada, columnas, análisis, parámetros Auto, escala, reporte y configuración PDF.
* Detección de sesiones heredadas con advertencia explícita antes de permitir su carga.
* Centralización de la captura y restauración de configuraciones para reducir duplicación entre reporte y sesiones.
* Eliminación de referencias circulares dentro de las comparativas de modelos para permitir serialización segura y archivos más compactos.

### Corregido
* Eliminación de la singularidad y resultados inestables en linderos Norte-Sur o con pendiente prácticamente infinita.
* Cálculo de residuos ortogonales unificado para rectas horizontales, oblicuas y verticales.
* Calculadora de proyección adaptada para informar cuando una recta vertical u horizontal no permite resolver un valor único.
* Corrección del error `TclError: invalid command name ... notebook` al usar la rueda del ratón después de cambiar o cerrar el módulo Linderos.
* Sustitución del enlace global `bind_all(<MouseWheel>)` por un enlace local al canvas de vista previa.
* Cancelación de trabajos diferidos de renderizado y validación al destruir la vista, evitando callbacks sobre widgets inexistentes.

### v260625.0849

#### Modificado

##### linderos

### Añadido
* Validación automática de datos pegados desde Excel con resumen de filas válidas, rechazadas, columnas, separador y códigos detectados.
* Vista previa tabular de las coordenadas interpretadas antes de ejecutar el ajuste.
* Botón principal **Validar y calcular linderos** dentro de la pestaña Datos.
* Controles de procesamiento inicial en la misma pestaña para seleccionar modo, geometría y tolerancia sin navegar previamente a Modelos.
* Mensajes explícitos para entradas vacías, columnas inválidas, tolerancias no positivas y conjuntos sin modelos calculables.

### Cambiado
* El separador de entrada ahora utiliza detección automática de tabuladores, punto y coma, espacios o comas.
* La importación conserva inicialmente los valores como texto para normalizar coordenadas con separadores regionales.
* El área para pegar contenido de Excel aumentó de tamaño y el panel derecho presenta instrucciones y diagnóstico antes del cálculo.

### Corregido
* Lectura de coordenadas con coma de miles, por ejemplo `340,207.2910` y `2,305,127.3640`.
* Lectura de coordenadas con formato europeo, por ejemplo `340.207,2910`.
* Retornos silenciosos durante la validación que dejaban al operador sin explicación sobre por qué no comenzaba el cálculo.

## postproceso
Linea base publicada: `260623.0600`
Changelog fuente:
- `C:\00_PROYECTOS\CyC_Suite\V1_(DEV)\postproceso\CHANGELOG.md`

### v260707.1610

#### Modificado

##### postproceso

- **postproceso/vista.py**: El botón para priorizar estrategias desde un reporte PDF deja de estar en la barra fija principal y pasa al panel de ajustes avanzados, dentro de la sección de formato de reportes.
- **postproceso/controlador.py**: Al aceptar la reanudación de estrategias pendientes detectadas al cargar un Rover ya procesado, el sistema inicia automáticamente la siguiente estrategia sin requerir un segundo clic en el botón de postproceso.
- **postproceso/controlador.py**: La base de conocimiento global se mueve a una ruta de usuario en `LOCALAPPDATA`, migrando la DB heredada del módulo si existe, para evitar errores SQLite por bases de sólo lectura.
- **postproceso/controlador.py**: El panel avanzado ya no llama al método eliminado `setup_perfiles_ui`; los eventos de perfiles, conocimiento, PDF y GeoCore se conectan directamente sobre los widgets reales del panel.
- **postproceso/controlador.py**: Al cargar sesiones previas, el sistema usa el `CyC_postproceso_auditoria.log` para reconocer evidencia de catálogo FIX agotado y evitar reabrir familias dinámicas equivalentes ya evaluadas.
- **postproceso/catalogo_ciclo_fix.py**: La reconciliación reconoce la marca `catalogo_agotado_auditado` y el estado `resuelto` como evidencia suficiente para no presentar nuevamente dinámicas regeneradas.
- **postproceso/repositorio_conocimiento.py**: La base SQLite de conocimiento normaliza permisos de escritura antes de abrirse para reducir errores `attempt to write a readonly database` en DB migradas o copiadas.
- **postproceso/vista.py**: El panel normal de reportes se simplifica a un único botón dinámico de vista previa, deshabilitado cuando no existe resultado y renombrado a `Generar Reporte` cuando hay datos reportables.
- **postproceso/controlador.py**: La acción visible de reporte deja de generar o abrir PDFs directamente; ahora siempre abre el editor/vista previa para que el usuario exporte desde allí.
- **postproceso/vista.py**: La sección de datos del proyecto se mueve al editor de reporte dentro del modo de vista previa, dejando el panel normal enfocado en archivos y parámetros de postproceso.
- **postproceso/vista.py**: La vista previa PDF incorpora desplazamiento horizontal y deja de forzar el ancho interno del lienzo, corrigiendo el recorte al aplicar zoom.
- **postproceso/controlador.py**: La detección de catálogo agotado revisa el log de auditoría completo de forma acotada y guarda una marca persistente en el sidecar cuando el cierre ocurre por agotamiento real.
- **postproceso/controlador.py**: Cuando una memoria ya marcada como `catalogo_agotado_auditado` conserva un ciclo activo heredado, el ciclo se cierra automáticamente para evitar reabrir barridos dinámicos ya agotados.
- **postproceso/catalogo_ciclo_fix.py**: El particionado del catálogo ignora ciclos activos heredados cuando la memoria ya está marcada como resuelta o agotada, evitando prompts por estrategias dinámicas recreadas.
- **postproceso/catalogo_ciclo_fix.py**: Las familias dinámicas de un catálogo auditado como agotado se reconocen como consumidas aunque se regeneren con nuevos PRN, ventanas o firmas, manteniendo pendientes sólo las estrategias realmente nuevas.
- **postproceso/catalogo_ciclo_fix.py**: La equivalencia por familia queda acotada a cierres fuertes de catálogo o a sesiones antiguas sin firmas, preservando la detección de recetas modificadas cuando existen huellas funcionales.
- **postproceso/catalogo_ciclo_fix.py**: La expansión final del ciclo FIX filtra familias dinámicas ya consumidas para evitar que una segunda generación vuelva a llenar el barrido con variantes regeneradas del mismo diagnóstico.
- **postproceso/vista.py**: El botón dinámico de generación/vista previa de reporte se reubica dentro del bloque `Estado del procesamiento`, debajo del estado de estrategias y del botón de pausa.
- **postproceso/vista.py**: La numeración visible del flujo de punto estático se ajusta a `1. Archivos de entrada` y `2. Parámetros y ajustes`, al mover los datos del proyecto al editor de reportes.
- **postproceso/controlador.py**: El botón principal de postproceso actualiza su texto y color según el estado real: iniciar, continuar, ejecutándose o iniciar nuevo postproceso para archivos ya procesados.
- **postproceso/controlador.py**: La pausa del ciclo FIX cancela continuaciones programadas y deja marcada la solicitud para detener el barrido al concluir la estrategia en curso.

#### Agregado

##### postproceso

- **postproceso/vista.py**: La vista previa de reportes incorpora controles de zoom `- / +` y etiqueta de porcentaje, manteniendo el renderizado fiel del PDF real.
- **postproceso/tests/test_catalogo_ciclo_fix.py**: Añadida prueba de regresión para sesiones auditadas como agotadas que vuelven a generar IDs dinámicos pendientes.
- **postproceso/tests/test_catalogo_ciclo_fix.py**: Añadida cobertura para evitar que estrategias dinámicas regeneradas por familia vuelvan a quedar pendientes después de agotar el catálogo, sin ocultar estrategias nuevas reales.
- **postproceso/tests/test_catalogo_ciclo_fix.py**: Añadida cobertura para impedir que la expansión acotada reabra familias dinámicas ya consumidas dentro del mismo ciclo automático.
- **postproceso/vista.py**: El botón premium principal incorpora un método de actualización directa de título/subtítulo para conservar textos dinámicos sin remapeos automáticos indeseados.

#### Eliminado

##### postproceso

- Sin eliminaciones en esta versión.

### v260706.2204

#### Modificado

##### postproceso

- **postproceso/vista.py**: Corregido el registro inicial de widgets del panel izquierdo para ignorar componentes ocultos del editor de reportes. Esto evita el error `TclError: window ... isn't packed` al abrir el módulo.
- **postproceso/catalogo_ciclo_fix.py**: Reforzada la reconciliación del catálogo FIX para que las estrategias dinámicas regeneradas no vuelvan a aparecer como pendientes cuando el ciclo anterior ya consumió todos sus IDs, incluso si la sesión no quedó marcada formalmente como cerrada.

#### Agregado

##### postproceso

- **postproceso/catalogo_ciclo_fix.py**: El estado `catalogo_ciclo` guarda huellas funcionales del catálogo y familias dinámicas evaluadas para distinguir recetas dinámicas ya aplicadas de estrategias nuevas agregadas después.
- **postproceso/tests/test_catalogo_ciclo_fix.py**: Añadidas pruebas de regresión para sesiones recargadas con ciclos activos ya consumidos y para evitar ocultar dinámicas realmente nuevas cuando existe huella previa.

#### Eliminado

##### postproceso

- Sin eliminaciones en esta versión.

### v260706.2133

#### Modificado

##### postproceso

- **postproceso/vista.py**: La vista previa se convierte en modo editor de reportes; al abrirla, el panel izquierdo cambia a controles de identidad visual y al volver restaura los controles normales de postproceso.
- **postproceso/controlador.py**: Conectada la edición de logotipo, texto de encabezado y paleta con la generación temporal de vista previa y con la exportación final del reporte.
- **postproceso/reporteador_pdf.py** y **postproceso/reporteador_pdf_v2.py**: V1 y V2 ahora reciben opciones visuales desde `datos_trabajo`, incluyendo logotipo, entidad emisora y paleta.
- **postproceso/reporte_v1_secciones.py**: Las secciones principales de V1 adoptan la paleta activa del reporte.

#### Agregado

##### postproceso

- **postproceso/tema_reportes.py**: Nuevo catálogo común de 10 paletas de reporte, con `Paleta de colores CyC` como opción predeterminada.
- **postproceso/vista.py**: Añadido indicador de página visible y total de páginas en el lienzo de previsualización.
- **postproceso/vista.py**: Añadidos controles para seleccionar logotipo, editar encabezado, escoger paleta, actualizar la vista previa y guardar/exportar el reporte desde el editor.

#### Eliminado

##### postproceso

- Sin eliminaciones en esta versión.

### v260706.2057

#### Modificado

##### postproceso

- **postproceso/controlador.py**: La vista previa de reportes ahora genera un PDF temporal del formato seleccionado y lo envía al visor, evitando reconstrucciones parciales que omitían secciones, páginas o datos calculados del reporte real.
- **postproceso/vista.py**: El lienzo de vista previa renderiza todas las páginas del PDF real mediante PyMuPDF, conservando la composición, textos, tablas, encabezados y pies del documento final V1/V2.
- **postproceso/reporteador_pdf.py** y **postproceso/reporteador_pdf_v2.py**: Los generadores aceptan una ruta de salida opcional para crear documentos temporales de previsualización sin cambiar el flujo normal de generación final.

#### Agregado

##### postproceso

- **postproceso/controlador.py**: Añadida carpeta temporal `CyC_postproceso_preview` para previsualizaciones sobrescribibles por formato, sin contaminar la carpeta de trabajo con reportes adicionales.

#### Eliminado

##### postproceso

- Se deja de usar la maqueta resumida como fuente principal de la vista previa cuando existe un resultado completo; la fuente visual pasa a ser el PDF generado.

### v260706.2021

#### Modificado

##### postproceso

- **postproceso/vista.py**: Ajustada la vista previa de reportes para usar un lienzo visual tipo hoja, con fondo gris, página blanca centrada, título de previsualización en tiempo real y recalculo responsivo del área desplazable, siguiendo el patrón operativo de la herramienta de presupuestos.

#### Agregado

##### postproceso

- **postproceso/vista.py**: Añadida actualización automática del lienzo al cambiar entre formatos V1/V2 o al renderizar estados sin datos, reiniciando la posición de lectura al inicio de la hoja.

#### Eliminado

##### postproceso

- Sin eliminaciones en esta versión.

### v260706.1845

#### Modificado

##### postproceso

- **postproceso/vista.py**: Modificado el método `actualizar_vista_previa` para usar el módulo `os` (agregando la importación omitida) y cambiar los tamaños de fuente flotantes `7.5` a enteros `8` para evitar excepciones `TclError` en entornos Windows.
- **postproceso/controlador.py**: Refactorizadas las llamadas directas a `btn_abrir_pdf.pack` y `btn_regenerar.pack` reemplazándolas con los métodos dinámicos de visualización de la vista (`mostrar_zona_reportes` y `ocultar_zona_reportes`).

#### Agregado

##### postproceso

- **postproceso/vista.py**: Implementado el visor visual de reporte A4 nativo que renderiza dinámicamente las versiones V1 (Formal) y V2 (Ejecutivo Auditado) a partir de los datos actuales de procesamiento.
- **postproceso/controlador.py**: Añadidos los métodos controladores del visor de reporte (`mostrar_vista_previa_reporte`, `ocultar_vista_previa_reporte`, `cambiar_formato_previa` y `_actualizar_botones_selector_previa`).

#### Eliminado

##### postproceso

- **postproceso/controlador.py**: Realizada limpieza de código redundante y métodos duplicados al final del archivo (flujos duplicados de asistente y presets de experto).

### v260626.0743

#### Modificado

##### postproceso

### Cambiado
- **Alineación visual inicial con la guía CyC:** La interfaz de Postproceso GNSS adopta los tokens oficiales de color de la Suite (`CYC_VERDE`, `CYC_AMARILLO` y neutrales), reduciendo acentos azules, rojos y naranjas en controles, paneles, consola, resultados y diálogos auxiliares.
- **Estructura principal 50/50:** El layout operativo migra a `grid` con dos columnas uniformes y una fila expansible, preparando el módulo para una composición más consistente con la guía visual general.
- **Paneles y tarjetas normalizados:** Los contenedores principales, tarjetas plegables, botones premium, campos de entrada y panel avanzado usan superficies, bordes y textos de la paleta neutral definida para la Suite.
- **Progreso y estados visuales:** Las barras, etiquetas de avance, estados de estrategias y botones de reporte se ajustan a variantes verdes/neutrales para mantener una lectura visual unificada.
- **Estilos ttk aislados:** Los controles `ttk/ttkbootstrap` del módulo usan estilos propios `Postproceso.*`, evitando `bootstyle` genéricos y reduciendo dependencia visual del tema global del Hub.
- **Diálogos auxiliares normalizados:** Las ventanas creadas desde el controlador, incluyendo generación de reportes, línea de control en desarrollo y diagnóstico de convergencia, adoptan la paleta oficial sin acentos heredados.
- **Botones inmunes al tema externo:** Los botones Tk visibles del módulo se crean con `autostyle=False` cuando `ttkbootstrap` está activo, evitando que el tema global vuelva a pintarlos de azul.
- **Columna izquierda desplazable:** La sección de configuración, archivos, parámetros y acciones usa un contenedor con scroll vertical para que los botones inferiores sigan accesibles en ventanas de poca altura.
- **Filas con acciones laterales robustas:** El selector de modo y las entradas de archivos migran a `grid` con columnas mínimas para que botones como `Examinar` o `Línea A-B` no queden recortados al reducir el ancho disponible.
- **Auditoría visual runtime:** Se agrega `auditoria_visual.py` para revisar colores efectivos, estilos `ttk` aplicados en ejecución y posibles recortes de texto en botones, cubriendo casos que no se detectan con una búsqueda estática de código.
- **Punto de inspección en la vista:** `TabPostproceso` expone `auditar_interfaz_visual()` para validar la interfaz activa desde pruebas, consola de desarrollo o futuras herramientas internas.
- **Fase 4 MVC progresiva:** La selección de archivos ya no se resuelve dentro de `vista.py`; la vista emite el evento y el controlador decide el diálogo y la ruta resultante.
- **Línea de control desacoplada:** La ventana experimental A-B se extrae a `vista_linea_control.py`, dejando al controlador con la lógica geodésica, validaciones, reintentos y reportes, pero sin construir directamente filas, etiquetas y botones complejos.
- **Acciones principales siempre visibles:** Los botones de inicio de postproceso y priorización desde reporte se mueven a una barra fija inferior del panel izquierdo, dejando sólo la configuración como zona desplazable.
- **Progreso general más legible:** El porcentaje del avance general se muestra sobre la propia barra de progreso, igualando el patrón visual del proceso actual.
- **Pausa con ancho protegido:** El botón de pausa usa texto breve y columna propia para evitar recortes cuando el estado de estrategias contiene textos largos.

### Verificado
- **Sintaxis validada:** Se compiló `vista.py`, `controlador.py`, `constants.py` y `versiones.py` sin errores después de los ajustes de Fase 1 y Fase 2.
- **Fase 3 validada:** No quedan usos de `bootstyle` en `vista.py`; los `Combobox`, `Notebook`, botones y barras principales usan estilos locales del módulo.
- **Limpieza de colores heredados:** La búsqueda de acentos azules, rojos, naranjas y grises fuera de guía no devuelve coincidencias en `vista.py` ni `controlador.py`.
- **Accesibilidad vertical validada por estructura:** La columna izquierda ya no depende de que todo el contenido quepa simultáneamente en el viewport; el scroll se limita a esa columna para no interferir con la consola ni otros controles con rueda propia.
- **Acciones laterales verificables:** Los botones laterales de filas críticas conservan columna propia y texto breve, evitando recortes parciales de controles en ventanas no maximizadas.
- **Fase 6 validada en runtime:** La auditoría efectiva de `TabPostproceso` en una ventana de prueba `1100x760` reportó `OK: 136 widget(s), 16 boton(es) auditado(s)`.
- **Prueba automatizada de auditoría:** `python -B -m unittest postproceso.tests.test_auditoria_visual` valida que el auditor detecte botones azules heredados y acepte botones con paleta CyC.
- **Fase 4 validada por sintaxis:** Se compiló `vista.py`, `controlador.py` y `vista_linea_control.py` después de extraer el componente de línea de control.
- **Popup A-B verificado:** Se instanció `VentanaLineaControl` con precarga simulada y callbacks externos, confirmando que expone rutas sin ejecutar procesos ni depender de diálogos internos.
- **Footer operativo validado:** Se instanció `TabPostproceso`, se confirmó que los botones principales viven en el footer fijo y que `barra_progreso_general` actualiza el porcentaje embebido.

## rinex
Linea base publicada: `260623.0100`
Changelog fuente:
- `C:\00_PROYECTOS\CyC_Suite\V1_(DEV)\rinex\CHANGELOG.md`

### v260626.0716

#### Modificado

##### rinex

### Añadido
- **Bloque 4 de alineación MVC:** La vista del Asistente RINEX GNSS queda preparada para emitir eventos de interfaz mientras el controlador decide acceso, catálogo y acciones externas.

### Cambiado
- **Versión centralizada de sesión:** El módulo RINEX toma ahora su versión activa desde `versiones.py` con el identificador `260626.0716`.
- **Catálogo de estaciones:** La lista de estaciones RGNA deja de consultarse desde la vista; el controlador la obtiene desde el modelo y la inyecta en el control visual.
- **Asistente manual INEGI:** El cálculo de nombres oficiales pasa al controlador; la vista sólo muestra el texto resultante.
- **Monetización no bloqueante:** El Asistente RINEX GNSS deja de condicionar su ejecución al estado `BASICO`/`Donador`; el botón principal siempre permite iniciar el flujo técnico y el controlador sólo notifica eventos pasivos al sistema de monetización.

### Corregido
- **Dependencias cruzadas en la vista:** Se eliminan imports directos de monetización, modelo RINEX y navegador web desde `vista.py`, reduciendo acoplamiento y preparando una internacionalización futura más limpia.
- **Bloqueo comercial eliminado:** Se retira la compuerta `Requiere Pro` del flujo activo del Asistente RINEX GNSS conforme a la política documentada: la licencia reconoce estados e informa banners, pero no bloquea herramientas, descargas, cálculos ni flujos de trabajo.

### v260625.1813

#### Modificado

##### rinex

### Añadido
- **Inicio de migración visual a la guía CyC:** Se incorporan tokens de paleta oficial en la vista del Asistente RINEX GNSS para preparar la estandarización transversal de la interfaz.
- **Versión centralizada de sesión:** El módulo RINEX toma ahora su versión activa desde `versiones.py` con el identificador `260625.1813`.

### Cambiado
- **Paleta de acentos:** Los controles principales pasan a usar el verde oficial `#1A7B3E` y el amarillo `#FFC439` para acciones restringidas, evitando variantes cromáticas no definidas por la guía.
- **Jerarquía operativa inicial:** La columna de configuración, Rover, servidor y productos queda priorizada a la izquierda; metadatos, ayuda y log quedan a la derecha como zona de resultados/proceso.
- **Estructura 50/50 del flujo principal:** El cuerpo del Asistente RINEX GNSS usa ahora columnas uniformes por `grid`, con configuración/insumos a la izquierda y metadatos/log a la derecha.
- **Ayuda permanente compacta:** El texto descriptivo extenso se reduce a una guía breve para no competir visualmente con los campos operativos ni con el registro técnico.
- **Antenas ATX:** La interfaz ya identifica correctamente el producto de antenas como `igs20.atx`, consistente con el motor de descarga.

### Corregido
- **Acentos fuera de guía:** Se elimina el rojo de la acción principal de unión/descarga y se reemplazan controles secundarios grises por variantes neutrales con borde o texto verde.
- **Estados de advertencia:** Las advertencias de rango horario dejan de depender de texto rojo y se muestran con semántica neutral/accionable.
- **Ajuste responsivo inicial:** El panel de configuración conserva scroll local y el log técnico crece dentro de su columna para reducir ocultamientos en ventanas de menor altura.

## Suite_Core
Linea base publicada: `260705.0219`
Changelog fuente:
- `C:\00_PROYECTOS\CyC_Suite\V1_(DEV)\CHANGELOG.md`

### v260708.0850

#### Modificado

##### Suite_Core

- **Aviso de microparches OTA**: el aviso emergente del updater deja de usar `messagebox` para actualizaciones disponibles y ahora muestra un panel `CustomTkinter` con changelog legible en un cuadro de texto desplazable.
- **Política de microparches**: el updater interpreta `changelog`, `changelog_detallado`, `url_changelog` o `changelog_url` desde `version.json`; si existe URL remota HTTPS, descarga el Markdown para mostrarlo en el aviso.
- **Creador de microparches OTA**: la política `version_schema8.json` generada incluye el placeholder `url_changelog` para publicar el changelog correspondiente en el repositorio de updates.
- **Publicador de microparches OTA**: la pestaña de publicación permite seleccionar, tomar, abrir y editar el changelog OTA; al preparar el microparche copia el Markdown al repo de updates y firma `version.json` con `url_changelog`.

#### Agregado

##### Suite_Core

- **Vista de changelog en arranque**: el panel de actualización incluye área de lectura con scroll para revisar los cambios antes de descargar el microparche o instalador.

#### Eliminado

##### Suite_Core

- **Aviso plano para actualización disponible**: se retira el flujo limitado de `messagebox.askyesno/showinfo` para presentar cambios de actualización.

### v260707.1903

#### Modificado

##### Suite_Core

- **Generador de changelog CyC**: se agregó el canal `parche_acumulativo` para producir notas generales específicas de parches acumulativos OTA.
- **Publicador de releases**: la pestaña Microparche OTA ahora permite generar changelog de microparche normal o acumulativo sin salir del flujo de publicación.
- **Lectura de manifiestos**: el detector de módulos ahora interpreta tanto `seleccionados` de microparches como `archivos[].ruta` de manifiestos acumulativos.

#### Agregado

##### Suite_Core

- **Changelog acumulativo**: se añadió salida `CHANGELOG_GENERAL_PARCHE_ACUMULATIVO_*.md` con título y referencia al manifiesto acumulativo usado.

#### Eliminado

##### Suite_Core

- Sin eliminaciones en esta versión.

### v260707.1842

#### Modificado

##### Suite_Core

- **Creador de microparches OTA**: los archivos `.py` seleccionados ahora se procesan desde una copia temporal sanitizada antes de copiarse crudos o compilarse con Nuitka.
- **Seguridad de distribución parcial**: el flujo de microparches queda alineado con la sanitización del compilador de releases para evitar que bloques internos de desarrollo viajen en parches.
- **Panel de desarrollo del Hub**: se restauró el binding recursivo de tarjetas internas para evitar el error `AttributeError: '_tkinter.tkapp' object has no attribute '_bind_recurse_widget'` al abrir herramientas de desarrollo.
- **Simulaciones del panel dev**: se restauraron helpers locales de `seguridad.py` para entitlement y mantenimiento simulado, evitando errores al abrir la tarjeta "Estados de licencia".

#### Agregado

##### Suite_Core

- **Sanitización DEV_ONLY en microparches**: se agregó eliminación de bloques `# <DEV_ONLY>` / `# </DEV_ONLY>` sobre copias temporales, manteniendo intacto `V1_(DEV)`.
- **Limpieza de temporales auxiliares**: se elimina el directorio de fuentes sanitizadas tanto al terminar correctamente como ante errores de compilación.
- **Estado dev local persistente**: se agregó almacenamiento temporal de simulaciones de desarrollo en AppData, marcado como `DEV_ONLY` para que no viaje a releases.

#### Eliminado

##### Suite_Core

- Sin eliminaciones en esta versión.

### v260706.1906

#### Modificado

##### Suite_Core

- **Pruebas de telemetría**: se alinearon los tests con la política vigente: `reportar()` permanece desactivado cuando la suite se ejecuta desde código fuente Python y se activa únicamente al simular entorno release con `sys.frozen=True`.
- **Versionado core/telemetría**: `versiones.py` actualiza `suite_core` y `telemetria` para reflejar la corrección de verificación automatizada.

#### Agregado

##### Suite_Core

- **Cobertura explícita de modo fuente**: se agregó una prueba que confirma que en Python no se reporta ni se genera cola local.
- **Cobertura explícita de release**: se agregó una prueba que confirma que en entorno congelado/release se encola el evento cuando Supabase no está configurado.

#### Eliminado

##### Suite_Core

- Sin eliminaciones en esta versión.

### v260705.1057

#### Modificado

##### Suite_Core

- **Verificación dual de releases**: `cyc_updater.py` ahora consulta tanto la página pública de distribución como GitHub Releases y selecciona la versión más reciente entre ambas fuentes.
- **Selección de enlace de descarga**: cuando las fuentes no coinciden, el enlace usado por el aviso de actualización corresponde a la fuente que publique la versión mayor detectada.
- **Vista de prueba de actualizaciones**: el panel de desarrollo del Hub reutiliza la misma lectura dual del updater para mostrar al desarrollador el comportamiento que verá un usuario final.
- **Versionado del core**: `suite_core` fue actualizado en `versiones.py` para reflejar cambios realizados en componentes centrales de Main/Hub y updater.

#### Agregado

##### Suite_Core

- **Diagnóstico de fuentes remotas**: el estado de actualización conserva información de versiones detectadas en GitHub Pages y GitHub Releases, consistencia entre fuentes y errores por fuente cuando existan.
- **Preferencia por publicación oficial**: el acceso a la página del release ahora puede abrir la URL de publicación del release seleccionado cuando esté disponible.
- **Regla de mantenimiento del changelog core**: este archivo queda reservado para registrar cambios exclusivos de Main/Hub, updater, telemetría y seguridad.

#### Eliminado

##### Suite_Core

- Sin eliminaciones en esta versión.

## Linea base usada

- `control_personal`: `260518.1000`
- `conversiones`: `260527.2100`
- `datalink`: `260408.1500`
- `gnss`: `260525.2200`
- `linderos`: `260428.1833`
- `postproceso`: `260623.0600`
- `presupuestos`: `260425.1120`
- `rinex`: `260623.0100`
- `suite`: `260705.0219`
- `suite_core`: `260705.0219`
