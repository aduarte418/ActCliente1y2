# Informe de Auditoría y Rendimiento Web

Este fichero contiene el Informe de Auditoría Web con sus respectivas capturas de pantalla. 

En primer lugar, se selecciona una web SPA dinámica, como Youtube en este caso. Se pulsa la tecla F12 para acceder a las DevTools y aparece la siguiente pantalla junto al contenido de la web.

![](/resources/screenshots/ViewYT.png)

Después se hace clic en la opción Network para comenzar con la Auditoría de Red. Aparecerá la siguiente vista:

![](/resources/screenshots/ViewNetworkF12.png)

Una vez aquí se podrán examinar las pestañas "Doc" y "JS". 

Se recarga la página y se puede observar la siguiente imagen:

![](/resources/screenshots/ViewNetworkDoc.png)

La pestaña Doc muestra que el tamaño del HTML inicial que envía el servidor es 17.179 kB

Por otro lado, la pestaña JS muestra el tamaño total de los scripts de JavaScript en la siguiente imagen, el cual es 21.254 kB.

![](/resources/screenshots/ViewNetworkJS.png)


De acuerdo al HTML examinado en la pestaña Doc, Youtube utiliza SSR o CSR


· Análisis del Motor del navegador

Para analizar el motor del navegador, se ha realizado una pequeña grabación de rendimiento de unos 5 segundos, quedando en la pestaña Performance un registro a modo de línea del tiempo de las fases ejecutadas.

Se puede apreciar que, en primer lugar, durante el primer segundo, justo después de realizar la petición para mostrar la página web, se ejecutan las fases de Parsing HTML y Evaluate Script (franjas azul y amarilla respectivamente, como se puede observar). 

![](/resources/screenshots/ViewPerformanceParsingEvaluate.png)

En este momento, el motor del navegador está leyendo el código y convirtiéndolo a la estructura AST (Árbol de Sintaxis Abstracta) durante la fase de Parsing. Después es interpretado y transformado en un bytecode que es evaluado en la fase Evaluate Script.

Posteriormente, cuando han transcurrido unos dos segundos, y después de haber vuelto a ejecutar las fases de Parsing y Evaluate Script, así como otras muchas tareas que incluyen evaluar el estilo de la página, tiene lugar la fase de Compile Code (JIT), en color rosado y localizable en la penúltima franja.

![](/resources/screenshots/ViewPerformanceJIT.png)

En este momento, una vez que se ha interpretado el código y se han revisado las partes más ejecutadas (hot code), el motor lo compila directamente a código máquina que se ejecuta en un instante (fase de Compilador Optimizador JIT).


· Análisis del Sandbox a través de Console

Se abre la pestaña Console y se ejecuta la línea de código 'const a = "eoo"; console.log(a);'. El resultado se muestra en la siguiente captura:  

![](/resources/screenshots/ViewConsoleLog.png)

Como se puede observar, sólo imprime por consola el valor de una variable (constante) declarada previamente.


En cambio, después se prueba un código "maligno" que intente leer un archivo del disco duro (un simple FileReader, por ejemplo), aparece el siguiente error:

![](/resources/screenshots/ViewConsoleError.png)

Salta error al leer el archivo porque al intentar forzar que se lea un archivo de una ruta determinada directamente, sin pedir input al usuario para seleccionar o arrastar el archivo a leer, 


· Análisis de Bloqueo

Si se vuelve a la pestaña Network y se revisan los scripts de JavaScript, en este caso se observa que no hay scripts que lleguen a pesar 1 MB (el mayor es de 14 kB). 

![](/resources/screenshots/ViewConsoleScript.png)
En caso de que el script llegase a ser más pesado, si el script se ejecutase de manera síncrona, 


