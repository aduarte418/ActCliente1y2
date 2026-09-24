# Informe de Integración

Este fichero contiene el Informe de Resultados del experimento de Integración en HTML


A continuación, se muestra el resultado obtenido en la pestaña Performance tras abrir las DevTools al cargar por primera vez el HTML sin haber ejecutado aún ningún script.

![](/Actividad2/resources2/screenshots2/ResultadoEstandarDT.png)


Posteriormente, se procede a documentar cada escenario del experimento de integración.
En primer lugar, el script 1 insertado en el head, visualizándose primero el código en el index.html...

![](/Actividad2/resources2/screenshots2/IndexHTMLHeadScript.png)

... y luego el resultado tras consultar las DevTools

![](/Actividad2/resources2/screenshots2/DevToolsHeadScript1.png)

Tarda 0.06 s en pintar el título (en este caso, el mayor elemento visible que se renderiza). Eso sí, se destaca que en la consola salta el error de que no puede preparar las propiedades de un elemento que aún no existe (ya que no ha cambiado el elemento por acción del script), porque se ha ejecutado el script en el head, antes de se hubiera renderizado el texto, situado en el body.

Ahora, se procede a probar el mismo script pero situándolo en el body, justo antes de cerrarse éste y justo después de donde se sitúa el elemento h1 con el título.

Muestra de código:

![](/Actividad2/resources2/screenshots2/IndexHTMLBodyScript1.png)

Captura de DevTools:

![](/Actividad2/resources2/screenshots2/DevToolsBodyScript1.png)

Se puede observar que tarda 0.05 s en pintar el título, pero más importante, que esta vez el texto ha cambiado por el definido en el script1 ("Cambiado por X"), ya que el script se ejecuta una vez que se ha creado el elemento que modifica (al final del body). Además, no se detecta error en consola. 


Se continúan realizando pruebas, en este caso integrando el script async en el head:

![](/Actividad2/resources2/screenshots2/IndexHTMLHeadScriptAsync.png)

En este caso se prueba con el script 3 y se observa que, además del tiempo de 0.07s para pintar el título, ahora el script se ejecuta pese a estar colocado, ya que mientras éste se descarga el HTML continúa pintándose, de modo que una vez descargado el script la página ya estaba formada y éste puede actuar y realizar su correspondiente modificación al título.

![](/Actividad2/resources2/screenshots2/DevToolsAsyncScript3.png)


Después se prueba el script 2 defer en el head:

![](/Actividad2/resources2/screenshots2/IndexHTMLHeadScriptDefer.png)


Los resultados muestran, además del tiempo de 0.06 s, que el script se descargue de forma paralela al procesamiento del HTML, sin pausar ni bloquear este proceso, ejecutándose el script una vez la página ha sido procesada y pintada.

![](/Actividad2/resources2/screenshots2/DevToolsDeferScript2.png)


Finalmente, se prueba a integrar el script como módulo en el head:


![](/Actividad2/resources2/screenshots2/IndexHTMLHeadModuleScript.png)

Ahora se prueba en las DevTools, observándose un tiempo de 0.07 s.

![](/Actividad2/resources2/screenshots2/DevToolsHeadModuleScript.png)

Eso sí, se registran dos errores, apreciados en rojo en la consola. El primero es relativo al acceso al script, especificándose que no se puede utilizar el script como modulo sin un servidor. El segundo registra un fallo de red al apuntar al script.










