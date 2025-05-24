# ☠️ ARP-Poisoning
### **Laboratorio: Simulación de Ataque MiTM con ARP Poisining en Ettercap**


## 🎯 Objetivo
Comprender cómo funciona un ataque de MiTM y observar sus efectos en una red local, utilizando herramientas básicas de Kali Linux.

## 📋 Requisitos
-	Kali Linux (máquina atacante)
-	Windows (máquina víctima)
-	Metasploitable (máquina víctima)
-	Todas las máquinas conectadas a la misma red local (puede ser una red virtual como en VirtualBox o VMware)

## 🔧Herramientas
-	Ettercap (incluida en Kali)
-	Wireshark (opcional, para análisis de tráfico)
-	Browser: Para navegación web desde Windows

## ☑ Actividades a realizar en el Laboratorio
### 1-Configuración de red.
Verifica que todas las máquinas a utilizar estén en la misma red:
- En Kali y Metasploitable: `ip a` o `ifconfig`
- En Windows: `ipconfig`

Anota las IPs de:
- Kali Linux *(ej. 192.168.62.141)*
- Windows *(ej. 192.168.62.145)*
- Metasploitable *(ej. 192.168.62.136)*

### 2-Realizar comunicación HTTP desde Windows.
El equipo Metasploitable viene habilitado el servicio HTTP, por lo que dispone de un pequeño sitio web, para instancias de pruebas.
Desde Windows, a través de un navegador ingresa la dirección IP del equipo Metasploitable *(ej. 192.168.62.136)*

![image](https://github.com/user-attachments/assets/f1cf062e-4038-438f-8a85-f924a9540653)
![image](https://github.com/user-attachments/assets/eba21a05-5b58-4e69-b88a-ee4f43e6081f)

Intente acceder al sitio, puede intentar con usuario: admin y password: admin.

Abre Wireshark en Kali Linux, elije la interfaz `eth0` o la que este disponible en su sistema y que esta se encuentre habilitada:

![image](https://github.com/user-attachments/assets/b92315c6-1a24-4345-a833-ebcbf08b2195)
![image](https://github.com/user-attachments/assets/151da619-0ffd-416d-9b2f-ab37bb4818e8)


Cabe destacar que Wireshark es una herramienta que actúa como un “sniffer” de todos los paquetes que en este caso nuestra maquina linux logre detectar.
Podemos aplicar un filtro por `http` para validar si se evidencia tráfico web:

![image](https://github.com/user-attachments/assets/26c44a95-7804-4248-a070-b37044e2e065)

No se tiene evidencia de trafico http, aún teniendo la conexión entre el equipo Windows y la pagina alojada en Metasploitable.


### 3-Ejecutar ataque MiTm a través ARP Poisining desde Kali.
Abra la herramienta Ettercap en Kali Linux:
- Primero abrimos una terminal en Kali 
- Luego ejecutamos el commando `Ettercap -G`

![image](https://github.com/user-attachments/assets/58de8260-aa7c-453f-8c46-5f8b921105bd)
![image](https://github.com/user-attachments/assets/29db702a-758e-4eb0-8303-83e309c848b7)

Se despliega la herramienta Ettercap, en modalidad gráfica. A través de esta herramienta realizaremos nuestro ataque MiTm ejecutando un ARP Poisining.
Le damos un clic en el icono “check”, tal como se muestra en la imagen:

![image](https://github.com/user-attachments/assets/0bf7558f-5335-4b49-af41-cf2a3f6b5948)

Luego debemos verificar los hosts que esten presentes en nuestra red, por lo que debemos de desplegar el menu en la opción de “los tres puntos”, tal como se muestra en la imagen:

![image](https://github.com/user-attachments/assets/bce4945d-255a-491b-87e4-d6f08057a13e)

Luego elegimos la opción `Hosts` y a continuación la opción `Host list`

![image](https://github.com/user-attachments/assets/dd137f08-0c66-4ab0-9367-232099d0ace9)

Debiese desplegarse el listado con los hosts presentes en nuestra red. Si no llega a desplegarse el listado de hosts, se debe elegir la opción `Scan for hosts`, de modo que se muestren los hosts correspondientes.

Debemos identificar tanto la máquina Windows, como el Webserver (Mestasploitable) de modo que las etiquetemos como nuestras maquinas “Target”.
Seleccionamos por ejemplo la máquina Metasploitable y la agregamos como el target 1, por tanto teniendo seleccionada la máquina en el listado, damos clic en el botón `Add to Target 1`.

![image](https://github.com/user-attachments/assets/6e190713-087c-4ea1-9913-c17da6fa8636)

Evidenciamos que en los registros con los detalles de acción de Ettercap, ya ha quedado clasificada como TARGET1.
Realizamos la misma acción, pero con la maquina Windows y le indicamos a Ettercap que sera el Target 2.

![image](https://github.com/user-attachments/assets/880ab7fc-b7d8-4546-a27c-fc9df2e74916)

Luego debemos elegir el tipo de ataque a ejecutar, que para este caso será el de ARP Poisoning:

![image](https://github.com/user-attachments/assets/4c2d58c4-841b-447a-a0dc-ab79c760b8ff)
![image](https://github.com/user-attachments/assets/e60a4f96-0194-422e-821e-9333f95a767c)

### 4-Observar el tráfico.
Abre nuevamente el navegador web en el equipo Windows, intenta ingresar nuevamente a la pagina alojada en Metasploitable.
Abre Wireshark en Kali y filtra por `http`

![image](https://github.com/user-attachments/assets/718d4685-6922-439d-8a77-81ed1126cae7)

Ahora ya se logra evidenciar que se captura tráfico http entre el equipo Windows y el Webserver de Mestasploitable.

![image](https://github.com/user-attachments/assets/00f739ef-821e-4fc6-9b7b-8f8402101822)

Podemos evidenciar incluso el intento de sesión y la captura de las credenciales de acceso al sitio web:

![image](https://github.com/user-attachments/assets/ce45af8a-0f36-4de6-a118-87013f53ab81)



















