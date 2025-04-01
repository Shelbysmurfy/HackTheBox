# RESOLUCIÓN DE LA MÁQUINA ADMINISTRATOR

Abrimos la máquina y vemos su IP.

![image](https://github.com/user-attachments/assets/2a07e988-f296-4a0d-a38d-0b84a7ea8a66)

También nos dan unas credenciales válidas de inicio "Olivia:ichliebedich".

![image](https://github.com/user-attachments/assets/9912c488-92ab-4d77-be82-80eb76f90b39)

Hacemos un nmap para poder ver los puertos que estan abiertos para saber servicios,versiones...

![image](https://github.com/user-attachments/assets/74a7a697-26ab-4f50-9597-2f310a4da437)

Vamos a usar la herramienta crackmapexec para autenticarnos em SMB con las credenciales que tenemos, y si la autentificación es exitosa, ejecutar un ataque " RID Brute-Force" para descubrir otros usuarios válidos en el dominio. Po último filtraremos la salida con "grep SidTypeUser", para solo ver las ususarios encontrados.

![image](https://github.com/user-attachments/assets/584c90e3-4779-43db-8642-33d623a8265c)

Tenemos una lista de los usuarios existentes en el sistema, pero aún no se conoce la relación entre ellos y su acceso. Para ello vamos a usar BloodHound.

![image](https://github.com/user-attachments/assets/fcb3ee29-7133-41a5-9fcc-9f0b6a034541)

Entramos en la herramienta bloodhound, y importamos todos los archivos.json

![image](https://github.com/user-attachments/assets/3145c442-e48d-4c1a-b6cd-1609505ce0bf)

Una vez dentro buscamos al usuario olivia desde la barra de búsqueda y vamos al apartado "OUTBOUND OBJECT CONTROL", para ver si tiene permisos sobre otros usuarios.

![image](https://github.com/user-attachments/assets/ba1723af-d25a-4e40-b589-8fc17ab8d06d)

Una vez encontrado que el usuario olivia tiene permisos sobre el usuario michael, vamos a ver si este también los tiene sobre otro usuario.

![image](https://github.com/user-attachments/assets/0945725e-7a66-4d08-94b8-d7574d556626)

Y encontramos que el usuario michael tiene permisos sobre el usuario benjamin, pero si intentamos hacer lo mismo vemos que ya no hay mas usuarios con los que escalar privilegios.

Ahora vamos a hacer uso de la herramienta "bloodyAD" para desde el usuario Olivia indicar la contraseña que va a tener el usuario michael.

![image](https://github.com/user-attachments/assets/84ce7afa-6153-49b9-ad7e-8b283f54a19f)

Y ahora desde el usuario michael indicar la contraseña de benjamin.

![image](https://github.com/user-attachments/assets/80b82aee-8d9c-4e74-b4ff-b00a18978685)

Una vez obtenido las credenciales de benjamin podemos conectarnos al servicio ftp con estas.

![image](https://github.com/user-attachments/assets/873f39b1-e997-467d-ad38-837adbc81ce0)

Hacemos ls y vemos un archivo.psafe3, nos lo traemos a nuestra máquina.

![image](https://github.com/user-attachments/assets/7af92319-7df1-42e3-b6c6-471fff7fae0a)

Craqueamos la contraseña del archivo con hashcat.

![image](https://github.com/user-attachments/assets/56781f25-d4d2-4c6a-98cd-2c6b8b59cc68)
![image](https://github.com/user-attachments/assets/6f3d20cb-c63f-46aa-9886-e58cb07aa0b3)

Abrimos el archivo con "passwordsafe" y la credencial obtenida "tekieromucho".

![image](https://github.com/user-attachments/assets/8d80b84a-1bcf-4d7d-8726-cb3262b950f4)

Una vez dentro le damos click derecho a cada usuario y copiamos los usuarios y contraseñas de estos en un archivo.txt

![image](https://github.com/user-attachments/assets/11492e17-b0de-4811-8fbf-df18fe23b407)

Probamos cada una de ellas para el servicio evil-winrm, y ganamos acceso con las credenciales "emily:UXLCI5iETUsIBoFVTj8yQFKoHjXmb".

![image](https://github.com/user-attachments/assets/07055a98-6532-4aaa-ae0a-9a876224d2a8)

Vamos al directorio /Desktop y encontramos la primera flag, la del usuario.

![image](https://github.com/user-attachments/assets/05e606ac-878a-47c6-8362-236af6836ab8)

## SUBMIT USER FLAG

![image](https://github.com/user-attachments/assets/70f06088-99c2-4ea4-9a50-ef5041bfebbf)

Encontramos que el usuario emily tiene el permiso GenericWrite sobre el usuario Ethan, este es un nivel de permiso en Active Directory (AD) que permite a un usuario o grupo modificar casi todos los atributos de un objeto, sin tener control administrativo completo sobre dicho objeto.

![image](https://github.com/user-attachments/assets/0a105b9a-da27-4af7-9a4f-31fcdeccb74c)

Como se puede ver en este gráfico útil, este permiso se puede explotar mediante Kerberoasting.

![image](https://github.com/user-attachments/assets/79858271-5b43-4023-b4b9-a40762d60fef)

Debido a los permisos de Emliy sobre Ethan, se puede utilizar un ataque Kerberoasting dirigido, para ello vamos a traernos un repositorio de github.

Github: https://github.com/ShutdownRepo/targetedKerberoast

![image](https://github.com/user-attachments/assets/a79e4952-b3a8-4b6d-a175-e040388d6ba8)

Cuando lo ejecutaba me daba el error "KRB_AP_ERR_SKEW (Clock skew too great)", que significa que hay una diferencia de tiempo entre tu máquina (Kali Linux) y el Controlador de Dominio (DC) de administrator.htb.

Para ello hay que utilizar estos dos comandos: 

![image](https://github.com/user-attachments/assets/2818b524-a359-4c04-835a-5301b4924f85)

Y seguidamente si ejecutamos el archivo.py junto con las credenciales y el dominio obtenemos resultado.

![image](https://github.com/user-attachments/assets/1fe8fe39-6236-4c3a-a2e4-867c2010f594)

Guardamos el hash en un archivo.txt, lo craqueamos con john the ripper y obtenemos la contraseña de ethan "limpbizkit".

![image](https://github.com/user-attachments/assets/4719a8dc-1cf6-4a1d-b1f0-47b8adf811ec)

Teniendo esta credencial volvemos a la herramienta "bloodhount", miramos sobre quien tiene permisos ethan y vemos esto: 

![image](https://github.com/user-attachments/assets/f5972909-5875-446c-8fb9-9260381940ac)

Tenemos la combinación de GetChanges y GetChangesAll. La combinación de estos dos permisos nos otorga la capacidad de realizar un ataque DCSync.

Para ello tendremos que ejecutar la herramienta secretdump.py

Github: https://github.com/fin3ss3g0d/secretsdump.py

![image](https://github.com/user-attachments/assets/11776bdc-7d83-44cf-84da-1155676da04a)

Esta herramienta, primero se conecta de forma remota al controlador de dominio a través de smbexec o wmiexec utilizando las credenciales de inicio de sesión de usuario proporcionadas y obtiene altos privilegios, luego exporta el hash de la cuenta local desde el registro y, al mismo tiempo, exportar los hashes de todos los usuarios del dominio a través de Dcsync o desde el archivo NTDS.dit. Su mayor ventaja es que admite la conexión a controladores de dominio desde computadoras fuera del dominio.

![image](https://github.com/user-attachments/assets/9af8f5dd-9296-4a5d-9ebe-0a772a6ef5cc)
![image](https://github.com/user-attachments/assets/aa78e836-ab24-4f26-bd5a-d2029813b3c9)

He obtenido el hash NTLM del usuario Administrator.

![image](https://github.com/user-attachments/assets/11c13c73-d345-426c-b308-64e3d0de502b)

Usamos la herramienta evil-winrm para conectarnos al servidor con las credenciales obtenidas "Administrator:3dc553ce4b9fd20bd016e098d2d2fd2e".

![image](https://github.com/user-attachments/assets/cff40c42-b265-4b92-a543-5d32fde6d420)

Vamos al directorio /Desktop y encontramos la segunda flag, la del usuario root.

![image](https://github.com/user-attachments/assets/ab6d175c-dd45-44c2-84ee-ceefbab2ab69)

## SUBMIT ROOT FLAG

![image](https://github.com/user-attachments/assets/4f574eef-3f70-4a75-a238-d215671a9e4b)
