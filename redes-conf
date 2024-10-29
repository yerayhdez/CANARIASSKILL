# Configuración de Red

## Máquinas Virtuales
- **Firewall**: Ubuntu con `iptables` configurado para filtrar tráfico.
- **Servidor Windows**: Actúa como controlador de dominio.
- **Cliente Windows**: Forma parte del dominio.
- **Servidor Web Ubuntu**: Alojamiento de página web accesible desde el exterior.

## Direccionamiento IP
| Máquina          | Dirección IP       | Rol                    |
|------------------|--------------------|------------------------|
| Windows Server   | 10.0.0.3           | Controlador de dominio |
| Windows Cliente  | DHCP (10.0.0.50)   | Cliente de dominio     |
| Ubuntu Web Server| 10.0.0.2           | Servidor Web           |
| Ubuntu DMZ       | 10.0.0.4           | DMZ                    |

## Reglas de Firewall
- **INPUT**: Permitir tráfico HTTP hacia el servidor web; bloquear ping desde la red local.
- **FORWARD**: Permitir que los clientes de la red local accedan a Internet.
- **OUTPUT**: Permitir acceso desde el servidor web a Internet para actualizaciones.
