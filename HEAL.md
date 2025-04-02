# RESOLUCIÓN DE LA MÁQUIN HEAL

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/81770c0d-150c-4e42-8c75-c7e330599021)

Hacemos un nmap para poder ver los puertos que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/c29551b0-1376-4125-9868-a6740bbfbdbd)

Añadimos el dominio que nos mencionan en el /etc/hosts

![image](https://github.com/user-attachments/assets/9ec92737-e102-484a-9d19-6bdcfd379095)

Abrimos la web.

![image](https://github.com/user-attachments/assets/94fa2780-ab17-4d03-9fc5-55806b73fe5f)

Hacemos fuerza bruta con ffuf en busca de subdominios.

![image](https://github.com/user-attachments/assets/c7f374c0-8542-46a5-b623-a89a56c2aa73)

Lo añadimos al /etc/hosts.

![image](https://github.com/user-attachments/assets/f7cce4b1-60d2-41ea-8a2c-d2ad19a6129a)

Abrimos la nueva ruta.

![image](https://github.com/user-attachments/assets/177a0dbd-76d1-4d21-a60d-04ff27d5926c)

Encontramos dos versiones, intentamos buscar exploits para estas pero no encontramos nada.

Nos creamos un usuario nuevo y nos logueamos con el.

![image](https://github.com/user-attachments/assets/4c885a14-56c7-4b3e-9353-bcdff34282ed)

Abajo del todo tenemmos un botón de "EXPORT AS PDF", vamos a capturar la petición con Burpsuite.

![image](https://github.com/user-attachments/assets/c60a274d-8b9f-4a85-a6e8-65012cee58b6)

![image](https://github.com/user-attachments/assets/1e8ca1fd-e3ba-4fe9-ba9b-58e6776e0c18)

Sabiendo que tenemos un archivo.pdf y que el host el "api.heal.htb", vamos a hacer uso de gobuster para ver si encontramos algo.

![image](https://github.com/user-attachments/assets/f1814da9-f767-478a-be1b-90434cb0c518)

Encontramos el parámetro download con diferentes extensiones, usamos la básica para ver si podemos abrir el pdf.

![image](https://github.com/user-attachments/assets/0acd0cd1-f600-4ecf-aa3b-3bf5ea7389ef)

Seguidamente intentamos ver si podemos inyectar comandos a partir de la ruta que tenemos y conseguimos ver el /etc/passwd

Vemos que tenemos 3 usuarios: ron, ralph y postgres.

![image](https://github.com/user-attachments/assets/97019381-9b74-431a-9a4a-be98cf5d3fa9)



NOSE COMO SEGUIR





Si nos vamos al apartado de survey vemos esto: 

![image](https://github.com/user-attachments/assets/84430e53-2dd9-4091-a6a9-c9c0b2301f81)

Y si clicamos en el botón verde, nos salta un error, pero en la url vemos un posible subdominio.

![image](https://github.com/user-attachments/assets/457491d8-09e8-4b89-90f9-1d34e4b49430)

Lo añadimos en el /etc/hosts y ya no nos da error.

![image](https://github.com/user-attachments/assets/7c72f054-89fb-4a06-9a6c-5f5e78b58f1b)

![image](https://github.com/user-attachments/assets/0497c942-a6cd-46b4-a31f-ad4d6917ef2e)

Si nos vamos a /index.php vemos un posible correo de administrador.

![image](https://github.com/user-attachments/assets/0dd45f7a-4563-4718-972f-16de0c9cae19)





AQUI TENGO UN LOGIN PERO ME FALTA LA CONTRASEÑA
