# RESOLUCIÓN DE LA MÁQUINA ESCAPETWO

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/4003bae0-fe89-4bd7-b4c7-5334c4c2d835)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/5ad2f064-2a23-498c-98d6-73059dff774a)
![image](https://github.com/user-attachments/assets/f299663f-4056-4b70-a93b-7fd00c3aefb3)

En la máquina nos dan unas credenciales válidas.

![image](https://github.com/user-attachments/assets/0f1fbc85-c9ee-44be-82e6-efed96ba8c1a)

Vamos a usarlas con el servicio smb.

![image](https://github.com/user-attachments/assets/dcc401f1-b45e-4bb9-98b4-16881fdd7695)

Con la herramienta netexec y las credenciales obtenidas miramos las credenciales activas.

![image](https://github.com/user-attachments/assets/7422ef25-c8b8-4e05-852a-0e2278ff3787)

Entramos en el directorio /Accounting Department con el usuario "sequel.htb\\rose", y vemos esto: 

Con el usuario rose, no te deja entrar, pero poniendo sequel.htb delante, sí deja.

![image](https://github.com/user-attachments/assets/d0a7cca8-0018-4881-869f-8d7bfb8b85ee)

Nos traemos los archivos a nuestra máquina, y los abrimos en busca de información, en el accounts.xlsx, encontramos un archivo llamado sharedStrings.xml con posibles credenciales.

![image](https://github.com/user-attachments/assets/c4bd6c18-01df-4130-a19d-d906ce3ddf53)

Con la herramienta netexec y las credenciales nuevas obtenidas, buscamos posibles credenciales y usuarios válidos.

Encontramos posibles usuarios.

![image](https://github.com/user-attachments/assets/7a1d6695-46f4-480a-a0a8-d77958142838)

Miramos con la versión que estamos trabajando para luego ponerla como ruta de búsqueda.

![image](https://github.com/user-attachments/assets/55534ebd-9f3b-42f0-a6f4-136cd472a0e0)

Encontramos una posible credencial dentro de un archivo de configuración.

![image](https://github.com/user-attachments/assets/13a735e6-cbb0-43de-b1da-4b7a65414a20)

Probamos la password con el usuario ryan, usando el comando smbmap para que me muestre directorios que puedo leer, ver o escribir, y me devuelve resultado.

![image](https://github.com/user-attachments/assets/7cf3625d-d335-4982-b921-50ef3aaa301a)

Por tanto ahora vamos a usar smbclient para ganar acceso al directorio Users.

![image](https://github.com/user-attachments/assets/82582d0a-4ea2-48dc-8732-2b9a4fd3fdc7)

## SUBMIT USER FLAG

Encontramos la primera flag, la del user.

![image](https://github.com/user-attachments/assets/eb13abaa-12a1-4bca-9f3c-b282b0f2f1c6)

![image](https://github.com/user-attachments/assets/4a160b73-aed8-4153-ada2-cf24857a83bc)

![image](https://github.com/user-attachments/assets/73664c89-5e39-44dd-862f-709aa79f9c11)

## SUBMIT ROOT FLAG

Encontramos la segunda flag, la del root.

![image](https://github.com/user-attachments/assets/fad66420-686e-41e9-b7ea-c852baa82105)

![image](https://github.com/user-attachments/assets/a4540a7e-d759-4e4c-abf7-497f8fb86984)

![image](https://github.com/user-attachments/assets/df9ac1d7-bfaa-4a00-9693-aa5101c5fe04)

