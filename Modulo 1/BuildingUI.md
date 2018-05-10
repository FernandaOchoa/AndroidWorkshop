# Creación de una interfaz de usuario sencilla 
En esta lección, usarás Android Studio Layout Editor para crear un diseño que incluya un cuadro de texto y un botón.  

![Mobile Sample](https://developer.android.com/training/basics/firstapp/images/screenshot-activity1.png)**Figura 1:** Captura de pantalla del diseño final. 

La interfaz de usuario para una app de Android se construye usando una jerarquía de diseños (objetos `ViewGroup`) y *widgets* (objetos `View`). Los diseños son contenedores invisibles que controlan la manera en que se posicionan sus vistas secundarias en la pantalla. Los widgets son componentes de la IU, como los botones y los cuadros de texto. 

![ViewGroup](https://developer.android.com/images/viewgroup_2x.png)**Figura 2:** Ilustración de cómo los objetos `ViewGroup` forman ramas en el diseño y contienen objetos `View`.

Android proporciona un vocabulario `XML` para las clases `ViewGroup` y `View`, por lo que la mayor parte de tu IU se define en archivos `XML`. Sin embargo, el propósito no es enseñarte a escribir en lenguaje `XML`, sino mostrarte cómo crear diseños usando **Android Studio Layout Editor**, que te permite construirlos fácilmente arrastrando y soltando vistas.

## Abrir el editor de diseño 
Para comenzar, configura tu lugar de trabajo de la siguiente manera:

* En la ventana Project de Android Studio, abre **app > res > layout > activity_main.xml**.
* Para hacer más espacio para el editor de diseño, oculta la ventana **Project** seleccionando **View > Tool Windows > Project** (o haciendo clic en **Project** ![Project](https://developer.android.com/studio/images/buttons/window-project.png) en el lado izquierdo de Android Studio).
* Si en tu editor se muestra el código fuente XML, haz clic en la pestaña **Design** en la parte inferior de la ventana.
* Haz clic en **Select Design Surface** ![Design Surface](https://developer.android.com/studio/images/buttons/layout-editor-design.png) y selecciona **Blueprint**.
* Haz clic en **Show** ![Show](https://developer.android.com/studio/images/buttons/layout-editor-show-constraints.png) en la barra de herramientas y asegúrate de que **Show Constraints** esté seleccionado.
* Asegúrate de que **Autoconnect** esté desactivada. En la información sobre la herramienta de la barra de herramientas debe aparecer la opción **Turn On Autoconnect** ![Autoconnect](https://developer.android.com/studio/images/buttons/layout-editor-autoconnect-on.png) (ya que ahora está desactivada).
* Haz clic en **Default Margins** ![Default Margins](https://developer.android.com/studio/images/buttons/layout-editor-margin.png) en la barra de herramientas y selecciona 16 (puedes ajustar el margen para cada vista posteriormente).
* Haz clic en **Device in Editor** ![Device Editor](https://developer.android.com/studio/images/buttons/layout-editor-device.png) en la barra de herramientas y selecciona Pixel XL. 

Ahora tu editor deberá verse como en la figura 3.

![Imagen 3](https://developer.android.com/training/basics/firstapp/images/layout-editor_2x.png)**Figura 3:** Visualización de `activity_main.xml` en el editor de diseño.

En la ventana **Component Tree** de la parte inferior izquierda se muestra la jerarquía de vistas del diseño. En este caso, la vista raíz es un ConstraintLayout que contiene únicamente un objeto `TextView`.

**ConstraintLayout** es un diseño que define la posición para cada vista a partir de restricciones sobre vistas del mismo nivel y del diseño primario. De esta manera, puedes crear tanto diseños simples como complejos con una jerarquía de vista plana. Es decir, se evita la necesidad de diseños anidados (un diseño dentro de otro, como se muestra en la figura 2), lo que puede aumentar el tiempo necesario para dibujar la IU.
Por ejemplo, puedes declarar el siguiente diseño (en la figura 4):  

![Margins](https://developer.android.com/training/basics/firstapp/images/constraint-example_2x.png)**Figura 4:** Ilustración de dos vistas ubicadas dentro de un `ConstraintLayout`.

* La vista A se muestra a 16 dp de la parte superior del diseño primario.
* La vista A se muestra a 16 dp de la parte izquierda del diseño primario.
* La vista B se muestra a 16 dp a la derecha de la vista A. 
* La vista B se encuentra alineada con la parte superior de la vista A.

## Agregar un cuadro de texto

![CuadroTexto](https://developer.android.com/training/basics/firstapp/images/constraint-textbox_2x.png)**Figura 5:** El cuadro de texto tiene restricciones respecto de las partes superior e izquierda del diseño primario. 

* Primero debes quitar lo que ya está en el diseño. Para eso, haz clic en **TextView** en la ventana **Component Tree** y luego presiona Suprimir.
* Desde la ventana **Palette**, a la izquierda, haz clic en **Text** en el subpanel izquierdo y luego arrastra **Plain Text** hacia el editor de diseño y suéltalo cerca de la parte superior del diseño. Este es un widget `EditText` que acepta entradas de texto sin formato.
* Haz clic en la vista del editor de diseño. Ahora podrás ver los controladores para cambiar el tamaño en cada esquina (cuadrados) y los anclajes de restricción en cada lado (círculos).
Si deseas un mayor control, puedes acercar la vista en el editor mediante los botones de la barra de herramientas.

* Haz clic sobre el anclaje del lado superior y, sin soltar el botón, arrástralo hacia arriba hasta que se acople a la parte superior del diseño y suéltalo. Eso es una restricción; especifica que la vista debe estar a 16 dp de la parte superior del diseño (ya que configuraste los márgenes predeterminados en 16 dp).
* Del mismo modo, crea una restricción desde el lado izquierdo de la vista hasta el lado izquierdo del diseño. 

# Agregar un botón

![BotonBlueprint](https://developer.android.com/training/basics/firstapp/images/constraint-button_2x.png)**Figura 6:** El botón tiene restricciones respecto del lado derecho del cuadro de texto y de su línea de base. 

* Desde la ventana **Palette**, haz clic en **Widgets** en el subpanel izquierdo, arrastra **Button** hacia el editor de diseño y suéltalo cerca del lado derecho.
Crea una restricción desde el lado izquierdo del botón hasta el lado derecho del cuadro de texto.
* Para restringir las vistas en una alineación horizontal, debes crear una restricción entre las líneas de base del texto. Para eso, haz clic en el botón y luego en **Edit Baseline** ![Baseline](https://developer.android.com/studio/images/buttons/layout-editor-action-baseline.png), que se muestra justo debajo de la vista seleccionada en el editor de diseño. El anclaje de línea de base aparece dentro del botón. Haz clic sobre este anclaje y, sin soltar el botón, arrástralo hacia el anclaje de línea de base que se muestra en el cuadro de texto. 

## Cambiar las strings de IU
Para generar una vista previa de la IU, haz clic en **Select Design Surface** ![Design S](https://developer.android.com/studio/images/buttons/layout-editor-design.png) en la barra de herramientas y selecciona **Design**. Ten en cuenta que la entrada de texto se completa previamente con “Name” y el botón lleva la etiqueta “Button”. Cambiarás estas strings. 

* Abre la ventana **Project** y luego abre **app > res > values > strings.xml**.
Este es un archivo de `recursos de strings` en el que debes especificar todas tus strings de IU. Esto te permite controlar todas las strings de IU en una única ubicación, lo que permite encontrarlas, actualizarlas y localizarlas (si se compara con fijar strings en el código de tu diseño o tu app) más fácilmente.

* Haz clic en **Open editor** en la parte superior de la ventana del editor. Con esto se abre `Translations Editor`, que proporciona una interfaz simple para agregar y editar tus strings predeterminadas, y ayuda a mantener organizadas todas tus strings traducidas. 

![Add](https://developer.android.com/training/basics/firstapp/images/add-string_2x.png)**Figura 7:** Diálogo para agregar una string nueva.

* Haz clic en **Add Key** ![AddKey](https://developer.android.com/studio/images/buttons/add-sign-green-icon.png) a fin de crear una string nueva como `“texto indicado”` para el cuadro de texto.
* Escribe `“edit_message”` como nombre para la clave.
Escribe `“Enter a message”` como valor.
Haz clic en **OK**.
Agrega otra clave llamada `“button_send”` con el valor `“Send”`. 

Ahora podrás configurar estas strings para cada vista. Para eso, regresa al archivo de diseño haciendo clic en **activity_main.xml** en la barra de pestañas y agrega las strings de la siguiente manera:

* Haz clic en el cuadro de texto del diseño y, si la ventana **Attributes** no está visible a la derecha, haz clic en **Attributes** ![Attrib](https://developer.android.com/studio/images/buttons/window-properties.png) en la barra lateral derecha.
* Ubica la propiedad **text** (actualmente fijada en "Name") y borra el valor.
* Ubica la propiedad **hint** y haz clic en **Pick a Resource** ![Pick](https://developer.android.com/studio/images/buttons/pick-resource.png) a la derecha del cuadro de texto. Dentro del diálogo que se muestra, haz doble clic en **edit_message** en la lista.
* Ahora haz clic en el botón en el diseño, ubica la propiedad **text**, haz clic en **Pick a Resource** ![Pick](https://developer.android.com/studio/images/buttons/pick-resource.png) y selecciona **button_send**. 

## Hacer que el tamaño del cuadro de texto sea flexible
Para crear un diseño que contemple diferentes tamaños de pantallas, ahora harás que el cuadro de texto se estire a fin de llenar todo el espacio horizontal que queda (luego de considerar el botón y los márgenes).

Antes de continuar, haz clic en **Show** ![Show](https://developer.android.com/studio/images/buttons/layout-editor-design.png)  en la barra de herramientas y selecciona **Blueprint**. 

* Selecciona ambas vistas (haz clic con el botón primario en una, mantén presionado Shift y haz clic con el mismo botón en la otra) y luego haz clic con el botón secundario en cualquiera de las vistas y selecciona **Chain > Create Horizontal Chain**.
Una `cadena` es una restricción bidireccional entre dos o más vistas que te permite organizar las vistas encadenadas de forma simultánea. 

![Center Horizontal](https://developer.android.com/training/basics/firstapp/images/constraint-centered_2x.png)**Figura 8:** Resultado al hacer clic en Center Horizontally. 

* Selecciona el botón y abre la ventana **Attributes**. Usando el inspector de vistas de la parte superior de la ventana **Attributes**, fija el margen derecho en 16.
* Ahora, haz clic en el cuadro de texto para ver sus atributos. Haz clic dos veces en el indicador de ancho para fijarlo en **Match Constraints**, como se indica en la referencia. 1 de la figura 9.  

![Match](https://developer.android.com/training/basics/firstapp/images/properties-margin_2x.png)**Figura 9:** Hacer clic para cambiar el ancho a Match Constraints.   

“Match constraints” significa que el ancho se expande para cumplir con la definición de las limitaciones horizontales y los márgenes. Por lo tanto, el cuadro de texto se estirará para llenar el espacio horizontal (luego de considerar el botón y todos los márgenes).   

![D10](https://developer.android.com/training/basics/firstapp/images/constraint-chain_2x.png)**Figura 10:** El cuadro de texto se estirará hasta llenar el espacio sobrante.

El diseño quedará hecho y deberá tener el aspecto de la figura 10.

Si te parece que tu diseño no quedó como se esperaba, haz clic en el vínculo que sigue para ver cómo debería verse tu XML y compararlo con lo que ves en la pestaña **Text**. (Si tus atributos aparecen en un orden diferente, no habrá problemas).

## XML del Diseño Final 
![carbon](https://user-images.githubusercontent.com/9124597/39890161-8eb3cf50-545f-11e8-8275-83f44d3cdc81.png)

## Ejecutar la app

Si tu app ya está instalada en el dispositivo, simplemente haz clic en **Apply Changes** ![Apply](https://developer.android.com/studio/images/buttons/toolbar-apply-changes.png) en la barra de herramientas para actualizar la app con el nuevo diseño. También puedes hacer clic en **Run** ![Run](https://developer.android.com/studio/images/buttons/toolbar-run.png) para instalar y ejecutar la app.

[Referencia Inglés](https://developer.android.com/training/basics/firstapp/building-ui)