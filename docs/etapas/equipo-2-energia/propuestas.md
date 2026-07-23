# Propuestas de Aplicaciones para Red Cóndor
## Equipo 2: Energía

Basado en la investigación sobre paneles solares, baterías, consumo del ESP32 y dimensionamiento de autonomía, proponemos las siguientes aplicaciones para el **Proyecto Red Cóndor**. Las propuestas buscan conectar energía autónoma con necesidades reales de puestos rurales, rescatistas y Defensa Civil en la zona de Malargüe y alrededores.

---

## 1. Nodos Sensores Autónomos Solares para Puestos Rurales

**Descripción:**  
Dispositivos compactos alimentados por panel monocristalino de 5-10 W + batería LiFePO4 de 10-30 Ah, con ESP32 en deep sleep, sensores ambientales (temperatura, humedad, presión, humedad de suelo) y módulo LoRa.

**Funcionalidad:**  
- Monitoreo de condiciones agroclimáticas (heladas, sequía, viento).  
- Alertas vía LoRa a puestos vecinos o central.  
- Datos históricos para planificación de siembras o protección de animales.

**Consideraciones energéticas:**  
- El consumo estimado de 0,1–0,3 Wh/día solo es alcanzable con transmisiones muy poco frecuentes y hardware bien optimizado. Sin mediciones reales de consumo este valor es una estimación optimista.  
- Autonomía teórica de 4-7 días sin sol. En inviernos de Malargüe (días cortos, nubes y nieve) la autonomía real puede ser menor.  
- Las LiFePO4 no se pueden cargar de forma segura por debajo de 0 °C. Se requiere aislamiento térmico o calentamiento activo, lo que reduce la autonomía neta.  
- Costo estimado de prototipo de laboratorio: USD 150-250. Un equipo robusto de campo (carcasa IP67 real, BMS de calidad, montaje resistente) probablemente supere ese rango en Argentina.

---

## 2. Estaciones de Monitoreo para Rescate y Defensa Civil

**Descripción:**  
Nodos más robustos con panel de 10-20 W, batería LiFePO4 de 30-60 Ah (o mayor), carcasa IP67, sensores ambientales + GPS, y posible sensor de movimiento. Transmisión LoRa y/o radioenlace punto a punto.

**Uso principal:**  
- Datos de condiciones meteo y ubicación para equipos de rescate.  
- Monitoreo de ríos, caminos y zonas de riesgo.  
- Apoyo a alertas tempranas de Defensa Civil.

**Consideraciones energéticas:**  
- Se recomienda sobredimensionar la batería o el panel respecto a los nodos de puesto.  
- 5 días de autonomía debe tomarse como un objetivo mínimo, no como garantía, especialmente en inviernos con varios días nublados o con nieve sobre el panel.  
- El calentamiento de la batería en temperaturas bajo cero es un punto crítico a resolver en el prototipo.  
- Monitoreo remoto del estado de batería y producción solar es altamente recomendable.

---

## 3. Gateway / Repetidor Principal

**Descripción:**  
Nodo concentrador en punto elevado con buena visibilidad solar y radio.  
- Panel: 30-80 W  
- Batería: 100-200+ Ah LiFePO4  
- ESP32 o ESP32-S3 + gateway LoRa + posible radioenlace hacia infraestructura central.

**Justificación:**  
Mayor consumo por estar más tiempo activo o procesando datos de varios nodos. Actúa como punto de concentración de la red.

**Consideraciones:**  
- Requiere diseño más cuidadoso de la autonomía y posible respaldo (generador portátil) para emergencias prolongadas.  
- Debe reportar su propio estado de batería y salud del sistema.

---

## 4. Sistemas Híbridos Solares + Eólicos (opcional)

**Descripción:**  
Complementar el panel solar con un pequeño aerogenerador (50-200 W) en sitios con buen recurso eólico.

**Observaciones:**  
Es una opción secundaria. Los aerogeneradores pequeños agregan partes móviles, vibración y mantenimiento. En la mayoría de los casos de nodos de bajo consumo, un panel más grande o más capacidad de batería suele ser más simple y confiable. Solo se recomienda si se confirma buen recurso eólico local y se acepta el costo de mantenimiento extra.

---

## 5. Aplicaciones Transversales

- Monitoreo de infraestructura crítica (vibración/nivel en represas, canales o caminos remotos).  
- Estaciones meteo de bajo impacto para zonas de valor turístico/astronómico.  
- Kits didácticos de energía solar + ESP32 para capacitación de productores y rescatistas.  
- Diseño modular que permita aumentar batería o panel según resultados de campo.

---

## Beneficios y Limitaciones

| Aspecto              | Comentario |
|----------------------|----------|
| **Autonomía**        | Independiente de la red eléctrica. La autonomía real en invierno depende fuertemente del manejo del frío y de la nieve sobre el panel. |
| **Mantenimiento**    | Bajo, pero no nulo. Requiere visitas periódicas o telemetría del estado del sistema. |
| **Costo**            | Bajo a mediano plazo si se evita generadores a combustible. El costo inicial de un equipo robusto puede superar las estimaciones de prototipo. |
| **Escalabilidad**    | Buena, siempre que se resuelva el consumo real y el comportamiento en frío. |
| **Fiabilidad en frío** | Punto crítico. Las LiFePO4 necesitan estrategia clara de protección térmica para poder cargarse. |
| **Integración**      | Compatible con LoRa, ESP32 y el resto de los equipos del proyecto. |

---

## Recomendaciones para la Siguiente Etapa (Prototipado)

1. **Prioridad 1:** Construir 2-3 prototipos y **medir el consumo real** durante al menos 1-2 semanas (incluyendo condiciones de frío y baja insolación).  
2. Resolver de forma explícita el problema de carga de LiFePO4 bajo 0 °C (calentamiento, aislamiento o batería con calentador integrado).  
3. Validar orientación e inclinación del panel en sitio real o con simulación de invierno.  
4. Coordinar con Equipo Comunicaciones el perfil de tráfico LoRa (frecuencia e impacto en consumo).  
5. Documentar costos reales de componentes en Argentina (no solo estimaciones de laboratorio).  
6. Elaborar un manual simple de instalación y mantenimiento orientado a usuarios finales.

---

**Nota final:**  
Las propuestas son técnicamente viables, pero dependen de mediciones reales de consumo y de una solución concreta al problema de carga en frío. Se recomienda avanzar a prototipos instrumentados antes de escalar o presentar números definitivos de autonomía y costo.

---

*Documento revisado – Equipo 2 Energía | Proyecto Red Cóndor*
