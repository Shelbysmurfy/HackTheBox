# RESOLUCIÓN DE LA MÁQUINA DOG

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/c1557284-7744-46cf-965c-a3c165712e2f)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/353828dc-ed80-48af-9508-5829c2e56404)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/15be516d-ac1e-4048-8bbb-fecd897cc60b)

Abrimos la web.

![image](https://github.com/user-attachments/assets/cef31291-4d3c-40e1-b7e2-d243ef3d6786)

Vemos un login donde hay un apartado que es "RESET PASSWORD", donde si ponemos un usuario nos dice si existe o no.

Hemos intentado con admin y nos ha mostrado esto: 

![image](https://github.com/user-attachments/assets/1dffc2fb-6b67-40ae-86b3-ee38059f1910)

Por tanto hemos buscado información en la web, y al probar el usuario "dogBackDropSystem", nos ha devuelto un error diferente y nos ha redirigido a la opción Login.

![image](https://github.com/user-attachments/assets/0e163a80-9d2a-4f57-a165-e0dc2c46b4de)

Probamos a buscar una posible contraseña para este usuario con hydra y una solicitud hhtp-post-form  pero no encontramos nada.

Vamos a hacer un dirsearch.

![image](https://github.com/user-attachments/assets/37b23ab0-8e7a-4634-b39b-f5dd094a298c)
![image](https://github.com/user-attachments/assets/c619d7a9-000b-4c76-ac81-d8a35035e589)

Sabiendo que estamos tratando con git vamos a traernos todo lo que tenemos a nuestra máquina con la herramienta Githack.

![image](https://github.com/user-attachments/assets/62c103fa-4469-4809-8453-630ef4c56021)

![image](https://github.com/user-attachments/assets/1d744d10-394b-476f-b5fb-20314b75ca4a)

En el archivo settings.php encontraremos la contraseña de la base de datos de backdrop.

![image](https://github.com/user-attachments/assets/3b7bdbf5-42c3-42c7-999b-ef8d76653f21)

Probamos a conectarnos con las credenciales "dogBackDropSystem:BackDropJ2024DS2024", pero no podemos.

Entonces buscamos posibles o contraseñas o usuarios en la web y encontramos un correo.

![image](https://github.com/user-attachments/assets/061e1df1-56c1-4308-b42c-e32a91ad9e75)

Probamos con este pero tampoco podemos, vemos otro correo en /.git/logs/HEAD, que tiene la misma estructura que el anterior pero tampoco funciona.

Sabiendo que los correos acaban en "dog.htb", vamos a hacer una búsqueda con grep en nuestra terminal con lo que nos hemos traido con Githack.

![image](https://github.com/user-attachments/assets/8fc7bed1-4bbe-432b-855b-c08287009127)

Probamos las credenciales "tiffany@dog.htb:BackDropJ2024DS2024", y esta vez ganamos acceso.

![image](https://github.com/user-attachments/assets/4d63f782-1357-451b-8859-131ecca9176f)

![image](https://github.com/user-attachments/assets/f43d7bb3-b249-40fb-94d1-959f782bf1c4)

Encontramos una subida de archivos pero solo nos deja subir archivos con estas extensiones: 

![image](https://github.com/user-attachments/assets/2b61c446-00dd-4b29-b8a2-21e80cb29721)

En muchos sitios de la página encuentro esta versión: 

![image](https://github.com/user-attachments/assets/731d5218-2546-467e-a0b1-b28722536e3f)

Vamos a buscar si hay algun exploit para esta "Backdrop cms 1.27.1".

![image](https://github.com/user-attachments/assets/754a17c3-54f8-4e1b-a145-b63253bb9e1c)

Nos lo descargamos.

![image](https://github.com/user-attachments/assets/690ad9a0-ef2f-43ec-9e21-ecf35e2802b6)

Vamos a la ruta que nos indican y vemos una subida de archivo.tar

![image](https://github.com/user-attachments/assets/b6f13717-517f-4424-b144-d53e96392e52)

Nos vamos a nuestra terminal ejecutamos el archivo, pero vemos que el script nos crea un archivo .zip, estos están deshabilitados en la web por lo que tomaremos la carpeta llamada shell creada por el script y la comprimiremos con tar.

![image](https://github.com/user-attachments/assets/b0c8b5c1-dabc-41ce-a7c8-1b8b5b5be469)

![image](https://github.com/user-attachments/assets/e077d681-ef6b-4bf7-aa42-2302e5614040)

Subimos el archivo shell.tar correctamente.

![image](https://github.com/user-attachments/assets/b0fb5aed-c167-4134-ad8d-69316e1a5eb0)

Seguidamente nos vamos a la ruta que nos indica el exploit y vemos nuestro archivo.

![image](https://github.com/user-attachments/assets/0d002523-8610-426d-bee1-19e79a25d3eb)

Miramos el /etc/passwd y vemos dos usuarios (jobert y johncusack).

![image](https://github.com/user-attachments/assets/23b2dbb5-b386-4886-92d3-cc9944964083)

Hacemos hydra para los dos usuarios pero no encontramos nada.

Probamos a usar la credencial que habíamos encontrado antes "BackDropJ2024DS2024", para los dos usuarios y nos funciona para el usuario "johncusack".

![image](https://github.com/user-attachments/assets/7aaacb4f-95c1-4a01-99cf-9fce503d7645)
![image](https://github.com/user-attachments/assets/021e7ba1-35b6-48f2-ad35-f6edcc2118db)

Hacemos ls y vemos la primera flag, la del user.

![image](https://github.com/user-attachments/assets/18cbc510-e9d6-460b-9a2e-8cf1d401d1bb)

## SUBMIT USER FLAG

![image](https://github.com/user-attachments/assets/4b0ff049-e484-431c-8fcf-b1d2fd404cca)

Hacemos sudo -l y vemos esto: 

![image](https://github.com/user-attachments/assets/1d604095-6d18-4dcc-b9e4-378c4719bca3)

bee --> es una herramienta que permite gestionar el servidor web desde el cli, y eso nos permitirá realizar ejecucion de comandos con php.

Tenemos un archivo en el directorio /home que contiene esto: 

![image](https://github.com/user-attachments/assets/f6c697a3-f309-4577-a82b-123239131835)

Nos da esta pista: 

![image](https://github.com/user-attachments/assets/0adaed13-903a-40e5-b24e-434d3a96c600)

Después de estar probando diferentes comandos conseguimos obtener la segunda flag, la del usuario root.

Para ello hay que estar en el directorio /var/www/html

![image](https://github.com/user-attachments/assets/e727bc3c-c770-428d-9ec3-dfb5cb9d3121)

## SUBMIT ROOT FLAG

![image](https://github.com/user-attachments/assets/2cb60ce3-5877-41b1-9882-16d239f315df)


