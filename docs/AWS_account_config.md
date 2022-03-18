# Configurar una cuenta de AWS
Si no tiene una cuenta de AWS, complete los siguientes pasos para crear una. Consultar como [configurar una cuenta de AWS](https://docs.aws.amazon.com/es_es/greengrass/v2/developerguide/setting-up.html#set-up-aws-account).

## Registrar una cuenta de AWS
1. Abrir https://portal.aws.amazon.com/billing/signup.
2. Seguir las instrucciones en línea. Parte del procedimiento de registro implica recibir una llamada telefónica e introducir un código de verificación en el teclado del teléfono.

## Crear un usuario administrador y añadir el usuario a un grupo de administradores
1. Iniciar sesión en la [consola de IAM](https://console.aws.amazon.com/iam/) como propietario de la cuenta seleccionando el usuario Root e introduciendo la dirección de correo electrónico de su cuenta de AWS. En la siguiente página, introduzca su contraseña.
2. En el panel de navegación, seleccionar __Administracion del acceso > Usuarios > Añadir usuario__.
![image](https://user-images.githubusercontent.com/46561573/156385293-88205ea0-e20c-4999-bf3a-65854a9b73cf.png)
3. Introducir el __nombre de usuario__, por ejemplo, GreengrassAdmin.
4. Seleccionar __Seleccione el tipo de credenciales de AWS > Contraseña: acceso a la consola de administración de AWS > Contraseña personalizada__ e introducir la nueva contraseña. (Opcional) Por defecto, AWS requiere que el nuevo usuario cree una nueva contraseña al iniciar la sesión por primera vez. Puede desactivar la casilla junto a El usuario debe crear una nueva contraseña en el siguiente inicio de sesión para permitir que el nuevo usuario restablezca su contraseña después de iniciar sesión.
![image](https://user-images.githubusercontent.com/46561573/156385504-b509bf77-bd4f-4554-917d-9bb2f5c212f0.png)
6. Seleccionar __Siguiente: Permisos__.
7. Seleccionar __Establecer permisos > Añadir usuario a grupo__.
8. Seleccionar __Crear grupo__. En el cuadro de diálogo Crear grupo, en Nombre del grupo introduzca Administradores.
9. Seleccionar __Filtrar políticas__ y, a continuación, seleccione __AWS managed - job function__ para filtrar el contenido de la tabla. 
10. En la lista de políticas, seleccionar la casilla __AdministratorAccess__ y pulsar __Crear grupo__.
![image](https://user-images.githubusercontent.com/46561573/156386216-f918c0a7-b5c1-48eb-8595-1e626ece0ebf.png)
11. De nuevo en la lista de grupos, seleccionar la casilla del nuevo grupo. Actualizar el navegador si es necesario para ver el grupo en la lista.
![image](https://user-images.githubusercontent.com/46561573/156387465-526d01c5-ac61-4782-a898-ab8271e28a7a.png)
12. Seleccionar __Siguiente: Etiquetas__. (Opcional) Añada metadatos al usuario adjuntando etiquetas como pares clave-valor. Para obtener más información sobre el uso de etiquetas en IAM, consulte [Etiquetado de entidades IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html) en la Guía del usuario de IAM.
13. Seleccionar __Siguiente: Revisar__ para ver la lista de permisos de grupo que se añadirán al nuevo usuario. Una vez revisado, seleccionar __Crear usuario__.
![image](https://user-images.githubusercontent.com/46561573/156387769-b65ec95b-08a7-4346-91ce-a9dd26eec961.png)

