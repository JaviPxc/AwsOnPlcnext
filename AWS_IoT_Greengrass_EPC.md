[Tutorial de introducción](https://docs.aws.amazon.com/es_es/greengrass/v2/developerguide/getting-started.html) para aprender acerca de las características básicas de AWS IoT Greengrass V2.


# Configurar una cuenta de AWS
- [Configurar una cuenta de AWS](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_account_config.md#configurar-una-cuenta-de-aws).
- [Crear un usuario en AWS Identity and Access Management (IAM) con permisos de administrador](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_account_config.md#crear-un-usuario-administrador-y-añadir-el-usuario-a-un-grupo-de-administradores).

# Configurar el entorno
- Comprobar que el dispositivo tiene [acceso a internet](https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/Comprobar_acceso_a_internet.md).
- Comprobar que el dispositivo tiene Python3.5 o posterior instalado.
   - Introducir este comando: ```python3 --version```.
- [Configurar el entorno para AWS IoT Greengrass Core en un dispositivo Linux]https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_device_env_config.md#configurar-el-entorno-en-un-dispositivo-linux).

# Instalar AWS CLI en el dispositivo
   - AWS Command Line Interface(AWS CLI) instalado y configurado con credenciales en el equipo de desarrollo y en el dispositivo. Asegúrese de usar la misma Región de AWS para configurar el AWS CLI en el equipo de desarrollo y en el dispositivo. Para utilizar AWS IoT Greengrass V2 con AWS CLI, debe tener una de las siguientes versiones o posterior:
      - Versión mínima de AWS CLI V1: v1.18.197
      - Versión mínima de AWS CLI V2: v2.1.11
https://docs.aws.amazon.com/es_es/cli/latest/userguide/getting-started-install.html

# Instalar el software AWS IoT Greengrass Core
Seguir los pasos de esta sección para configurar su equipo como dispositivo de AWS IoT Greengrass Core que puede utilizar para el desarrollo local. En esta sección, descarga y ejecuta un instalador que hace lo siguiente para configurar el software de AWS IoT Greengrass Core para su dispositivo:

### Instalar el software AWS IoT Greengrass Core (consola)
1. Iniciar sesión en la [consola de AWS IoT Greengrass](https://console.aws.amazon.com/greengrass).
2. Ir a __Greengrass > Introducción > Configurar un dispositivo de núcleo__.
3. En __Paso 1: Registrar un dispositivo del núcleo de Greengrass__, introducir el nombre del objeto de AWS IoT en __Nombre del dispositivo de núcleo__. Por ejemplo, GreengrassQuickStartCoreHolcim.
4. En __Paso 2: agregar a un grupo de objetos para aplicar una implementación continua__, eligir el grupo de AWS IoT al que desea añadir su dispositivo de núcleo en __Grupo de objetos > Nombre del grupo de objetos__. Por ejemplo, crear un nuevo grupo llamado GreengrassQuickStartHolcimGroup.
5. En __Paso 3: instalar el software de Greengrass Core__, completar los siguientes pasos:
   - Eligir el sistema operativo de su dispositivo de núcleo: Linux o Windows.
   - Paso __3.1: instalar Java en el dispositivo__. Realizado previamente en (https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/AWS_IoT_Greengrass_EPC.md#configurar-un-dispositivo-Linux). El software AWS IoT Greengrass Core se ejecuta en Java.
   - Paso __3.2: configurar las credenciales de AWS en el dispositivo__. El instalador de Greengrass utiliza las credenciales de AWS para aprovisionar los recursos de AWS que necesita. Para aumentar la seguridad, le recomendamos que obtenga credenciales temporales para un rol de IAM que sólo permita los permisos mínimos necesarios para el aprovisionamiento. Para obtener más información, consultar [Política de IAM mínima para que el instalador aprovisione los recursos](https://docs.aws.amazon.com/greengrass/v2/developerguide/provision-minimal-iam-policy.html). Puede proporcionar credenciales como variables de entorno. Para ello, en su dispositivo, realice una de las siguientes acciones para recuperar las credenciales y ponerlas a disposición del instalador de AWS IoT Greengrass Core:
      - Opción 1: Utilizar las credenciales a largo plazo de un usuario de IAM:
         - Proporcionar el ID de la clave de acceso y la clave de acceso secreta del usuario de IAM. Para obtener más información sobre cómo recuperar credenciales a largo plazo, consultar [Administración de claves de acceso para usuarios de IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
          ![image](https://user-images.githubusercontent.com/46561573/156746711-227d0a4d-b1d7-444d-b157-eb1691a63e98.png)
         - Ejecutar los siguientes comandos (Linux) para proporcionar las credenciales al software del núcleo de AWS IoT Greengrass (sustituir el texto después del signo “=” por la información especificada).
         ```
            export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
            export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
          ```
      - Opción 2: (Recomendado) Utilizar credenciales de seguridad temporales de un rol de IAM:
         - Proporcionar el ID de la clave de acceso, la clave de acceso secreta y el token de sesión de un rol de IAM que escoja. Para obtener más información sobre cómo recuperar estas credenciales, consultar [Uso de credenciales de seguridad temporales con la CLI de AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_use-resources.html#using-temp-creds-sdk-cli).
         - Ejecutar los siguientes comandos (Linux) para proporcionar las credenciales al software del núcleo de AWS IoT Greengrass (sustituir el texto después del signo “=” por la información especificada).
         ```
            export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
            export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
            export AWS_SESSION_TOKEN=AQoDYXdzEJr1K...o5OytwEXAMPLE=
          ```
_Nota_: El instalador no guarda ni almacena sus credenciales.

   - Paso __3.3: ejecutar el instalador__. AWS IoT Greengrass proporciona un instalador que se puede utilizar para configurar un dispositivo de Greengrass Core en cuestión de minutos. El instalador se ejecuta en el dispositivo y hace lo siguiente:
      - Aprovisiona el dispositivo de Greengrass Core como un objeto de AWS IoT con un certificado de dispositivo y permisos predeterminados. [Más información](https://docs.aws.amazon.com/console/greengrass/v2/provision-greengrass-core).
      - Crear un usuario y un grupo del sistema, ggc_user y ggc_group, que el software utiliza para ejecutar componentes en el dispositivo. Realizado previamente en (https://github.com/JaviPxc/LinuxOnPLCnext/blob/main/AWS_IoT_Greengrass_EPC.md#configurar-un-dispositivo-Linux).
      - Conectar el dispositivo a AWS IoT.
      - Instalar y ejecutar el software más reciente de AWS IoT Greengrass Core como servicio del sistema que se ejecuta automáticamente en el arranque. En los dispositivos Linux, esto requiere el sistemade inicio  _systemd_.
      - Instalar el componente AWS IoT Greengrass CLI, que es una herramienta de línea de comandos que le permite desarrollar componentes personalizados de Greengrass en el propio dispositivo.
   Para ello, ejecutar los siguientes comandos:
      - Ejecutar el comando: ```curl -s https://d2s8p88vqu9w66.cloudfront.net/releases/greengrass-nucleus-latest.zip > greengrass-nucleus-latest.zip && unzip greengrass-nucleus-latest.zip -d GreengrassCore```. Para descargar la última versión del software AWS IoT Greengrass Core en un fichero _greengrass-nucleus-latest.zip_ y descomprimirlo en _GreengrassCore_.
      - Ejecutar el comando: ```sudo -E java -Droot="/greengrass/v2" -Dlog.store=FILE \
  -jar ./GreengrassInstaller/lib/Greengrass.jar \
  --aws-region region \
  --thing-name MyGreengrassCore \
  --thing-group-name MyGreengrassCoreGroup \
  --thing-policy-name GreengrassV2IoTThingPolicy \
  --tes-role-name GreengrassV2TokenExchangeRole \
  --tes-role-alias-name GreengrassCoreTokenExchangeRoleAlias \
  --component-default-user ggc_user:ggc_group \
  --provision true \
  --setup-system-service true \
  --deploy-dev-tools true```
  Para lanzar el instalador, sustituir los valores de los argumentos en su comando de la siguiente manera:
      - _/greengrass/v2 o C:\NGreengrass\Nv2_: La ruta del directorio raíz que se utilizará para instalar el software de AWS IoT Greengrass Core.
      - _GreengrassInstaller_: La ruta del directorio donde se ha descomprimido el instalador del software de AWS IoT Greengrass Core.
      - _region_: La región de AWS en la que buscar o crear recursos.
      - _MyGreengrassCore_. El nombre del dispositivo Greengrass Core dentro de AWS IoT. Si el objeto no existe, el instalador lo crea. El instalador descarga los certificados para autenticarse como el objeto de AWS IoT. Para obtener más información, consulte [Autenticación y autorización de dispositivos para AWS IoT Greengrass](https://docs.aws.amazon.com/greengrass/v2/developerguide/device-auth.html).
      - _MyGreengrassCoreGroup_. El nombre del grupo al que pertenece el dispositivo Greengrass Core dentro de AWS IoT. Si el grupo no existe, el instalador lo crea y añade el dispositivo. Si el grupo existe y tiene una implementación activa, el dispositivo central descarga y ejecuta el software que la implementación especifica.
      - _GreengrassV2IoTThingPolicy_: El nombre de la política de AWS IoT que permite a los dispositivos Greengrass Core comunicarse con AWS IoT y AWS IoT Greengrass. Si la política de AWS IoT no existe, el instalador crea una política permisiva de AWS IoT con este nombre. Por defecto, _GreengrassV2TokenExchangeRoleAccess_. Puede restringir los permisos de esta política para su caso de uso. Para obtener más información, consultar [Política mínima de AWS IoT para dispositivos centrales de AWS IoT Greengrass V2](https://docs.aws.amazon.com/greengrass/v2/developerguide/device-auth.html#greengrass-core-minimal-iot-policy).
      - _GreengrassV2TokenExchangeRole_: El nombre del rol de IAM que permite al dispositivo de Greengrass Core obtener credenciales temporales de AWS. Si el rol no existe, el instalador lo crea y crea y adjunta una política llamada _GreengrassV2TokenExchangeRole_. Para obtener más información, consultar [Autorizar a los dispositivos para que interactúen con los servicios de AWS](https://docs.aws.amazon.com/greengrass/v2/developerguide/device-service-role.html).
      - _GreengrassCoreTokenExchangeRoleAlias_: El alias del rol de IAM que permite al dispositivo de Greengrass Core obtener credenciales temporales posteriormente. Si el alias del rol no existe, el instalador lo crea y lo apunta al rol de IAM que usted especifique. Para obtener más información, consulte Autorizar a los dispositivos centrales para que interactúen con los servicios de AWS.
   Por ejemplo,  ```sudo -E java -Droot="/greengrass/v2" -Dlog.store=FILE -jar ./GreengrassCore/lib/Greengrass.jar --aws-region eu-west-2 --thing-name GreengrassQuickStartCoreHolcim --thing-group-name GreengrassQuickStartHolcimGroup --component-default-user ggc_user:ggc_group --provision true --setup-system-service true --deploy-dev-tools true```.  
   Cuando ejecute este comando, debería ver los siguientes mensajes para indicar que el instalador tuvo éxito.
   ```
Successfully configured Nucleus with provisioned resource details!
Configured Nucleus to deploy aws.greengrass.Cli component
Successfully set up Nucleus as a system service
```

_Nota_: Si ejecuta AWS IoT Greengrass en un dispositivo con memoria limitada, puede controlar la cantidad de memoria que utiliza el software de AWS IoT Greengrass. Para controlar la asignación de memoria, puede establecer las opciones de tamaño de la pila de la JVM en el parámetro de configuración jvmOptions.

_Nota_: Si tienes un dispositivo Linux y no tiene __systemd__, el instalador no configurará el software como un servicio del sistema, y no verás el mensaje de éxito para configurar el núcleo como un servicio del sistema. Ejecutar el siguiente comando para ejecutar el software:
   ```sudo /greengrass/v2/alts/current/distro/bin/loader```
Si se ha podido ejecutar, el software imprime el siguiente mensaje si se lanza con éxito: _Launched Nucleus successfully._ En este caso es necesario dejar el shell de comandos actual abierto para mantener el software de AWS IoT Greengrass Core en ejecución.






















XXXXXXXXX   TO BE TESTED XXXXXXXXXXXXXX




Instalación mediante Docker:
- Instalar Portainer en el EPC 15xx: https://www.plcnextstore.com/977
- Abrir Portainer e instalar https://hub.docker.com/r/amazon/aws-iot-greengrass 
- Crear grupo y descargar los certificados: https://docs.aws.amazon.com/es_es/greengrass/v1/developerguide/gg-config.html
  - Ir a AWS Iot > Greengrass > Classiv (V1) > Groups > Create.
  - Download at the end the certificates.
  
- Ejecutar AWS IoT Greengrass localmente:
   - Descomprima los certificados y el archivo de configuración (que descargó al crear su grupo de Greengrass) en una ubicación conocida como, por ejemplo, /tmp. Por ejemplo:
     '''tar xvzf ca0a5a103e-setup.tar.gz -C /tmp/'''
  
   - Review (Revisar)Autenticación del servidor en la AWS IoT Guía para desarrolladores y elija el certificado de CA raíz adecuado. 
   Le recomendamos que utilice puntos de enlace de Amazon Trust Services (ATS) y certificados de CA raíz de ATS.
   Para puntos de enlace de ATS (preferidos), descargue el certificado de CA raíz de ATS. En el siguiente ejemplo se descarga AmazonRootCA1.pem.

   '''
   cd /tmp/certs/
   sudo wget -O root.ca.pem https://www.amazontrust.com/repository/AmazonRootCA1.pem
   '''



- Descargar AWS Greengrass docker:  https://github.com/aws-greengrass/aws-greengrass-docker/releases/


Steps to run AWS IoT Greengrass in an EPC 15xx

