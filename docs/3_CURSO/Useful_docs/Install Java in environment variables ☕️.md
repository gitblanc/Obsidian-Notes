1. Lo primero es lo primero, debe descargar el JDK de Oracle para tener la última versión de Java.

![Descarga de Java JDK](https://bgsoaring.org/images/java-programming/how-to-compile-java-programs-through-windows-cmd.jpg)

2. Siga las instrucciones para instalar el JDK. Es importante tomar nota de la ruta de la instalación de JDK.

![Camino JDK](https://bgsoaring.org/images/java-programming/how-to-compile-java-programs-through-windows-cmd_2.jpg)

3.Cree un directorio central para guardar todos sus archivos Java. Por ejemplo, creé una carpeta en **C: Java** y coloqué mis archivos .java y proyectos dentro de esta carpeta.

![Carpeta Java](https://bgsoaring.org/images/java-programming/how-to-compile-java-programs-through-windows-cmd_3.jpg)

4. Haga clic en el icono de Inicio de Windows y busque **Sistema** y pulsa enter. Seleccionar **Configuración avanzada del sistema** a la izquierda y luego seleccione **Variables de entorno**.

![Variables de entorno de Windows](https://bgsoaring.org/images/java-programming/how-to-compile-java-programs-through-windows-cmd_4.jpg)

5. Debajo **Variables del sistema** desplazarse hacia abajo a la variable **Camino**.

![Variable de ruta del sistema de Windows 7](https://bgsoaring.org/images/java-programming/how-to-compile-java-programs-through-windows-cmd_5.jpg)

6. Golpear **Editar** al principio de **Valor variable**. Necesitamos ubicar la ruta del compilador Javaen la ruta de Windows. El compilador debe ubicarse en la carpeta bin JDK. Por ejemplo, desde la instalación, grabé que mi carpeta bin estaba en la siguiente ubicación: **C: Archivos de programa (x86) Javajdk1.7.0_06bin;** pero tu ubicación puede ser diferente. Asegúrese de incluir un punto y coma al final de la cadena que acaba de agregar. Presiona OK y cierra esto.

Si esto se hace incorrectamente, recibirá el siguiente error cuando intente compilar:

_"Javac" no se reconoce como un comando interno o externo, programa operativo o archivo por lotes_

7. A continuación, debemos abrir una ventana de terminal o un shell CMD. Haga clic en el icono de Windows y busque "CMD" y luego presione enter. Cambie al directorio de sus archivos java personales. Por ejemplo, ingresaría **cd java** ya que esa es la carpeta java personal que creé arriba. Ahora nuestro directorio actual dentro del shell CMD es **c: java**.

![Java CD CMD](https://bgsoaring.org/images/java-programming/how-to-compile-java-programs-through-windows-cmd_6.jpg)

8. Escribir **javac JavaFileName.java** donde el "JavaFileName.java "es el nombre del archivo java que desea compilar. Este archivo se puede crear con cualquier editor de texto o IDE y contiene su código real. Después de presionar la tecla Intro, debería ver una nueva línea en blanco en el CMD sin nada en ella. Ahora verifique dentro de su carpeta Java personal. Si la compilación fue exitosa, debería ver un nuevo archivo .class.

![](https://bgsoaring.org/images/java-programming/how-to-compile-java-programs-through-windows-cmd_7.jpg)

9. Para ejecutar realmente el intérprete y ver el tipo de salida en **java YourFileName** sin la extensión .java y su programa debería ejecutarse. Mi ejemplo simplemente genera algo de texto.

![](https://bgsoaring.org/images/java-programming/how-to-compile-java-programs-through-windows-cmd_8.jpg)