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



## Misión 2: Sabiduría de Yoda – Algoritmos de Enrutamiento y Rutas

En la galaxia de las redes, como en la Fuerza, existen dos caminos para guiar los paquetes hacia su destino: el enrutamiento estático y el enrutamiento dinámico. Ambos permiten que la información circule por la HoloRed, pero sus filosofías de funcionamiento y aplicación son muy distintas.

### 🔹 Enrutamiento Estático

El enrutamiento estático consiste en configurar manualmente las rutas en los routers.

**Ventajas:**

- Mayor control sobre la ruta de los paquetes.
- Bajo consumo de CPU/RAM.
- Más seguro (no comparte información con otros routers).

**Desventajas:**

- No se adapta automáticamente a fallos.
- Difícil de mantener en redes grandes.
- Susceptible a errores humanos.

Ejemplo: una base rebelde con un único enlace a la flota.

---

### 🔹 Enrutamiento Dinámico

Usa protocolos para intercambiar información de rutas automáticamente.

**Ventajas:**

- Se adapta automáticamente a fallos y cambios.
- Fácil de mantener en redes grandes.
- Alta escalabilidad.

**Desventajas:**

- Requiere más CPU/RAM.
- Posible convergencia lenta en algunos casos.
- Configuración inicial más compleja.

Ejemplo: una red rebelde interplanetaria con muchas rutas posibles.

---

### 📘 Tipos de protocolos dinámicos

| Tipo                 | Ejemplo | Características principales                                               |
|----------------------|---------|----------------------------------------------------------------------------|
| Vector de Distancia  | RIP     | Basado en número de saltos, envía tabla completa periódicamente.           |
| Estado de Enlace     | OSPF    | Conoce toda la red, calcula rutas óptimas con Dijkstra. Convergencia rápida.|

---

### 🌌 Conclusión

El enrutamiento estático es como un Jedi calculando cada movimiento con precisión; el dinámico es como fluir con la Fuerza, adaptándose al cambio. Saber cuándo usar cada uno es esencial para que la red rebelde sobreviva.


## Misión 3: Los Nombres del Holonet – DNS y Resolución de Nombres

El DNS (Domain Name System) es el sistema que permite a las redes convertir nombres simbólicos (como `echo.base`) en direcciones IP comprensibles por las máquinas (como `192.168.50.100`). Sin él, la comunicación se vuelve compleja y propensa a errores, como tratar de encontrar un Ewok en la noche de Endor.

### 🔹 ¿Cómo funciona el DNS?

1. Un dispositivo (PC, terminal, servidor) solicita resolver un nombre de dominio.
2. El servidor DNS local revisa su base de datos.
3. Si tiene el registro, responde con la IP asociada.
4. El dispositivo usa esa IP para establecer la conexión.

### 🔹 ¿Qué es un servidor DNS?

Es un equipo configurado para almacenar registros de nombres y responder a las solicitudes de resolución. Puede ser local o público.

### 🔹 ¿Qué es un registro A?

Es el tipo de registro DNS más común. Asocia un nombre con una dirección IPv4.

Ejemplo:

- Dominio: `holonet.rebelion.org`
- Registro A → `192.168.100.200`

Esto indica que cualquier equipo que use ese nombre se conectará a la IP correspondiente.

### 🔹 ¿Qué pasa si el DNS falla?

- Los nombres no pueden resolverse.
- Servicios como web, correo o SSH por nombre fallan.
- Solo podrías acceder a recursos si conoces su IP exacta.

🛡️ Conclusión: El DNS es esencial para que los sistemas rebeldes puedan comunicarse eficientemente. Sin él, la coordinación de las bases y flotas sería prácticamente imposible.


## Misión 4: “Es una trampa… de protocolos!” – TCP vs UDP en las transmisiones

Durante la batalla sobre Endor, Luke Skywalker nota diferencias en las transmisiones de datos: algunas son rápidas pero pueden perder información, mientras que otras tardan más pero llegan completas y en orden. Esta diferencia se debe al uso de los dos principales protocolos de transporte en redes TCP/IP: TCP y UDP.

### 🔹 TCP (Transmission Control Protocol)

TCP es un protocolo confiable y orientado a conexión. Antes de enviar datos, establece una conexión entre origen y destino mediante un proceso llamado “three-way handshake”. Garantiza que:

- Los datos lleguen íntegros y en el mismo orden en que fueron enviados.
- Se retransmitan los paquetes perdidos.
- Se controle el flujo y la congestión.

🟢 Ventajas:

- Fiabilidad total en la transmisión.
- Corrección de errores automática.
- Ideal para transferencias de archivos y comunicaciones críticas.

🔴 Desventajas:

- Mayor retardo (latencia) debido a los mecanismos de control.
- Más consumo de recursos (encabezados más grandes, seguimiento de estados).

🛠️ Ejemplo galáctico:

- Transferencia de los planos de la Estrella de la Muerte desde una base rebelde a la flota.
- Administración remota de routers mediante SSH.
- Descarga segura de datos tácticos.

---

### 🔹 UDP (User Datagram Protocol)

UDP es un protocolo no confiable y sin conexión. No establece ningún tipo de negociación previa entre emisor y receptor. Los datos se envían directamente como “datagramas” y no hay confirmación de recepción.

🟢 Ventajas:

- Muy rápido y con menor sobrecarga.
- Ideal para transmisiones en tiempo real donde la velocidad es prioritaria.

🔴 Desventajas:

- No hay garantía de entrega ni de orden.
- No hay corrección de errores ni control de congestión.

🛠️ Ejemplo galáctico:

- Stream de vídeo desde una cámara en un X-Wing durante un combate.
- Transmisión de coordenadas de combate a cazas en tiempo real.
- Audio en tiempo real entre bases durante operaciones encubiertas.

---

### 🌌 Conclusión

TCP y UDP son como dos naves diferentes:

- TCP es como una nave diplomática de la República: lenta pero segura, siempre entrega el mensaje correctamente.
- UDP es como el Halcón Milenario: veloz, directo, pero puede perder algo en el camino.

Ambos son necesarios en la red rebelde, dependiendo de si se necesita garantizar la entrega (TCP) o reaccionar con rapidez ante el enemigo (UDP).


## Misión 5: Comunicación Segura o lado oscuro – Criptografía y Seguridad de la Red

La seguridad de las comunicaciones rebeldes es fundamental para evitar que los mensajes caigan en manos del Imperio. Para proteger la información transmitida entre bases y agentes, se utiliza la criptografía: el arte de cifrar los datos de forma que solo los destinatarios autorizados puedan entenderlos.

### 🔹 Tipos de cifrado: Simétrico vs Asimétrico

#### ✅ Cifrado simétrico

- Utiliza la misma clave para cifrar y descifrar el mensaje.
- Requiere que ambas partes (emisor y receptor) conozcan y protejan esta clave previamente.
- Es rápido y eficiente en procesamiento.

🛠️ Ejemplo rebelde:
- Leia y Luke comparten una frase secreta como “endor42” para intercambiar mensajes cifrados. Ambos la conocen y pueden descifrar sus holomensajes. Esto es cifrado simétrico.

🔒 Ventaja:
- Rápido y con baja sobrecarga computacional.

⚠️ Desventaja:
- Dificultad para intercambiar la clave de forma segura si las partes aún no se conocen.

---

#### ✅ Cifrado asimétrico

- Utiliza un par de claves: una clave pública (que puede compartirse) y una clave privada (que se mantiene en secreto).
- Lo que se cifra con una clave solo puede descifrarse con la otra.
- Ideal para entornos donde no se puede intercambiar una clave previamente.

🛠️ Ejemplo rebelde:
- La Alianza quiere enviar un mensaje seguro a un nuevo aliado. El aliado publica su clave pública, y la Alianza usa esa clave para cifrar el mensaje. Solo el aliado podrá descifrarlo con su clave privada. Así, nadie más podrá leerlo, ni siquiera si es interceptado.

🔒 Ventaja:
- No requiere compartir claves secretas previamente.
- Permite firmar digitalmente los mensajes.

⚠️ Desventaja:
- Más lento y con mayor consumo de recursos que el cifrado simétrico.

---

### 🔐 Autenticación y No Repudio

Además de proteger la confidencialidad, la criptografía debe asegurar:

- 🆔 Autenticación: saber con certeza quién envió el mensaje.
- 📜 No repudio: el emisor no puede negar haberlo enviado.
  
Esto se logra mediante firmas digitales, que usan la clave privada del emisor para “firmar” el mensaje. Cualquiera puede verificar la firma con su clave pública.

🛠️ Ejemplo rebelde:
- Un mensaje firmado por la clave privada de Mon Mothma puede ser verificado por cualquier base aliada para confirmar su autenticidad.

---

### 🔧 Protocolos seguros: ¿Por qué usar SSH en lugar de Telnet?

Telnet transmite los datos (incluyendo contraseñas) en texto plano, lo que permite que cualquier espía imperial que intercepte el tráfico pueda leer la información.

SSH (Secure Shell), en cambio:

- Cifra toda la comunicación entre cliente y servidor.
- Usa criptografía asimétrica para establecer una sesión segura.
- Protege credenciales y comandos enviados.

🛠️ En la red rebelde:
- SSH es esencial para administrar remotamente routers y servidores sin que el Imperio pueda interceptar configuraciones sensibles.

---

### 🌌 Conclusión

La criptografía es la única barrera entre la libertad de la galaxia y el control del Imperio. Ya sea mediante claves compartidas entre rebeldes (cifrado simétrico) o intercambios seguros con aliados nuevos (asimétrico), proteger los mensajes es vital. Además, protocolos como SSH garantizan que incluso la administración de equipos sea segura y libre del ojo imperial.
