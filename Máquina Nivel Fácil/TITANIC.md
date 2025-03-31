# RESOLUCIÓN DE LA MÁQUINA TITANIC

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/cd1f56cd-0ffa-44d5-96c6-d31ced2c23e1)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/59620e66-ac4f-44f2-9eaa-d15cda74d86a)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/bde78e2f-032d-426a-97b8-76e50efebd3f)

Cambiamos el dominio del /etc/hosts

![image](https://github.com/user-attachments/assets/7869a8e7-1164-408d-9efd-6fce5ea56fd5)

Abrimos la web.

![image](https://github.com/user-attachments/assets/886fcb06-9b5e-42fd-a858-cd5801e6b07f)

Hacemos gobuster y vemos el directorio /download que contiene esto: 

![image](https://github.com/user-attachments/assets/840686a0-e25a-49f4-b4a6-5a5e83654bf4)

![image](https://github.com/user-attachments/assets/a434ce88-af54-444b-adf8-6c6ab6ccc31e)

Capturamos la petición y vemos que nos dice que requiere el parámetro "ticket".

![image](https://github.com/user-attachments/assets/8235b72d-18ff-4f58-a8f8-cae7b2020e16)

Añadimos el parámetro "ticket", junto a "/etc/passwd", y nos devuelve resultado. Vemos que tenemos el usuario "developer".

![image](https://github.com/user-attachments/assets/113bebc5-b503-479d-83a0-cf0e6e098833)

Usamos una ruta básica donde acostumbra a estar la flag del user y la encontramos.

![image](https://github.com/user-attachments/assets/7fe07a7b-0b74-453f-a6d8-f5d46d6e76ee)

## SUBMIT USER FLAG

![image](https://github.com/user-attachments/assets/b670ebba-8f3e-4990-b897-e184d09cfa55)

Hacemos fuerza bruta con ffuf en busca de subdomios.

![image](https://github.com/user-attachments/assets/19185587-8a25-4b90-9c53-3ea62f560700)

Encontramos el subdominio "dev", lo añadimos en el /etc/hosts, y seguidamente en nuestra ruta.

![image](https://github.com/user-attachments/assets/7e6be206-6cbe-4263-ada2-307f80b5f33d)

![image](https://github.com/user-attachments/assets/5ef67b77-fd23-4d31-b5c0-d0bd6980a677)

Nos registramos y vemos esto: 

![image](https://github.com/user-attachments/assets/79388dcb-97e9-4740-a1a5-7a4a355cb740)

Encontramos un repositorio con información sobre un path y una base de datos.

![image](https://github.com/user-attachments/assets/bebc57ff-1179-4293-9fe0-580b1e3f770c)

![image](https://github.com/user-attachments/assets/2dde18ce-2ce0-4c0a-8be9-14e883029726)

A partir de esto nos vamos al burpsuite y añadimos la ruta que nos dicen pero no obtenemos resultado.

Y después de buscar un buen rato rutas posibles donde poder encontrar información sobre la base de datos y la ruta de esta, encontramos que el archivo app.ini nos puede dar esta información: 

![image](https://github.com/user-attachments/assets/37cb77dc-a9dc-4ab1-8cdc-257f635721e9)

Probamos la ruta y vemos mucha información.

![image](https://github.com/user-attachments/assets/84787162-3acf-473e-9bdd-79ac87fb8595)

Nos traemos la base de datos a nuestra máquina con curl.

![image](https://github.com/user-attachments/assets/e6ebeb1a-47c0-4e0f-9001-7e5199f02108)

Abrimos la base de de datos gitea.db con sqlite3.

![image](https://github.com/user-attachments/assets/9fc599eb-df3d-4288-a2fe-3a7a46450089)

Nos vamos a la tabla user, y vemos posibles credenciales (hay que añadir el salt, sino no podremos decodearla).

![image](https://github.com/user-attachments/assets/aedd2e1d-edb4-4754-a134-aff218a1644d)

Seguidamente vamos a traernos la herramienta "gitea2hashcat.py". Vamos a ejecutar la password cifrada primero con esta herramienta y luego usaremos hashcat para sacar la contraseña.

Como podemos ver en la imagen, sin el "salt" no nos dejaba.

![image](https://github.com/user-attachments/assets/7f0b4797-635d-49f3-8498-d54bacd6db9f)

Creamos un archivo.txt con el hash obtenido y lo ejecutamos con la herramienta hashcat.

![image](https://github.com/user-attachments/assets/4fabe960-702b-464d-868c-ddbd5ff68ef8)

![image](https://github.com/user-attachments/assets/79071b81-379a-4b43-b838-9f121150965f)

Seguidamente usamos el parámetro "show" para ver la credencial obtenida.

![image](https://github.com/user-attachments/assets/59088c25-11e5-45f3-bc02-02273c2cc2aa)

Y nos conectamos al servicio ssh con las credenciales obtenidas "developer:25282528".

![image](https://github.com/user-attachments/assets/0f6d6a8d-4a03-4515-bf93-8a394ecbf43a)
![image](https://github.com/user-attachments/assets/326b7094-d5c1-4410-8880-78347f536316)

Al conectarnos como hemos visto ya somos usuario root.

Nos vamos al directorio root y podemos ver la segunda flag, la del usuario root.

![image](https://github.com/user-attachments/assets/30d72bd1-8742-49cd-9fde-9c9ae8ef17e0)

## SUBMIT ROOT FLAG

![image](https://github.com/user-attachments/assets/c822c84e-3ab1-46ea-86db-286d72589bfe)

