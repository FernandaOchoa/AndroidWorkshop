# Aspectos fundamentales de la aplicación

Las aplicaciones de Android se escriben en lenguaje de programación Java. Las herramientas de Android SDK compilan tu código, junto con los archivos de recursos y datos, en un APK: un paquete de Android, que es un archivo de almacenamiento con el sufijo `.apk.` Un archivo de APK incluye todos los contenidos de una aplicación de Android y es el archivo que usan los dispositivos con tecnología Android para instalar la aplicación.

Una vez instalada en el dispositivo, cada aplicación de Android se aloja en su propia zona de pruebas de seguridad: 

* El sistema operativo Android es un sistema Linux multiusuario en el que cada aplicación es un usuario diferente.
* De forma predeterminada, el sistema le asigna a cada aplicación una ID de usuario de Linux única (solo el sistema utiliza la ID y la aplicación la desconoce). El sistema establece permisos para todos los archivos en una aplicación de modo que solo el ID de usuario asignado a esa aplicación pueda acceder a ellos.
* Cada proceso tiene su propio equipo virtual (EV), por lo que el código de una aplicación se ejecuta de forma independiente de otras aplicaciones.
* De forma predeterminada, cada aplicación ejecuta su proceso de Linux propio. Android inicia el proceso cuando se requiere la ejecución de alguno de los componentes de la aplicación, luego lo cierra cuando el proceso ya no es necesario o cuando el sistema debe recuperar memoria para otras aplicaciones.  

De esta manera, el sistema Android implementa el principio de mínimo privilegio. Es decir, de forma predeterminada, cada aplicación tiene acceso solo a los componentes que necesita para llevar a cabo su trabajo y nada más. Esto crea un entorno muy seguro en el que una aplicación no puede acceder a partes del sistema para las que no tiene permiso.

Sin embargo, hay maneras en las que una aplicación puede compartir datos con otras aplicaciones y en las que una aplicación puede acceder a servicios del sistema: 

* Es posible disponer que dos aplicaciones compartan la misma ID de usuario de Linux para que puedan acceder a los archivos de la otra. Para conservar recursos del sistema, las aplicaciones con la misma ID de usuario también pueden disponer la ejecución en el mismo proceso de Linux y compartir el mismo EV (las aplicaciones también deben estar firmadas con el mismo certificado).
* Una aplicación puede solicitar permiso para acceder a datos del dispositivo como los contactos de un usuario, los mensajes de texto, el dispositivo de almacenamiento (tarjeta SD), la cámara, Bluetooth y más. 

Esto cubre los aspectos básicos sobre cómo una aplicación de Android existe en el sistema. El resto de este documento te presenta lo siguiente:

* Los componentes del framework central que define tu aplicación.
* El archivo de manifiesto en el que declaras los componentes y las funciones necesarias del dispositivo para tu aplicación.
* Los recursos independientes del código de la aplicación y que permiten que tu aplicación optimice correctamente su comportamiento para una variedad de configuraciones de dispositivos. 

## Componentes de la aplicación 
Los componentes de la aplicación son bloques de creación esenciales de una aplicación para Android. Cada componente es un punto diferente a través del cual el sistema puede ingresar a tu aplicación. No todos los componentes son puntos de entrada reales para el usuario y algunos son dependientes entre sí, pero cada uno existe como entidad individual y cumple un rol específico; cada uno es un bloque de creación único que ayuda a definir el comportamiento general de tu aplicación.

Hay cuatro tipos diferentes de componentes de una aplicación. Cada tipo tiene un fin específico y un ciclo de vida diferente que define cómo se crea y se destruye el componente.

Aquí te mostramos los cuatro tipos de componentes de una aplicación: 

**Actividades**
Una *actividad* representa una pantalla con interfaz de usuario. Por ejemplo, una aplicación de correo electrónico tiene una actividad que muestra una lista de los correos electrónicos nuevos, otra actividad para redactar el correo electrónico y otra actividad para leer correos electrónicos. Si bien las actividades trabajan juntas para proporcionar una experiencia de usuario consistente en la aplicación de correo electrónico, cada una es independiente de las demás. De esta manera, una aplicación diferente puede inicial cualquiera de estas actividades (si la aplicación de correo electrónico lo permite). Por ejemplo, una aplicación de cámara puede iniciar la actividad en la aplicación de correo electrónico que redacta el nuevo mensaje para que el usuario comparta una imagen.

Una actividad se implementa como una subclase de `Activity`y puedes obtener más información acerca de este tema en la guía para desarrolladores [Actividades](https://developer.android.com/guide/components/activities/).

**Servicios**

Un servicio es un componente que se ejecuta en segundo plano para realizar operaciones prolongadas o tareas para procesos remotos. Un servicio no proporciona una interfaz de usuario. Por ejemplo, un servicio podría reproducir música en segundo plano mientras el usuario se encuentra en otra aplicación, o podría capturar datos en la red sin bloquear la interacción del usuario con una actividad. Otro componente, como una actividad, puede iniciar el servicio y permitir que se ejecute o enlazarse a él para interactuar.

Un servicio se implementa como una subclase de `Service` y puedes obtener más información acerca de este tema en la guía para desarrolladores [Servicios](https://developer.android.com/guide/components/services).

**Proveedores de contenido**
Un *proveedor de contenido* administra un conjunto compartido de datos de la app. Puedes almacenar los datos en el sistema de archivos, en una base de datos SQLite, en la Web o en cualquier otra ubicación de almacenamiento persistente a la que tu aplicación pueda acceder. A través del proveedor de contenido, otras aplicaciones pueden consultar o incluso modificar los datos (si el proveedor de contenido lo permite). Por ejemplo, el sistema Android proporciona un proveedor de contenido que administra la información de contacto del usuario. De esta manera, cualquier app con los permisos correspondientes puede consultar parte del proveedor de contenido (como `ContactsContract.Data`) para la lectura y escritura de información sobre una persona específica.

Los proveedores de contenido también son útiles para leer y escribir datos privados de tu aplicación y que no se comparten. Por ejemplo, la aplicación de ejemplo `Bloc de notas` usa un proveedor de contenido para guardar notas.

Un proveedor de contenido se implementa como una subclase de `ContentProvider` y debe implementar un conjunto estándar de API que permitan a otras aplicaciones realizar transacciones. Para obtener más información, lee la guía para desarrolladores [Proveedores de contenido](https://developer.android.com/guide/topics/providers/content-providers).

**Receptores de mensajes**

Un *receptor de mensajes* es un componente que responde a los anuncios de mensajes en todo el sistema. Muchos mensajes son originados por el sistema; por ejemplo, un mensaje que anuncie que se apagó la pantalla, que la batería tiene poca carga o que se tomó una foto. Las aplicaciones también pueden iniciar mensajes; por ejemplo, para permitir que otras aplicaciones sepan que se descargaron datos al dispositivo y están disponibles para usarlos. Si bien los receptores de mensajes no exhiben una interfaz de usuario, pueden `crear una notificación de la barra de estado` para alertar al usuario cuando se produzca un evento de mensaje. Aunque, comúnmente, un receptor de mensajes es simplemente una "puerta de enlace" a otros componentes y está destinado a realizar una cantidad mínima de trabajo. Por ejemplo, podría iniciar un servicio para que realice algunas tareas en función del evento.

Un receptor de mensajes se implementa como una subclase de `BroadcastReceiver` y cada receptor de mensajes se proporciona como un objeto `Intent`. Para obtener más información, consulta la clase [BroadcastReceiver](https://developer.android.com/reference/android/content/BroadcastReceiver).

Un aspecto exclusivo del diseño del sistema Android es que cualquier aplicación puede iniciar un componente de otra aplicación. Por ejemplo, si quieres que el usuario tome una foto con la cámara del dispositivo, probablemente haya otra aplicación para eso y tu aplicación pueda usarla, en lugar de desarrollar una actividad para tomar una foto. No necesitas incorporar ni establecer un enlace con el código de la aplicación de cámara. En su lugar, puedes simplemente iniciar la actividad en la aplicación de cámara que toma la foto. Cuando termines, la foto aparecerá en tu aplicación para que puedas usarla. Al usuario le parecerá que la cámara en realidad forma parte de tu aplicación.

Cuando el sistema inicia un componente, inicia el proceso para esa aplicación (si es que no se está ejecutando) y crea una instancia de las clases necesarias para el componente. Por ejemplo, si tu app inicia la actividad en la app de cámara que toma una foto, esa actividad se ejecuta en el proceso que pertenece a la app de cámara, no en el proceso de tu app. Por lo tanto, a diferencia de lo que sucede con las apps en la mayoría de los demás sistemas, las apps de Android no tienen un solo punto de entrada (por ejemplo, no existe la función `main()`).

Como el sistema ejecuta cada aplicación en un proceso independiente con permisos de archivo que limitan el acceso a otras aplicaciones, tu aplicación no puede activar directamente un componente de otra aplicación. Sin embargo, el sistema Android sí puede hacerlo. Por lo tanto, para activar un componente en otra aplicación, debes enviar un mensaje al sistema que especifique tu *intent* de iniciar un componente específico. Luego, el sistema activa ese componente por ti.

## El archivo de manifiesto

Para que el sistema Android pueda iniciar un componente de la app, el sistema debe reconocer la existencia de ese componente leyendo el archivo `AndroidManifest.xml` de la app (el archivo de “manifiesto”). Tu aplicación debe declarar todos sus componentes en este archivo, que debe encontrarse en la raíz del directorio de proyectos de la aplicación.

El manifiesto puede hacer ciertas cosas además de declarar los componentes de la aplicación, como por ejemplo:

* Identificar los permisos de usuario que requiere la aplicación, como acceso a Internet o acceso de lectura para los contactos del usuario.
* Declarar el nivel de API mínimo requerido por la aplicación en función de las API que usa la aplicación.
* Declarar características de hardware y software que la aplicación usa o exige, como una cámara, servicios de bluetooth o una pantalla multitáctil.
* Bibliotecas de la API a las que la aplicación necesita estar vinculada (además de las Android framework API), como la biblioteca Google Maps .
* Y más.

[Referencia Inglés](https://developer.android.com/guide/components/fundamentals)
