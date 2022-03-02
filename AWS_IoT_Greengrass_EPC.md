# Pasos previos
- Completar el [tutorial "Getting Started"](https://docs.aws.amazon.com/es_es/greengrass/v2/developerguide/getting-started.html).
   - Tener una cuenta de AWS. Consultar como [configurar una cuenta de AWS](https://docs.aws.amazon.com/es_es/greengrass/v2/developerguide/setting-up.html#set-up-aws-account).
   - Tener creado un usuario en AWS Identity and Access Management (IAM) con permisos de administrador.
   - Un equipo de desarrollo con Windows, macOS o UNIX con conexión a Internet.
   - Un dispositivo para configurarlo como Greengrass core device (EPC) con conexión a Internet y permisos de administrador.  
   - Tener Python3.5 o posterior instalado en el dispositivo e incluido en el PATH.
   - AWS Command Line Interface(AWS CLI) instalado y configurado con credenciales en el equipo de desarrollo y en el dispositivo. Asegúrese de usar la misma Región de AWS para configurar el AWS CLI en el equipo de desarrollo y en el dispositivo. Para utilizar AWS IoT Greengrass V2 con AWS CLI, debe tener una de las siguientes versiones o posterior:
      - Versión mínima de AWS CLI V1: v1.18.197
      - Versión mínima de AWS CLI V2: v2.1.11

## Configurar una cuenta de AWS
Si no tiene una cuenta de AWS, complete los siguientes pasos para crear una.
### Para registrar una cuenta de AWS
1. Abrir https://portal.aws.amazon.com/billing/signup.
2. Siga las instrucciones en línea. Parte del procedimiento de registro implica recibir una llamada telefónica e introducir un código de verificación en el teclado del teléfono.
### Para crear un usuario administrador para usted y añadir el usuario a un grupo de administradores (consola)
1. Iniciar sesión en la [consola de IAM](https://console.aws.amazon.com/iam/) como propietario de la cuenta seleccionando el usuario Root e introduciendo la dirección de correo electrónico de su cuenta de AWS. En la siguiente página, introduzca su contraseña.
2. En el panel de navegación, seleccionar __Administracion del acceso > Usuarios > Añadir usuario__.
3. Introducir el __nombre de usuario__, por ejemplo, GreengrassAdmin.
4. Seleccionar __Seleccione el tipo de credenciales de AWS > Contraseña: acceso a la consola de administración de AWS > Contraseña personalizada__ e introducir la nueva contraseña.


Traducción realizada con la versión gratuita del traductor www.DeepL.com/Translator






















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

