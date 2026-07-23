# Preguntas Abiertas - Equipo 2: Energía

## Análisis Crítico de las Preguntas Abiertas

Esta sección es una de las más importantes del equipo, pero actualmente es **demasiado genérica y poco priorizada**. Muchas preguntas son válidas, pero están dispersas y no reflejan la urgencia real del proyecto. 

**Crítica principal:**  
Estamos haciendo muchas preguntas teóricas sin haber validado lo más básico. Esto es típico de proyectos que se quedan en la fase de planificación y nunca llegan a implementación. Las preguntas abiertas deben ser **priorizadas por impacto** (qué nos puede hacer fracasar) y no solo listadas.

### Preguntas Críticas (Alta Prioridad - Resolver YA)

1. **Autonomía real en invierno**  
   ¿Cuántos días consecutivos sin sol efectivo (nieve, nubes bajas, tormenta) son comunes en Bardas Blancas y corredores cercanos?  
   *Esto es crítico*: Si la respuesta es más de 7-10 días, nuestro dimensionamiento actual falla.

2. **Comportamiento en frío extremo**  
   ¿Cuánta capacidad real pierde una batería LiFePO4 a -15°C / -20°C? ¿Se ha medido en condiciones similares?  
   *Riesgo*: Subestimar esto puede dejar repetidores muertos en pleno temporal.

3. **Adopción por el usuario final**  
   ¿Los puesteros están dispuestos a llevar power banks o paneles plegables adicionales? ¿Ven esto como una molestia o como algo útil?  
   *Crítico*: Si no aceptan el dispositivo por peso o complejidad, todo el esfuerzo energético es inútil.

4. **Mantenimiento a largo plazo**  
   ¿Quién va a subir a los repetidores solares a cambiar baterías o limpiar paneles cada 1-2 años? ¿Existe logística real y presupuesto para eso?

5. **Costo real vs. presupuesto**  
   ¿Cuál es el precio real en Argentina (incluyendo envío e impuestos) de paneles monocristalinos 10-20W, baterías LiFePO4 y reguladores MPPT? ¿Cabe dentro del presupuesto escolar?

### Preguntas Secundarias (Media / Baja Prioridad)

- ¿Qué reguladores MPPT baratos y confiables hay disponibles localmente?
- ¿Es viable usar baterías 18650 recicladas o de segunda mano para nodos móviles?
- ¿Cómo afecta la altitud y el viento fuerte al rendimiento de los paneles?
- ¿Cuál es el consumo medido real de un T-Beam/T-Echo con Meshtastic en deep sleep (no teórico)?

---

## Observaciones Generales y Recomendaciones

- **Falta de priorización**: No todas las preguntas tienen el mismo peso. Deberíamos marcar claramente cuáles son “bloqueantes” para el proyecto.
- **Falta de acción**: Muchas preguntas solo se responden saliendo al campo o comprando y midiendo hardware. Seguir acumulando preguntas sin validar nada es riesgoso.
- **Optimismo excesivo**: Seguimos asumiendo que la tecnología va a comportarse como en laboratorio. La realidad de Malargüe es más dura.

**Próximos pasos recomendados:**
1. Responder las 5 preguntas críticas antes de avanzar a Etapa 2.
2. Realizar al menos una prueba de consumo real en frío (aunque sea en freezer + mediciones).
3. Entrevistar a 3-4 puesteros reales sobre el tema de portabilidad y mantenimiento.

---

**Última actualización:** [23/07/2026]  
**Responsable:** Equipo 2 - Energía
