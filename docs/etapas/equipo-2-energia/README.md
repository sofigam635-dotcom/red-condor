# Equipo 2: Energía - Red Cóndor

## Objetivo del Equipo

Analizar, proponer y validar soluciones energéticas para alimentar dispositivos LoRa/Meshtastic en zonas remotas de montaña sin acceso a la red eléctrica convencional.

**Enfoque principal:** Lograr autonomía confiable en condiciones climáticas extremas de Malargüe (frío intenso, nieve, viento y períodos prolongados de baja radiación solar).

---

## Temas Investigados

- **Paneles solares**: Tipos, eficiencia, orientación y potencia requerida.
- **Baterías**: Tecnologías disponibles y comportamiento en frío extremo.
- **Consumo energético**: Análisis del ESP32 + LoRa en diferentes modos (especialmente deep sleep).
- **Autonomía y dimensionamiento**: Cálculo realista de días de funcionamiento y estrategias para días nublados.

---

## Hallazgos Principales

- **Paneles**: Se recomienda **monocristalino** por su mayor eficiencia (18-22%) y mejor rendimiento en bajas temperaturas y poca luz. Orientación hacia el Norte con inclinación de 30°-40° en Malargüe.
- **Baterías**: **LiFePO4** es la tecnología más adecuada por su larga vida útil (2000-5000 ciclos), seguridad y mejor comportamiento en frío.
- **Consumo**: Con buena configuración de Meshtastic (deep sleep), se puede lograr un consumo promedio de 2-5 mA, permitiendo autonomías aceptables con baterías 18650 + power banks.
- **Autonomía**: Los cálculos teóricos son optimistas. Se debe sobredimensionar considerando pérdidas y varios días sin sol.

---

## Análisis Crítico

El diseño energético propuesto es técnicamente viable, pero presenta riesgos importantes de subestimación de la realidad del terreno:

- Los cálculos de autonomía (7-10 días para repetidores) pueden ser insuficientes en inviernos duros de Bardas Blancas.
- El mantenimiento de repetidores en altura es complejo y costoso.
- La carga adicional (power banks, paneles portátiles) puede reducir la adopción por parte de los puesteros.
- Existe riesgo de dependencia excesiva de condiciones climáticas favorables.

**Conclusión crítica**: Debemos priorizar robustez y simplicidad por sobre características avanzadas. La energía es uno de los puntos más críticos del proyecto; si falla aquí, falla todo el sistema.

---

## Propuestas y Recomendaciones

### Para Nodos Móviles (Puesteros)
- Configuración base: Batería 18650 interna + Power Bank 10.000 mAh.
- Opcional: Panel solar plegable 5W para estancias largas.
- Enfoque: Máxima simplicidad de uso.

### Para Repetidores Fijos
- Panel monocristalino 10-20W.
- Batería LiFePO4 10-20 Ah + regulador MPPT.
- Empezar con pocos repetidores en ubicaciones accesibles.

### Mejoras Inmediatas
1. Medir consumo real de hardware con Meshtastic en modo ahorro.
2. Realizar pruebas en condiciones de frío.
3. Implementar alertas automáticas de batería baja y nodo offline.
4. Sobredimensionar baterías y paneles (factor 1.5x mínimo).

---

## Dudas y Preguntas Abiertas

- ¿Cuál es la duración real de períodos sin sol en la zona de Bardas Blancas?
- ¿Disponibilidad y precio real de LiFePO4 y paneles en Mendoza/Argentina?
- ¿Aceptarán los puesteros llevar componentes adicionales?
- ¿Cómo garantizamos el mantenimiento a largo plazo de los repetidores?

---

**Responsables:** Equipo 2 - Energía  
**Última actualización:** [Fecha actual]  
**Estado:** En desarrollo
