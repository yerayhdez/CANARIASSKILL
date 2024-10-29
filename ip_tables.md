# Script para configurar iptables en el Firewall de Ubuntu

## Limpiar reglas existentes
```bash
iptables -F        # Eliminar todas las reglas
iptables -X        # Eliminar cadenas personalizadas
iptables -t nat -F # Eliminar reglas NAT
```

# Políticas por defecto
```
iptables -P INPUT DROP    # Denegar todo el tráfico de entrada
iptables -P FORWARD DROP  # Denegar todo el tráfico de reenvío
iptables -P OUTPUT ACCEPT  # Permitir todo el tráfico de salida
```
# Permitir tráfico en la interfaz de bucle (localhost)
```
iptables -A INPUT -i lo -j ACCEPT
```
# Permitir tráfico de entrada del servidor web
```
iptables -A INPUT -p tcp --dport 80 -j ACCEPT # HTTP
iptables -A INPUT -p tcp --dport 443 -j ACCEPT # HTTPS
```
# Permitir tráfico SSH (opcional, si necesitas acceder por SSH al firewall)
```
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
# Permitir tráfico de la red local hacia el servidor web
```
iptables -A INPUT -s 10.0.0.0/24 -p tcp --dport 80 -j ACCEPT
```
# Permitir tráfico de salida hacia la red local
```
iptables -A FORWARD -i eth0 -o eth1 -j ACCEPT # Permitir tráfico desde la red local a la red externa
iptables -A FORWARD -i eth1 -o eth0 -m state --state ESTABLISHED,RELATED -j ACCEPT # Permitir tráfico de respuesta
```
# No permitir ping al firewall desde la red local
```
iptables -A INPUT -p icmp -j DROP
```
# Guardar las reglas
```
iptables-save > /etc/iptables/rules.v4
```
