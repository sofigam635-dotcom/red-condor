# Investigación y Fundamentos Técnicos de Infraestructura - Equipo 5

Este documento compila el marco teórico, el análisis del entorno operativo y las decisiones de arquitectura tecnológica para la infraestructura física, de red y de energía de la Red Cóndor en el departamento de Malargüe, Mendoza.

## 1. Contexto Territorial y Exigencias Ambientales

La infraestructura de comunicaciones de la Red Cóndor está proyectada para desplegarse en el corredor rural que abarca desde Bardas Blancas hasta el Puesto Piuquenes y pasos fronterizos. El entorno presenta desafíos críticos que condicionan el diseño de hardware:

* **Inclemencias Térmicas Severas:** Durante el período invernal se registran temperaturas extremas de hasta -20 °C, acompañadas por amplitudes térmicas diarias que superan los 30 °C.
* **Inestabilidad de Suministro Eléctrico:** Las zonas rurales carecen de red eléctrica o sufren cortes de suministro prolongados durante temporales de viento y nieve.
* **Carga Mecánica y Radiación UV:** La altitud de la zona andina expone el equipamiento a alta radiación ultravioleta y vientos superiores a 100 km/h, provocando la cristalización rápida y degradación de plásticos convencionales.

## 2. Ciclo Operativo del Puestero y su Impacto en el Diseño

La actividad ganadera en la región sigue el ciclo de veranada e invernada:

* **Veranada (Noviembre a Abril):** Los puesteros ascienden a pastizales de alta montaña de difícil acceso y sin cobertura celular.
* **Invernada (Mayo a Octubre):** El ganado y los puesteros descienden a zonas más bajas. Este período define la ventana de mantenimiento del sistema.

El diseño energético del nodo móvil debe adaptarse a la permanencia continua del usuario en el puesto, requiriendo configuraciones que toleren de 3 a 15 días sin recarga eléctrica de red.

## 3. Química y Almacenamiento Energético: LiFePO4

Para la alimentación de nodos repetidores solares y sistemas de respaldo se ha seleccionado la química de **Fosfato de Hierro y Litio (LiFePO4)**.

### Comparativa Técnica de Químicas Energéticas:

1. **LiFePO4 (Litio-Ferrofosfato):**
   * **Desempeño en frío:** Mantiene la estabilidad de descarga en temperaturas bajo cero (-20 °C).
   * **Vida útil:** Soporta entre 2000 y 3000+ ciclos de descarga profunda.
   * **Seguridad:** Inmune a embalamiento térmico y explosión por cortocircuito.
2. **Li-Ion (Litio-Cobalto/Manganeso):**
   * Sufre degradación severa de capacidad a temperaturas inferiores a 0 °C y un promedio de solo 500 ciclos de vida útil.
3. **Plomo-Ácido (VRLA/Gel):**
   * Elevado peso, menor eficiencia de carga fotovoltaica y vida útil reducida ante descargas profundas constantes.

## 4. Arquitectura de Red Mesh LoRa y Meshtastic

La capa de comunicación de campo utiliza modulación por espectro ensanchado por chirp (CSS) mediante tecnología LoRa en frecuencias no licenciadas (868 / 915 MHz).

* **Topología en Malla (Mesh):** El protocolo Meshtastic permite que cada nodo funcione como repetidor pasivo. Si un nodo móvil no tiene línea de visión directa con el Gateway, el mensaje salta a través de repetidores intermedios hasta alcanzar el punto con conectividad a internet.
* **Bajo Consumo:** Transmisiones en ráfaga con potencias de 20 a 22 dBm (100-150 mW), permitiendo que un nodo entre en modo de suspensión profunda (*deep sleep*) consumiendo menos de 1 mA.

## 5. Arquitectura del Gateway Rural y Borde (Offline-First)

El Gateway ubicado en zonas rurales (como Bardas Blancas) vincula la red de radiofrecuencia con la infraestructura IP del servidor central.

* **Sistema Operativo:** Base en Debian 12 (Bookworm) LTS.
* **Contenerización (Docker):** Despliegue modular de servicios mediante Docker Compose para garantizar reproducibilidad y facilidades de actualización.
* **Desacoplamiento de Mensajería (Mosquitto MQTT):** Los mensajes recibidos por la interfaz serie LoRa se publican en un broker MQTT local, desvinculando la recepción RF del procesamiento.
* **Procesamiento de Reglas (Node-RED):** Módulo de lógica que evalúa los mensajes entrantes, extrae coordenadas GPS y formatea las alertas.
* **Persistencia Local (InfluxDB):** Almacenamiento local en base de datos de series temporales. Ante la pérdida de internet, la telemetría se resguarda localmente y se sincroniza al restablecerse la conexión a través de Tailscale VPN.
