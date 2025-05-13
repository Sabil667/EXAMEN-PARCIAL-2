# EXAMEN-PARCIAL-2
Link de mi repositorio: https://github.com/Sabil667/EXAMEN-PARCIAL-2.git

## Misión 1: Reconexión en la Base Eco (Hoth) – Direccionamiento IP y Subredes

Para restaurar la comunicación en la Base Eco de Hoth y conectar todos sus departamentos con la antena principal, partimos del bloque de red asignado `172.16.0.0/24`, que ofrece 256 direcciones IP totales (254 útiles). Dado que cada sector requiere su propia subred y el espacio IP es limitado, aplicaremos subnetting con VLSM (Variable Length Subnet Masking) para optimizar el uso de direcciones.

### Plan de Subredes

| Departamento            | Hosts necesarios | Subred asignada  | Máscara CIDR         | IP de red      | Rango de hosts              | Broadcast         | Hosts útiles |
|-------------------------|------------------|------------------|-----------------------|----------------|-----------------------------|-------------------|--------------|
| Comando Central         | ~50              | 172.16.0.0/26    | /26 (255.255.255.192) | 172.16.0.0     | 172.16.0.1 – 172.16.0.62    | 172.16.0.63       | 62           |
| Defensa Perimetral      | ~30              | 172.16.0.64/27   | /27 (255.255.255.224) | 172.16.0.64    | 172.16.0.65 – 172.16.0.94   | 172.16.0.95       | 30           |
| Centro Médico           | ~20              | 172.16.0.96/27   | /27 (255.255.255.224) | 172.16.0.96    | 172.16.0.97 – 172.16.0.126  | 172.16.0.127      | 30           |
| Hangar y Taller         | ~14              | 172.16.0.128/28  | /28 (255.255.255.240) | 172.16.0.128   | 172.16.0.129 – 172.16.0.142 | 172.16.0.143      | 14           |
| Enlace troncal (antena) | 2                | 172.16.0.144/30  | /30 (255.255.255.252) | 172.16.0.144   | 172.16.0.145 – 172.16.0.146 | 172.16.0.147      | 2            |

- 🔹 Total de direcciones utilizadas: 64 + 32 + 32 + 16 + 4 = 148
- 🔹 Total de direcciones IP útiles: 138
- 🔹 Bloque aún disponible para expansión futura: 172.16.0.148 – 172.16.0.255

### Subred destinada al enlace troncal con la antena

- Subred: `172.16.0.144/30`
- Ideal para enlaces punto a punto (2 hosts útiles)

### ✅ Conclusión

La red `172.16.0.0/24` se ha dividido cuidadosamente usando subnetting con máscaras variables para satisfacer los requerimientos específicos de cada departamento en Hoth. Se ha optimizado el espacio IP evitando desperdicio de direcciones, se ha reservado una subred exclusiva para el enlace interplanetario, y se ha dejado espacio para futuras ampliaciones. Esta estrategia garantiza eficiencia, seguridad por segmentación y compatibilidad con el crecimiento de la red rebelde.
