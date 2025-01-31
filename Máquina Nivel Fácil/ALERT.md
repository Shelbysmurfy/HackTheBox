# RESOLUCIÓN DE LA MÁQUINA ALERT

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/d11f6e60-0c79-4b3e-8656-d29206b561f6)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/709e7702-e62a-43c1-a99f-ebe5e3d0810e)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/a8312df8-38f7-455d-95f2-3820a558bbed)

Abrimos la web y vemos esto: 

![image](https://github.com/user-attachments/assets/d0d30ed1-937c-48a7-a1bf-c3d796e01d00)

Hacemos fuerza bruta con gobuster.

![image](https://github.com/user-attachments/assets/cdb67ea8-03a0-4be7-8afb-0963878dd4e8)

Ahora hacemos un fuzzing para descubrir directorios y archivos ocultos.

![image](https://github.com/user-attachments/assets/e7e7b5d1-e900-4f91-a654-2e21d663c190)

Creamos un archivo malicioso, shell.md

![image](https://github.com/user-attachments/assets/a9095a14-d105-4a2b-bb17-4a426749645b)

Seguidamente desde la página subimos el archivo que hemos creado.

![image](https://github.com/user-attachments/assets/22fee107-2b8b-4907-b7fc-a2ef1e707fbe)

Copiamos el link de la página a la que nos lleva.

![image](https://github.com/user-attachments/assets/5b16f1a7-c18c-4cb3-9cf3-64fa164a0e3d)

Y lo pegamos junto a un correo inventado, en el apartado de Contact Us.

![image](https://github.com/user-attachments/assets/086ecbc0-afc4-4a8f-83be-5f9966dead42)

Mientras estamos en escucha desde nuestra terminal y recibiremos un mensaje.

![image](https://github.com/user-attachments/assets/e9e4ba62-785a-4325-90e2-8971ae3dc527)

Lo decodeamos y sacamos el usuario: albert, junto a un hash.

![image](https://github.com/user-attachments/assets/ae95ac27-6a6d-44ce-8264-96e4c1a85ec4)

Identificamos que tipo de hash tenemos con hash-identifier.

![image](https://github.com/user-attachments/assets/41444c2e-8529-4a9e-a11a-76aafe0f9890)

Guardamos el hash en un archivo .txt, y usamos john the ripper para descifrar el mensaje que esconde.

![image](https://github.com/user-attachments/assets/57091eea-644c-43f5-8e77-73ab860feff9)

Nos conectamos al servicio ssh con las credenciales obtenidas (albert:manchesterunited)

![image](https://github.com/user-attachments/assets/6be92468-d7b7-443b-a996-831b79c27618)
![image](https://github.com/user-attachments/assets/14c090fa-8f8d-4042-8ad5-e50758d957e9)

## SUBMIT USER FLAG

Encontramos la primera flag, la del usuario.

![image](https://github.com/user-attachments/assets/1883155b-2aef-41b0-bc9b-c09a8e0b800a)

![image](https://github.com/user-attachments/assets/2f1571f7-1b64-4a72-9824-fc7425439d90)

## SUBMIT ROOT FLAG

Hacemos netstat -tuln y vemos esto: 

![image](https://github.com/user-attachments/assets/ac1a16a7-f2a4-4945-a903-8450034189a4)

Nos conectamos al servicio ssh, basandonos en el localhost y el puerto 8080.

![image](https://github.com/user-attachments/assets/2687554c-b191-491a-96d5-987433acf238)
![image](https://github.com/user-attachments/assets/a49d373d-3078-4d19-8688-4216fdd09930)

Vamos al navegador y abrimos la web, puerto 8080.

![image](https://github.com/user-attachments/assets/8510350c-2df3-4aab-a99d-81c2075841b3)

Nos vamos al servicio ssh, y en el directorio /opt, en la carpeta config, tenemos un archivo con una reverse shell.

![image](https://github.com/user-attachments/assets/44ad579a-bc19-4498-86d3-81e1fa40705c)

La editamos y ponemos nuestra IP (tun0), y un puerto cualquiera.

![image](https://github.com/user-attachments/assets/be5a275d-b5bc-4d21-ac95-08d53c000e1a)

Nos vamos al navegador, lo abrimos y mientras nos ponemos en escucha con netcat para ganar acceso a la máquina.

![image](https://github.com/user-attachments/assets/b0cf1045-5101-4e77-8677-f00a96c210e5)

Y ya tenemos la segunda flag, la del usuario root.

![image](https://github.com/user-attachments/assets/c1f56ffc-0b0a-4746-896a-701816b028c6)

![image](https://github.com/user-attachments/assets/34c07dcd-99e2-4bf2-aed8-b331b9b47f23)



