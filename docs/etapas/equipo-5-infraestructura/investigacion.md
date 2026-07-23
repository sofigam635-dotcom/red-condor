# Investigación y Fundamentos Técnicos de Infraestructura - Equipo 5

[cite_start]Este documento compila el marco teórico, el análisis del entorno operativo y las decisiones de arquitectura tecnológica para la infraestructura física, de red y de energía de la Red Cóndor en el departamento de Malargüe, Mendoza[cite: 700, 705, 1225].

---

## 1. Contexto Territorial y Exigencias Ambientales

[cite_start]La infraestructura de comunicaciones de la Red Cóndor está proyectada para desplegarse en el corredor rural que abarca desde Bardas Blancas hasta el Puesto Piuquenes y pasos fronterizos[cite: 706, 749, 1280]. El entorno presenta desafíos críticos que condicionan el diseño de hardware:

* [cite_start]**Inclemencias Térmicas Severas:** Durante el período invernal se registran temperaturas extremas de hasta -20 °C, acompañadas por amplitudes térmicas diarias que superan los 30 °C[cite: 760, 1228].
* [cite_start]**Inestabilidad de Suministro Eléctrico:** Las zonas rurales carecen de red eléctrica o sufren cortes de suministro prolongados durante temporales de viento y nieve[cite: 720, 760, 1236].
* [cite_start]**Carga Mecánica y Radiación UV:** La altitud de la zona andina expone el equipamiento a alta radiación ultravioleta y vientos superiores a 100 km/h, provocando la cristalización rápida y degradación de plásticos convencionales[cite: 622, 633, 1241].

---

## 2. Ciclo Operativo del Puestero y su Impacto en el Diseño

[cite_start]La actividad ganadera en la región sigue el ciclo de veranada e invernada[cite: 727, 728]:

* [cite_start]**Veranada (Noviembre a Abril):** Los puesteros ascienden a pastizales de alta montaña de difícil acceso y sin cobertura celular[cite: 729, 761].
* [cite_start]**Invernada (Mayo a Octubre):** El ganado y los puesteros descienden a zonas más bajas[cite: 730]. [cite_start]Este período define la ventana de mantenimiento del sistema[cite: 744].

[cite_start]El diseño energético del nodo móvil debe adaptarse a la permanencia continua del usuario en el puesto, requiriendo configuraciones que toleren de 3 a 15 días sin recarga eléctrica de red[cite: 740, 894, 896].

---

## 3. Química y Almacenamiento Energético: LiFePO4

[cite_start]Para la alimentación de nodos repetidores solares y sistemas de respaldo se ha seleccionado la química de **Fosfato de Hierro y Litio (LiFePO4)**[cite: 625, 878, 1240].

### Comparativa Técnica de Químicas Energéticas:

1. **LiFePO4 (Litio-Ferrofosfato):**
   * [cite_start]Desempeño en frío: Mantiene la estabilidad de descarga en temperaturas bajo cero (-20 °C)[cite: 625, 1240].
   * [cite_start]Vida útil: Soporta entre 2000 y 3000+ ciclos de descarga profunda[cite: 878, 1240].
   * [cite_start]Seguridad: Inmune a embalamiento térmico y explosión por cortocircuito[cite: 1240].
2. **Li-Ion (Litio-Cobalto/Manganeso):**
   * [cite_start]Sufre degradación severa de capacidad a temperaturas inferiores a 0 °C y un promedio de solo 500 ciclos de vida útil[cite: 1240].
3. **Plomo-Ácido (VRLA/Gel):**
   * [cite_start]Elevado peso, menor eficiencia de carga fotovoltaica y vida útil reducida ante descargas profundas constantes[cite: 1240].

---

## 4. Arquitectura de Red Mesh LoRa y Meshtastic

[cite_start]La capa de comunicación de campo utiliza modulación por espectro ensanchado por chirp (CSS) mediante tecnología LoRa en frecuencias no licenciadas (868 / 915 MHz)[cite: 707, 831, 832].

* [cite_start]**Topología en Malla (Mesh):** El protocolo Meshtastic permite que cada nodo funcione como repetidor pasivo[cite: 1285]. [cite_start]Si un nodo móvil no tiene línea de visión directa con el Gateway, el mensaje salta a través de repetidores intermedios hasta alcanzar el punto con conectividad a internet[cite: 1285].
* [cite_start]**Bajo Consumo:** Transmisiones en ráfaga con potencias de 20 a 22 dBm (100-150 mW), permitiendo que un nodo entre en modo de suspensión profunda (*deep sleep*) consumiendo menos de 1 mA[cite: 832, 879, 888].

---

## 5. Arquitectura del Gateway Rural y Borde (Offline-First)

[cite_start]El Gateway ubicado en zonas rurales (como Bardas Blancas) vincula la red de radiofrecuencia con la infraestructura IP del servidor central[cite: 707, 847, 1268].

* [cite_start]**Sistema Operativo:** Base en Debian 12 (Bookworm) LTS[cite: 851, 852].
* [cite_start]**Contenerización (Docker):** Despliegue modular de servicios mediante Docker Compose para garantizar reproducibilidad y facilidades de actualización.
* [cite_start]**Desacoplamiento de Mensajería (Mosquitto MQTT):** Los mensajes recibidos por la interfaz serie LoRa se publican en un broker MQTT local, desvinculando la recepción RF del procesamiento[cite: 626, 853, 854].
* [cite_start]**Procesamiento de Reglas (Node-RED):** Modulo de lógica que evalúa los mensajes entrantes, extrae coordenadas GPS y formatea las alertas[cite: 626, 855, 1288].
* [cite_start]**Persistencia Local (InfluxDB):** Almacenamiento local en base de datos de series temporales[cite: 855, 1237]. [cite_start]Ante la pérdida de internet, la telemetría se resguarda localmente y se sincroniza al restablecerse la conexión a través de Tailscale VPN[cite: 627, 856, 1237].
