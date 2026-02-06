Desarrollar una aplicación Cliente-Servidor(múltiples clientes, es decir, con hilos). Tras establecer la comunicación:

AP1- El Servidor genera una Clave pública y privada RSA (Cifrado asimétrico). Guardará la clave privada en un directorio de claves privadas asimétricas.

AP2- El Servidor envía la clave pública RSA al cliente

AP3- El cliente guardará la clave pública en un directorio de claves públicas (asimétricas).

AP4- El cliente Generará una clave privada del algoritmo Chacha20 (Cifrado simétrico) y lo almacenará en un directorio de claves privadas simétricas.

AP5- El cliente cifrará la clave privada del algoritmo Chacha20 utilizando la clave pública RSA(del cifrado asimétrico). El resultado se lo enviará al Servidor.

AP6- El servidor guardará la clave en un directorio de claves privadas simétricas. Si todo es correcto, cifrará el mensaje "ESTUPENDO" utilizando la clave privada del cifrado simétrico(Chacha20). Enviará el texto resultante al Cliente.

AP7- El cliente descifrará el mensaje utilizando la clave privada del cifrado simétrico(Chacha20). Si el texto es "ESTUPENDO", permitirá escribir mensajes utilizando ese sistema de cifrado de ahora en adelante. Cada vez que el Servidor reciba uno de esos mensajes, le devolverá un "OK" también cifrado.

AP8- Cuando el cliente escriba "FIN", se borrarán las claves tanto en cliente como en servidor y se cerrará la conexión.

-------------------
Mejora: 
-El servidor tendrá una base de datos ejercicioCifrado.
-Dicha base de datos tendrá una tabla usuarios, con un nombre y una contraseña.
-Al establecer conexión el Cliente con el Servidor, este le enviará un menú: 
    1. Ya tengo cuenta
    2. Crear nueva cuenta
-Si pulsa 1, le pedirá usuario y contraseña. El usuario viajará sin cifrar, mientras que la contraseña irá cifrada. Puede interesar almacenar cada clave de cada usuario en el servidor con el nombre de dicho usuario.
-El servidor buscará las claves asociadas para desencriptar y comprobar si existe un usuario con esa contraseña en base de datos.
-El servidor 

-Si hubiera pulsado la opción 2, el Servidor hará lo del punto AP1 y AP2(provisionalmente se pondrá un nombre aleatorio al fichero de clave) y le pedirá en texto plano "Introduce usuario" 
-El cliente usará la clave pública recibida para cifrar el nombre de usuario y mandarlo.
-El servidor guardará el nombre de usuario provisionalmente y le mandará otro mensaje "Introduce la contraseña"
-El cliente usará la clave pública para cifrar la contraseña.
-El servidor guardará nombre y contraseña en base de datos.

Trabajar Cifrado Asimétrico - https://blog.alvarodeleon.com/encriptar-y-desencriptar-con-rsa-en-java/

Algoritmos simétricos de la clase Cipher en Java - https://docs.oracle.com/en/java/javase/21/docs/specs/security/standard-names.html
