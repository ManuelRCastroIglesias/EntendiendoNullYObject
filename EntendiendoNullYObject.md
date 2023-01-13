# Entendiendo Null y Object

## ¿Como lo entendí?

## ¿Porqué Null es un Object?

La historia es larga, muy larga; pero intentaré comprimirla, así que perdonen que omita y simplifique muchas cosas.

Las (computadoras / ordenadores / procesadores) son una máquina hecha solo de interruptores (on / off).

Debido a ello es posible hacer cálculos utilizando números en base 2, mediante lógica booleana (verdadero / falso).

Esto por sí solo es muy ineficiente, ya que hay que proporcionar toda la lógica cada vez que se quiere hacer algo un poco más complejo.

Para ello se decidió asignar a cada representación de un carácter (letra o símbolo) un valor numérico con lo que fue posible crear operandos _<kbd style=font-size:1.05rem>(+, -, *, /, etc.)</kvd>_ y variables (aquí me refiero al concepto matemático). A estas representaciones se les llamó _<kbd style=font-size:1.05rem>char</kbd>_ y a la unión de varios _<kbd style=font-size:1.05rem>char</kbd>_ se les llamó _<kbd style=font-size:1.05rem>string</kbd>_.

Ahora ya tenemos números (en base 2) y variables; los operandos se puede decir que es una variable que contiene una lógica booleana.

Y con estas herramientas ya estamos en posición de hacer cálculos complejos, ¿... o no?

Bueno... sí podemos, pero aún tenemos que escribir todas las operaciones cada vez.

¡Pero llegó la memoria!, es decir, la capacidad de almacenar un valor o resultado en una caja. Pero para que esto fuese útil era necesario que esa caja tuviera una forma de ser identificada, y para ello se le asignó una dirección (puntero) mediante el cual se podía recuperar lo guardado allí. Esto trajo la posibilidad de guardar algo en una caja específica.

Hasta aquí la cosa es conocimiento básico, ahora avancemos un paso más allá.

La memoria es una cosa física (objeto), y tiene existencia propia, se use o no.

Cuando no se usa, se puede decir que está vacía _<kbd style=font-size:1.05rem>empty</kbd>_ y cuando se usa, contiene algo en esa dirección.

Con lo que sabemos hasta ahora ya podemos _definir_ lo que llamaremos *primitivos*:
- _<kbd style=font-size:1.05rem>boolean</kbd>_ *true y false*, necesarios para la lógica booleana.
- _<kbd style=font-size:1.05rem>number</kbd>_ *números* que son una secuencia de unos y ceros (base 2).
- _<kbd style=font-size:1.05rem>char / string</kbd>_ *carácter o cadena* que son una secuencia especial de unos y ceros que representan ese carácter o cadena.
- <kbd style=font-size:1.05rem>empty</kbd> que representa una posición de memoria vacía y no está descrita en ningún lenguaje (por lo que yo sé) ya que es implícita.
- <kbd style=font-size:1.05rem>reference</kbd> referencia a una posición de memoria y que no se considera un primitivo propiamente dicho, y también es implícita.

y ya podemos entender lo que significa pasar *por valor* o *por referencia*, lo primero es pasar el contenido y lo segundo su ubicación.

Pero recordar cada posición de memoria *referencia* es complicado, así que le ponemos una etiqueta a esa posición y la llamamos *propiedad o clave* _<kbd style=font-size:1.05rem>key</kbd>_.

Con esto ya podemos entender lo que es un _<kbd style=font-size:1.05rem>Object</kbd>_, y es el par _<kbd style=font-size:1.05rem>{key, value}</kbd>_ _<kbd style=font-size:1.05rem>{propiedad: valor}</kbd>_, o lo que es lo mismo, el nombre de la etiqueta y su contenido.

Y ya podemos definir unos nuevos primitivos:
- el _<kbd style=font-size:1.05rem>NULL</kbd>_, que es el _<kbd style=font-size:1.05rem>Object {empty, empty}</kbd>_, es decir, el objeto que no tiene ni etiqueta, ni contenido; pero sí es una posición de memoria.
- el _<kbd style=font-size:1.05rem>UNDEFINED</kbd>_, que es el _<kbd style=font-size:1.05rem>Object{key, empty}</kbd>_, es decir, el objeto que tiene una etiqueta, pero, en el que aún no hemos guardado nada.

¿Y qué pasa con los objetos, posiciones de memoria, en las que guardamos un valor y no le ponemos una etiqueta?  
Vale, por convención (porqué así se decidió), se dice que la etiqueta es idéntica al valor y ese contenido en memoria está "congelado" no sé puede cambiar, es decir, es ***inmutable***, y por lo tanto equivale a un ***primitivo***; por lo que no se permite guardar algo sin etiquetar que no sea un ***primitivo***.

Antes de continuar veamos que otros ***objetos primitivos*** se han definido y porqué.
- _<kbd style=font-size:1.05rem>bigint</kbd>_, números muy grandes, debido a cómo se definieron los valores numéricos que están limitados en tamaño (no caben todos), y a la necesidad de usar números mayores; se decidió añadir la posibilidad de representar un número en forma de cadena, pero considerándolo siempre como un número. ¡Complicado! pero es la mejor solución posible por el momento.
- _<kbd style=font-size:1.05rem>symbol</kbd>_, *símbolo*; debido al comportamiento y limitaciones de los _<kbd style=font-size:1.05rem>object</kbd>_ y a los problemas que ocasionaban dichos comportamientos, fue necesario crear este tipo de primitivo, que no es más que hacer que la _<kbd style=font-size:1.05rem>key</kbd>_ pudiese ser única e inmutable. Pero esto permite crear elementos primitivos complejos, que siempre se pasarán por valor y no por referencia.
- _<kbd style=font-size:1.05rem>date</kbd>_, valores de tipo fecha o tiempo, esto está propuesto desde hace ya, bastante tiempo, pero por causa de que no existe un sistema único para representarlo no ha logrado avanzar en su implementación. A mí, se me ocurre pensar que pudiese utilizarse el ISO como estándar, y añadir un método de conversión a las necesidades del programador o programa. Esto no rompería necesariamente la web; ya que las versiones anteriores, al no usar esa etiqueta de primitivo no se verían afectadas y proporcionarían el marco inicial para la estandarización del código. Está el problema de que nombre darle, por supuesto, pero como ahora ya es posible utilizar como identificador caracteres Unicode, es posible añadir un nuevo prefijo (p. e. _<kbd style=font-size:1.05rem>™</kbd>_ _<kbd style=font-size:1.05rem>U+2122</kbd>_ o mejor aún _<kbd style=font-size:1.05rem>®</kbd>_ _<kbd style=font-size:1.05rem>U+00AE</kbd>_) ya que ellos permitirían usar las actuales palabras clave como identificadores; mejor aún los símbolos _<kbd style=font-size:1.05rem>º</kbd>_ y _<kbd style=font-size:1.05rem>ª</kbd>_ que por lo que sé, están en casi todos los teclados, y por lo que son fáciles de insertar, harían con ello toda la programación nueva más estable y confiable.

Después de ver los primitivos intentaré explicar por qué un _<kbd style=font-size:1.05rem>NULL</kbd>_ es de tipo _<kbd style=font-size:1.05rem>Object</kbd>_; como expliqué anteriormente, el _<kbd style=font-size:1.05rem>Object</kbd>_ es en realidad un _<kbd style=font-size:1.05rem>Object{key: value}</kbd>_ donde el _<kbd style=font-size:1.05rem>value</kbd>_ es un primitivo, pero en realidad, al final, puede guardar cualquier cosa, ¡incluso otro _<kbd style=font-size:1.05rem>Object</kbd>_!, por lo que podemos decir que cualquier _<kbd style=font-size:1.05rem>Object</kbd>_ es una colección de _<kbd style=font-size:1.05rem>Object</kbd>_, y el _<kbd style=font-size:1.05rem>Object</kbd>_ más simple, es decir el más básico, es el _<kbd style=font-size:1.05rem>Object{key: value}</kbd>_ que está vacío _<kbd style=font-size:1.05rem>Object{empty, empty}</kbd>_; y es por ello que podemos decir que _<kbd style=font-size:1.05rem>NULL</kbd>_ es el primitivo de todo _<kbd style=font-size:1.05rem>Object</kbd>_ y además es también, por lógica, un _<kbd style=font-size:1.05rem>Object</kbd>_.

Espero que haya quedado claro.

## ¿Y, ... eso es todo lo que se necesita para programar?

**Empecemos por entender lo que es programar** Programar es crear una serie (secuencial) de instrucciones (operaciones) para obtener un resultado, es decir, una especie de receta. ¡Sencillo! ¿no?

A cada instrucción la llamaremos **Sentencia** y al conjunto de **sentencias** (receta) las llamaremos programa o rutina, utilizo el término *rutina* de forma intencional, ya que será necesario para explicar otras cosas más adelante.

Como comenté en la sección anterior en el caso de hacer operaciones, aquí pasa lo mismo. Habrá que escribir, una y otra vez, toda la lógica.

Para mejorar y simplificar eso, se decidió asignar a cada instrucción **sentencia** un número, se puede decir que a cada **sentencia** se le asignó una posición de memoria, por lo que cada **sentencia** es un objeto en el que la _<kbd style=font-size:1.05rem>key</kbd>_ es un número entero positivo, es decir, un **número natural** y con eso, sí, ya podemos empezar a hacer programación.

- Una aclaración: Los números naturales es el conjunto de los enteros positivos, y este conjunto empieza en **¡cero!** y no en **uno**. Esto nos lleva a una curiosidad informática, los índices como están numerados secuencialmente con un número natural, todos empiezan en **cero**. Y no es algo que hayan inventado los informáticos, sino que es una consecuencia lógica del uso de dicho sistema de numeración. ***¡Y que no te cuenten cuentos!***.

Ahora observamos que tenemos que escribir una y otra vez la misma instrucción, es decir, repetir y repetir.

Para evitarlo se inventaron dos cosas:
- Guardar la instrucción *sentencia* en una variable _<kbd style=font-size:1.05rem>Object</kbd>_ para volver a llamarla,
- y una instrucción llamada _<kbd style=font-size:1.05rem>GOTO</kbd>_, que no es otra cosa que saltar (*ir a*) hacia adelante (*a una línea posterior*), o hacia atrás (*a una línea anterior*) y con eso ya podemos hacer ciclos también llamados _*bucles*_.

### ¡Y por fin, nació la informática!

Pero leer y entender el código era un suplicio.

Como la ***rutina*** (programa) tenía una instrucción **END** que indicaba donde terminaba, a algún avispado, se le ocurrió que si esos ciclos o trozos de código ***subrutinas*** que se repetían una y otra vez, podía ponerlas después del final, y llamarlas con el _<kbd style=font-size:1.05rem>GOTO</kbd>_ y mediante otro _<kbd style=font-size:1.05rem>GOTO</kbd>_ regresar a donde la habían llamado. El proceso era más o menos así, primero guardabas el número de línea en una variable, te desplazabas con el _<kbd style=font-size:1.05rem>GOTO</kbd>_ a la **subrutina** y al final de ésta con otro _<kbd style=font-size:1.05rem>GOTO</kbd>_ te desplazabas al número de línea que habías guardado antes.  
Pero a pesar de que esto ayudaba a escribir menos código repetido, seguir la secuencia del programa era un verdadero infierno.

Otro genio se dijo: _"¿Y si hago lo mismo que hicimos con las variables, es decir, a la línea, y a la subrutina les pongo una etiqueta?"_ **¡SORPRESA, REALMENTE FUNCIONÓ!**, el código se volvió mucho más legible y comprensible.

Pero otros _<kbd style=font-size:1.05rem>(que de haberlas, hailas)</kbd>_ empezaron a hacer cosas, muy, pero que muy raras, como acceder a posiciones de memoria a los que no debían acceder; o desde una **subrutina** saltar a otra y de ahí, a otra, y haciendo ciclos rarísimos, inventando así **¡EL CÓDIGO ESPAGUETI!**.

Otro genio más, este de los buenos, se dijo: _¿Y si..., tuviera una instrucción que al saltar se llevase el valor de la variable, no tendría que acordarme de ponerla en la subrutina, tan solo con decirle al final que regresase a dónde fue llamada, así podría mejorar y simplificar el código?_ y se inventó el _<kbd style=font-size:1.05rem>GOSUB[etiqueta] ... RETURN</kbd>_.

Otro, viendo lo anterior, se inventó, una instrucción a la que llamó _<kbd style=font-size:1.05rem>FOR ... TO ... ENDFOR</kbd>_.

Otro, se inventó, la instrucción _<kbd style=font-size:1.05rem>IF ... THEN ... ENDIF</kbd>_

Algún otro, mejoró esta última y la cambió por _<kbd style=font-size:1.05rem>IF ... THEN ... ELSE ... ENDIF</kbd>_

A otro más, se le ocurrió combinar el _<kbd style=font-size:1.05rem>IF</kbd>_ y el _<kbd style=font-size:1.05rem>FOR</kbd>_ y se inventó, el _<kbd style=font-size:1.05rem>WHILE ... ENDWHILE</kbd>_

Otro hizo una variante, el _<kbd style=font-size:1.05rem>DO ... WHILE</kbd>_ con lo que se ahorraba el _<kbd style=font-size:1.05rem>ENDWHILE</kbd>_

#### ¡Y la cosa empezó a coger velocidad, rápidamente!

A partir de este punto solo voy a listar los cambios sin muletillas.

* **funciones** Las funciones surgen, para solventar el problema de pasar valores a las **subrutinas** mediante **GOSUB**, y supongo que quien lo hizo fue un matemático, ya que la solución fue utilizar la notación (_manera de representar las cosas_) en que se escriben las fórmulas o funciones matemáticas; es decir, *_<kbd style=font-size:1.05rem>f(x){operaciones}=resultado</kbd>_* con lo que quedaría *_<kbd style=font-size:1.05rem>GOSUB(var, var, ... ){sentencias, ..., return}</kbd>_*; pero para que la instrucción tuviese un nombre nuevo y como se basó en la notación matemática de las funciones se usó el término:  
**`function etiqueta( ){ }`** y para llamarlas se usa **` etiqueta( )`**.
 
 Y a la manera de programar organizando el código mediante **`function( ){ }`** se le denominó
 ##### PROGRAMACIÓN ESTRUCTURADA en funciones,
 a lo que muchos programadores, hoy en día, les gusta llamar **programación funcional** porqué usan la notación de las funciones, _a las que llaman **method** (métodos)_, en los lenguajes modernos, y así evitar decir que usan la notación de la programación estructurada, que se considera anticuada.

 * El siguiente avance fue encapsular los **`method`** junto a sus variables, _que pasaron a llamarse **parameter** o parámetros_, y guardándolas en objetos _<kbd style=font-size:1.05rem>Object{parameter: value, ..., method: function(){} ... }</kbd>_  y la vamos a llamar _<kbd style=font-size:1.05rem>OBJECT</kbd>_. ¡Menuda ocurrencia! y después le vamos a cambiar el nombre por el de _<kbd style=font-size:1.05rem>CLASS</kbd>_ cuándo nos damos cuenta de que _<kbd style=font-size:1.05rem>OBJECT</kbd>_ ya se usaba para otra cosa, y a esta "NUEVA" forma de programar la llamaremos **PROGRAMACION ORIENTADA EN OBJETOS** _<kbd style=font-size:1.05rem>¡Toma ya! ¡pero que listos somos!</kbd>_ ¿Y no acabo de entender por qué no le cambiamos el nombre a "programación orientada en clases"?

 #### ¿Y de dónde surge la manía de cambiarle el nombre a todo, cuando se hace una mejora o modificación?
 Bueno, ¡es interesante!  
 Cuando **Edsger Wybe Dijkstra** decide publicar un ensayo (carta) en donde explica por qué considera que los lenguajes de alto nivel, más cercanos al lenguaje humano, deben prohibir el uso del _<kbd style=font-size:1.05rem>GOTO</kbd>_, el editor de esta y por razones puramente comerciales, decidió titularla ___Go To Statement Considered Harmful___ _(La sentencia Goto considerada perjudicial)_. Los _gurús_ (maestros) de la programación interpretaron ___Harmful___ como **peligroso o malévolo**, cuando **Dijkstra** solo decía que era perjudicial para la programación por ser innecesaria, al haber otros mecanismos (_forma de hacer las cosas_) más modernos y menos propensos a generar comportamientos de baja calidad.  Y de ahí la aversión general a usar terminología anterior o anticuada.  
 Siguiendo ese mismo modo de pensar, tenemos varias etiquetas que se encuentran en la misma situación _, `var, div y otras</kbd>_, las cuales no se prohíben porqué su uso está tan extendido que provocaría un verdadero caos en los programas más antiguos.  

 Hablemos un poco de ellas.

 La etiqueta _<kbd style=font-size:1.05rem>div</kbd>_ que su uso está prácticamente restringido al lenguaje *HTML* y similares.  
 Cuando se definió por primera vez tenía la intencionalidad de ser un contenedor genérico para englobar otras cosas, pero lo mismo que con _<kbd style=font-size:1.05rem>GOTO</kbd>_, se empezó a usar para todo, y surgieron nuevas etiquetas más específicas, que mediante su semántica permiten mejorar la calidad y comprensión del código. Pero los programadores, que no es que les agrade mucho eso de cambiar su manera de hacer las cosas, insisten en seguir usándolas a pesar de todo, y los que hacen los **estándares** por el temor a romper lo que ya está hecho, no prohíben su uso.

Algo similar sucede con la etiqueta _<kbd style=font-size:1.05rem>var</kbd>_ para la que se han creado, en dos fases, tres nuevas etiquetas, _<kbd style=font-size:1.05rem>let, const y symbol</kbd>_ las dos primeras de uso en prácticamente todos los lenguajes modernos tienen el siguiente uso:
- _<kbd style=font-size:1.05rem>let</kbd>_ para las variables que van a cambiar de valor a lo largo del tiempo.
- y _<kbd style=font-size:1.05rem>const</kbd>_ para aquellas variables que mantienen fijo su valor, (p. e. _PI = 3.141592..._).

Éstas etiquetas, en JavaScript y lenguajes afines, su comportamiento está más relajado, _<kbd style=font-size:1.05rem>let</kbd>_ es equivalente a _<kbd style=font-size:1.05rem>var</kbd>_ pero restringiendo su uso al contenedor _<kbd style=font-size:1.05rem>Object</kbd>_ también llamado ___scope___ o ámbito, y así evitar que a dicha variable pueda accederse desde cualquier lugar, pero pudiendo redefinirla para que contenga una cosa diferente. Y la etiqueta _<kbd style=font-size:1.05rem>const</kbd>_ que impide redefinirla, pero aún le permite cambiar su valor.

¿Y cómo hacemos que esa variable, no sólo, no se pueda redefinir si no que tampoco se le pueda cambiar su valor?, bueno pues como ya nos estamos acostumbrando, definimos una nueva etiqueta llamada _<kbd style=font-size:1.05rem>symbol</kbd>_ y como nos consideramos muy listos, le añadimos un montón de funcionalidades extras, haciéndola sumamente complicada. Pero eso sí, seguimos sin prohibir el uso de _<kbd style=font-size:1.05rem>var</kbd>_ y los programadores insistimos en seguir usando esa etiqueta.


