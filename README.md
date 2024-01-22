Julio Francés Prieto 2ºASIR

**DOCUMENTACIÓN CIBERSHOP**

Ésta página web está dedicada mayormente al usuario final, pudiendo éste crearse una cuenta, añadir objetos a su carro de compras y pagar por 2 medios distintos los productos que se le enviaran.

No obstante también si accede el usuario con DNI 49465917R tendrá acceso a una pestaña que crea de nuevo la base de datos.

**Estructura de archivos**

Los archivos están ubicados en la misma carpeta

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.001.png)

**Flujo de navegación**

**[Flujo de Navegación.mp4](https://drive.google.com/file/d/1bRtS46S_9AQKg8cJQaObNCTLNwz_6kfW/view?usp=drive_link)**





**index.php**

En esta página, se presenta una breve descripción de la web y los servicios que ofrece. Además, se incluye un menú a la izquierda que proporciona enlaces a diferentes secciones del sitio.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.002.png)

Al pasar el cursor sobre el menú, se destacan las opciones disponibles, aunque algunas de ellas pueden no estar accesibles.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.003.png)

> [!NOTE]
> En el código, se utiliza la variable $\_SESSION['usuario'] para gestionar la sesión del usuario. Si esta variable está definida y su valor es '49465917R', se muestra un enlace adicional que dirige a la página adminPanel.php. Esto indica que el acceso a esta página está reservado para un usuario específico.

En el inicio del código, se configura el manejo de errores de PHP con las líneas:

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.004.png)

Estas líneas permiten mostrar todos los errores durante la ejecución del script, facilitando la detección y corrección de posibles problemas en el código PHP.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.005.png)
























Para poder comprar necesitas estar registrado en la base de datos e iniciado sesión, así es como se hace:

**registrar.php**

Además del menú de la izquierda, en el centro de la página contamos con un formulario en el cual todos los campos son obligatorios:

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.006.png)














En el código está puesto que el patrón del DNI y el del teléfono, además de una función para que al introducir 3 números en el teléfono ponga un espacio y sea más legible y bonito, todos los datos se envían a procesar\_registro.php

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.007.png)

**procesar\_registro.php**

Primero de todo, nos conectamos a la base de datos cibershop con el usuario insertador, el cuál solo puede insertar y seleccionar

Al pulsar el botón de registrarse en procesar registro se comprueba si el método de solicitud es POST (en todos los formularios se comprueba y si no se cumple se imprime no se ha enviado ningún dato y te redirige a formulario.php), luego si el DNI existe, si es así primero se comprueba si existe en la tabla de clientes, si no existe se insertan los datos. Si algo de eso ha dado problemas se indica con el mensaje correspondiente al error.

Seguidamente se imprime un texto en pantalla y se redirige a formulario.php para que puedas iniciar sesión.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.008.png)

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.009.png)

> [!TIP]
> Para hacer que te redirija a formulario.php en 4 segundos, lo he hecho con javascript, coje el span con el id countdown y cada segundo le resta 1 hasta que llegue a 0 a la variable segundo la cual es la que se muestra en el span

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.010.png)

**formulario.php**

En el centro de la página contamos con un formulario con los dos campos necesarios para iniciar sesión.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.011.png)

Al introducir datos en los dos campos y darle a iniciar sesión se procesan los datos en procesar\_login.php

**procesar\_login.php**

En el procesar\_login, se establece una conexión con la base de datos utilizando las credenciales del usuario seleccionador (que tiene privilegios limitados para seleccionar). Se utilizan los datos proporcionados por el formulario anterior, específicamente el DNI y la contraseña.

Primero, realizamos una consulta a la BD para seleccionar la contraseña del usuario cuyo DNI coincide con el proporcionado por el usuario. Luego, verificamos si la consulta ha devuelto algún resultado utilizando mysqli\_fetch\_assoc. Si no se obtiene un resultado, se imprime un mensaje indicando que el usuario no existe en la base de datos.

Si la consulta ha obtenido un resultado, se extrae la contraseña almacenada en la base de datos y se compara con la contraseña proporcionada por el usuario. Si no coinciden, se imprime un mensaje indicando que la contraseña es incorrecta. Si es correcta, primero almacena en la variable de sesión $SESSION[‘usuario’] el DNI y después te redirige a productos.php

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.012.png)

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.013.png)













**productos.php**

En productos.php, como ya tenemos un valor en la variable $SESSION[‘usuario’] nos aparece el contenido de la página. Dentro del div contenido-productos, se encuentran los productos que son cada uno un div.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.014.png)

Esto se hace seleccionando todos los productos y de cada columna obtenida sacar los datos del producto:

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.015.png)

Además también existe un desplegable con todas las categorías disponibles para filtrar. Esto se hace primero haciendo una query a la BD seleccionando los nombres de las categorías que después se ponen como valor del desplegable.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.016.png)

El desplegable tiene un función llamada filtrarProductos() que se activa cuando cambia el valor de este. La función realiza una solicitud AJAX al servidor basándose en la categoría seleccionada por el usuario. El resultado obtenido del servidor se inserta dinámicamente en el contenido de otra parte de la página obtener\_productos.php que hace lo mismo que productos.php pero la consulta se hace indicando la categoría seleccionada por el usuario y actualiza el div identificado por el id "contenido-productos".

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.017.png)

Para añadir un producto al carro podemos indicar las unidades que están limitadas al stock actual del producto. Si hacemos click en añadir al carro primero se muestra un mensaje diciendo producto añadido al carro y seguidamente se ejecuta la función agregarAlCarro() que agrega un producto al carro de compras mediante una solicitud AJAX al servidor. La información del producto, la cantidad y el usuario se envían al servidor para su procesamiento en el archivo PHP anadircarro.php.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.018.png)

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.019.png)

**obtener\_productos.php**

Recibimos el valor de la categoría de productos.php y hacemos la consulta de los productos con esa variable

![ref1]

![ref2]





















**anadircarro.php**

Primero comprueba que exista una sesión y después el método de solicitud. Con el usuario insertador insertamos las variables recibidas en la tabla carrocliente, si ha salido mal se imprime texto y si no no llega a mostrarse esta pagina y es como si productos.php se actualizara

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.022.png)

Si queremos ver el carro del cliente vamos a la página carrocliente.php



**carrocliente.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.023.png)

Funciona como productos.php, seleccionando mediante una sentencia todo de la tabla carrocliente. Además, gracias a que almacenamos el id del producto se puede mostrar mediante otra sentencia el nombre y precio del producto.

Esto se muestra en una formulario que contiene una tabla, que contiene un checkbox en cada línea para indicar cuál artículo quieres comprar o también un checkbox con id select-all que al ser seleccionado por cada checkbox que hay lo pone como seleccionado.

Si hacemos click en comprar seleccionados iremos a procesar\_compra.php

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.024.png)

**procesar\_compra.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.025.png)

Aquí nos encontramos con un ticket con los artículos que queremos comprar, esto se hace primero seleccionando el id del carro que es lo único que pasamos del formulario anterior mediante el checkbox, por lo que ahora tenemos que sacar su id, precio, cantidad de la tabla carrocliente.

Además con el id también sacamos el precio de cada artículo y lo multiplicamos por cada unidad lo que nos da el subtotal de cada carro, seguidamente se añade a $total el subtotal del carro hasta que no haya más carros.

Contamos con dos botones para pagar con tarjeta o contrareembolso, los dos hacen lo mismo pero en el de pago de tarjeta hay 3 campos para indicar la tarjeta aunque no se comprueba que exista.

En cada uno se pasan 2 variables, $carrosSeleccionados que es el id del carro y $cantidad la cantidad de productos del carro

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.026.png)

**pagoContraReembolso.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.027.png)

Con el usuario eliminador nos conectamos a la BD cibershop, si la variable $carrosSeleccionados existe por cada id de carro hacemos las siguientes operaciones: 

- Obtenemos el id del producto, DNI y Stock. 

- Comprobamos que el Stock sea mayor que 0, si lo es hacemos lo siguiente:

  - Insertamos la fecha, el id del producto, las unidades y el DNI. 

  - Eliminamos los datos de carrocliente que coincida con el id del carro

  - Actualizamos el stock restando la cantidad de productos que compramos

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.028.png)








**pagoTarjeta.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.029.png)

En pagoTarjeta.php hay un formulario con tres campos, número de la tarjeta de crédito, CVV y fecha de expiración. El primer campo cuenta con un script para que al introducir 4 números se ponga un espacio y sea más legible y bonito, además se limita la cantidad de carácteres. También se limitan en el CVV y en la fecha de expiración además de poner un patrón para poder enviar el formulario.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.030.png)

**procesar\_pago.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.031.png)

Al enviarse el formulario, se hacen las mismas operaciones de pagoContraReembolso.php

Con el usuario eliminador nos conectamos a la BD cibershop, si la variable $carrosSeleccionados existe por cada id de carro hacemos las siguientes operaciones: 

- Obtenemos el id del producto, DNI y Stock. 

- Comprobamos que el Stock sea mayor que 0, si lo es hacemos lo siguiente:

  - Insertamos la fecha, el id del producto, las unidades y el DNI.

  - Eliminamos los datos de carrocliente que coincida con el id del carro

  - Actualizamos el stock restando la cantidad de productos que compramos




**contacto.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.032.png)

Hay tres campos en los que se tiene que poner el nombre, email y el mensaje a enviar. Cuando le das click a enviar se envía el contenido a procesar-contacto.php

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.033.png)

**procesar-contacto.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.034.png)

Con el usuario insertador nos conectamos a cibershop, seleccionamos los clientes de la bd y verificamos si existe alguno con el email indicado por el usuario. Si es así se inserta el nombre, email, mensaje y fecha actual en la tabla contacto, y después te redirige a productos.php, si no salta un mensaje indicando que el correo debe de estar registrado.

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.035.png)















**cerrarSesion.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.036.png)

En esta parte tenemos dos botones para decir si queremos cerrar sesión, si decimos si se hace un session\_destroy() y nos redirige a formulario.php. Si decimos que no nos redirige a productos.php

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.037.png)















**no\_authorized.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.038.png)

Esta pestaña es a la que nos redirige adminPanel.php cuando no tenemos la variable $SESSION[‘usuario’]=49465917R.


![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.039.png)



















**adminPanel.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.040.png)

A esta página aparece en el menú si la variable $SESSION[‘usuario’]=49465917R (se comprueba en cada página). Dentro de ésta hay un botón que ejecuta crearBD.php

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.041.png)























**crearBD.php**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.042.png)

Al ejecutar crearBD.php, se inicia estableciendo la conexión con el usuario "root" en la base de datos "cibershop". A continuación, se verifica la existencia de la base de datos y se crea si aún no existe. Posteriormente, se procede a eliminar las tablas si ya existen y se vuelven a crear.

El script incluye una función que ejecuta todas las sentencias presentes en archivos SQL. Entre estos archivos, uno se encarga de crear usuarios en la base de datos y asignarles permisos, otro inserta datos de usuarios en la tabla "clientes", y el último introduce información de productos en la tabla "productos".

Al finalizar, se lleva a cabo la destrucción de la sesión, seguida de la redirección a formulario.php. 

> [!WARNING]
> Si se quiere crear todo de una si no esta configurado desde el Visual Studio (por ejemplo) se comenta el primer if de la página (línea 7 a 11) y se puede ejecutar sin errores (siempre que tengas los archivos SQL).

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.043.png)

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.044.png)

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.045.png)

**Base de datos**
> [!NOTE]
> En la base de datos hay 5 tablas:

- Clientes:

  - PK: DNI (Clave Primaria)
  - Restricción única: Correo (Email)
  - Atributos: Contrasena, Nombre, Apellido, Correo, Telefono, Genero, DirEntrega

- Productos:

  - PK: Id\_producto (Clave Primaria)
  - Atributos: Nombre, Descripcion, Precio, Stock, Categoria

- Ventas:

  - PK: Id\_venta (Clave Primaria)
  - FK: Id\_producto (Clave Foránea referenciando Productos), DNI (Clave Foránea referenciando Clientes)
  - Atributos: Fecha, Unidades




- Contacto:

  - PK: Id\_contacto (Clave Primaria)
  - FK: Correo (Clave Foránea referenciando a Clientes)
  - Atributos: Nombre, Correo, Mensaje, Fecha

- CarroCliente:

  - PK: Id\_carro (Clave Primaria)
  - FK: DNI\_cliente (Clave Foránea referenciando a Clientes), Id\_producto (Clave Foránea referenciando Productos)
  - Atributos: Cantidad

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.046.png)




















**Configuración php.ini**

**post\_max\_size = 40M**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.047.png)

**allow\_url\_fopen = off**

![](Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.048.png)

[ref1]: Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.020.png
[ref2]: Fotos/Aspose.Words.f610e770-a25b-401f-8c05-ab6782a68a05.021.png
