# RESOLUCIÓN DE LA MÁQUINA CICADA

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/10bb9292-d070-46a5-96dd-853a5693063a)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/154166d7-5f9d-4833-96e5-44e2e0039182)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/263d3482-43f6-40e9-bd4f-5858112a389d)
![image](https://github.com/user-attachments/assets/12584577-371e-4c78-9c1c-3d4e5cf91a08)

Hacemos un smbclient para ver si hay recursos compartidos.

![image](https://github.com/user-attachments/assets/3088077e-bc6b-46e7-91f1-3a7ee419d172)

En el HR, encontramos un archivo .txt

![image](https://github.com/user-attachments/assets/6fec7ee9-4e80-407d-8d95-a78bfbe82b97)

Nos llevamos el archivo a nuestra máquina y lo abrimos, en el encontramos una contraseña: Cicada$M6Corpb*@Lp#nZp!8

![image](https://github.com/user-attachments/assets/e0c17dc2-f9c5-464b-8ce3-baeacae69dbd)

Vemos que este habla sobre un usuario, pero no lo sabemos, así que vamos a hacer uso de la herramienta netexec, y lo usaremos con la opción --rid-brute para recuperar los usuarios del sistema.

![image](https://github.com/user-attachments/assets/d169985c-25d7-414f-a27b-daa41f984deb)

Ahora vamos a crear un archivo.txt con todos los posibles usuarios.

![image](https://github.com/user-attachments/assets/3916b5dc-a215-4803-af34-1c3f548bd44b)

Hacemos uso otra vez de la herramienta netexec, pero ahora buscando el usuario correcto, para la contraseña que tenemos.

Tendremos que añadir "--continue-on-success", para que no me muestre un error cuando la contraseña es correcta.

![image](https://github.com/user-attachments/assets/68b84242-714c-4030-942c-381b70543589)

Haciendo uso de la herramienta enum4linux no encontramos nada, pero hay una herramienta muy parecida a esta pero mas actualizada que se llama enum4linux-ng, en ella vemos un usuario y una contraseña.

Usuario: david.orelious    Password: aRt$Lp#7t*VQ!3

![image](https://github.com/user-attachments/assets/dc9e5ccc-d83e-4df4-83d2-92d2f3b2493b)

![image](https://github.com/user-attachments/assets/1cb5877f-eb65-40d7-b91d-8577430c1f5c)

Hacemos un nmap con las credenciales obtenidas para ver a que archivos compartidos podemos entrar.

![image](https://github.com/user-attachments/assets/7fea20e5-611b-4ce3-a667-c60c24007e07)

Nos metemos en el /DEV, y vemos esto: 

![image](https://github.com/user-attachments/assets/de96ffb2-709b-40bf-9678-f3883447ac95)

Nos lo pasamos a nuestra máquina y lo abrimos.

Usuario: emily.oscars  Password: Q!3@Lp#M6b*7t*Vt

![image](https://github.com/user-attachments/assets/2706a269-a0bd-4f3b-94ec-f04d225939fb)

Nos conectamos al servicio evil-winrm con las credenciales obtenidas, ya que tenemos el puerto 5985 abierto.

![image](https://github.com/user-attachments/assets/f02ffefd-dd53-4785-abd1-f538c02d9dee)

## SUBMIT USER FLAG

Encontramos la primera flag, la del user.

![image](https://github.com/user-attachments/assets/6b246337-8743-4e95-ae37-7a30d6af99c0)

![image](https://github.com/user-attachments/assets/062c3357-76b6-4fb4-983e-5dce758a0470)

## SUBMIT ROOT FLAG

Miramos sobre que tengo privilegios.

![image](https://github.com/user-attachments/assets/f8dca8bb-c444-4a5f-8783-f443c8345032)

Y seguidamente voy a extraer la base de datos SAM para extraer los hashes NTLM/NTHash que estan almacenadas en el sistema: 

![image](https://github.com/user-attachments/assets/8e21e8d3-63f2-4d57-b1ae-8793f6589875)

![image](https://github.com/user-attachments/assets/fbf05632-d529-4938-bc6a-91cd67d6d535)

Nos conectamos como administrator con las credenciales conseguidas y conseguimos la segunda flag, la del root.

![image](https://github.com/user-attachments/assets/f27796db-4750-4d98-8477-e405410b2b13)

![image](https://github.com/user-attachments/assets/9bf37177-e2e5-4554-8bd3-3540c15f538b)

