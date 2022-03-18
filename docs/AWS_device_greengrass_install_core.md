## Instalar el software AWS IoT Greengrass Core
1. Después de [obtener las credenciales de usuario](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_account_greengrass_config.md) y de [configurar las variables de entorno con las credenciales](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_device_greengrass_env_config.md).
2. _Ejecutar el instalador__. AWS IoT Greengrass proporciona un instalador que se puede utilizar para configurar un dispositivo de Greengrass Core en cuestión de minutos. El instalador se ejecuta en el dispositivo y hace lo siguiente:
      - Aprovisiona el dispositivo de Greengrass Core como un objeto de AWS IoT con un certificado de dispositivo y permisos predeterminados. [Más información](https://docs.aws.amazon.com/console/greengrass/v2/provision-greengrass-core).
      - Crear un usuario y un grupo del sistema, ggc_user y ggc_group, que el software utiliza para ejecutar componentes en el dispositivo. Marcado como opcional al [configurar el entorno para AWS IoT Greengrass Core en un dispositivo Linux](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_device_env_config.md#configurar-el-entorno-en-un-dispositivo-linux).
      - Conectar el dispositivo a AWS IoT.
      - Instalar y ejecutar el software más reciente de AWS IoT Greengrass Core como servicio del sistema que se ejecuta automáticamente en el arranque. En los dispositivos Linux, esto requiere el sistemade inicio  _systemd_.
      - Instalar el componente AWS IoT Greengrass CLI, que es una herramienta de línea de comandos que le permite desarrollar componentes personalizados de Greengrass en el propio dispositivo.
   Para ello, ejecutar los siguientes comandos:
      - Ejecutar el comando: ```mkdir /opt/plcnext/aws/GreengrassCore```. Crear un directorio donde instalar todo el software relacionado con _GreengrassCore_.
	  - Ejecutar el comando: ```cd /opt/plcnext/aws/```. Cambiar a este directorio.
	  - Ejecutar el comando: ```curl -s https://d2s8p88vqu9w66.cloudfront.net/releases/greengrass-nucleus-latest.zip > greengrass-nucleus-latest.zip && unzip greengrass-nucleus-latest.zip -d /opt/plcnext/aws/GreengrassCore```. Para descargar la última versión del software AWS IoT Greengrass Core en un fichero _greengrass-nucleus-latest.zip_ y descomprimirlo en _GreengrassCore_.
      - Ejecutar el comando: ```sudo -E java -Droot="/greengrass/v2" -Dlog.store=FILE \
  -jar /opt/plcnext/aws/GreengrassCore/lib/Greengrass.jar \
  --aws-region eu-west-2 \
  --thing-name GreengrassCoreHolcim \
  --thing-group-name GreengrassCoreHolcimGroup \
  --thing-policy-name GreengrassV2TokenExchangeRoleAccess \
  --tes-role-name GreengrassV2TokenExchangeRole \
  --tes-role-alias-name GreengrassV2TokenExchangeRoleAlias \
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





