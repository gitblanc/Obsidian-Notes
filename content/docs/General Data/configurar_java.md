---
title: Configurar versión de Java en Eclipse 🏔️
---
Para configurar Java XX como la versión por defecto en Eclipse en Ubuntu, sigue estos pasos:
1. **Instala Java XX** (si no lo has hecho): Asegúrate de tener Java XX instalado. Si ya lo tienes, verifica la ruta de instalación, generalmente en `/usr/lib/jvm/` (`/opt/` en distribuciones Linux con múltiples versiones instalaas) o donde hayas instalado el JDK.
2. **Configura Java XX en Eclipse:** Abre Eclipse y sigue estos pasos:
    - **Accede a la configuración de JREs instaladas**:
        - Ve a `Window` > `Preferences` (o en `Eclipse` > `Preferences` en algunas versiones).
        - Expande la sección `Java` y selecciona `Installed JREs`.
    - **Agrega Java XX**:
        - Haz clic en `Add...`.
        - Selecciona `Standard VM` y haz clic en `Next`.
        - En el campo `JRE home`, busca y selecciona la carpeta donde instalaste Java XX, como `/usr/lib/jvm/jdk-XX`.
        - Asigna un nombre a esta JRE, como `Java XX`, y haz clic en `Finish`.
    - **Establece Java XX como predeterminado**:
        - En la lista de JREs instaladas, marca el checkbox junto a Java XX para establecerla como la predeterminada.
        - Haz clic en `Apply and Close`.
3. **Configura el JDK del Proyecto (opcional)**: Si tienes un proyecto específico que quieres que use Java XX, también puedes configurarlo de esta forma:
    - Haz clic derecho en tu proyecto y selecciona `Properties`.
    - Ve a `Java Build Path`, luego selecciona la pestaña `Libraries`.
    - Haz clic en `Add Library...`, selecciona `JRE System Library`, y selecciona `Installed JREs...`.
    - Escoge Java XX como el JRE para este proyecto y guarda los cambios.

Con esto, Eclipse debería estar configurado para usar Java XX como la versión predeterminada para todos los proyectos nuevos y específicos en los que lo configures.