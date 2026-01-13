# Cómo Crear Custom GPTs: Metodología Prompt + Knowledge Base

Este repositorio contiene un ejemplo completo de cómo estructurar un Custom GPT separando correctamente lo que va en el **prompt de sistema** versus lo que va en la **base de conocimiento**.

## El Principio Fundamental

> **El prompt define el "cómo" (comportamiento). La base de conocimiento contiene el "qué" (información de referencia).**

Esta separación no es arbitraria. Tiene razones técnicas y prácticas:

### ¿Por qué separar?

1. **Límites de contexto**: El prompt de sistema tiene límites de tokens. Meter toda la información ahí es ineficiente.

2. **Actualización**: La información de referencia cambia más frecuentemente que el comportamiento. Separar permite actualizar la KB sin tocar el prompt.

3. **Claridad de rol**: El modelo entiende mejor su rol cuando las instrucciones de comportamiento están separadas de los datos de referencia.

4. **Retrieval selectivo**: La KB se consulta por relevancia. No todo se carga siempre—solo lo que el modelo necesita para la pregunta actual.

---

## Qué va en el Prompt de Sistema

El prompt contiene las **instrucciones de operación**:

| Elemento | Ejemplo |
|----------|---------|
| Identidad y tono | "Eres un coach directo pero motivador" |
| Flujo de conversación | "Pregunta una cosa a la vez en este orden..." |
| Modos de operación | "Modo Práctica, Modo Preparación, Modo Revisión" |
| Formato de respuestas | "Después de cada respuesta: qué funcionó, qué mejorar, ejemplo" |
| Reglas y restricciones | "Máximo 5-7 preguntas por sesión" |
| Comportamientos prohibidos | "No copies respuestas textualmente" |

### Características del buen prompt

- **Específico en comportamiento**: No "sé amable", sino "celebra los aciertos antes de señalar mejoras"
- **Estructurado en flujo**: Paso 1, Paso 2, etc.
- **Claro en formato**: Cómo debe verse cada tipo de respuesta
- **Explícito en límites**: Qué NO debe hacer

---

## Qué va en la Base de Conocimiento

La KB contiene los **datos de referencia** que el modelo consulta:

| Elemento | Ejemplo |
|----------|---------|
| Información de dominio | Preguntas comunes de entrevista por tipo |
| Frameworks y metodologías | Explicación detallada de STAR |
| Ejemplos y templates | Respuestas modelo para estudiar |
| Listas y catálogos | Red flags, tips, errores comunes |
| Contenido que cambia | Preguntas para roles específicos |

### Características de buena KB

- **Organizada en archivos temáticos**: Un archivo por tema, no un mega-documento
- **Searchable**: Títulos y headers claros para que el retrieval funcione
- **Ejemplos concretos**: No solo teoría, ejemplos aplicables
- **Actualizable**: Estructurada para poder agregar/modificar sin rehacer todo

---

## Estructura de Este Ejemplo

```
interview-prep-gpt/
├── SYSTEM_PROMPT.md          # Prompt de sistema completo
├── README.md                 # Este archivo
└── kb/                       # Base de conocimiento
    ├── 01_preguntas_por_tipo.md
    ├── 02_framework_star.md
    ├── 03_respuestas_ejemplo.md
    ├── 04_red_flags_y_tips.md
    └── 05_preguntas_para_entrevistador.md
```

---

## Cómo Implementar en ChatGPT

### 1. Crear el GPT

- Ve a https://chat.openai.com/gpts/editor
- Click en "Create a GPT"

### 2. Configurar el prompt

- En la pestaña "Configure"
- Copia el contenido de `SYSTEM_PROMPT.md` en el campo "Instructions"

### 3. Subir la base de conocimiento

- En la sección "Knowledge"
- Sube todos los archivos de la carpeta `kb/`
- ChatGPT los indexará automáticamente

### 4. Configurar capacidades

- Desactiva "Web Browsing" (no lo necesita)
- Desactiva "DALL-E" (no lo necesita)
- Desactiva "Code Interpreter" (no lo necesita)

### 5. Probar y ajustar

- Usa la preview para probar diferentes escenarios
- Ajusta el prompt según el comportamiento observado

---

## Checklist de Validación

Antes de publicar, verifica:

### Prompt
- [ ] ¿Tiene identidad clara?
- [ ] ¿El flujo de conversación está definido?
- [ ] ¿Los modos de operación están explicados?
- [ ] ¿El formato de respuestas está especificado?
- [ ] ¿Las restricciones están claras?

### Knowledge Base
- [ ] ¿Está organizada en archivos temáticos?
- [ ] ¿Los headers son descriptivos para el retrieval?
- [ ] ¿Hay suficientes ejemplos concretos?
- [ ] ¿La información es precisa y actualizada?
- [ ] ¿Cada archivo tiene un propósito claro?

### Testing
- [ ] ¿El flujo inicial funciona correctamente?
- [ ] ¿El modelo usa la KB cuando debe?
- [ ] ¿El tono es consistente?
- [ ] ¿Maneja bien casos edge?
- [ ] ¿El feedback es útil y específico?

---

## Errores Comunes a Evitar

### En el Prompt

❌ **Demasiado vago**: "Sé útil y amigable"
✅ **Específico**: "Celebra aciertos antes de señalar mejoras, máximo 2 puntos de mejora por respuesta"

❌ **Demasiado largo**: Meter toda la información en el prompt
✅ **Conciso**: Solo comportamiento, la información va en KB

❌ **Sin estructura**: Párrafos de texto corrido
✅ **Estructurado**: Secciones claras con headers

### En la Knowledge Base

❌ **Un solo archivo gigante**: Todo en un documento
✅ **Archivos temáticos**: Un archivo por tema

❌ **Solo teoría**: "El framework STAR es importante"
✅ **Ejemplos concretos**: Respuestas modelo completas

❌ **Headers genéricos**: "Sección 1", "Información"
✅ **Headers descriptivos**: "Preguntas de Recursos Humanos", "Framework STAR"

---

## Adaptando Esta Metodología

Para crear tu propio Custom GPT:

1. **Define el problema** que resuelve
2. **Identifica el comportamiento** necesario → esto va al prompt
3. **Identifica la información** de referencia → esto va a la KB
4. **Escribe el prompt** siguiendo la estructura de este ejemplo
5. **Organiza la KB** en archivos temáticos con buenos headers
6. **Prueba** con casos reales y ajusta

---

## Licencia

Este ejemplo es de uso libre. Úsalo como template para tus propios proyectos.
