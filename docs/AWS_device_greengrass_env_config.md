## Instalar el software AWS IoT Greengrass Core
1. Después de [obtener las credenciales de usuario](https://github.com/JaviPxc/AwsOnPlcnext/blob/main/docs/AWS_account_greengrass_config.md).
2. Conectar por SSH.
3. Configurar las variables de entorno con las credenciales de acceso.
   - Opción 1: Utilizar las credenciales a largo plazo de un usuario de IAM:
        - Ejecutar los siguientes comandos (Linux) para proporcionar las credenciales al software del núcleo de AWS IoT Greengrass (sustituir el texto después del signo “=” por la información especificada).
        ```
            export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
            export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
        ```
   - Opción 2: (Recomendado) Utilizar credenciales de seguridad temporales de un rol de IAM:         
        - Ejecutar los siguientes comandos (Linux) para proporcionar las credenciales al software del núcleo de AWS IoT Greengrass (sustituir el texto después del signo “=” por la información especificada).
        ```
            export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
            export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
            export AWS_SESSION_TOKEN=AQoDYXdzEJr1K...o5OytwEXAMPLE=
        ```
_Nota_: El instalador no guarda ni almacena sus credenciales.



