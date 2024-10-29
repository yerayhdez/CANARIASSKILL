# Plan de Pruebas

Este documento describe los pasos para la configuración y prueba de las máquinas virtuales en el entorno de red.

## 1. Configuración de Red
- Las máquinas virtuales deben configurarse en modo "Red interna".
- La máquina de Ubuntu Firewall se usará como enrutador para conectarse con la red real del equipo participante.

## 2. Nombres de las Máquinas
Los nombres de las máquinas están especificados en el Anexo I: Topología de la Red.

## 3. Direccionamiento de Red
El direccionamiento IP se encuentra en el Anexo II: Direccionamiento.

## 4. Configuración de la Máquina Virtual 1: Windows Server
1. Configura un controlador de dominio para `canariasskills.edu`.
2. Habilita el servicio DHCP para el rango de direcciones de red `10.0.0.40/24` a `10.0.0.240/24`.
3. Crea una unidad organizativa llamada **Usuarios** y añade dos usuarios de dominio:
   - Usuario: tu nombre completo de participante, Contraseña: `P@rticipante`
   - Usuario específico para el servidor web: `web`, Contraseña: `Serv1dor`
4. Configura mediante GPO una directiva para que los usuarios del dominio de Windows no puedan acceder al **Panel de Control**.

## 5. Configuración de la Máquina Windows 10
1. Cambia el nombre de la máquina a `Cliente1`.
2. Configura la red mediante DHCP.
3. Une el equipo al dominio AD de Windows.
4. Inicia sesión con el usuario del dominio creado anteriormente.
5. Verifica que el usuario no tenga acceso al **Panel de Control**.

## 6. Configuración de la Máquina Ubuntu Servidor Web
1. Une el equipo al dominio AD de Windows.
2. Configura la red de manera estática según las direcciones del Anexo II.
3. Instala el servidor web **Apache2**.
4. Modifica la página web para que muestre tu nombre de participante.

## 7. Configuración de la Máquina Ubuntu Firewall (iptables)
1. Configura dos tarjetas de red: una para la red local y otra para la red real, usando las IP especificadas en el Anexo II.
2. Configura el equipo para que permita el enrutamiento entre las interfaces de red.
3. Establece las políticas de filtrado por defecto en `DROP` y configura las reglas de `INPUT`, `OUTPUT`, y `FORWARD` según los siguientes requisitos:
   - Todas las máquinas de la red local deben poder navegar por Internet.
   - No se puede hacer ping al firewall desde ningún equipo de la red local ni desde el equipo del competidor.
   - El PC del competidor debe poder acceder a la página web del servidor web.

---
