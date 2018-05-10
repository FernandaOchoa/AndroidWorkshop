# Creando un Proyecto
Aprenderás a crear un nuevo proyecto de Android con Android Studio. También se describen algunos de los archivos del proyecto.

* En la ventana **Welcome to Android Studio**, haz clic en **Start a new Android Studio project**.

![Android](https://developer.android.com/training/basics/firstapp/images/studio-welcome_2x.png) 

O bien, si tienes un proyecto abierto, selecciona **File > New Project**.

* En la pantalla **New Project**, ingresa los siguientes valores:  
**Nombre de la app:** “My First App”  
**Dominio de la empresa:** “example.com” 

Si lo deseas, puedes cambiar la ubicación del proyecto, pero deja las demás opciones como están. 

* Haz clic en **Next**.
* En la pantalla **Target Android Devices**, conserva los valores predeterminados y haz clic en **Next**. 
* En la pantalla **Add an Activity to Mobile**, selecciona **Empty Activity** y haz clic en **Next**.
* En la pantalla **Configure Activity**, conserva los valores predeterminados y haz clic en **Finish**.

Luego de un tiempo de procesamiento, Android Studio abrirá el IDE.

![Ide](https://developer.android.com/training/basics/firstapp/images/studio-editor_2x.png)

Tómate un momento para revisar los archivos más importantes.

Primero, asegúrate de que la ventana **Project** esté abierta (selecciona **View > Tool Windows > Project**) y la vista **Android** esté seleccionada en la lista desplegable de la parte superior de la ventana. Podrás ver los siguientes archivos:

**app > java > com.example.myfirstapp > MainActivity.java** 

Esta es la activity principal (el punto de entrada para tu app). Cuando compilas y ejecutas la app, el sistema inicia una instancia de esta  `Activity` y carga su diseño. 

**app > res > layout > activity_main.xml** 

Este archivo XML define el diseño para la IU de la activity. Contiene un elemento `TextView` con el texto “Hello world!”. 

**app > manifests > AndroidManifest.xml** 

El `archivo de manifiesto` describe las características fundamentales de la app y define cada uno de sus componentes. 

**Gradle Scripts > build.gradle** 

Verás dos archivos con este nombre: uno para el proyecto y otro para el módulo de la “app”. Cada módulo tiene su propio archivo `build.gradle`, pero este proyecto por el momento tiene un solo módulo. Trabajarás principalmente con el archivo `build.gradle` del módulo para configurar la forma en que las herramientas de Gradle compilan y crean tu app.

[Referencia Inglés](https://developer.android.com/training/basics/firstapp/creating-project)