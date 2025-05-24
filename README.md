# ARP-Poisining
Laboratorio: Simulación de Ataque MiTM con ARP Poisining en Ettercap

## Objetivo
Comprender cómo funciona un ataque de MiTM y observar sus efectos en una red local, utilizando herramientas básicas de Kali Linux.

# Requisitos:
-	Kali Linux (máquina atacante)
-	Windows (máquina víctima)
-	Metasploitable (máquina víctima)
-	Todas las máquinas conectadas a la misma red local (puede ser una red virtual como en VirtualBox o VMware)

## Herramientas:
-	Ettercap (incluida en Kali)
-	Wireshark (opcional, para análisis de tráfico)
-	Navegación web desde Windows

## Actividades a realizar en el Laboratorio:
### 1. Configuración de red
Verifica que todas las máquinas a utilizar estén en la misma red:
- En Kali y Metasploitable: `ip a` o `ifconfig`
- En Windows: `ipconfig`

Anota las IPs de:
- Kali Linux (ej. 192.168.62.141)
- Windows (ej. 192.168.62.145)
- Metasploitable (ej. 192.168.62.136)
