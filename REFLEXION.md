# Reflexión

**Equipo:** Ian_Rodriguez_Pulido.  
**Integrante:** Ian Saonni Rodríguez Pulido. **Cohorte:** COH2.  
**Features entregadas:** `climate_panel`, `fog_lights`, `ambient_light`.  
**Enlace al pull request:** pendiente de publicación.

## Qué quería lograr

Nunca había trabajado con una interfaz simulada relacionada con automóviles.
Tampoco conocía el uso de modelos de lenguaje y prompts para ejecutar acciones
en un vehículo. Quería que las instrucciones se percibieran dentro de la cabina:
que cambiar el clima, encender las exploradoras o elegir un color ambiental
tuviera una respuesta visible, además de la confirmación del asistente. Escogí
estas funciones porque combinan confort, información persistente y efectos
que se pueden observar en la simulación.

## Qué diseñé y qué pasó

Para el climatizador utilicé referencias de un Audi y pedí perillas, rejillas y
animaciones. Al verlo funcionando ajusté el tamaño del módulo y la pantalla, y
corregí la orientación: en nuestro vehículo el acompañante está a la izquierda.
Para las exploradoras pedí un indicador de encendido en el tablero y luz
amarilla sobre el suelo. Para la iluminación ambiental elegí color y transición
suave. La preparación de la entrega llevó a separar estas representaciones de
los controles manuales y de otras mejoras que habíamos desarrollado.

## Dónde la IA me ayudó y dónde me engañó

La IA ayudó a analizar el código, convertir mis referencias en dibujos y
conectar las representaciones con el estado del vehículo. Sin embargo, una
propuesta inicial invirtió la ubicación de las perillas respecto a los ocupantes.
Lo detecté al revisar el resultado y pedí la corrección con referencias. También
se aclaró que el climatizador sí corresponde al catálogo de feedback: lo que
necesitaba adaptarse era su implementación para cumplir el alcance del PR.

## Qué haría con un segundo día

Me gustaría acercar la simulación a un carro actual, con más pantallas y una
apariencia más atractiva. Siento que la parte visual es importante para entender
el funcionamiento de la cabina. También comprobaría qué información sigue
siendo legible mientras se conduce y qué efectos pueden distraer.

## Qué aprendí

Aprendí que pequeñas palabras en un prompt pueden cambiar mucho el resultado.
A veces ocho intentos no bastan para que una IA haga lo que uno imagina. No
basta con tener una idea: hay que saber escribirla, aportar referencias y
revisar lo que aparece en pantalla. Me llevo la importancia de describir la
posición, el comportamiento y la relación con las instrucciones, y de verificar
el resultado en lugar de asumir que la primera respuesta cumple lo pedido.
