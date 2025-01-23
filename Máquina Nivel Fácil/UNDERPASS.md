# RESOLUCIÓN DE LA MÁQUINA UNDERPASS

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/0faeffa1-175e-442b-94cc-3ead92c1c1e3)

Hacemos un nmap para poder ver los puertos que estan abiertos para la IP seleccionada.

![image](https://github.com/user-attachments/assets/ae3e5261-2d5d-413e-a66b-eee752c3ae5d)

Ahora hacemos un escaneo de los puertos que hemos visto que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/39d63f27-2bf7-466c-bce4-1ff5de93b604)

Abrimos la web.

![image](https://github.com/user-attachments/assets/c67df07c-7ff9-4b21-96e8-5c9cf00a1986)

Hacemos fuerza bruta con gobuster y no encontramos nada.

![image](https://github.com/user-attachments/assets/d71a9d90-2250-4573-ad37-2781b9179f94)

Hacemos una enumeración para encontrar posibles puertos UDP abiertos y vemos esto: 

![image](https://github.com/user-attachments/assets/8f588dc1-3c41-4fc0-9cfd-ccf97b0db62e)

Hacemos un snmpwalk, ya que es el tipo de servicio que hay en el puerto 161 (UDP).

![image](https://github.com/user-attachments/assets/34509378-f749-4b26-8b0d-661a812370fb)

En el encontramos "daloradius server", que al parecer es una aplicación de gestión web para gestionar puntos de acceso.

![image](https://github.com/user-attachments/assets/d1f70681-7cc1-43af-8424-9387821ef3cc)

También encontramos el dominio "underpass.htb", que lo pondremos en nuestro /etc/hosts, para poder tener acceso.

![image](https://github.com/user-attachments/assets/fbeced47-fe5a-41d7-affb-27c018a238d6)

![image](https://github.com/user-attachments/assets/881ac612-7fa9-4389-a51e-b9705682a27e)

Sabiendo que hay un posible aplicación de gestión de web, la añadiremos a nuestra url.

![image](https://github.com/user-attachments/assets/32846429-bee4-4b00-8754-580dd0448428)

Al no mostrarnos nada haremos uso de la herramienta dirsearch para ver posibles directorios activos.

![image](https://github.com/user-attachments/assets/809fc4ff-baa9-4c7f-80a2-b94bb779be12)

Como sigue sin mostrarnos nada haremos otro dirsearch pero añadiendo a la ruta /app.

![image](https://github.com/user-attachments/assets/15aaa782-c975-4a57-a43b-abb1dcf04d5c)

Encontramos una ruta de un login.

![image](https://github.com/user-attachments/assets/5423b89f-0306-4e7e-b416-ae553e6a3104)

En ella usaremos unas credenciales default, que hemos encontrado en el proyecto de github que estaba mirando antes.

![image](https://github.com/user-attachments/assets/7ebe8d61-0ff2-4886-a474-b0199365da5d)

Pero no funciona.

![image](https://github.com/user-attachments/assets/55dd5ad4-9550-4750-85c1-c25afbedd868)

Haciendo uso de la herramienta gobuster, encontramos una ruta diferente que también contiene un login.

![image](https://github.com/user-attachments/assets/7f842974-d44e-4967-ab17-79664e2b51f9)

![image](https://github.com/user-attachments/assets/cd306ec5-de50-45aa-aa45-ab7603549556)

Probamos las credenciales default que habíamos mencionado antes y ganamos acceso.

![image](https://github.com/user-attachments/assets/19d715e3-8821-4a22-93db-49f239ac5092)

Nos vamos al apartado de users, y encontramos un usuario con la password crackeada.

![image](https://github.com/user-attachments/assets/05817ce3-2b9b-42d6-95da-7e57958dd151)

Usamos la herramienta crackstation para descifrarla.

![image](https://github.com/user-attachments/assets/6f14d7f2-7419-46f0-85dc-9ae5df719977)

Nos conectamos al servicio ssh con las credenciales obtenidas.

![image](https://github.com/user-attachments/assets/5323df31-1fb2-4a74-86fe-c0af76d53c87)

### SUBMIT USER FLAG

En el directorio /home/svcMosh, encontramos la flag del user.

![image](https://github.com/user-attachments/assets/21a915f8-9468-430a-9afb-98fa906404a0)

![image](https://github.com/user-attachments/assets/876c09c7-5fc9-46e9-9290-c42c2c863b3c)

### SUBMIT ROOT FLAG

Hacemos sudo -l y vemos esto: 

![image](https://github.com/user-attachments/assets/6d51813f-0957-4acf-a979-5fbadfd5ad2c)

Ejecutamos el comando: "mosh --server="sudo /usr/bin/mosh-server" localhost", para ganar acceso como root.

![image](https://github.com/user-attachments/assets/595c050c-c8fc-4ee1-aa41-f04e59ececc0)

Y ya somos root.

![image](https://github.com/user-attachments/assets/99c27875-8baa-4eab-a05b-235947978b2e)




