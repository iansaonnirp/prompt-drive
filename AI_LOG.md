# Registro de uso de IA

**Equipo:** Ian_Rodriguez_Pulido.
**Autor:** Ian Saonni Rodríguez Pulido. **Cohorte:** COH2.
**Estado:** documentos revisados por el autor; publicación autorizada.
**Entrega seleccionada:** `climate_panel`, `fog_lights`, `ambient_light`.
Las sesiones sobre música, conducción, teclado y lectura documentan el trabajo
de exploración; esos cambios no se incluyen en el PR de estas tres funciones.

## Asistentes usados y tareas

Codex: análisis de las instrucciones de Cabina Abierta, preparación del fork y
la rama, propuesta de acciones, implementación de `ambient_light`, borrador de
la nota de diseño, compilación y comprobaciones en Chrome sin ventana visible.
El usuario eligió desarrollar la luz ambiental con color y transición suave.
La implementación y la nota todavía necesitan la revisión del autor.

## Tres prompts usados

1. Revisar, analizar y clonar `cabina-abierta`, y explicar la actividad y cómo
   correrla. Resultado: materiales clonados y explicación de la separación
   entre la guía del reto y el simulador `prompt-drive`.
2. Comenzar con el fork de `iansaonnirp` y el equipo `Ian_Rodriguez_Pulido`.
   Resultado: fork clonado, etiqueta oficial descargada, rama creada y
   compilación base verificada.
3. Elección: «Luz ambiental: color y transición suave». Resultado: feature DOM
   para nueve colores y OFF, transición CSS, movimiento reducido y nota de diseño.

## Un resultado que requirió corrección

La explicación inicial decía que no hacía falta instalar dependencias. El
proyecto no tiene dependencias declaradas, pero `npm run dev` usa `npx serve`:
en este computador npx necesitó descargar `serve` la primera vez. La ejecución
permitió detectar y corregir esa precisión.

El script de comprobación también necesitó ajustes: inicialmente intentó
serializar un objeto completo del motor, y después asumió que una transición
había terminado tras 500 ms reales. Se corrigió para consultar un booleano,
activar la pestaña y esperar el valor final calculado por el navegador. Estos
fallos pertenecían al script de prueba, no se tomaron como evidencia de éxito.

## Texto y código generado

Codex escribió la primera versión del código y de la nota de diseño.
Porcentaje del system prompt escrito por IA: no aplica; esta sesión no modificó
ningún system prompt de un asistente de conducción.

## Pendientes del autor

Revisar la intensidad y la posición del efecto en conducción de día y de noche,
corregir la nota con sus observaciones y completar su reflexión personal.
No se han inventado observaciones del estudio ni experiencias del autor.

## Segunda sesión: diagnóstico del teclado

El autor pidió explicar el lenguaje, la arquitectura y la organización, y revisar
por qué el teclado dejaba de responder al hacer clic dentro de la demo (3100).
Codex reprodujo el fallo con eventos reales de Chrome: después de enfocar un
campo de la página padre, volver al juego no recuperaba el foco de `game-main`.
El motor cancelaba la acción predeterminada de mousedown, impidiendo esa
recuperación. Enfocar el contenedor explícitamente restauró la recepción de teclas.

La corrección se implementó en `scripts/build-main.js`, mediante un parche
que enfoca únicamente la superficie del juego en pointerdown, antes de que
la consola consuma el evento. Respeta el bloqueo de teclas y los controles de
edición. Este cambio de infraestructura es independiente de la feature de luz
ambiental; al preparar el PR del reto debe revisarse qué archivos se incluyen.

## Tercera sesión: música del vehículo

El autor proporcionó el MP3 Acoustic Folk de AtlasAudio, su enlace de Pixabay y
pidió reproducirlo al poner música, mostrarlo en la consola y revisar el volumen.
Codex encontró que p00 no ejecutaba reproducción y que la API ya tenía volumen
absoluto. Integró el archivo local en el reproductor existente, añadió volumen
relativo, controles y pasos de demo, y documentó el origen/licencia del recurso.
La espera por autorización de audio se comunica al panel de la demo. No se
implementó reconocimiento de voz: las órdenes siguen siendo llamadas de la API.

## Cuarta sesión: inicio y controles externos

El autor pidió retirar la opción musical del panel externo, iniciar con el carro
quieto y abrir navegación en la consola del vehículo. Codex retiró el bloque de
botones musicales y sus manejadores, conservó las órdenes del guion y los controles
táctiles, y cambió el inicio para no restaurar conducción automática, crucero ni
la última aplicación de la consola. Las opciones explícitas de lanzamiento por
URL siguen disponibles para ejecuciones configuradas.

El autor corrigió después el alcance: pidió conservar la recuperación original
de la conducción. Codex retiró los dos parches de inicio de piloto automático
y crucero, y regeneró el motor. Se mantienen navegación como pantalla inicial,
la retirada de botones musicales externos y la corrección del foco del teclado.

## Quinta sesión: panel físico de climatización

El autor pidió un panel como el del Audi A4, debajo de la pantalla y a la
izquierda del conductor, conectado a instrucciones y con animaciones; aportó
una fotografía como referencia. Codex creó un dibujo original en Canvas,
montado como una superficie 3D independiente en la consola. Se adaptó a dos
zonas, las temperaturas disponibles en VehicleState, sin inventar una tercera.

El panel observa temperatura, ventilador, A/C, circulación, dirección del aire,
desempañadores y calefacción de asientos. Los clics explícitos escriben al almacén
validado y respetan el bloqueo benchmark. Las animaciones sólo leen estado y
respetan movimiento reducido. Se conservan la navegación inicial y la
recuperación original de configuración de conducción.

La comprobación con Chrome usó instrucciones por API y clics reales sobre la
superficie 3D. Las capturas permitieron corregir tamaño/posición para evitar
que el volante y el borde de la ventana ocultaran controles. También se corrigió
la carga inicial de la textura cuando el ventilador está apagado y no hay
animaciones. Se regeneró el bundle desde fuentes; no se modificó a mano.

El autor pidió después reducir un poco el módulo y ampliar la pantalla principal.
Codex redujo ancho y alto del clima un 12 % y amplió la pantalla un 12,5 %,
conservando las proporciones, el montaje y la proyección de controles.

El autor aclaró que el acompañante ocupa el lado izquierdo y el conductor el
derecho. Codex invirtió las perillas y los controles de calefacción, junto con
sus campos de estado y las zonas de clic. También añadió las rejillas centrales
del aire entre pantalla y climatización, con dibujo original inspirado en las
cuatro fotografías aportadas: láminas horizontales, pestañas y borde metálico.
Se integraron en el montaje 3D y en su visibilidad y liberación de recursos.

El autor pidió mejorar el acabado visual de las rejillas y añadir una salida
a la derecha. Codex redibujó cavidades, láminas, sombras, pestañas cromadas,
ruedecillas y aluminio cepillado. Añadió una carcasa lateral trapezoidal junto
al cuadro de instrumentos e integró el conjunto central con un inserto metálico.
Se ajustó la posición vertical del clima para que quedaran visibles ambos
controles y las nuevas salidas. Las capturas de Chrome sirvieron para revisar
posición, profundidad y contornos antes de completar la compilación.

## Sexta sesión: lectura y exploradoras

El autor pidió dos luminarias de lectura en el marco superior, exploradoras con
iluminación amarilla del suelo y testigo en el tablero, conectadas a órdenes de
voz. Aclaró que se utilizaría el asistente existente y que no debía añadirse un
botón de micrófono. Codex conservó las llamadas vehicle.set de ese flujo.

Codex sustituyó el ejemplo de lectura por dos carcasas/lentes visibles, con
encendido independiente y asignación según el lado del piloto. Añadió dos focos
3D amarillos en el frontal bajo y el testigo EXPL. ON/OFF en el cuadro principal.
Las pruebas incluyen apagado, independencia, movimiento reducido, modo benchmark
y envío desde la demo; las capturas se revisan para comprobar visibilidad real.
Las primeras capturas permitieron detectar que el prototipo de malla no
mostraba luz aunque el estado indicara encendido. La implementación final usa
focos nativos del motor; se verificó la iluminación visible del pavimento.

## Séptima sesión: preparar la entrega de COH2

El autor eligió climatizador, exploradoras y luz ambiental para entregar.
Codex creó `prompt-drive-entrega` desde el commit de `cabina-abierta-v1.0`,
conservando el desarrollo completo en su carpeta original. La adaptación del
climatizador reúne dibujo, animaciones y rejillas en un archivo de feedback,
elimina los clics que cambiaban estado y utiliza los handles existentes para
montarse en el tablero. El testigo de exploradoras pasa a una malla y textura
propias, sin editar el código del cluster. La luz ambiental mantiene CSS.

La explicación previa de Codex sugirió excluir el climatizador de la entrega.
El autor preguntó por qué no sería feedback; al contrastar el catálogo, Codex
reconoció que clima sí pertenece al reto. La limitación era el alcance de los
archivos y los controles manuales de la implementación, no la categoría.
Este incidente muestra la necesidad de comprobar las recomendaciones de IA
con las reglas y el código antes de decidir qué presentar.

Durante la adaptación, clonar una textura de Three compartía su Source con
la original. Las capturas mostraron mapas repetidos donde debía aparecer el
clima y los demás elementos. Codex corrigió el montaje construyendo texturas
independientes y repitió la comprobación visual. La primera prueba del servidor
Python tampoco respondió al navegador; la validación pasó a servidores HTTP
temporales de Node dentro del mismo proceso de prueba, sin añadir dependencias
ni archivos al PR. Las esperas se ajustaron para verificar el valor dibujado,
en lugar de asumir que una transición terminó en un tiempo fijo de ejecución.

### Tres prompts representativos de las funciones entregadas

1. «Luz ambiental: color y transición suave». Resultado: nueve colores y OFF,
   transiciones CSS y una nota que explica sutileza y limitaciones.
2. Petición de un climatizador como el Audi, debajo de la pantalla, que
   interactúe con las instrucciones y tenga animaciones. Resultado: dibujo
   Canvas de dos zonas; las revisiones ajustaron escala, orientación y rejillas.
3. Petición de exploradoras con testigo en el tablero y camino iluminado de
   amarillo sobre el suelo. Resultado: SpotLights independientes y un testigo
   persistente; la captura visual permitió descartar la primera malla ineficaz.

### Redacción y contribución

Codex escribió el código de las tres funciones, los borradores de notas, este
registro, una descripción del PR y un guion en inglés para el video. También
redactó REFLEXION.md a partir de la experiencia expresada por el autor:
primera aproximación a interfaces de automóviles y acciones mediante LLM,
importancia de precisar los prompts, iteraciones y deseo de una cabina actual.
El autor eligió funciones y referencias, evaluó resultados visuales y pidió
correcciones. Debe revisar que la reflexión represente su experiencia.

No se escribió ni cambió el system prompt del asistente: el porcentaje pedido
por la plantilla no aplica a este trabajo de feedback. No se realizó un estudio
con usuarios ni se grabó o publicó un video de entrega durante esta preparación.
Las comprobaciones técnicas no sustituyen la evaluación humana de distracción.

### Validación final de la entrega

Compilación completa y sintaxis correctas. Chrome verificó snapshot inicial,
clima por zona, ausencia de escrituras durante dibujo/clics en benchmark,
exploradoras independientes y testigo ON/OFF, nueve colores y OFF, movimiento
reducido, desactivación y limpieza/reinicialización. Una segunda ejecución
comprobó recarga y pasos relevantes del guion oficial por postMessage, sin
errores de JavaScript. El script de prueba corrigió una carrera al consultar
el contexto viejo durante una recarga: se espera a que desaparezca y se carga
el nuevo. También se hizo depender la transición de exploradoras del tiempo
transcurrido, para no prolongarla en navegadores que dibujan pocos cuadros.

Los resultados y capturas se guardaron fuera del PR. No se realizaron commits,
push ni publicación. El video en inglés y la revisión personal de los textos
siguen pendientes; no se presentan capturas estáticas como video de entrega.

## Publicación de la entrega

El autor confirmó que revisó los documentos, proporcionó el enlace público de
su video y pidió publicar la entrega. Codex añadió el enlace, repitió la
compilación completa y publicó el commit de código `7da067a` con exactamente
siete archivos. Reflexión y registro se publican en la rama de documentación
del fork, fuera del diff del PR hacia el repositorio original.

Video proporcionado por el autor:
https://drive.google.com/file/d/1BvKci1K0tcKMqeN87mj7C3lh905Hqfpx/view?usp=sharing

El navegador de investigación no pudo abrir el enlace de Drive. La publicación
utiliza el enlace que el autor identificó como público; Codex no afirma haber
verificado la duración ni el contenido del video.
