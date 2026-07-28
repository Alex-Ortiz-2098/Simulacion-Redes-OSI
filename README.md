# Diseño y Simulación de Arquitecturas de Red (Modelos OSI y TCP/IP)

## 📌 Sobre el Proyecto
El presente proyecto tiene como objetivo el diseño, configuración y simulación de dos redes independientes (denominadas Red A y Red B) empleando el simulador Cisco Packet Tracer. El propósito principal es consolidar los conceptos fundamentales de las capas de Enlace y de Red de los modelos OSI y TCP/IP. 

A través de este entorno, se visualiza y analiza el comportamiento real del tráfico de red, el direccionamiento IP, el funcionamiento del protocolo ARP y el enrutamiento de paquetes entre distintas subredes.

## ⚙️ Metodología y Herramientas Utilizadas
El proyecto se llevó a cabo utilizando **Cisco Packet Tracer**. La implementación se dividió en las siguientes fases:
* **Cálculo de Subredes (Subnetting):** Se determinaron las máscaras de red óptimas para cubrir la cantidad de dispositivos necesarios dejando un margen de expansión del 50%, optimizando el uso de direcciones IP privadas.
* **Configuración de Dispositivos:** Se asignaron direcciones IP, máscaras de subred y gateways a PCs, switches, hubs y routers de frontera[cite: 2].
* **Simulación y Monitoreo:** Mediante la consola de comandos de las PCs (usando `ping` y `arp -a`) y la herramienta *Event List* del simulador, se analizó el flujo de paquetes (ICMP, ARP, TCP, HTTP) paso a paso.

---

## 🖥️ Arquitectura 1: Red A - Capa de Enlace y Protocolo ARP

**¿Qué hace?**
Busca analizar el funcionamiento de la capa de enlace, profundizando en el comportamiento del protocolo ARP, la actualización de las tablas de direcciones físicas y las diferencias en la gestión del tráfico entre dispositivos de interconexión.

![Topología Red A] <img width="991" height="425" alt="imagen" src="https://github.com/user-attachments/assets/82135a81-f11d-4913-b915-f2fd87f03099" />


**¿Cómo lo hace?**
* **Estructura:** Se diseñó una LAN interna bajo la red base 192.168.0.0/27 (soportando hasta 30 hosts) y una red externa bajo 212.198.20.192/29, ambas comunicadas a través de un router de frontera[cite: 2].
* **Resolución ARP:** Al ejecutar peticiones ICMP (Ping) entre dispositivos, se observó cómo los equipos emisores que desconocen la dirección MAC del destinatario generan solicitudes *ARP Request* (inundando la red) para obtener el *ARP Reply* y completar dinámicamente sus tablas ARP.
* **Dominios de Colisión (Switch vs. Hub):** Se contrastó el comportamiento de un hub (Capa 1), el cual reenvía tramas por todos sus puertos generando tráfico innecesario y colisiones, frente a un switch (Capa 2), que crea dominios de colisión separados y envía la información únicamente al puerto del dispositivo destino tras aprender su MAC.

---

## 🌐 Arquitectura 2: Red B - Capa de Red y Subnetting

**¿Qué hace?**
Se centra en la capa de Red, con el objetivo principal de realizar un subnetting eficiente y comprobar el enrutamiento de paquetes entre múltiples subredes internas y un servidor ubicado en una red externa.

![Topología Red B]<img width="876" height="372" alt="imagen" src="https://github.com/user-attachments/assets/17067041-5531-4bad-86ea-20155da32729" />


**¿Cómo lo hace?**
* **Estructura y Subnetting:** Se dividió una red mayor en múltiples subredes más pequeñas (con máscaras /23, /25, /26, /27 y /28) conectadas a diferentes interfaces de un mismo router[cite: 2]. Este router actúa como puente hacia una red externa donde se aloja un Servidor Web (145.12.13.2/24).
* **Enrutamiento de Paquetes (ICMP):** Se validó la comunicación entre equipos de diferentes subredes[cite: 2]. El proceso demostró cómo un paquete debe dirigirse primero a la dirección MAC del gateway (el router), el cual a su vez realiza su propio proceso ARP en la subred de destino para poder entregar el paquete final.
* **Análisis de Protocolos Superiores (TCP/HTTP):** Se simuló el acceso al servidor externo mediante un navegador web.
  * Se observó el protocolo **TCP** (Capa de Transporte) segmentando datos, asegurando su entrega en orden y sin errores.
  * Se analizó el protocolo **HTTP** (Capa de Aplicación) procesando la solicitud y permitiendo la visualización de la interfaz del servidor web.

---

## 💡 Conclusiones del Proyecto
El desarrollo de esta topología permitió observar de manera tangible la lógica detrás del Modelo OSI. Se comprobó la vital importancia de las tablas ARP para vincular direcciones lógicas con físicas, la eficiencia de los switches para segmentar colisiones, y el rol indispensable de los routers y el subnetting para administrar y dirigir el tráfico de manera estructurada y escalable entre redes diferentes.
