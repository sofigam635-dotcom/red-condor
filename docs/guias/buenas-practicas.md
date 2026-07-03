# Guía de buenas prácticas para Red Cóndor

## 1. Cómo escribir commits

Los commits son mensajes que explican QUÉ cambiaste y POR QUÉ. Van a quedar en la historia del proyecto para siempre.

### Regla básica

```
tipo: descripción breve (máximo 50 caracteres)

(opcional) Explicación más detallada de lo que hiciste.
```

### Tipos de commit

| Tipo | Cuándo usarlo | Ejemplo |
|------|---------------|---------|
| `feat:` | Agregás contenido nuevo | `feat: agrega investigación sobre baterías LiFePO4` |
| `fix:` | Corregís un error | `fix: corrige nombre de archivo con espacios` |
| `docs:` | Cambiás documentación | `docs: agrega preguntas abiertas del equipo 1` |
| `style:` | Cambiás formato (tildes, espacios, etc.) | `style: agrega tildes y eñes en README` |
| `refactor:` | Reorganizás sin cambiar contenido | `refactor: mueve zonas-usuarios a carpeta correcta` |
| `chore:` | Tareas de mantenimiento | `chore: agrega .gitkeep en carpetas vacías` |

### Ejemplos concretos

**Bien** ✅
```
feat: agrega investigación sobre antenas LoRa para zona de montaña
docs: expande preguntas abiertas sobre consumo energético en frío
fix: corrige error en el cálculo de autonomía de batería
```

**Mal** ❌
```
.
update
cambios
INVESTIGACION.md
hola profe
```

### ¿Por qué es importante?

Cuando alguien revise el historial del proyecto (vos, tus compañeros, el profe) va a entender rápidamente qué cambió sin tener que leer el archivo completo.

---

## 2. Cómo nombrar archivos

### Reglas

- **Sin espacios**: usá guiones `-` en lugar de espacios
- **Sin mayúsculas**: todo en minúsculas
- **Extensión correcta**: `.md` para documentos
- **Solo letras, números y guiones**: nada de `¿?¡!.,()`

| Bien ✅ | Mal ❌ |
|---------|--------|
| `zonas-usuarios.md` | `zonas en las que viven los posibles usuarios` |
| `preguntas-abiertas.md` | `PREGUNTAS ABIERTAS.md` |
| `investigacion-energia.md` | `inv estigación (2).md` |

---

## 3. Cómo hacer preguntas (Issues)

**Toda pregunta o duda va en un Issue de GitHub.** No uses los archivos del repo para hacerle consultas al profe.

### Pasos:

1. Andá a la pestaña **Issues** del repo
2. Hacé clic en **New Issue**
3. Elegí la plantilla **"Consulta o duda"**
4. Completá el formulario
5. Antes de publicar, preguntate: ¿revisé los documentos del repo?

### Reglas:
- **Una duda = un Issue** (no mezcles preguntas distintas)
- **Usá títulos claros**: `[CONSULTA] ¿Cómo calcular la autonomía de la batería?`
- **Explicá qué intentaste**: ayuda a que te respondan mejor

---

## 4. Cómo trabajar en equipo

### Estructura de carpetas

Cada equipo tiene su carpeta en `docs/etapas/equipo-X-nombre/`:

```
equipo-1-comunicaciones/
├── README.md              # Objetivos del equipo
├── investigacion.md        # Resultados de la investigación
├── preguntas-abiertas.md   # Dudas que surgieron
└── propuestas.md           # Ideas para aplicar al proyecto
```

### Qué va en cada archivo

- **README.md**: No se modifica (lo puso el profe). Tiene los objetivos del equipo.
- **investigacion.md**: Todo lo que investigaron del tema con sus fuentes.
- **preguntas-abiertas.md**: Las dudas que todavía no pudieron responder.
- **propuestas.md**: Ideas de cómo aplicar lo que aprendieron a Red Cóndor.

### No toques archivos de otros equipos

Cada equipo trabaja en SU carpeta. Si necesitás preguntarle algo a otro equipo, usá Issues.

---

## 5. Fork vs trabajar directo

- **Si trabajás directo en el repo**: hacé `git pull` antes de empezar y `git push` después.
- **Si trabajás desde un fork**: hacé un Pull Request (PR) y usá la plantilla.

En ambos casos, escribí commits descriptivos (punto 1 de esta guía).
