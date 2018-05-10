# Ejecutando la Aplicación
Ahora podrás ejecutar la app en un dispositivo real o un emulador.

## Realizar la ejecución en un dispositivo real

Configura tu dispositivo de la siguiente manera:

* Conecta tu dispositivo a tu máquina de desarrollo con un cable USB. Si realizas desarrollos en Windows, es posible que debas **instalar el controlador USB adecuado para tu dispositivo**.
* Habilita **USB debugging** en **Developer options** de la siguiente manera.
* Primero, debes habilitar las opciones para programador:

    * Abre la app **Settings**.
    * (Solo en Android 8.0 o versiones posteriores) Selecciona **System**.
    * Desplázate hasta abajo y selecciona **About phone**.
    * Desplázate hasta abajo y presiona **Build number** siete veces.
    * Cuando regreses a la pantalla anterior, verás **Opciones para programador** cerca de la parte inferior.
    * Abre **Developer options** y desplázate hacia abajo hasta encontrar y habilitar **USB debugging**.
    
Ejecuta la app en tu dispositivo de la siguiente manera:
* En Android Studio, haz clic en el módulo **app** de la ventana **Project** y selecciona **Run > Run** (o haz clic en **Run** ![play](https://developer.android.com/studio/images/buttons/toolbar-run.png) en la barra de herramientas).
* En la ventana **Select Deployment Target**, selecciona tu dispositivo y haz clic en **OK**

![Deployment](https://developer.android.com/training/basics/firstapp/images/run-device_2x.png)

Android Studio instala la app en tu dispositivo conectado y lo inicia.

Con esto, se ejecutará **“Hello world”** en tu dispositivo.

## Realizar la ejecución en un emulador

Ejecuta la app en un emulador de la siguiente manera:

* En Android Studio, haz clic en el módulo app de la ventana **Project** y selecciona **Run > Run** (o haz clic en **Run** ![play](https://developer.android.com/studio/images/buttons/toolbar-run.png) en la barra de herramientas).
* En la ventana **Select Deployment Target**, haz clic en **Create New Virtual Device**.

![Create Virtual Device](https://developer.android.com/training/basics/firstapp/images/run-avd_2x.png)

* En la pantalla **Select Hardware**, selecciona un teléfono, como **Pixel**, y haz clic en **Next**.
* En la pantalla **System Image**, selecciona la versión con el nivel de **API** más alto. Si no tienes instalada esa versión, se mostrará un vínculo **Download** en el que debes hacer clic para completar la descarga.
* Haz clic en **Next**.
* En la pantalla **Android Virtual Device (AVD)**, deja los ajustes tal como están y haz clic en **Finish**.
* En el diálogo **Select Deployment Target**, selecciona el dispositivo que acabas de crear y haz clic en **OK**. 

Android Studio instala la app en el emulador y la ejecuta. 

Con esto, se ejecutará “hello world” en tu dispositivo.

[Referencia Inglés](https://developer.android.com/training/basics/firstapp/running-app)