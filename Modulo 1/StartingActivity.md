# Iniciar otra activity
Ahora tendrás una app que mostrará una activity (una única pantalla) con un campo de texto y un botón. Agregarás a `MainActivity` un fragmento de código que iniciará una nueva activity para mostrar el mensaje cuando el usuario toque **Send**.

## Responder al botón Send
Agrega un método en `MainActivity.java` al cual llame el botón de la siguiente manera:

* En el archivo **app > java > com.example.myfirstapp > MainActivity.java**, agrega el código auxiliar del método `sendMessage()` como se muestra a continuación:

![carbon 1](https://user-images.githubusercontent.com/9124597/39891134-7372bec4-5462-11e8-86e4-b688ff5d8994.png) 

Es posible que veas un error, ya que Android Studio no puede resolver la clase `View` que se usa como argumento del método. Por lo tanto, haz clic para posicionar tu cursor en la declaración `View` y luego realiza una corrección rápida presionando Alt + Enter (en Mac, Option + Enter). (Si aparece un menú, selecciona **Import class**). 

* Regresa al archivo activity_main.xml para llamar a este método desde el botón:
    * Haz clic para seleccionar el botón en el editor de diseño.
    * En la ventana **Attributes**, encuentra la propiedad **onClick** y selecciona **sendMessage [MainActivity]** en la lista desplegable. 

Ahora, cuando se presione el botón, el sistema llamará al método `sendMessage()`.

Toma nota de los detalles de este método que se requieren para que el sistema lo reconozca como compatible con el atributo `android:onClick`. En concreto, el método debe declarar lo siguiente:

* acceso público;
* un valor de retorno vacío;
* una `View` como único parámetro (es el objeto `View` en el que se hizo clic). 

Luego, completarás este método para leer el contenido del campo de texto y proporcionar dicho texto a otra activity. 

## Crear un intent 
Un `Intent` es un objeto que proporciona enlace de tiempo de ejecución entre componentes separados, como dos activity. El `Intent` representa la “intención de hacer algo” de una app. Puedes usar las intents para varias tareas, pero en esta lección tu intent inicia otra activity.

En `MainActivity.java`, agrega la constante `EXTRA_MESSAGE` y el código `sendMessage()`, como se muestra a continuación: 

![carbon 2](https://user-images.githubusercontent.com/9124597/39891540-79c71bde-5463-11e8-9f1b-e17a8fe3677a.png) 

Android Studio nuevamente mostrará los errores **Cannot resolve symbol**. Presiona Alt + Enter (en Mac, Option + Return). Tus importaciones deben tener el siguiente aspecto final: 

![carbon 3](https://user-images.githubusercontent.com/9124597/39891615-a4c2fd6c-5463-11e8-9025-e05a2028eff4.png) 

Queda un error para **DisplayMessageActivity**, pero no hay inconveniente; podrás corregirlo en la sección siguiente.

Esto es lo que sucede en `sendMessage()`:

* El constructor de `Intent` toma dos parámetros:
    * un elemento `Context` como su primer parámetro (se usa this porque la clase `Activity` es una subclase de `Context`); 
    * la `Class` del componente de la app a la cual el sistema debe entregar la `Intent` (en este caso, la activity que debe iniciarse).
* El método `putExtra()` agrega el valor de `EditText` a la intent.  Un `Intent` puede llevar tipos de datos como pares clave-valor denominados *extras*. Tu clave es una constante pública `EXTRA_MESSAGE` porque la activity siguiente usa la clave para obtener el valor de texto. Se recomienda definir claves para los extras de intents usando el nombre del paquete de tu app como prefijo. Esto garantiza que las claves sean únicas, en el caso de que tu app interactúe con otras apps.
* El método `startActivity()` inicia una instancia de la `DisplayMessageActivity` especificada por el `Intent`. Ahora deberás crear esa clase.

## Crear la segunda activity

* En la ventana **Project**, haz clic con el botón secundario en la carpeta app y selecciona **New > Activity > Empty Activity**.
* En la ventana **Configure Activity**, ingresa “DisplayMessageActivity” en **Activity Name** y haz clic en **Finish** (deja todas las demás propiedades en sus valores predeterminados).  

Android Studio realiza tres acciones automáticamente:

* Crea el archivo `DisplayMessageActivity.java`.
* Crea el archivo de `diseño activity_display_message.xml` correspondiente.
* Agrega el elemento `activity` obligatorio en `AndroidManifest.xml`.

Si ejecutas la app y tocas el botón en la primera activity, la segunda se iniciará, pero estará vacía. Esto sucede porque la segunda activity usa el diseño vacío proporcionado por la plantilla. 

## Agregar una vista de texto 
La activity nueva incluye un archivo de diseño en blanco, por lo que ahora agregarás una vista de texto en la que aparecerá el mensaje.

* Abre el archivo **app > res > layout > activity_display_message.xml.**
* Haz clic en **Turn On Autoconnect** ![Connect](https://developer.android.com/studio/images/buttons/layout-editor-autoconnect-on.png)  en la barra de herramientas (luego debe habilitarse, como se muestra en la figura 1). 

![Fig1](https://developer.android.com/training/basics/firstapp/images/constraint-textview_2x.png)**Figura 1:** La vista de texto centrada en la parte superior del diseño. 

* En la ventana **Pallete**, haz clic en **Text** y luego arrastra un **TextView** hacia el diseño; ubícalo cerca de la parte superior del diseño, en un punto cercano al centro para que se acople a la línea vertical que aparece. La opción “Autoconnect” agrega restricciones a la derecha y a la izquierda para ubicar la vista en el centro horizontal.
* Crea una restricción más desde la parte superior de la vista de texto hasta la parte superior del diseño, para que tenga el aspecto de la figura 1. 

Como alternativa, puedes realizar algunas modificaciones en el estilo de texto expandiendo **textAppearance** en la ventana **Attributes** y cambiar atributos como **textSize** y **textColor**.

## Mostrar el mensaje
A continuación, modificarás la segunda activity para que muestre el mensaje que pasó la primera.

* En `DisplayMessageActivity.java`, agrega el siguiente código al método `onCreate()`: 

![carbon 4](https://user-images.githubusercontent.com/9124597/39892461-5b2cd56c-5466-11e8-8388-bc270d17da98.png) 

* Presiona Alt + Enter (en Mac, Option + Return) para importar las clases faltantes. Tus importaciones deben tener el siguiente aspecto final: 

![carbon 5](https://user-images.githubusercontent.com/9124597/39892519-865d9bae-5466-11e8-8fbf-870d4d9ac9c6.png) 

## Agregar navegación superior
En cada pantalla de tu app que no sea la entrada principal (todas las pantallas que no sean la de inicio) se debe proporcionar navegación. De esta forma, el usuario puede regresar a la pantalla primaria lógica en la jerarquía de la app presionando el botón Up en la `barra de la app`.

Lo único que debes hacer es declarar la activity primaria lógica en el archivo `AndroidManifest.xml`. Para ello, abre el archivo en **app > manifests > AndroidManifest.xml**, ubica la etiqueta `<activity>` para `DisplayMessageActivity` y reemplázala por lo siguiente: 

![carbon 6](https://user-images.githubusercontent.com/9124597/39892625-dc9b3ec2-5466-11e8-9a3b-f34295e49a7a.png) 

El sistema de Android agregará automáticamente el botón Up en la barra de la app. 

## Ejecutar la app 
Ahora ejecuta nuevamente la app haciendo clic en **Apply Changes** ![Changes](https://developer.android.com/studio/images/buttons/toolbar-apply-changes.png)  en la barra de herramientas. Cuando se abra, escribe un mensaje en el campo de texto y toca **Send** para que el mensaje aparezca en la segunda activity. 

![Final](https://developer.android.com/training/basics/firstapp/images/screenshot-activity2.png)**Figura 2:** Capturas de pantalla de ambas actividades. 

Eso es todo. ¡Has compilado tu primera app de Android!

[Referencia Inglés](https://developer.android.com/training/basics/firstapp/starting-activity)