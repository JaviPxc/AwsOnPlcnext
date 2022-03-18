
# Instalar el software AWS IoT Greengrass Core (consola)
1. Iniciar sesión en la [consola de AWS IAM](https://console.aws.amazon.com/iam).
2. Configurar las credenciales de AWS en el dispositivo__. El instalador de Greengrass utiliza las credenciales de AWS para aprovisionar los recursos de AWS que necesita. Para aumentar la seguridad, le recomendamos que obtenga credenciales temporales para un rol de IAM que sólo permita los permisos mínimos necesarios para el aprovisionamiento. Para obtener más información, consultar [Política de IAM mínima para que el instalador aprovisione los recursos](https://docs.aws.amazon.com/greengrass/v2/developerguide/provision-minimal-iam-policy.html). Puede proporcionar credenciales como variables de entorno. Para ello, en su dispositivo, realice una de las siguientes acciones para recuperar las credenciales y ponerlas a disposición del instalador de AWS IoT Greengrass Core:
    - Opción 1: Utilizar las credenciales a largo plazo de un usuario de IAM:
        - Proporcionar el ID de la clave de acceso y la clave de acceso secreta del usuario de IAM. Para obtener más información sobre cómo recuperar credenciales a largo plazo, consultar [Administración de claves de acceso para usuarios de IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
	    - Ir a __Consola IAM > Administracion de acceso > Usuarios > Seleccionar Usuario > Credenciales de Seguridad > Crear una clave de acceso__
	    - Copiar la clave de acceso y la clave privada.
          ![image](https://user-images.githubusercontent.com/46561573/156746711-227d0a4d-b1d7-444d-b157-eb1691a63e98.png)

    - Opción 2: (Recomendado) Utilizar credenciales de seguridad temporales de un rol de IAM:
        - Proporcionar el ID de la clave de acceso, la clave de acceso secreta y el token de sesión de un rol de IAM que escoja. Para obtener más información sobre cómo recuperar estas credenciales, consultar [Uso de credenciales de seguridad temporales con la CLI de AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_use-resources.html#using-temp-creds-sdk-cli).
