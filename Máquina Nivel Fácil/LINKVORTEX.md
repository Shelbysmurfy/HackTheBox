# RESOLUCIÓN DE LA MÁQUINA LINKVORTEX

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/dfe04f8d-3ac5-44d1-8a34-cd834d4cd3fa)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/77fdf363-6ebc-4641-ab0e-5b3076c58398)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/5827deff-5c51-4a32-bf08-7a2598f834e7)

Hacemos fuerza bruta con dirsearch.

![image](https://github.com/user-attachments/assets/6e6955bf-c659-4881-9a7e-6cf9caa847e2)

En el robots.txt encontramos esto: 

![image](https://github.com/user-attachments/assets/79a48b2d-dc3c-4282-a543-fb094f6521a7)

Y en el /ghost, un login.

![image](https://github.com/user-attachments/assets/582fac33-ec3a-44b7-b892-3ec020b229a9)

Gracias a la herramienta wappalizer encontramos la versión de ghost, que es la 5.58

![image](https://github.com/user-attachments/assets/5ec896b9-c972-449a-80e3-a1d8763c8cb9)

Buscamos por internet y vemos que es vulnerable, pero que para iniciarla hace falta un usuario y una contraseña, que deben ser los del login.

![image](https://github.com/user-attachments/assets/d9358e23-d378-4593-8acc-5f6c7da50d65)

Vamos a hacer un dirsearch, pero ahora añadiendo un "dev.", delante de la ruta, para así poder ver los subdominios, que a menudo contienen recursos adicionales o entornos específicos.

![image](https://github.com/user-attachments/assets/4e75ff65-2646-48a4-9129-abb98416768a)

Nos descargamos GitHack de un repositorio de github.

![image](https://github.com/user-attachments/assets/83d70243-8f3f-4ec2-b0fa-ab2a74b0eeae)

Y seguidamente con python ejecutamos Githack.py, para la ruta con la que estamos trabajando.

![image](https://github.com/user-attachments/assets/2a734095-c93f-4b9f-be5d-02448f960e1d)

Y en el archivo authentication.test.js, grepeando por password encontramos esto: 

![image](https://github.com/user-attachments/assets/8819afdc-5627-49ea-a93f-ebb6bd8f0b20)

No tenemos el mail, pero si sabemos que seguramente se relacione con admin, ya que en el sitemap hemos encontrado posts publicados por el usuario: admin

![image](https://github.com/user-attachments/assets/57988e74-3a5a-4ce5-84d6-87f4c00ddef0)

Hemos probado mails comunes para este usuario, y luego uno mas personalizado, pensando en el nombre de la web y hemos ganado acceso.

Mail: admin@linkvortex.htb      Password: OctopiFociPilfer45

![image](https://github.com/user-attachments/assets/64c414cb-3a0e-4d92-ad34-6ef91ba06853)

Como ya tenemos unas credenciales válidas ahora vamos a explotar la vulnerabilidad que habíamos encontrado antes. 

Para ello nos traemos el repositorio a nuestra máquina.

![image](https://github.com/user-attachments/assets/d0192d7f-27ce-47b1-a993-81e750409561)

Nos metemos donde está el archivo y lo ejecutamos.

![image](https://github.com/user-attachments/assets/a9d52454-9f5c-4c34-b127-d3e26609b2dc)

Una vez dentro nos dice que pongamos que queremos leer, y l indicamos el /etc/passwd, para ver posibles usuarios.

![image](https://github.com/user-attachments/assets/e0752644-c324-425a-9840-ee3e936aeaa4)

Hacmeos fuerza bruta para el usuario y no encontramos nada.

Antes, cuando hemos usado GitHack, había un archivo, que me mostraba que existia un archivo de configuración.

![image](https://github.com/user-attachments/assets/5fdf5608-77f6-419f-a690-e129cc98b50b)

Lo miramos gracias al exploit que hemos encontrado, y vemos unas posibles credenciales.

![image](https://github.com/user-attachments/assets/f69188de-69ab-44bb-be20-e159c458380e)

![image](https://github.com/user-attachments/assets/bbd17f73-7fd5-49c6-a6ce-25e355145ef8)

Nos conectamos al servicio ssh con las credenciales obtenidas.

![image](https://github.com/user-attachments/assets/a22fd8ce-ce4f-4bf2-ac46-41320b06767a)

Nos vamos al directorio /home, y encontramos un archivo que parece importante pero que no podemos abrir.

![image](https://github.com/user-attachments/assets/89996b45-efe2-4bbc-913a-7574b0d7f1f0)

Hacemos sudo -l y vemos esto: 

![image](https://github.com/user-attachments/assets/0950ac4d-64b5-4711-9494-d69b188e55ca)

Nos vamos al archivo de directorio /opt para ver el archivo que hemos visto hace un momento, ya que puede ser útil para escalar privilegios. 

![image](https://github.com/user-attachments/assets/e970c1a7-4dde-447e-9e63-d1fa25f86c0d)

Volvemos a la ruta de /home/bob, y hacemos ls -l para ver que permisos tienen los archivos y vemos que el archivo gg, tiene permisos de root, y parece ser el archivo que tiene la segunda flag, la del root.

![image](https://github.com/user-attachments/assets/641a5304-2d5a-4eb1-b92d-fe18530c886f)

Sabiendo esto y el archivo del directorio /opt, creamos un archivo igual pero con la extensión .png

![image](https://github.com/user-attachments/assets/d8d016bd-0a43-4f66-9c5a-3413f1e7b4e7)

Activamos el CHECK_CONTENT a true, ya que en el script vemos que está en false, ejecutamos el comando /usr/bin/bash, ya que al hacer sudo-l hemos visto que está activo y necesitamos ser root, seguidamente escribimos la ruta del archivo que se supone que nos leerá archivo, y el archivo con extensión .png, que es lo que nos pedía.

![image](https://github.com/user-attachments/assets/8f68fcb2-8c69-4bcc-9a6d-a983b8fca42a)

## SUBMIT USER FLAG

En el directorio /home también encontramos la primera flag, la del user.

![image](https://github.com/user-attachments/assets/538d78fe-b522-40a7-b9a3-4bfad82c6ef7)

![image](https://github.com/user-attachments/assets/cfc01a29-097e-4a49-902b-8d86fa5fa7b9)

## SUBMIT ROOT FLAG

![image](https://github.com/user-attachments/assets/05aa4881-d2c5-40c5-b80a-327c1bb8d912)

![image](https://github.com/user-attachments/assets/c3983a25-3385-4706-b5a7-1471efe1afdf)

