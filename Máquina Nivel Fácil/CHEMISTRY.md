# RESOLUCIÓN DE LA MÁQUINA CHEMISTRY

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/394bab51-2143-4995-b377-4965e9b1127e)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/338e6ff5-dce1-4d9d-99a9-cfb1c84ed90a)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/3f2d1540-528e-48a6-967b-5656431efeb6)

Nos metemos en el puerto 5000 y vemos esto: 

![image](https://github.com/user-attachments/assets/aaa83344-d72b-4e29-a5f5-1331c9f51301)

Nos registramos y ganamos acceso a una subida de archivos.

![image](https://github.com/user-attachments/assets/d0e3dee7-d1df-4fa7-9e56-ee49ef633b46)

Github para crear nuestro archivo vulnerable .cif "https://github.com/materialsproject/pymatgen/security/advisories/GHSA-vgv8-5cpj-qj2f"

![image](https://github.com/user-attachments/assets/57082989-8f92-4e7f-b543-b652d72e5027)

Creamos nuestro archivo vulnerable, poniendo como IP el tun0, y puerto el 5555.

Lo subimos a la páqgina y ganamos acceso, dándole a view, mientras estamos en escucha desde nuestra terminal.

![image](https://github.com/user-attachments/assets/c0cca4f1-4fff-4ef9-b083-0ae6acc8ff8d)

Encontramos uan base de datos con usuarios y posibles contraseñas, pero que estan codificadas en md5.

![image](https://github.com/user-attachments/assets/fd1e0d59-9175-4021-8b3f-38f111da0440)

![image](https://github.com/user-attachments/assets/c374a584-97ea-4424-ac5d-5a14b0f20ab3)

Nos vamos al directorio /home, y vemos que hay el usuario rosa, y que dentro está la primera flag, la del user.txt

![image](https://github.com/user-attachments/assets/a65e1736-dbf6-4155-8019-78324b479570)

Así que vamos a coger la posible contraseña que hemos visto antes en la base de datos del usuario rosa, y vamos a desencriptarla.

![image](https://github.com/user-attachments/assets/dffc9114-d6cc-46a4-b7cf-caca455175fa)

Nos conectamos por el servicio ssh, como usuario rosa.

![image](https://github.com/user-attachments/assets/bb362525-a872-4691-b247-52b4245864af)

## SUBMIT USER FLAG

Y ahora si podemos abrir la primera flag, la del user.

![image](https://github.com/user-attachments/assets/bc8a687f-5676-4694-8fe6-9bfcd5deb198)

![image](https://github.com/user-attachments/assets/1f4aecc1-a690-4a24-bf19-1d90a085c9fe)

## SUBMIT ROOT FLAG

Hacemos uso de netstat -l y vemos que en el purto 8080 (http-alt) parece que hay algún sitio web.

![image](https://github.com/user-attachments/assets/949bf517-e4d3-4df9-bae2-c34bfa15ad5f)

Haciendo uso de curl, encontramos esto: 

![image](https://github.com/user-attachments/assets/6776e3b4-3191-4743-bf09-5bec6f8d057c)

Miramos la vulnerabilidad.

![image](https://github.com/user-attachments/assets/4ca3e62b-3fae-41a6-b5e4-85a24fb51ec0)

Ahora usamos la vulnerabilidad para leer el /etc/passwd

![image](https://github.com/user-attachments/assets/0efe1151-8229-49a4-b1c2-360b5eb226a5)

Y de esta misma manera podemos encontrar la segunda flag, la del usuario root.

![image](https://github.com/user-attachments/assets/8aed665c-5507-4457-b010-14ccc15dc5fa)

![image](https://github.com/user-attachments/assets/c1cc624a-f544-427d-8d66-2d7c4f78ea16)

