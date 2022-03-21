# Configurar el entorno en un dispositivo Linux
Para configurar un dispositivo Linux con AWS IoT Greengrass V2:

1. Instalar el tiempo de ejecución de __Java__, que el software de AWS IoT Greengrass core requiere para ejecutarse. Se recomienda Amazon Corretto 11 u OpenJDK 11. Los siguientes comandos le muestran cómo instalar OpenJDK en su dispositivo.
   - ```mkdir /opt/plcnext/aws```. Crear un directorio donde instalar todo el software relacionado con AWS.
   - ```cd /opt/plcnext/aws```. Cambiar a este directorio.
   - ```wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.tar.gz```. Para descargar última versión de java. Se puede descargar en formato comprimido para Linux x64 desde https://www.oracle.com/java/technologies/downloads/#jdk17-linux o bien desde https://jdk.java.net/17/
   - ```tar -xvf jdk-17_linux-x64_bin.tar.gz```. Para descomprimir el fichero descargado con el entorno Java.
   - ```ln -sfn /opt/plcnext/aws/jdk-17.0.2/bin/java /usr/bin/java```. Crear un enlace símbolico que apunte al ejecutable de Java dentro de un directorio contenido en $PATH.
   - ```file /opt/plcnext/aws/jdk-17.0.2/bin/java```. Mostrar la ruta del intérprete para el ejecutable de java. Probablemente será /lib64/ld-linux-x86-64.so.2 y probablemente no exista.
   - ```su```. Loguearse como usuario root.
   - ```mkdir /lib64```- Crear el directorio lib64.
   - ```ln -sf /lib/ld-linux-x86-64.so.2 /lib64/ld-linux-x86-64.so.2```. Crear un enlace simbólico en el nuevo directorio que apunte a la librería existente.
   - ```java --version```. Comprobar que Java está incluido en el PATH y la versión instalada.
![image](https://user-images.githubusercontent.com/46561573/156546221-3f0b64ec-aa5c-454c-aa99-4a92aa53c572.png)

2. Instalar todas las demás dependencias necesarias en su dispositivo como se indica en la lista de requisitos en [Requisitos del dispositivo](https://docs.aws.amazon.com/greengrass/v2/developerguide/setting-up.html#greengrass-v2-requirements).

3. Crear el usuario y el grupo del sistema (Linux) por defecto que ejecuta los componentes en su dispositivo. En este tutorial vamos a optar por dejar que el instalador del software de AWS IoT Greengrass core cree este usuario y grupo más adelante durante la instalación con el argumento --component-default-user. Para obtener más información, consulte [Argumentos del instalador](https://docs.aws.amazon.com/greengrass/v2/developerguide/configure-installer.html).

_Opcional_: Se podrían ejecutar los siguientes comandos para crear el usuario y el grupo del sistema manualmente y comprobar que tiene permiso para ejecutar sudo con cualquier usuario y cualquier grupo (normalmente root):
   - ```sudo useradd --system --create-home ggc_user```. Para crear el usuario ggc_user.
   - ```sudo groupadd --system ggc_group```. Para crear el grupo ggc_group.
   - ```sudo visudo```. Para abrir el archivo __/etc/sudoers__.
   - Verificar que el permiso para el usuario sea como el siguiente ejemplo. ```root ALL=(ALL:ALL) ALL```

