# RESOLUCIÓN DE LA MÁQUINA CODE

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/ea571de9-f815-411b-ad5f-33f4450a4c88)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/5bb747d4-8c2a-490d-837b-79603576134e)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/9ebdc166-1183-446a-8cf2-7ae9307eb661)

Miramos la web por el puerto 5000 y vemos una consola python.

![image](https://github.com/user-attachments/assets/a88479f6-97e8-45f7-b42d-5c9a95454f2d)

Hacemos un "print(db)", y vemos la base de datos.

![image](https://github.com/user-attachments/assets/225b4f69-efa7-403b-af2e-f3bc9061555c)

Buscamos los usuarios usando SQLAlchemy.

![image](https://github.com/user-attachments/assets/301f813d-9f53-4eb2-931e-dcb8e8d6c5c3)

Probamos a buscar el id de la tabla user pero no me muestra nada.

![image](https://github.com/user-attachments/assets/698bba23-ea3f-4949-bf22-de27c6cf4e0b)

Después de un rato buscando encontramosm la manera de buscar el id dentro de la tabla user.

![image](https://github.com/user-attachments/assets/e7f84fea-307e-408a-bc73-43cb8139632e)

Encontramos usuarios y contraseñas dentro de la tabla user.

![image](https://github.com/user-attachments/assets/1b0a19de-d457-478f-b6b1-79a486ebdea9)

Buscamos el tipo de hash que tiene como contraseña los usuarios y vemos que es un md5.

![image](https://github.com/user-attachments/assets/7cc1bb9b-9bda-40e3-9c10-ec370b742e61)

Crackeamos la dos passwords con John the Ripper ("development:development", "martin:nafeelswordsmaster".

![image](https://github.com/user-attachments/assets/82463559-cb75-4201-9f1c-6f8006387064)

Logramos conectarnos al servicio ssh con el usuario martin.

![image](https://github.com/user-attachments/assets/b71d9d26-d1c7-4296-801c-17c9ea93ad4a)
![image](https://github.com/user-attachments/assets/2224894f-10e7-4227-8a6e-b105bcb245df)

Hacemos sudo -l y vemos esto: 

![image](https://github.com/user-attachments/assets/fd92a8fc-b0c6-4b88-9b99-b79c102a3cce)

Nos habla de el archivo backy.sh, el cual no podemos editar ya que no tenemos permisos sobre el, pero dentro de este hay otro archivo llamado task.jon.

Vamos hasta donde se encuentra y vemos que tiene este contenido: 

![image](https://github.com/user-attachments/assets/c41f89b9-86f5-4001-9e0c-f73e79091a4d)

Si en el apartado de "directories_to_archive", indicamos en vez de app, user.txt que es lo que buscamos, y lo ejecutamos obtenemos un archivo.tar

Este lo descomprimimos y obtenemos la primera flag, la del user.

![image](https://github.com/user-attachments/assets/7e49a32e-ed25-4a53-8123-e77900c74b37)

Y ahora hacemos lo mismo pero para el usuario root.

![image](https://github.com/user-attachments/assets/d23bc32e-aaf7-40ab-b57b-011e68f8c0f3)

Ejecutamos el permiso SUDO y vemos todos los directorios y archivos disponibles.

![image](https://github.com/user-attachments/assets/6b22544f-e6f2-459c-b3ee-5bb032fbc936)

Entre ellos esta el root.txt, así que primero descomprimimos el archivo.tar que hemos obtenido.

![image](https://github.com/user-attachments/assets/978ebbe5-de2f-432e-a99e-4ec261d79692)

Vemos que se nos crea un directorio "root", entramos en el y vemos la segunda flag, la del usuario root.

![image](https://github.com/user-attachments/assets/a757dc23-c9be-4edf-b48b-b73fa196fe0d)
