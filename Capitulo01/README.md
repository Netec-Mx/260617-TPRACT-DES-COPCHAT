---LAB_START---
LAB_ID: 01-00-01
---MARKDOWN---
# Investiga y escribe un breve informe sobre cómo la IA ha impactado en una industria específica que te interese.

## Metadatos

| Campo            | Detalle                                      |
|------------------|----------------------------------------------|
| **Duración**     | 10 minutos                                   |
| **Complejidad**  | Fácil                                        |
| **Nivel Bloom**  | Aplicar (Apply)                              |
| **Módulo**       | 1 — Productividad con IA Generativa          |
| **Lección**      | 1.1 — Productividad con IA Generativa        |

---

## Descripción General

En esta práctica explorarás, por primera vez, el uso de **GitHub Copilot Chat como herramienta de productividad general**, más allá de la generación de código. Seleccionarás una industria de tu interés, formularás prompts estructurados en Copilot Chat para investigar el impacto de la IA generativa en ella, y redactarás un informe breve de 300 a 500 palabras. El ejercicio te permitirá experimentar de manera directa las tres dimensiones de productividad estudiadas en la lección — **velocidad, calidad y enfoque** — aplicadas a una tarea de escritura técnica real.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Identificar al menos **tres formas concretas** en que la IA generativa ha transformado una industria de interés personal, con ejemplos específicos.
- [ ] Redactar un **informe breve y estructurado** (introducción, cuerpo con tres impactos, conclusión personal) utilizando Copilot Chat como asistente de investigación.
- [ ] Formular **prompts estructurados** (rol, tarea, contexto, restricciones, formato, criterios de aceptación) para obtener respuestas útiles y relevantes de Copilot Chat.
- [ ] Desarrollar un **criterio propio** sobre beneficios y limitaciones de la IA generativa en contextos industriales reales, validando la información generada con fuentes externas.

---

## Prerrequisitos

### Conocimiento previo

| Área                                      | Nivel requerido |
|-------------------------------------------|-----------------|
| Uso básico de Visual Studio Code          | Básico          |
| Comprensión del concepto de prompt        | Introductorio   |
| Lectura de la lección 1.1 del curso       | Completo        |

### Acceso y cuentas

| Recurso                                   | Estado requerido                                              |
|-------------------------------------------|---------------------------------------------------------------|
| Cuenta de GitHub con Copilot activo       | ✅ Suscripción activa verificada                              |
| VS Code con extensión Copilot Chat        | ✅ Instalada y sesión iniciada                                |
| Conexión a internet                       | ✅ Mínimo 10 Mbps estable                                     |
| Navegador web moderno                     | ✅ Chrome, Edge o Firefox (última versión estable)            |
| Procesador de texto o editor de notas     | ✅ Word, Google Docs, Notion o cualquier equivalente reciente |

> **Nota importante:** Antes de iniciar, confirma con tu instructor que tu suscripción a GitHub Copilot está activa. Si el ícono de Copilot en la barra de estado de VS Code aparece en gris o muestra un error de autenticación, resuelve el acceso antes de continuar.

---

## Entorno de Laboratorio

### Requisitos de hardware

| Componente         | Mínimo requerido                        | Recomendado         |
|--------------------|-----------------------------------------|---------------------|
| Procesador         | Intel Core i5 / AMD Ryzen 5 (64 bits)  | i7 / Ryzen 7        |
| RAM                | 8 GB                                    | 16 GB               |
| Espacio en disco   | 2 GB libres                             | 10 GB libres        |
| Resolución         | 1280 × 768                              | 1920 × 1080         |
| Conexión a internet| 10 Mbps                                 | 25 Mbps o superior  |

### Software necesario

| Herramienta                             | Versión mínima          |
|-----------------------------------------|-------------------------|
| Visual Studio Code                      | 1.90                    |
| Extensión GitHub Copilot Chat (VS Code) | Última disponible       |
| Navegador web (Chrome / Edge / Firefox) | Última versión estable  |
| Procesador de texto                     | Cualquier versión reciente |

### Verificación del entorno (antes de comenzar)

Ejecuta los siguientes pasos de verificación rápida en VS Code:

**1. Confirmar que Copilot Chat está activo:**

Abre la paleta de comandos con:
```
Ctrl+Shift+P   (Windows / Linux)
Cmd+Shift+P    (macOS)
```
Escribe:
```
GitHub Copilot: Sign In
```
Si ya tienes sesión iniciada, verás el mensaje `"Already signed in"` o el comando no estará disponible (lo que confirma que la sesión está activa). El ícono de Copilot en la barra de estado inferior debe mostrarse en color (no en gris).

**2. Abrir el panel de Copilot Chat:**
```
Ctrl+Alt+I   (Windows / Linux)
Cmd+Alt+I    (macOS)
```
O bien, haz clic en el ícono de chat (burbuja con el logo de Copilot) en la barra lateral izquierda de VS Code.

**3. Crear el archivo de trabajo para esta práctica:**

Abre una terminal integrada en VS Code:
```
Ctrl+`   (Windows / Linux / macOS)
```
Luego ejecuta:
```bash
# Crear una carpeta de trabajo para el laboratorio
mkdir -p ~/copilot-labs/lab-01-00-01
cd ~/copilot-labs/lab-01-00-01

# Crear el archivo donde redactarás tu informe
touch informe-impacto-ia.md
```
Abre el archivo recién creado en VS Code:
```bash
code informe-impacto-ia.md
```

> **Alternativa:** Si prefieres redactar el informe en Google Docs, Word o Notion, puedes hacerlo. El archivo `informe-impacto-ia.md` es solo una opción conveniente para mantener todo en el mismo entorno.

---

## Instrucciones Paso a Paso

---

### Paso 1 — Selecciona tu industria y activa Copilot Chat

**Objetivo:** Elegir la industria que investigarás y abrir el panel de Copilot Chat listo para formular tu primer prompt.

#### Instrucciones

1. **Elige una industria** de tu interés personal. Algunas sugerencias:

   | Industria         | Ejemplo de aplicación de IA generativa              |
   |-------------------|-----------------------------------------------------|
   | Salud             | Diagnóstico asistido, generación de informes clínicos |
   | Finanzas          | Detección de fraude, asesoría automatizada          |
   | Manufactura       | Mantenimiento predictivo, control de calidad visual |
   | Educación         | Tutoría personalizada, generación de contenido      |
   | Entretenimiento   | Creación de guiones, diseño de personajes con IA    |
   | Retail / Comercio | Recomendaciones personalizadas, gestión de inventario |
   | Transporte        | Optimización de rutas, vehículos autónomos          |

   > **Recomendación:** Elige la industria que más te motive o en la que tengas experiencia previa. La práctica será más significativa y el informe más auténtico.

2. **Abre el panel de Copilot Chat** en VS Code usando el atajo:
   ```
   Ctrl+Alt+I   (Windows / Linux)
   Cmd+Alt+I    (macOS)
   ```

3. **Verifica que el chat esté funcional** escribiendo un mensaje corto de prueba:
   ```
   Hola, ¿estás disponible?
   ```
   Deberías recibir una respuesta en pocos segundos. Si no hay respuesta, revisa la sección de Solución de Problemas al final de este documento.

4. **Anota en tu diario de aprendizaje** (o en el archivo `informe-impacto-ia.md`) la industria que elegiste y una frase breve que explique por qué te interesa.

#### Resultado esperado

- Panel de Copilot Chat abierto y respondiendo en VS Code.
- Industria seleccionada y anotada.

#### Verificación

✅ El ícono de Copilot en la barra de estado de VS Code está activo (con color, no en gris).
✅ Copilot Chat respondió al mensaje de prueba.
✅ Tienes anotada la industria elegida.

---

### Paso 2 — Formula el primer prompt estructurado para investigar impactos

**Objetivo:** Aplicar la estructura de prompt recomendada en la lección 1.1 para obtener información inicial sobre el impacto de la IA generativa en la industria elegida.

#### Instrucciones

1. **Revisa la estructura de prompt** de la lección antes de escribir:

   | Componente           | Descripción                                                    |
   |----------------------|----------------------------------------------------------------|
   | **Rol**              | Quién eres y qué necesitas                                     |
   | **Tarea**            | Objetivo concreto                                              |
   | **Contexto**         | Industria, alcance, audiencia del informe                      |
   | **Restricciones**    | Límites: extensión, nivel de detalle, idioma                   |
   | **Formato de salida**| Cómo quieres recibir la respuesta                              |
   | **Criterios**        | Condiciones para considerar la respuesta útil                  |

2. **Escribe el siguiente prompt en Copilot Chat**, adaptando `[INDUSTRIA]` a la que elegiste:

   ```
   Actúa como investigador especializado en transformación digital.
   
   Tarea: Identifica y describe al menos tres impactos concretos y específicos 
   que la IA generativa ha tenido en la industria de [INDUSTRIA].
   
   Contexto: Estoy redactando un informe breve (300-500 palabras) para un curso 
   de desarrollo de software. La audiencia son programadores que están aprendiendo 
   a usar GitHub Copilot Chat. El objetivo es conectar el impacto de la IA en 
   esta industria con el concepto de productividad en el desarrollo de software.
   
   Restricciones: 
   - Usa ejemplos reales o altamente verosímiles con nombres de empresas o 
     herramientas cuando sea posible.
   - Nivel de detalle: intermedio (no demasiado técnico, no demasiado superficial).
   - Idioma: español.
   
   Formato de salida: Lista numerada con tres impactos. Cada impacto debe tener:
   (a) nombre del impacto en negrita, (b) descripción de 2-3 oraciones, 
   (c) un ejemplo concreto.
   
   Criterios de aceptación: La respuesta es útil si cada impacto incluye 
   al menos un dato específico o ejemplo verificable.
   ```

3. **Espera la respuesta** de Copilot Chat (normalmente entre 5 y 15 segundos).

4. **Lee la respuesta completa** antes de continuar. Evalúa:
   - ¿Los tres impactos son distintos entre sí?
   - ¿Los ejemplos son específicos o genéricos?
   - ¿Hay algún dato que te parezca impreciso o que quieras verificar?

5. **Copia la respuesta** y pégala temporalmente en tu archivo `informe-impacto-ia.md` bajo una sección llamada `## Borrador - Impactos`. Este es tu material de trabajo, no el informe final.

#### Resultado esperado

Una lista de al menos tres impactos de la IA generativa en tu industria elegida, con ejemplos concretos, lista para ser revisada y refinada.

**Ejemplo de respuesta esperada (para la industria de Salud):**

```
1. **Diagnóstico médico asistido por IA**
   Los modelos de IA generativa han mejorado la precisión diagnóstica al 
   analizar imágenes médicas como radiografías y resonancias magnéticas. 
   Sistemas como Google Health's MedPaLM 2 pueden responder preguntas 
   clínicas con un nivel de precisión comparable al de médicos especialistas.
   Ejemplo: En 2023, el NHS del Reino Unido comenzó a usar herramientas de 
   IA para detectar cáncer de mama en mamografías, reduciendo tiempos de 
   diagnóstico en un 30%.

2. **Generación automática de documentación clínica**
   ...

3. **Personalización de tratamientos**
   ...
```

#### Verificación

✅ Copilot Chat generó una lista con al menos tres impactos distintos.
✅ Cada impacto incluye un ejemplo específico (empresa, herramienta o dato).
✅ El borrador está pegado en tu archivo de trabajo.

---

### Paso 3 — Refina y amplía la información con prompts de seguimiento

**Objetivo:** Practicar la iteración guiada (solicitar → revisar → aclarar → ajustar) para mejorar la calidad del material antes de redactar el informe final.

#### Instrucciones

1. **Identifica el impacto más interesante** de los tres que te proporcionó Copilot Chat en el paso anterior. Puede ser el más sorprendente, el más relevante para tu experiencia, o el que tenga el ejemplo menos desarrollado.

2. **Formula un prompt de seguimiento** para profundizar en ese impacto. Usa el contexto del chat anterior (Copilot Chat recuerda la conversación en la misma sesión):

   ```
   Profundiza en el impacto número [N] que mencionaste. 
   
   Específicamente necesito:
   - Un dato cuantitativo (porcentaje, cifra, estadística) que respalde el impacto.
   - Una limitación o riesgo real asociado a este uso de IA en [INDUSTRIA].
   - Una fuente o referencia que pueda citar o verificar.
   
   Mantén el idioma en español y el nivel de detalle intermedio.
   ```

3. **Lee la respuesta** y aplica criterio crítico:
   - Si Copilot menciona una estadística, márcala para verificar en el siguiente paso.
   - Si menciona una fuente, anótala. Copilot puede "alucinar" referencias; las verificarás en el Paso 4.
   - Si la información parece demasiado general, puedes pedir: `"Dame un ejemplo más específico con nombre de empresa o producto."`.

4. **Formula un tercer prompt** para obtener material para la conclusión personal:

   ```
   Basándote en los impactos que hemos discutido, ayúdame a reflexionar sobre 
   lo siguiente para incluirlo en la conclusión de mi informe:
   
   - ¿Cuál es el mayor beneficio que la IA generativa aporta a [INDUSTRIA]?
   - ¿Cuál es la limitación más importante que los profesionales de esa 
     industria deben considerar?
   - ¿Cómo se relaciona este impacto con la productividad de los 
     desarrolladores de software que construyen estas soluciones?
   
   Responde en formato de tres puntos breves (2-3 oraciones cada uno), 
   en español, listos para incorporar en una conclusión personal.
   ```

5. **Actualiza tu archivo de trabajo** con las respuestas de estos prompts de seguimiento.

#### Resultado esperado

Material enriquecido con:
- Al menos un dato cuantitativo para uno de los impactos.
- Una limitación o riesgo identificado.
- Reflexiones para la conclusión personal.

#### Verificación

✅ Realizaste al menos dos prompts de seguimiento (refinamiento e iteración).
✅ Tienes material para los tres impactos más datos adicionales.
✅ Identificaste al menos una limitación o riesgo de la IA en tu industria.
✅ Tienes notas para la conclusión personal.

---

### Paso 4 — Valida la información con fuentes externas

**Objetivo:** Aplicar el principio de **validación humana** de la lección 1.1, verificando al menos un dato o referencia generada por Copilot Chat con una fuente externa confiable.

#### Instrucciones

1. **Selecciona uno o dos datos específicos** de los generados por Copilot Chat que quieras verificar. Prioriza:
   - Estadísticas o cifras porcentuales.
   - Nombres de empresas o productos específicos.
   - Referencias a estudios o informes.

2. **Abre tu navegador** y realiza una búsqueda rápida. Fuentes recomendadas para verificar:

   | Tipo de fuente                       | Ejemplos                                              |
   |--------------------------------------|-------------------------------------------------------|
   | Publicaciones de investigación        | Google Scholar, ResearchGate, arXiv                   |
   | Medios tecnológicos especializados   | MIT Technology Review, Wired, TechCrunch              |
   | Informes de industria                | McKinsey Global Institute, Gartner, Deloitte Insights |
   | Blogs oficiales de empresas tech     | Google Blog, Microsoft AI Blog, IBM Research          |
   | Documentación oficial de herramientas| Sitios web de las herramientas mencionadas            |

3. **Registra el resultado de tu verificación** en tu archivo de trabajo:

   ```markdown
   ## Verificación de datos
   
   | Dato de Copilot Chat | Verificado | Fuente | Ajuste necesario |
   |----------------------|------------|--------|------------------|
   | [dato 1]             | ✅ / ❌ / ⚠️ | [URL]  | [ajuste si aplica] |
   | [dato 2]             | ✅ / ❌ / ⚠️ | [URL]  | [ajuste si aplica] |
   ```

   Usa:
   - ✅ si el dato fue confirmado.
   - ❌ si el dato resultó incorrecto o no encontraste respaldo.
   - ⚠️ si el dato es aproximado o hay versiones distintas.

4. **Si encontraste un dato incorrecto**, regresa a Copilot Chat y usa este prompt:

   ```
   El dato que mencionaste sobre [dato específico] parece no ser preciso. 
   Encontré que [lo que encontraste en tu investigación]. 
   ¿Puedes revisar y proporcionar información más precisa o alternativa 
   sobre este punto?
   ```

5. **Toma nota** en tu diario de aprendizaje sobre la experiencia de verificación:
   - ¿Copilot fue preciso o hubo alucinaciones?
   - ¿Cuánto tiempo tomó verificar?
   - ¿Cambia tu percepción sobre la confiabilidad de Copilot Chat?

> **Nota pedagógica:** La verificación es un paso crítico que refleja directamente la práctica de "Validación humana" descrita en la lección 1.1. Copilot Chat es un copiloto, no un piloto. La responsabilidad profesional de validar la información siempre recae en el desarrollador.

#### Resultado esperado

- Al menos un dato verificado con su fuente registrada.
- Una nota personal sobre la precisión de Copilot Chat en esta tarea.

#### Verificación

✅ Verificaste al menos un dato en una fuente externa.
✅ Registraste el resultado de la verificación en tu archivo de trabajo.
✅ Tienes una reflexión anotada sobre la confiabilidad de Copilot Chat.

---

### Paso 5 — Redacta el informe final

**Objetivo:** Producir el informe final de 300 a 500 palabras, estructurado y revisado, usando Copilot Chat para asistir en la redacción y formato.

#### Instrucciones

1. **Solicita a Copilot Chat que te ayude a estructurar el informe** con todo el material que has recopilado:

   ```
   Actúa como editor técnico en español.
   
   Tarea: Ayúdame a redactar un informe breve y bien estructurado sobre el 
   impacto de la IA generativa en la industria de [INDUSTRIA].
   
   Contexto: El informe es para un curso de desarrollo de software. 
   La audiencia son programadores que aprenden a usar GitHub Copilot Chat. 
   El objetivo es mostrar cómo la IA impacta industrias reales y conectarlo 
   con el concepto de productividad en el desarrollo de software.
   
   Material disponible (resume los puntos clave de lo que encontraste):
   - Impacto 1: [resumen de tu impacto 1]
   - Impacto 2: [resumen de tu impacto 2]
   - Impacto 3: [resumen de tu impacto 3]
   - Limitación identificada: [tu limitación]
   - Reflexión personal: [tus notas de conclusión]
   
   Restricciones:
   - Entre 300 y 500 palabras en total.
   - Estructura: Introducción (50-80 palabras), tres secciones de impacto 
     (60-80 palabras cada una), Conclusión personal (60-80 palabras).
   - Tono: profesional pero accesible, en primera persona para la conclusión.
   - Idioma: español.
   
   Formato de salida: Texto completo del informe listo para copiar, 
   con títulos de sección en negrita.
   ```

2. **Lee el borrador generado** completo. Evalúa:
   - ¿Refleja fielmente tu investigación y perspectiva?
   - ¿La introducción contextualiza bien el tema?
   - ¿Los tres impactos son claros y distintos?
   - ¿La conclusión es genuinamente personal o suena genérica?

3. **Personaliza la conclusión** — esta es la parte más importante para que el informe sea tuyo. Edita directamente en el archivo `informe-impacto-ia.md` para que la conclusión refleje tu opinión real. Puedes pedir ayuda a Copilot:

   ```
   La conclusión suena muy genérica. Ayúdame a reescribirla incorporando 
   esta perspectiva personal mía: [escribe 2-3 oraciones con tu opinión real 
   sobre el tema]. Mantén el tono profesional y el español.
   ```

4. **Copia el informe final** en tu archivo `informe-impacto-ia.md` con la siguiente estructura:

   ```markdown
   # Informe: Impacto de la IA Generativa en la Industria de [INDUSTRIA]
   
   **Autor:** [Tu nombre]  
   **Fecha:** [Fecha actual]  
   **Palabras:** [Cuenta de palabras aproximada]
   
   ## Introducción
   [Texto de introducción]
   
   ## Impacto 1: [Nombre del impacto]
   [Descripción y ejemplo]
   
   ## Impacto 2: [Nombre del impacto]
   [Descripción y ejemplo]
   
   ## Impacto 3: [Nombre del impacto]
   [Descripción y ejemplo]
   
   ## Conclusión Personal
   [Tu reflexión personal]
   
   ## Referencias verificadas
   - [Fuente 1]
   - [Fuente 2]
   ```

5. **Verifica el conteo de palabras**. En VS Code puedes seleccionar todo el texto del informe (`Ctrl+A`) y ver el conteo en la barra de estado inferior. El objetivo es entre 300 y 500 palabras en el cuerpo del informe (sin contar encabezados ni metadatos).

#### Resultado esperado

Un archivo `informe-impacto-ia.md` con el informe completo, estructurado, entre 300 y 500 palabras, con los tres impactos documentados y una conclusión personal auténtica.

#### Verificación

✅ El informe tiene entre 300 y 500 palabras en el cuerpo principal.
✅ Incluye introducción, tres secciones de impacto y conclusión personal.
✅ Cada impacto tiene un ejemplo concreto.
✅ La conclusión refleja una perspectiva personal genuina.
✅ Hay al menos una referencia verificada.

---

### Paso 6 — Reflexión final y registro en el diario de aprendizaje

**Objetivo:** Consolidar el aprendizaje de la práctica reflexionando sobre el uso de Copilot Chat como herramienta de productividad y registrando observaciones para prácticas futuras.

#### Instrucciones

1. **Abre tu diario de aprendizaje** (archivo de notas, Google Docs, Notion, o cualquier procesador de texto que uses a lo largo del curso).

2. **Responde las siguientes preguntas** en no más de 5-7 oraciones por pregunta:

   ```
   Reflexión de la Práctica 1:
   
   1. ¿En qué momentos Copilot Chat fue más útil durante esta práctica? 
      ¿Por qué?
   
   2. ¿En qué momentos Copilot Chat fue menos útil o generó información 
      que tuviste que corregir? ¿Cómo lo manejaste?
   
   3. ¿Cómo cambia tu percepción de la productividad cuando usas Copilot Chat 
      para una tarea de escritura/investigación vs. cuando lo imaginas 
      para una tarea de codificación?
   
   4. ¿Qué ajustarías en tu forma de formular prompts para la próxima práctica?
   ```

3. **Anota una métrica personal** de esta práctica:
   - ¿Cuánto tiempo te tomó completar el informe con Copilot Chat?
   - Estima cuánto tiempo te hubiera tomado sin Copilot Chat.
   - Esta comparación es tu primera "línea base" personal de productividad con IA.

   ```markdown
   ## Métrica personal - Práctica 1
   
   | Métrica                                    | Valor estimado |
   |--------------------------------------------|----------------|
   | Tiempo total con Copilot Chat              | ___ minutos    |
   | Tiempo estimado sin Copilot Chat           | ___ minutos    |
   | Número de prompts formulados               | ___            |
   | Datos que requirieron verificación externa | ___            |
   | Datos que resultaron incorrectos           | ___            |
   ```

4. **Guarda todos los archivos** generados durante la práctica. Los necesitarás como referencia en prácticas posteriores del curso (especialmente en las Prácticas 9 y 10).

#### Resultado esperado

- Reflexión documentada en el diario de aprendizaje.
- Métrica personal registrada como línea base.
- Archivos guardados y organizados.

#### Verificación

✅ Las cuatro preguntas de reflexión están respondidas en el diario.
✅ La métrica personal está registrada.
✅ El archivo `informe-impacto-ia.md` está guardado en `~/copilot-labs/lab-01-00-01/`.

---

## Validación y Pruebas

Al finalizar todos los pasos, verifica que tu práctica esté completa revisando esta lista:

### Lista de verificación final

| Criterio de validación                                                          | Estado    |
|---------------------------------------------------------------------------------|-----------|
| Copilot Chat fue utilizado para investigar (mínimo 3 prompts formulados)        | ☐ Sí / ☐ No |
| Los prompts incluyen estructura: Rol, Tarea, Contexto, Restricciones, Formato   | ☐ Sí / ☐ No |
| El informe tiene entre 300 y 500 palabras en el cuerpo principal                | ☐ Sí / ☐ No |
| El informe incluye introducción, tres impactos y conclusión personal            | ☐ Sí / ☐ No |
| Cada impacto tiene al menos un ejemplo concreto                                 | ☐ Sí / ☐ No |
| Al menos un dato fue verificado con una fuente externa                          | ☐ Sí / ☐ No |
| La conclusión expresa una perspectiva personal genuina                          | ☐ Sí / ☐ No |
| La reflexión y métrica personal están registradas en el diario de aprendizaje   | ☐ Sí / ☐ No |

### Prueba de calidad del informe

Comparte tu informe con un compañero o pide a Copilot Chat que lo evalúe con este prompt:

```
Actúa como evaluador de informes técnicos. Evalúa el siguiente informe 
según estos criterios:
1. Claridad y coherencia de la estructura (introducción, cuerpo, conclusión)
2. Especificidad de los ejemplos (¿son concretos o genéricos?)
3. Autenticidad de la conclusión personal (¿suena genuina o genérica?)
4. Conexión con el concepto de productividad en desarrollo de software

Para cada criterio, da una calificación de 1-5 y una sugerencia de mejora 
en una oración. Idioma: español.

[Pega aquí tu informe completo]
```

Usa la retroalimentación para identificar áreas de mejora, pero no es obligatorio reescribir el informe en esta práctica.

---

## Solución de Problemas

### Problema 1: Copilot Chat no responde o muestra error de conexión

**Síntoma:** El panel de Copilot Chat está abierto pero al enviar un mensaje aparece un mensaje de error como `"Request failed"`, `"Network error"`, o simplemente no hay respuesta después de 30 segundos.

**Causa probable:** Problema de autenticación con la sesión de GitHub, pérdida temporal de conexión a internet, o el servicio de GitHub Copilot está experimentando interrupciones.

**Solución:**

1. Verifica tu conexión a internet abriendo una página web en el navegador.
2. Cierra y vuelve a abrir VS Code completamente.
3. Verifica el estado del servicio en: [https://githubstatus.com](https://githubstatus.com). Busca la sección "GitHub Copilot".
4. Si el ícono de Copilot en la barra de estado está en gris, abre la paleta de comandos (`Ctrl+Shift+P`) y ejecuta:
   ```
   GitHub Copilot: Sign Out
   ```
   Luego vuelve a iniciar sesión con:
   ```
   GitHub Copilot: Sign In
   ```
5. **Plan de respaldo:** Si el problema persiste, realiza la investigación directamente en tu navegador usando [Bing Chat / Copilot](https://copilot.microsoft.com) o [ChatGPT](https://chatgpt.com) como alternativa temporal. Aplica la misma estructura de prompts y documenta los resultados. Informa al instructor para que valide tu suscripción.

---

### Problema 2: Las respuestas de Copilot Chat son demasiado genéricas o no incluyen ejemplos específicos

**Síntoma:** Copilot Chat responde con información muy superficial, sin nombres de empresas, herramientas o datos concretos. Por ejemplo: *"La IA ha mejorado la eficiencia en muchas áreas de la industria..."* sin detalles adicionales.

**Causa probable:** El prompt inicial no fue suficientemente específico en las restricciones o en los criterios de aceptación. Copilot Chat tiende a dar respuestas conservadoras y genéricas cuando las instrucciones son amplias.

**Solución:**

1. Agrega más especificidad al prompt. Usa este refinamiento:
   ```
   Tu respuesta anterior fue demasiado general. Necesito información más 
   específica. Por favor:
   - Nombra al menos dos empresas reales que usen IA generativa en [INDUSTRIA].
   - Incluye al menos un dato numérico (porcentaje, cifra, año).
   - Menciona al menos una herramienta o producto de IA específico 
     (por ejemplo: GPT-4, Gemini, Claude, Midjourney, etc.).
   
   Si no tienes información precisa, indícalo claramente y proporciona 
   la mejor aproximación disponible.
   ```
2. Si el problema persiste, intenta cambiar el ángulo de la pregunta:
   ```
   En lugar de hablar de [INDUSTRIA] en general, enfócate específicamente 
   en [subsector o área específica, p.ej., "diagnóstico por imagen en medicina" 
   o "trading algorítmico en finanzas"]. Dame tres casos de uso concretos 
   con nombres de herramientas o empresas.
   ```
3. Recuerda que cuanto más estrecho y específico sea el contexto del prompt, más útil y concreta será la respuesta de Copilot Chat. Este es el principio de **"Contexto y especificidad"** de la lección 1.1.

---

## Limpieza

Al finalizar la práctica, realiza las siguientes acciones para mantener tu entorno organizado:

1. **Guarda todos los archivos** generados:
   ```bash
   # Verificar que el archivo del informe existe y tiene contenido
   ls -la ~/copilot-labs/lab-01-00-01/
   cat ~/copilot-labs/lab-01-00-01/informe-impacto-ia.md | wc -w
   ```
   El segundo comando debe mostrar un número de palabras mayor a 300.

2. **Organiza tus notas** en el diario de aprendizaje. Asegúrate de que la reflexión y las métricas de esta práctica estén claramente etiquetadas como "Práctica 1" para poder referenciarlas en prácticas futuras.

3. **No es necesario desinstalar** ninguna herramienta ni cerrar sesión de Copilot. La sesión de GitHub Copilot puede permanecer activa para las prácticas siguientes.

4. **Opcional — Inicializar un repositorio Git** para versionar tu trabajo a lo largo del curso:
   ```bash
   cd ~/copilot-labs
   git init
   git add lab-01-00-01/informe-impacto-ia.md
   git commit -m "feat: add Lab 01-00-01 - AI impact report on [your industry]"
   ```
   Esto es opcional para esta práctica, pero se recomienda como buena práctica de organización.

---

## Resumen

### Lo que aprendiste en esta práctica

En esta práctica aplicaste por primera vez **GitHub Copilot Chat como herramienta de productividad general**, más allá de la generación de código. Los aprendizajes clave son:

| Concepto de la lección 1.1               | Cómo lo aplicaste en esta práctica                                  |
|------------------------------------------|---------------------------------------------------------------------|
| **Velocidad** (tiempo al primer borrador)| Copilot generó material inicial en segundos vs. minutos de búsqueda |
| **Calidad** (claridad, precisión)        | Iteraste con prompts de refinamiento y verificaste datos externos   |
| **Enfoque** (menos cambios de contexto) | Investigaste, estructuraste y redactaste sin salir de VS Code       |
| **Prompts estructurados**               | Aplicaste: Rol, Tarea, Contexto, Restricciones, Formato, Criterios  |
| **Validación humana**                   | Verificaste datos con fuentes externas antes de incluirlos          |
| **Iteración guiada**                    | Usaste prompts de seguimiento para profundizar y refinar            |

### Conexión con el curso

Esta práctica establece la **línea base de tu experiencia con Copilot Chat**. Las métricas y reflexiones que registraste hoy serán el punto de comparación para las prácticas avanzadas del Módulo 3 (especialmente las Prácticas 9 y 10), donde evaluarás tu evolución como desarrollador que trabaja con IA generativa.

### Recursos adicionales

- [GitHub Copilot Chat en VS Code — Documentación oficial](https://code.visualstudio.com/docs/copilot/copilot-chat)
- [Quantifying GitHub Copilot's impact on developer productivity — GitHub Research](https://github.blog/news-insights/research/quantifying-github-copilots-impact-on-developer-productivity-and-happiness/)
- [Ingeniería de prompts para Azure OpenAI — Microsoft Learn](https://learn.microsoft.com/es-es/azure/ai-services/openai/how-to/prompt-engineering)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [Métricas DORA para medir desempeño de entrega](https://dora.dev/)
- [Principios de IA Responsable de Microsoft](https://www.microsoft.com/es-es/ai/responsible-ai)

---

> **Recuerda:** Copilot Chat es un copiloto, no un piloto. La responsabilidad de la calidad, precisión y ética de tu trabajo siempre recae en ti como profesional. Esta práctica es el primer paso para desarrollar el criterio necesario para usar la IA de manera efectiva y responsable.

---
LAB_END---

---

# Utiliza Copilot Chat para automatizar una tarea repetitiva en tu código. Documenta el proceso y los resultados.

## Metadatos

| Campo            | Detalle                                      |
|------------------|----------------------------------------------|
| **Duración**     | 10 minutos (hasta 30 min en modo autónomo)   |
| **Complejidad**  | Fácil                                        |
| **Nivel Bloom**  | Aplicar (Apply)                              |
| **Módulo**       | 1 — Productividad con IA Generativa          |
| **Laboratorio**  | 01-00-02                                     |

---

## Descripción General

En esta práctica aplicarás directamente los conceptos de productividad con IA generativa vistos en la lección 1.1. Identificarás una tarea repetitiva típica del desarrollo de software —como generar pruebas unitarias para múltiples casos— y utilizarás Copilot Chat dentro de VS Code para automatizarla mediante prompts estructurados (Rol, Tarea, Contexto, Restricciones, Formato, Criterios de aceptación). Al finalizar, habrás ejecutado el código generado, verificado su funcionamiento y documentado el proceso completo, incluyendo una evaluación crítica de la calidad de la sugerencia recibida.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Identificar una tarea repetitiva concreta en un flujo de trabajo de codificación y justificar por qué es candidata a automatización con IA.
- [ ] Formular un prompt estructurado en Copilot Chat (Rol, Tarea, Contexto, Restricciones, Formato, Criterios) para generar código que automatice dicha tarea.
- [ ] Ejecutar y verificar el código generado por Copilot Chat utilizando las herramientas del entorno (Python/pytest o Node.js).
- [ ] Documentar el proceso de interacción con Copilot Chat y evaluar críticamente la calidad del código sugerido frente a buenas prácticas.

---

## Prerrequisitos

### Conocimiento previo

- Haber completado la **Práctica 1** del curso.
- Conocimiento básico de Python 3 o JavaScript/Node.js (sintaxis, funciones, ejecución en terminal).
- Haber leído la lección **1.1: Productividad con IA Generativa** y comprender la estructura de prompts recomendada.
- Familiaridad básica con el uso del panel de chat en VS Code.

### Acceso y cuentas

- Cuenta de **GitHub** con suscripción activa a **GitHub Copilot** (Individual, Team o Enterprise).
- Acceso a **Visual Studio Code** instalado y configurado en tu equipo.
- Extensión **GitHub Copilot Chat** instalada y autenticada en VS Code.
- Terminal con **Python 3.10+** o **Node.js 20 LTS** disponible.

---

## Entorno de Laboratorio

### Hardware recomendado

| Componente       | Mínimo                          | Recomendado                     |
|------------------|---------------------------------|---------------------------------|
| Procesador       | Intel Core i5 / AMD Ryzen 5 64-bit | Intel Core i7 / AMD Ryzen 7  |
| RAM              | 8 GB                            | 16 GB                           |
| Espacio en disco | 2 GB libres                     | 10 GB libres                    |
| Resolución       | 1280×768                        | 1920×1080                       |
| Conectividad     | 10 Mbps estable                 | 20 Mbps o superior              |

### Software requerido

| Herramienta                  | Versión mínima        | Propósito                                     |
|------------------------------|-----------------------|-----------------------------------------------|
| Visual Studio Code           | 1.90                  | Editor principal                              |
| GitHub Copilot Chat (ext.)   | Última disponible     | Asistente de IA conversacional                |
| Python                       | 3.10                  | Ejecución del código de práctica              |
| pytest                       | 7.x o superior        | Ejecución de pruebas unitarias                |
| pip                          | Incluido con Python   | Instalación de dependencias                   |
| Git                          | 2.40                  | Control de versiones                          |
| pylint o flake8              | pylint 3.x / flake8 7.x | Verificación de calidad del código         |
| Navegador web moderno        | Última versión estable | Acceso a documentación de referencia         |

> **Alternativa JavaScript:** Si prefieres Node.js, puedes usar `jest` o `vitest` en lugar de pytest. Los pasos del laboratorio incluyen variantes para ambos lenguajes donde aplique.

### Verificación del entorno (comandos de configuración)

Abre una terminal integrada en VS Code (**Terminal → New Terminal**) y ejecuta los siguientes comandos para confirmar que tu entorno está listo:

```bash
# Verificar Python
python --version
# Esperado: Python 3.10.x o superior

# Verificar pip
pip --version
# Esperado: pip 23.x o superior

# Instalar pytest si no está disponible
pip install pytest

# Verificar pytest
pytest --version
# Esperado: pytest 7.x o superior

# Instalar flake8 para linting
pip install flake8

# Verificar flake8
flake8 --version
# Esperado: 7.x o superior
```

```bash
# Alternativa Node.js — verificar entorno JavaScript
node --version
# Esperado: v20.x.x (LTS)

npm --version
# Esperado: 10.x o superior
```

```bash
# Verificar Git
git --version
# Esperado: git version 2.40.x o superior
```

```bash
# Verificar que Copilot Chat esté activo en VS Code
# En VS Code: View → Extensions → buscar "GitHub Copilot Chat"
# Debe aparecer como "Enabled" y sin errores de autenticación
```

---

## Pasos del Laboratorio

---

### Paso 1: Preparar el archivo de código base

**Objetivo:** Crear el archivo Python con la función de negocio que usaremos como punto de partida para la automatización, y preparar la estructura del proyecto.

#### Instrucciones

1. Abre **Visual Studio Code**.

2. Crea una carpeta nueva para este laboratorio. En la terminal integrada ejecuta:

   ```bash
   mkdir lab-01-00-02
   cd lab-01-00-02
   git init
   ```

3. Crea la estructura de archivos del proyecto:

   ```bash
   mkdir src tests
   touch src/__init__.py
   touch tests/__init__.py
   touch src/pricing.py
   touch tests/test_pricing.py
   touch notas_laboratorio.md
   ```

4. Abre `src/pricing.py` en VS Code y escribe (o copia) el siguiente código base:

   ```python
   # src/pricing.py
   """
   Módulo de cálculo de precios con descuentos por nivel de cliente.
   """

   def calculate_discount(amount, tier):
       """
       Devuelve el precio con descuento según el 'tier' del cliente.

       Args:
           amount (float): Monto original antes del descuento.
           tier (str): Nivel del cliente ('silver', 'gold', 'platinum').

       Returns:
           float: Precio final con descuento aplicado, redondeado a 2 decimales.

       Examples:
           >>> calculate_discount(100, 'gold')
           90.0
           >>> calculate_discount(200, 'silver')
           190.0
       """
       rates = {"silver": 0.05, "gold": 0.10, "platinum": 0.15}
       rate = rates.get(tier, 0.0)
       return round(amount * (1 - rate), 2)
   ```

5. Guarda el archivo con **Ctrl+S** (Windows/Linux) o **Cmd+S** (macOS).

6. Verifica que el archivo no tenga errores de sintaxis ejecutando:

   ```bash
   python -m py_compile src/pricing.py && echo "Sintaxis OK"
   ```

#### Salida esperada

```
Sintaxis OK
```

#### Verificación

- El archivo `src/pricing.py` existe y no produce errores al compilarse.
- La estructura del proyecto se ve así en el explorador de VS Code:

  ```
  lab-01-00-02/
  ├── src/
  │   ├── __init__.py
  │   └── pricing.py
  ├── tests/
  │   ├── __init__.py
  │   └── test_pricing.py
  └── notas_laboratorio.md
  ```

---

### Paso 2: Identificar la tarea repetitiva y diseñar el prompt

**Objetivo:** Reconocer qué parte del flujo de trabajo es repetitiva y formular un prompt estructurado siguiendo el modelo de la lección 1.1 (Rol, Tarea, Contexto, Restricciones, Formato, Criterios de aceptación).

#### Instrucciones

1. **Identifica la tarea repetitiva.** En este caso, la tarea es: *escribir manualmente múltiples pruebas unitarias para cada combinación de parámetros de `calculate_discount`*. Sin IA, un desarrollador tendría que escribir a mano cada `def test_...`, cubriendo tiers válidos, inválidos, valores límite y precisión de redondeo. Esto es repetitivo, propenso a omisiones y consume tiempo.

2. **Abre el panel de Copilot Chat** en VS Code:
   - Haz clic en el ícono de Copilot Chat en la barra lateral izquierda, **o**
   - Usa el atajo **Ctrl+Alt+I** (Windows/Linux) o **Cmd+Shift+I** (macOS), **o**
   - Ve a **View → Chat** en el menú.

3. **Asegúrate de tener `src/pricing.py` abierto** en el editor. Copilot Chat utilizará el archivo activo como parte del contexto.

4. Antes de enviar el prompt, **anota en `notas_laboratorio.md`** la descripción de la tarea repetitiva que identificaste. Usa esta plantilla:

   ```markdown
   ## Notas — Lab 01-00-02

   ### Tarea repetitiva identificada
   - **Descripción:** Escribir manualmente pruebas unitarias para cada caso de uso
     de la función `calculate_discount` (tiers válidos, inválidos, valores límite,
     redondeo).
   - **Por qué es repetitiva:** Cada caso de prueba sigue la misma estructura
     (arrange → act → assert), solo cambian los valores de entrada y salida esperada.
   - **Tiempo estimado sin IA:** 10–15 minutos para cubrir 8–10 casos.

   ### Prompt diseñado
   (completar en el siguiente paso)
   ```

5. **Diseña tu prompt estructurado.** Basándote en el modelo de la lección 1.1, construye el siguiente prompt (puedes ajustarlo según tu preferencia):

   ```
   Actúa como ingeniero de QA con experiencia en Python.
   Genera pruebas unitarias completas con pytest para la función
   `calculate_discount` definida en src/pricing.py (archivo activo).

   Cubre obligatoriamente estos casos:
   1. Tiers válidos: 'silver' (5%), 'gold' (10%), 'platinum' (15%).
   2. Tier inválido o desconocido: debe devolver el monto sin descuento.
   3. Valor límite: amount = 0.
   4. Valor negativo: amount = -50.
   5. Precisión de redondeo: amount = 99.99 con tier 'gold'.
   6. Tipo inesperado en tier: None como tier.

   Restricciones:
   - Usa pytest puro, sin fixtures externos ni librerías adicionales.
   - Nombres de test descriptivos en inglés (snake_case).
   - Compatible con Python 3.10+.
   - No repitas imports innecesarios.

   Formato de salida: un único bloque de código Python listo para guardar
   en tests/test_pricing.py y ejecutar con `pytest tests/`.

   Criterios de aceptación: todos los tests deben pasar con `pytest` sin
   modificaciones adicionales.
   ```

6. **Registra el prompt** en `notas_laboratorio.md` bajo la sección "Prompt diseñado".

#### Salida esperada

- Tienes el archivo `src/pricing.py` abierto en VS Code.
- El panel de Copilot Chat está visible.
- Has documentado la tarea repetitiva y el prompt diseñado en `notas_laboratorio.md`.

#### Verificación

- El prompt incluye los seis componentes del modelo de la lección: Rol, Tarea, Contexto (archivo activo), Restricciones, Formato y Criterios de aceptación.
- El archivo `notas_laboratorio.md` tiene contenido en las dos secciones indicadas.

---

### Paso 3: Enviar el prompt a Copilot Chat y obtener el código

**Objetivo:** Ejecutar la interacción con Copilot Chat, obtener el código generado y copiarlo al archivo de pruebas.

#### Instrucciones

1. En el panel de Copilot Chat, **pega o escribe el prompt** que diseñaste en el paso anterior.

   > **Consejo:** Si el panel de chat tiene un botón de adjuntar archivo (`@workspace` o `#file`), úsalo para referenciar explícitamente `src/pricing.py`. Escribe `#file:src/pricing.py` al inicio del prompt para asegurarte de que Copilot tenga el contexto correcto.

   Ejemplo con referencia explícita al archivo:
   ```
   #file:src/pricing.py

   Actúa como ingeniero de QA con experiencia en Python...
   (resto del prompt)
   ```

2. Presiona **Enter** para enviar el prompt.

3. **Espera la respuesta** de Copilot Chat. Debería aparecer un bloque de código Python con múltiples funciones `def test_...`.

4. **Lee la respuesta completa** antes de copiarla. Verifica visualmente que:
   - Hay al menos 6 funciones de test.
   - Cada función tiene un nombre descriptivo.
   - Se importa `pytest` y la función `calculate_discount`.
   - No hay referencias a fixtures o librerías externas no instaladas.

5. **Copia el código generado** y pégalo en `tests/test_pricing.py`. Puedes usar el botón "Copy" que aparece en el bloque de código dentro del chat, o seleccionar y copiar manualmente.

6. Guarda el archivo `tests/test_pricing.py` con **Ctrl+S**.

7. **Registra en `notas_laboratorio.md`** el código exacto que Copilot generó (cópialo tal cual, sin modificaciones aún):

   ```markdown
   ### Código generado por Copilot Chat (sin modificaciones)
   ```python
   # (pega aquí el código generado por Copilot)
   ```
   ```

#### Ejemplo de código que Copilot Chat típicamente genera

A continuación se muestra un ejemplo representativo de lo que Copilot Chat podría generar. **Tu resultado puede variar**; lo importante es evaluar lo que realmente recibas:

```python
# tests/test_pricing.py
"""
Unit tests for the calculate_discount function in src/pricing.py.
"""
import sys
import os

sys.path.insert(0, os.path.abspath(os.path.join(os.path.dirname(__file__), "..")))

from src.pricing import calculate_discount


def test_silver_tier_applies_5_percent_discount():
    assert calculate_discount(100, "silver") == 95.0


def test_gold_tier_applies_10_percent_discount():
    assert calculate_discount(100, "gold") == 90.0


def test_platinum_tier_applies_15_percent_discount():
    assert calculate_discount(100, "platinum") == 85.0


def test_unknown_tier_returns_full_amount():
    assert calculate_discount(100, "bronze") == 100.0


def test_zero_amount_returns_zero():
    assert calculate_discount(0, "gold") == 0.0


def test_negative_amount_applies_discount():
    assert calculate_discount(-50, "silver") == -47.5


def test_rounding_precision_with_gold_tier():
    assert calculate_discount(99.99, "gold") == 89.99


def test_none_tier_returns_full_amount():
    assert calculate_discount(100, None) == 100.0
```

> **Nota importante:** El código anterior es un ejemplo de referencia. Copilot Chat puede generar código diferente, con más o menos tests, con distintas estructuras de importación, o con enfoques alternativos. Tu tarea es evaluar lo que realmente recibas.

#### Salida esperada

- El archivo `tests/test_pricing.py` contiene el código generado por Copilot Chat.
- `notas_laboratorio.md` tiene el código original sin modificaciones registrado.

#### Verificación

- Ejecuta en la terminal:
  ```bash
  cat tests/test_pricing.py
  ```
  Debes ver el contenido del archivo con al menos 6 funciones de test.

---

### Paso 4: Ejecutar las pruebas y verificar el funcionamiento

**Objetivo:** Ejecutar el código generado por Copilot Chat con pytest para verificar que funciona correctamente, e identificar posibles fallos o ajustes necesarios.

#### Instrucciones

1. En la terminal integrada de VS Code, asegúrate de estar en la raíz del proyecto (`lab-01-00-02/`) y ejecuta:

   ```bash
   pytest tests/ -v
   ```

   La bandera `-v` (verbose) muestra el nombre de cada test y su resultado.

2. **Observa la salida.** Deberías ver algo similar a:

   ```
   ========================= test session starts ==========================
   platform linux -- Python 3.11.x, pytest-7.x.x
   collected 8 items

   tests/test_pricing.py::test_silver_tier_applies_5_percent_discount PASSED
   tests/test_pricing.py::test_gold_tier_applies_10_percent_discount PASSED
   tests/test_pricing.py::test_platinum_tier_applies_15_percent_discount PASSED
   tests/test_pricing.py::test_unknown_tier_returns_full_amount PASSED
   tests/test_pricing.py::test_zero_amount_returns_zero PASSED
   tests/test_pricing.py::test_negative_amount_applies_discount PASSED
   tests/test_pricing.py::test_rounding_precision_with_gold_tier PASSED
   tests/test_pricing.py::test_none_tier_returns_full_amount PASSED

   ========================== 8 passed in 0.12s ===========================
   ```

3. **Si algún test falla:** Anota el mensaje de error. Puede deberse a:
   - Un problema de importación (ruta de módulo incorrecta).
   - Un valor de retorno inesperado (diferencia en redondeo).
   - Un comportamiento de la función no contemplado en el prompt.

   En ese caso, **no modifiques el código aún**; primero regístralo como hallazgo en tus notas. Luego pasa al siguiente paso para ajustar.

4. **Si hay errores de importación**, verifica que el `sys.path` esté configurado correctamente en el archivo de test, o ejecuta pytest desde la raíz con:

   ```bash
   PYTHONPATH=. pytest tests/ -v
   ```

   En Windows (PowerShell):
   ```powershell
   $env:PYTHONPATH="."; pytest tests/ -v
   ```

5. Ejecuta también el linter para verificar la calidad del código generado:

   ```bash
   flake8 tests/test_pricing.py --max-line-length=100
   ```

6. **Registra los resultados en `notas_laboratorio.md`**:

   ```markdown
   ### Resultados de ejecución de pytest

   - **Comando ejecutado:** `pytest tests/ -v`
   - **Tests pasados:** X / Y
   - **Tests fallidos:** (lista si aplica)
   - **Errores de linting (flake8):** (lista si aplica)
   - **Observaciones:** (describe brevemente lo que observaste)
   ```

#### Salida esperada

```
========================== 8 passed in 0.12s ===========================
```

O, si hubo ajustes menores, todos los tests pasan después de las correcciones documentadas.

#### Verificación

- El comando `pytest tests/ -v` termina sin errores (`X passed`).
- `flake8` no reporta errores críticos (errores E, W) en el archivo generado, o los que reporta son menores y están documentados.

---

### Paso 5: Evaluar el código generado y documentar el proceso completo

**Objetivo:** Realizar una evaluación crítica del código generado por Copilot Chat comparándolo con buenas prácticas, identificar fortalezas y áreas de mejora, y completar la documentación del proceso.

#### Instrucciones

1. **Evalúa el código generado** usando la siguiente rúbrica. Para cada criterio, marca ✅ (cumple), ⚠️ (cumple parcialmente) o ❌ (no cumple) y añade una observación breve:

   | Criterio de evaluación                                        | Estado | Observación |
   |---------------------------------------------------------------|--------|-------------|
   | Cubre todos los casos solicitados en el prompt (6+ casos)     |        |             |
   | Nombres de test descriptivos y en snake_case                  |        |             |
   | No usa fixtures externos ni dependencias no instaladas        |        |             |
   | Importaciones correctas y sin redundancias                    |        |             |
   | Aserciones claras y directas (sin lógica condicional en test) |        |             |
   | Compatible con Python 3.10+ (sin sintaxis obsoleta)           |        |             |
   | Pasa flake8 sin errores críticos                              |        |             |
   | Todos los tests pasan con `pytest` sin modificaciones         |        |             |

2. **Identifica si realizaste modificaciones** al código generado. Si modificaste algo, documenta:
   - Qué cambiaste.
   - Por qué fue necesario el cambio.
   - Si el cambio fue por un error de Copilot, una mejora de estilo o una adaptación a tu entorno.

3. **Reflexiona sobre la automatización.** Responde estas preguntas en `notas_laboratorio.md`:

   ```markdown
   ### Evaluación de la automatización

   **¿Fue efectiva la automatización?**
   (Sí / No / Parcialmente — explica en 2–3 oraciones)

   **Tiempo estimado sin IA vs. con IA:**
   - Sin IA: ~___ minutos para escribir los tests manualmente.
   - Con IA: ~___ minutos usando Copilot Chat (incluyendo ajustes).
   - Ahorro estimado: ___ minutos.

   **Fortalezas del código generado:**
   1. ...
   2. ...

   **Áreas de mejora identificadas:**
   1. ...
   2. ...

   **¿Modificaste el código? ¿Por qué?**
   (describe aquí)

   **Lección aprendida sobre el uso de prompts estructurados:**
   (reflexión personal de 2–3 oraciones)
   ```

4. **Genera el mensaje de commit** para registrar tu trabajo. Puedes pedirle a Copilot Chat que te ayude con esto:

   En el panel de Copilot Chat, escribe:
   ```
   Redacta un mensaje de commit claro en inglés para los siguientes cambios:
   - Se añadió src/pricing.py con la función calculate_discount.
   - Se generaron tests unitarios en tests/test_pricing.py usando Copilot Chat.
   - Se documentó el proceso en notas_laboratorio.md.
   Usa el formato: tipo(alcance): descripción breve. Incluye un cuerpo con 2–3 puntos.
   ```

5. Ejecuta el commit con el mensaje sugerido (ajustándolo si es necesario):

   ```bash
   git add .
   git commit -m "feat(pricing): add calculate_discount with pytest coverage

   - Implement calculate_discount function with silver/gold/platinum tiers
   - Generate unit tests via Copilot Chat covering edge cases and rounding
   - Document automation process and evaluation in notas_laboratorio.md"
   ```

6. **Guarda todos los archivos** y verifica el estado del repositorio:

   ```bash
   git log --oneline
   git status
   ```

#### Salida esperada

```
# git log --oneline
a1b2c3d feat(pricing): add calculate_discount with pytest coverage

# git status
On branch main
nothing to commit, working tree clean
```

#### Verificación

- `notas_laboratorio.md` contiene las cuatro secciones completas:
  1. Tarea repetitiva identificada.
  2. Prompt diseñado.
  3. Código generado por Copilot Chat (sin modificaciones).
  4. Resultados de ejecución y evaluación.
- El repositorio tiene al menos un commit con todos los archivos.
- La rúbrica de evaluación está completada con al menos una observación por criterio.

---

## Validación y Pruebas

Ejecuta la siguiente secuencia de comandos para validar que todo el laboratorio está completo y funcional:

```bash
# 1. Verificar estructura del proyecto
echo "=== Estructura del proyecto ==="
ls -R lab-01-00-02/ 2>/dev/null || find . -type f | sort

# 2. Verificar sintaxis de ambos archivos Python
echo "=== Verificación de sintaxis ==="
python -m py_compile src/pricing.py && echo "src/pricing.py: OK"
python -m py_compile tests/test_pricing.py && echo "tests/test_pricing.py: OK"

# 3. Ejecutar todos los tests con reporte detallado
echo "=== Ejecución de tests ==="
pytest tests/ -v --tb=short

# 4. Verificar cobertura de casos (al menos 6 tests)
echo "=== Conteo de tests ==="
grep -c "^def test_" tests/test_pricing.py

# 5. Linting del código generado
echo "=== Linting ==="
flake8 src/pricing.py tests/test_pricing.py --max-line-length=100 --statistics

# 6. Verificar que el archivo de notas existe y tiene contenido
echo "=== Archivo de notas ==="
wc -l notas_laboratorio.md
```

**Criterios de éxito del laboratorio:**

| Criterio                                               | Resultado esperado                     |
|--------------------------------------------------------|----------------------------------------|
| `pytest tests/ -v` termina sin fallos                  | `X passed` (mínimo 6 tests)            |
| `grep -c "^def test_"` en test_pricing.py              | ≥ 6                                    |
| `flake8` sin errores críticos (E1xx, E2xx, E7xx)       | Exit code 0 o solo warnings menores    |
| `notas_laboratorio.md` tiene contenido                 | ≥ 20 líneas                            |
| `git log --oneline` muestra al menos 1 commit          | 1 commit registrado                    |

---

## Resolución de Problemas

### Problema 1: Error de importación al ejecutar pytest — `ModuleNotFoundError: No module named 'src'`

**Síntomas:**
```
ERROR tests/test_pricing.py - ModuleNotFoundError: No module named 'src'
```
Pytest no puede encontrar el módulo `src.pricing` al ejecutar los tests.

**Causa:**
El directorio raíz del proyecto no está en el `PYTHONPATH`, por lo que Python no puede resolver la importación relativa `from src.pricing import calculate_discount`. Esto ocurre cuando pytest se ejecuta sin configuración de ruta o cuando el archivo de test no incluye el ajuste de `sys.path`.

**Solución:**

Opción A — Variable de entorno (recomendada para desarrollo):
```bash
# Linux / macOS
PYTHONPATH=. pytest tests/ -v

# Windows (PowerShell)
$env:PYTHONPATH="."; pytest tests/ -v

# Windows (CMD)
set PYTHONPATH=. && pytest tests/ -v
```

Opción B — Archivo `conftest.py` en la raíz (solución permanente):
```bash
# Crear conftest.py en la raíz del proyecto
cat > conftest.py << 'EOF'
import sys
import os
sys.path.insert(0, os.path.abspath(os.path.dirname(__file__)))
EOF

# Ahora pytest funciona directamente
pytest tests/ -v
```

Opción C — Archivo `pytest.ini` o `pyproject.toml`:
```ini
# pytest.ini
[pytest]
pythonpath = .
```

Después de aplicar cualquiera de estas opciones, vuelve a ejecutar `pytest tests/ -v`.

---

### Problema 2: Copilot Chat no responde o genera código incompleto / sin contexto del archivo

**Síntomas:**
- Copilot Chat responde con código genérico que no hace referencia a `calculate_discount`.
- La respuesta es un mensaje de error de conectividad o un texto vacío.
- El código generado importa funciones o librerías que no existen en el proyecto.

**Causa:**
Existen dos causas posibles: (a) el archivo `src/pricing.py` no estaba activo/abierto en el editor cuando se envió el prompt, por lo que Copilot no tuvo contexto del código real; o (b) hay un problema de conectividad o autenticación con el servicio de GitHub Copilot.

**Solución:**

Para el problema de contexto:
```
1. Haz clic en la pestaña de src/pricing.py en el editor para asegurarte
   de que sea el archivo activo.

2. En el prompt, usa la referencia explícita al archivo:
   #file:src/pricing.py
   (escríbelo al inicio del mensaje en el panel de chat)

3. Alternativamente, selecciona todo el contenido de src/pricing.py
   (Ctrl+A), luego haz clic derecho → "Copilot: Explain This" para
   verificar que Copilot puede leer el archivo; si funciona, repite
   el prompt de generación de tests.
```

Para el problema de conectividad o autenticación:
```bash
# 1. Verifica tu conexión a internet
ping github.com

# 2. En VS Code, verifica el estado de Copilot:
#    - Clic en el ícono de Copilot en la barra de estado (parte inferior)
#    - Debe decir "GitHub Copilot: Ready"
#    - Si dice "Sign in", vuelve a autenticarte con tu cuenta GitHub

# 3. Recarga la ventana de VS Code si el problema persiste:
#    Ctrl+Shift+P → "Developer: Reload Window"

# 4. Si el problema continúa, usa el código de ejemplo del Paso 3
#    como respaldo y documenta el inconveniente en tus notas.
```

> **Nota para el instructor:** Si hay problemas generalizados de conectividad en el aula, el código de ejemplo del Paso 3 de este laboratorio puede usarse como respaldo para continuar con los pasos de ejecución y evaluación.

---

## Limpieza

Al finalizar el laboratorio, no es necesario eliminar los archivos generados, ya que serán útiles como referencia en prácticas posteriores (especialmente las Prácticas 7, 8 y 9 del Módulo 3). Sin embargo, realiza los siguientes pasos de organización:

```bash
# 1. Asegúrate de que todos los cambios están commiteados
git status
# Debe mostrar: "nothing to commit, working tree clean"

# 2. Si hay cambios pendientes, commitéalos
git add .
git commit -m "chore: finalize lab 01-00-02 documentation and cleanup"

# 3. Verifica el historial del repositorio
git log --oneline

# 4. Opcional: desactiva el entorno virtual si usaste uno
# deactivate  # (solo si usaste virtualenv o venv)

# 5. Cierra los paneles innecesarios en VS Code
# View → Close All Editors (solo si vas a continuar con otra práctica)
```

**Archivos que debes conservar para prácticas futuras:**

| Archivo                        | Por qué conservarlo                                              |
|--------------------------------|------------------------------------------------------------------|
| `src/pricing.py`               | Código base que puede extenderse en prácticas posteriores        |
| `tests/test_pricing.py`        | Suite de tests de referencia para comparaciones futuras          |
| `notas_laboratorio.md`         | Diario de aprendizaje requerido en Prácticas 9 y 10             |

---

## Resumen

En esta práctica aplicaste el ciclo completo de productividad con IA generativa descrito en la lección 1.1:

1. **Identificaste** una tarea repetitiva concreta (escritura manual de pruebas unitarias) y justificaste por qué es candidata a automatización.
2. **Formulaste un prompt estructurado** usando los seis componentes del modelo (Rol, Tarea, Contexto, Restricciones, Formato, Criterios de aceptación), comprobando que la especificidad del prompt impacta directamente la calidad de la respuesta.
3. **Ejecutaste y verificaste** el código generado con `pytest` y `flake8`, practicando la validación humana como parte esencial del flujo de trabajo con IA — *copiloto, no piloto*.
4. **Documentaste y evaluaste críticamente** el proceso, identificando fortalezas del código generado, áreas de mejora y el ahorro de tiempo real obtenido.

### Conceptos clave reforzados

- **Velocidad + Calidad + Enfoque:** La automatización con Copilot Chat no solo ahorró tiempo de escritura, sino que redujo el riesgo de omitir casos límite importantes.
- **Iteración guiada:** Si el primer resultado no fue perfecto, el ciclo "solicitar → revisar → aclarar → ajustar" permitió llegar a un código de calidad.
- **Validación humana obligatoria:** Ninguna sugerencia de IA debe aceptarse sin ejecutarla y revisarla con criterio profesional.
- **Documentación como práctica:** El archivo `notas_laboratorio.md` es parte del entregable, no un paso opcional.

### Recursos adicionales

- [GitHub Copilot Chat en VS Code — Documentación oficial](https://code.visualstudio.com/docs/copilot/copilot-chat)
- [Pytest — Documentación oficial](https://docs.pytest.org/en/stable/)
- [Ingeniería de prompts para Azure OpenAI — Microsoft Learn](https://learn.microsoft.com/es-es/azure/ai-services/openai/how-to/prompt-engineering)
- [Quantifying GitHub Copilot's impact on developer productivity (GitHub Research)](https://github.blog/news-insights/research/quantifying-github-copilots-impact-on-developer-productivity-and-happiness/)
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework)
- [Métricas DORA para medir desempeño de entrega](https://dora.dev/)

---

> **Recuerda:** Conserva tu archivo `notas_laboratorio.md` actualizado. Las prácticas del Módulo 3 (Prácticas 7, 8 y 9) requieren que reflexiones sobre las experiencias acumuladas en esta y otras prácticas anteriores.

---

# Realiza una comparación de tiempo entre escribir un fragmento de código manualmente y utilizar Copilot Chat para completarlo.

## Metadatos

| Campo            | Detalle                                      |
|------------------|----------------------------------------------|
| **Duración**     | 10 minutos (clase) / hasta 20 minutos autónomo |
| **Complejidad**  | Media                                        |
| **Nivel Bloom**  | Aplicar (Apply)                              |
| **Módulo**       | 1 — Productividad con IA Generativa          |
| **Práctica**     | 3 de 10                                      |

---

## Descripción General

En esta práctica realizarás un **experimento controlado de productividad**: implementarás la misma tarea de codificación dos veces —primero de forma completamente manual y luego con asistencia de GitHub Copilot Chat— midiendo el tiempo en cada caso. Los datos que recopiles te permitirán formular conclusiones propias y basadas en evidencia sobre el impacto real de la IA generativa en tu flujo de trabajo, conectando directamente con el concepto de productividad tridimensional (velocidad, calidad y enfoque) presentado en la lección 1.1.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Medir el tiempo requerido para escribir un fragmento de código de complejidad media de forma manual versus con Copilot Chat.
- [ ] Analizar las diferencias en productividad entre el desarrollo asistido por IA y el desarrollo tradicional usando datos propios.
- [ ] Evaluar la calidad del código producido en ambas modalidades aplicando criterios objetivos (legibilidad, manejo de errores, cobertura de casos).
- [ ] Formular conclusiones personales y fundamentadas sobre el impacto de Copilot Chat en la velocidad de desarrollo.

---

## Prerrequisitos

### Conocimiento previo
- Haber completado la **Práctica 1** (configuración inicial de VS Code + Copilot Chat) y la **Práctica 2** (primer uso de Copilot Chat con prompts básicos).
- Familiaridad básica con Python (u otro lenguaje compatible con Copilot Chat).
- Comprensión del concepto de productividad tridimensional (velocidad, calidad, enfoque) visto en la lección 1.1.

### Acceso y herramientas
- Cuenta de GitHub con suscripción activa a **GitHub Copilot** (individual, Teams o Enterprise).
- **VS Code 1.90 o superior** con la extensión **GitHub Copilot Chat** instalada y autenticada.
- **Python 3.10 o superior** instalado y accesible desde la terminal integrada.
- Cronómetro (el del teléfono móvil es suficiente) o cualquier herramienta de medición de tiempo.
- Archivo de notas o diario de aprendizaje (Word, Google Docs, Notion, etc.) para registrar resultados.

---

## Entorno de Laboratorio

### Tabla de software requerido

| Herramienta                  | Versión mínima       | Propósito                                 |
|------------------------------|----------------------|-------------------------------------------|
| Visual Studio Code           | 1.90                 | Editor principal                          |
| GitHub Copilot Chat (ext.)   | Última disponible    | Asistencia IA conversacional              |
| Python                       | 3.10                 | Lenguaje de implementación                |
| pylint o flake8 (opcional)   | pylint 3.x / flake8 7.x | Verificación de calidad de código    |
| Navegador web moderno        | Última versión estable | Acceso a GitHub si es necesario         |

### Verificación rápida del entorno

Abre la terminal integrada de VS Code (**Ctrl + `**) y ejecuta los siguientes comandos para confirmar que el entorno está listo:

```bash
# Verificar versión de Python
python --version

# Verificar que pylint está disponible (opcional pero recomendado)
pylint --version

# Verificar que Git está disponible
git --version
```

Si alguno de estos comandos falla, consulta la sección de **Solución de Problemas** al final de esta guía.

### Preparación del directorio de trabajo

```bash
# Crear directorio para la práctica (si no existe ya)
mkdir -p lab-copilot-comparacion
cd lab-copilot-comparacion

# Crear los archivos que usarás en la práctica
touch procesador_csv_manual.py
touch procesador_csv_copilot.py
touch resultados_comparacion.md
```

> **Nota:** Si prefieres usar otro lenguaje (JavaScript, Java, C#, TypeScript), los pasos son equivalentes; adapta los nombres de archivo y comandos de ejecución según corresponda.

---

## Pasos del Laboratorio

---

### Paso 1 — Definir la tarea de codificación y preparar el experimento

**Objetivo:** Establecer una tarea de complejidad media que sea idéntica en ambas rondas del experimento, garantizando condiciones comparables.

#### Instrucciones

1. Abre VS Code y navega al directorio `lab-copilot-comparacion` que creaste en la preparación.

2. Lee con atención la especificación de la tarea que implementarás en ambas rondas:

   > **Tarea:** Implementar una función llamada `procesar_ventas_csv` en Python que:
   > - Reciba como parámetro una lista de diccionarios (cada diccionario representa una fila de un CSV de ventas con los campos: `producto`, `cantidad`, `precio_unitario`, `descuento_pct`).
   > - Calcule el **total neto** de cada fila: `cantidad × precio_unitario × (1 - descuento_pct / 100)`.
   > - Retorne un diccionario con:
   >   - `"resumen"`: lista de diccionarios con `producto` y `total_neto` (redondeado a 2 decimales).
   >   - `"total_general"`: suma de todos los totales netos (redondeado a 2 decimales).
   >   - `"producto_top"`: nombre del producto con mayor total neto.
   > - Manejar casos borde: lista vacía, valores negativos en `cantidad` o `precio_unitario` (lanzar `ValueError`), descuento fuera del rango 0-100 (lanzar `ValueError`).

3. Abre tu archivo de notas y crea una **tabla de registro** con el siguiente formato:

   ```
   | Métrica                          | Manual | Con Copilot Chat |
   |----------------------------------|--------|-----------------|
   | Tiempo total (segundos)          |        |                 |
   | Líneas de código escritas        |        |                 |
   | Número de errores de ejecución   |        |                 |
   | Casos borde cubiertos (de 3)     |        |                 |
   | Legibilidad (1-5 subjetivo)      |        |                 |
   ```

4. Cierra cualquier archivo de código existente para evitar distracciones. Asegúrate de que el panel de Copilot Chat esté **cerrado** durante la ronda manual.

#### Resultado esperado

- Tienes clara la especificación de la tarea.
- Tu tabla de registro está lista en el archivo de notas.
- VS Code está abierto con `procesador_csv_manual.py` listo para editar.
- El panel de Copilot Chat está cerrado.

#### Verificación

Confirma que el archivo existe y está vacío:

```bash
# Debe mostrar 0 bytes
wc -c procesador_csv_manual.py
```

---

### Paso 2 — Ronda 1: Implementación manual (sin Copilot Chat)

**Objetivo:** Escribir la función `procesar_ventas_csv` completamente de forma manual, midiendo el tiempo con precisión.

#### Instrucciones

1. **Antes de escribir la primera línea de código**, inicia el cronómetro. Anota la hora de inicio en tu tabla de registro.

2. Abre `procesador_csv_manual.py` en VS Code y escribe el código **completamente a mano**, sin ninguna asistencia de IA. No uses Copilot Chat, no copies código de internet.

   > **Referencia de implementación esperada** (no copies esto directamente; úsalo solo como guía de lo que debes implementar por tu cuenta):
   >
   > La función debe incluir: validaciones de entrada, el cálculo del total neto por fila, la construcción del resumen, el cálculo del total general y la identificación del producto top.

3. Cuando hayas terminado de escribir el código y estés satisfecho con la implementación, **detén el cronómetro** y registra el tiempo en segundos en tu tabla.

4. Ejecuta el código con un conjunto de datos de prueba para verificar que funciona:

   ```bash
   python procesador_csv_manual.py
   ```

   Si necesitas un bloque de prueba rápido al final de tu archivo, puedes usar este fragmento de datos (escríbelo manualmente):

   ```python
   # Bloque de prueba — escríbelo al final de procesador_csv_manual.py
   if __name__ == "__main__":
       datos = [
           {"producto": "Laptop", "cantidad": 2, "precio_unitario": 1500.00, "descuento_pct": 10},
           {"producto": "Mouse", "cantidad": 5, "precio_unitario": 25.00, "descuento_pct": 0},
           {"producto": "Monitor", "cantidad": 1, "precio_unitario": 800.00, "descuento_pct": 15},
       ]
       resultado = procesar_ventas_csv(datos)
       print(resultado)
   ```

5. Registra en tu tabla:
   - **Tiempo total** (en segundos).
   - **Líneas de código** escritas (puedes contarlas con `wc -l procesador_csv_manual.py`).
   - **Número de errores** de ejecución que encontraste antes de que funcionara correctamente.
   - **Casos borde cubiertos** (¿manejaste lista vacía, valores negativos, descuento fuera de rango?).
   - **Legibilidad subjetiva** (del 1 al 5, siendo 5 muy legible).

#### Resultado esperado

El programa debe imprimir algo similar a:

```
{
  'resumen': [
    {'producto': 'Laptop', 'total_neto': 2700.0},
    {'producto': 'Mouse', 'total_neto': 125.0},
    {'producto': 'Monitor', 'total_neto': 680.0}
  ],
  'total_general': 3505.0,
  'producto_top': 'Laptop'
}
```

#### Verificación

```bash
# Contar líneas del archivo manual
wc -l procesador_csv_manual.py

# Ejecutar y verificar que no hay errores de Python
python procesador_csv_manual.py && echo "Ejecución exitosa"
```

> **Importante:** Tómate el tiempo que necesites en esta ronda. El objetivo no es ser rápido; es obtener una medición honesta de tu velocidad natural de codificación.

---

### Paso 3 — Ronda 2: Implementación con Copilot Chat

**Objetivo:** Implementar la misma función utilizando GitHub Copilot Chat como asistente, midiendo el tiempo y documentando el proceso de interacción.

#### Instrucciones

1. Abre el archivo `procesador_csv_copilot.py` en VS Code. Asegúrate de que esté vacío.

2. Abre el panel de **GitHub Copilot Chat**:
   - Atajo de teclado: **Ctrl + Alt + I** (Windows/Linux) o **Cmd + Opt + I** (macOS).
   - O haz clic en el ícono de Copilot Chat en la barra lateral izquierda.

3. **Inicia el cronómetro** en este momento.

4. En el panel de Copilot Chat, escribe el siguiente prompt estructurado (basado en la estructura de la lección 1.1: Rol, Tarea, Contexto, Restricciones, Formato, Criterios):

   ```
   Actúa como desarrollador Python senior.

   Tarea: Implementa una función llamada `procesar_ventas_csv` en Python.

   Contexto: La función recibe una lista de diccionarios, donde cada diccionario
   representa una fila de un CSV de ventas con los campos:
   - producto (str)
   - cantidad (int o float)
   - precio_unitario (float)
   - descuento_pct (float, porcentaje entre 0 y 100)

   La función debe:
   1. Calcular el total neto de cada fila: cantidad × precio_unitario × (1 - descuento_pct / 100)
   2. Retornar un diccionario con:
      - "resumen": lista de dicts con "producto" y "total_neto" (redondeado a 2 decimales)
      - "total_general": suma de todos los totales netos (redondeado a 2 decimales)
      - "producto_top": nombre del producto con mayor total neto

   Restricciones:
   - Manejar lista vacía (retornar estructura vacía sin error)
   - Lanzar ValueError si cantidad o precio_unitario son negativos
   - Lanzar ValueError si descuento_pct está fuera del rango 0-100
   - Python 3.10+, sin dependencias externas

   Formato de salida: Solo el código Python listo para ejecutar, con docstring y
   comentarios inline donde sea útil. Incluye un bloque if __name__ == "__main__"
   con los mismos datos de prueba que usé antes:
   [{"producto": "Laptop", "cantidad": 2, "precio_unitario": 1500.00, "descuento_pct": 10},
    {"producto": "Mouse", "cantidad": 5, "precio_unitario": 25.00, "descuento_pct": 0},
    {"producto": "Monitor", "cantidad": 1, "precio_unitario": 800.00, "descuento_pct": 15}]

   Criterios de aceptación: El código debe ejecutarse sin errores y producir el
   resultado correcto para los datos de prueba.
   ```

5. Revisa la respuesta de Copilot Chat. Si el código parece correcto y completo, cópialo a `procesador_csv_copilot.py` usando el botón **"Insert into file"** o copiando y pegando manualmente.

6. Si la respuesta tiene algún aspecto que quieres mejorar, realiza **una iteración de refinamiento** en Copilot Chat. Por ejemplo:

   ```
   El código funciona, pero ¿puedes agregar type hints a todos los parámetros
   y al valor de retorno de la función?
   ```

7. Una vez que el código esté en el archivo y estés satisfecho, **detén el cronómetro**.

8. Ejecuta el código para verificar que funciona:

   ```bash
   python procesador_csv_copilot.py
   ```

9. Registra en tu tabla los mismos campos que en la ronda manual:
   - **Tiempo total** (en segundos).
   - **Líneas de código** en el archivo final.
   - **Número de errores** de ejecución antes de que funcionara.
   - **Casos borde cubiertos** (¿cuántos de los 3 maneja Copilot por defecto?).
   - **Legibilidad subjetiva** (del 1 al 5).

#### Resultado esperado

El programa debe producir el mismo resultado que la versión manual:

```
{
  'resumen': [
    {'producto': 'Laptop', 'total_neto': 2700.0},
    {'producto': 'Mouse', 'total_neto': 125.0},
    {'producto': 'Monitor', 'total_neto': 680.0}
  ],
  'total_general': 3505.0,
  'producto_top': 'Laptop'
}
```

#### Verificación

```bash
# Contar líneas del archivo generado con Copilot
wc -l procesador_csv_copilot.py

# Ejecutar y verificar que no hay errores
python procesador_csv_copilot.py && echo "Ejecución exitosa"

# Comparar número de líneas entre ambas versiones
echo "Manual: $(wc -l < procesador_csv_manual.py) líneas"
echo "Copilot: $(wc -l < procesador_csv_copilot.py) líneas"
```

---

### Paso 4 — Comparar resultados y redactar conclusiones

**Objetivo:** Analizar los datos recopilados, completar la tabla comparativa y formular conclusiones fundamentadas sobre el impacto de Copilot Chat en la productividad.

#### Instrucciones

1. Abre tu archivo de notas y completa la tabla de registro con todos los datos de ambas rondas. Debería verse similar a esto (los valores son ejemplos; los tuyos serán diferentes):

   ```
   | Métrica                          | Manual | Con Copilot Chat |
   |----------------------------------|--------|-----------------|
   | Tiempo total (segundos)          |  420   |       95        |
   | Líneas de código escritas        |   38   |       52        |
   | Número de errores de ejecución   |    2   |        0        |
   | Casos borde cubiertos (de 3)     |    2   |        3        |
   | Legibilidad (1-5 subjetivo)      |    3   |        4        |
   ```

2. Calcula el **factor de aceleración** de tiempo:

   ```
   Factor de aceleración = Tiempo Manual / Tiempo Copilot Chat
   ```

   Ejemplo: 420 / 95 ≈ 4.4× más rápido con Copilot Chat.

3. En tu archivo de notas, abre `resultados_comparacion.md` y redacta una reflexión de al menos **5 oraciones** respondiendo las siguientes preguntas guía:

   - ¿Cuánto más rápido (o más lento) fuiste con Copilot Chat? ¿Qué factores explican esa diferencia?
   - ¿El código generado por Copilot Chat cubrió todos los casos borde especificados? ¿Fue necesario corregirlo?
   - ¿En qué aspectos fue mejor el código de Copilot Chat que el tuyo? ¿En qué aspectos fue peor o igual?
   - ¿Cuál fue el mayor desafío al usar Copilot Chat? (¿redactar el prompt? ¿evaluar la respuesta? ¿integrar el código?)
   - Basándote en la lección 1.1, ¿en cuál de las tres dimensiones (velocidad, calidad, enfoque) notaste el mayor impacto? ¿Por qué?

4. Guarda el archivo `resultados_comparacion.md`. Lo necesitarás en prácticas posteriores (especialmente en las Prácticas 9 y 10).

5. **Opcional pero recomendado:** Si tienes pylint o flake8 instalado, ejecuta el linter en ambos archivos para obtener una métrica objetiva de calidad:

   ```bash
   # Analizar calidad del código manual
   pylint procesador_csv_manual.py --score=yes

   # Analizar calidad del código generado con Copilot
   pylint procesador_csv_copilot.py --score=yes
   ```

   Registra las puntuaciones en tu tabla de resultados como una métrica adicional de calidad.

#### Resultado esperado

- La tabla comparativa está completamente llena con datos reales de tu experimento.
- El archivo `resultados_comparacion.md` contiene tu reflexión personal fundamentada en datos.
- Tienes una comprensión propia y basada en evidencia del impacto de Copilot Chat en tu productividad.

#### Verificación

```bash
# Verificar que ambos archivos de código existen y tienen contenido
ls -lh procesador_csv_manual.py procesador_csv_copilot.py

# Verificar que el archivo de resultados tiene contenido
wc -l resultados_comparacion.md
```

---

## Validación y Pruebas

Para confirmar que la práctica fue completada correctamente, verifica los siguientes criterios:

### Lista de verificación de completitud

```bash
# 1. Verificar que ambos archivos Python existen y son ejecutables
python procesador_csv_manual.py && echo "✅ Versión manual: OK"
python procesador_csv_copilot.py && echo "✅ Versión Copilot: OK"

# 2. Verificar que ambas versiones producen el mismo resultado
python -c "
import subprocess, sys

r1 = subprocess.run([sys.executable, 'procesador_csv_manual.py'], capture_output=True, text=True)
r2 = subprocess.run([sys.executable, 'procesador_csv_copilot.py'], capture_output=True, text=True)

if r1.stdout.strip() == r2.stdout.strip():
    print('✅ Ambas versiones producen el mismo resultado')
else:
    print('⚠️  Las versiones producen resultados diferentes — revisa la implementación')
    print('Manual:', r1.stdout.strip())
    print('Copilot:', r2.stdout.strip())
"
```

### Prueba de casos borde

Crea un archivo temporal de prueba para verificar el manejo de errores en ambas versiones:

```python
# Guarda como test_casos_borde.py y ejecuta con: python test_casos_borde.py
import sys

def probar_archivo(nombre_modulo, archivo):
    """Prueba los casos borde de una implementación."""
    import importlib.util
    spec = importlib.util.spec_from_file_location(nombre_modulo, archivo)
    mod = importlib.util.module_from_spec(spec)
    spec.loader.exec_module(mod)
    fn = mod.procesar_ventas_csv

    pruebas_pasadas = 0

    # Caso 1: Lista vacía
    try:
        resultado = fn([])
        assert resultado["total_general"] == 0 or resultado == {"resumen": [], "total_general": 0.0, "producto_top": None}
        print(f"  ✅ {nombre_modulo}: Lista vacía manejada correctamente")
        pruebas_pasadas += 1
    except Exception as e:
        print(f"  ❌ {nombre_modulo}: Lista vacía — {e}")

    # Caso 2: Cantidad negativa debe lanzar ValueError
    try:
        fn([{"producto": "X", "cantidad": -1, "precio_unitario": 100, "descuento_pct": 0}])
        print(f"  ❌ {nombre_modulo}: No lanzó ValueError para cantidad negativa")
    except ValueError:
        print(f"  ✅ {nombre_modulo}: ValueError para cantidad negativa")
        pruebas_pasadas += 1
    except Exception as e:
        print(f"  ⚠️  {nombre_modulo}: Excepción inesperada para cantidad negativa — {e}")

    # Caso 3: Descuento fuera de rango debe lanzar ValueError
    try:
        fn([{"producto": "X", "cantidad": 1, "precio_unitario": 100, "descuento_pct": 110}])
        print(f"  ❌ {nombre_modulo}: No lanzó ValueError para descuento > 100")
    except ValueError:
        print(f"  ✅ {nombre_modulo}: ValueError para descuento fuera de rango")
        pruebas_pasadas += 1
    except Exception as e:
        print(f"  ⚠️  {nombre_modulo}: Excepción inesperada para descuento fuera de rango — {e}")

    return pruebas_pasadas

print("=== Pruebas de casos borde ===\n")
print("Versión Manual:")
p1 = probar_archivo("manual", "procesador_csv_manual.py")
print(f"  → {p1}/3 casos borde cubiertos\n")

print("Versión Copilot Chat:")
p2 = probar_archivo("copilot", "procesador_csv_copilot.py")
print(f"  → {p2}/3 casos borde cubiertos\n")

print(f"Diferencia en cobertura de casos borde: {p2 - p1:+d} a favor de {'Copilot' if p2 > p1 else 'Manual' if p1 > p2 else 'ninguno (empate)'}")
```

```bash
python test_casos_borde.py
```

---

## Solución de Problemas

### Problema 1: GitHub Copilot Chat no responde o muestra "Unable to connect"

**Síntomas:**
- El panel de Copilot Chat muestra un error de conexión.
- Los mensajes enviados al chat quedan en estado de carga indefinida.
- Aparece el mensaje "GitHub Copilot is not connected" en la barra de estado de VS Code.

**Causa:**
La extensión de GitHub Copilot Chat requiere conexión activa a internet y autenticación válida con GitHub. El problema puede deberse a sesión expirada, red bloqueada o suscripción inactiva.

**Solución:**
1. Verifica tu conexión a internet (mínimo 10 Mbps recomendado).
2. En VS Code, abre la paleta de comandos (**Ctrl + Shift + P**) y ejecuta `GitHub Copilot: Sign Out`, luego `GitHub Copilot: Sign In` para renovar la sesión.
3. Verifica que tu suscripción está activa en [github.com/settings/copilot](https://github.com/settings/copilot).
4. Si el problema persiste en un entorno de clase con red corporativa, es posible que un firewall esté bloqueando `*.githubcopilot.com`. Solicita al instructor los ejemplos de código pre-generados de respaldo.
5. Como alternativa temporal, puedes completar la ronda con Copilot Chat usando únicamente el autocompletado en línea (sin el panel de chat) escribiendo el inicio de la función y dejando que Copilot sugiera el resto con **Tab**.

---

### Problema 2: Python no se encuentra o la versión es incompatible

**Síntomas:**
- El comando `python --version` devuelve `command not found` o muestra una versión anterior a 3.10.
- Al ejecutar los archivos `.py` aparece un error de sintaxis relacionado con características modernas de Python.
- VS Code muestra "Select Python Interpreter" en la barra de estado sin un intérprete activo.

**Causa:**
Python no está instalado, no está en el PATH del sistema, o VS Code está usando un intérprete de una versión diferente a la esperada.

**Solución:**
1. Verifica si Python está disponible con un nombre alternativo:
   ```bash
   python3 --version
   # En Windows también puede ser:
   py --version
   ```
2. Si Python no está instalado, descárgalo desde [python.org](https://python.org) e instala la versión 3.10 o superior. En Windows, marca la opción **"Add Python to PATH"** durante la instalación.
3. En VS Code, selecciona el intérprete correcto:
   - Abre la paleta de comandos (**Ctrl + Shift + P**).
   - Escribe `Python: Select Interpreter` y elige la versión 3.10+.
4. Si la práctica es urgente y no puedes instalar Python, puedes usar **JavaScript/Node.js** como alternativa: la tarea de codificación es equivalente en cualquier lenguaje compatible con Copilot Chat.

---

## Limpieza

Al finalizar la práctica, organiza los archivos generados para que estén disponibles en prácticas futuras:

```bash
# Verificar el contenido del directorio de trabajo
ls -lh lab-copilot-comparacion/

# Estructura esperada al finalizar:
# procesador_csv_manual.py      — Implementación manual
# procesador_csv_copilot.py     — Implementación con Copilot Chat
# resultados_comparacion.md     — Tabla y reflexiones
# test_casos_borde.py           — Script de validación (opcional)
```

> **No elimines estos archivos.** Las prácticas 7, 8, 9 y 10 pueden requerir que consultes tus anotaciones y código de esta práctica. Guarda el directorio `lab-copilot-comparacion` en tu repositorio local o en tu diario de aprendizaje.

```bash
# Opcional: si usas Git, registra el trabajo realizado
git add procesador_csv_manual.py procesador_csv_copilot.py resultados_comparacion.md
git commit -m "lab 01-00-03: comparación productividad manual vs Copilot Chat

- Implementación manual: tiempo registrado, casos borde documentados
- Implementación con Copilot Chat: prompt estructurado, iteración de refinamiento
- Tabla comparativa y reflexiones en resultados_comparacion.md

Co-authored-by: GitHub Copilot <copilot@github.com>"
```

---

## Resumen

### Lo que realizaste en esta práctica

En esta práctica ejecutaste un **experimento controlado de productividad** con dos condiciones comparables: implementación manual e implementación asistida por Copilot Chat. Mediste tiempo, calidad y cobertura de casos borde, y tradujiste esos datos en conclusiones personales y fundamentadas.

### Conceptos clave aplicados

| Concepto de la lección 1.1                  | Cómo lo aplicaste en esta práctica                                                        |
|---------------------------------------------|-------------------------------------------------------------------------------------------|
| **Productividad tridimensional**            | Mediste las tres dimensiones: velocidad (tiempo), calidad (errores, casos borde) y enfoque (interrupciones al codificar) |
| **Prompt estructurado**                     | Usaste la estructura Rol–Tarea–Contexto–Restricciones–Formato–Criterios en la ronda con Copilot Chat |
| **Iteración guiada**                        | Realizaste al menos un ciclo de refinamiento del prompt para mejorar el resultado inicial  |
| **Validación humana**                       | Ejecutaste el código, probaste casos borde y evaluaste la calidad antes de aceptar el resultado |
| **Métricas de impacto**                     | Registraste tiempo al primer borrador, defectos y cobertura como métricas reales de productividad |

### Reflexión final

Los datos que recopilaste son únicos y personales: reflejan tu nivel actual de experiencia, tu familiaridad con el lenguaje y tu capacidad para redactar prompts efectivos. No existe un resultado "correcto"; el valor está en haber medido con honestidad y en haber formulado conclusiones propias. A medida que avances en el curso y tu habilidad con Copilot Chat mejore, el factor de aceleración tenderá a aumentar — especialmente cuando domines la redacción de prompts contextualizados.

### Recursos adicionales

- [Quantifying GitHub Copilot's impact on developer productivity (GitHub Research)](https://github.blog/news-insights/research/quantifying-github-copilots-impact-on-developer-productivity-and-happiness/) — Estudio de referencia sobre impacto en productividad.
- [GitHub Copilot Chat en VS Code — Documentación oficial](https://code.visualstudio.com/docs/copilot/copilot-chat) — Referencia de comandos y funcionalidades del panel de chat.
- [Ingeniería de prompts para Azure OpenAI](https://learn.microsoft.com/es-es/azure/ai-services/openai/how-to/prompt-engineering) — Principios aplicables para mejorar la calidad de tus prompts.
- [Métricas DORA](https://dora.dev/) — Framework de métricas para medir el desempeño de equipos de desarrollo de software.

---

> **Recuerda:** Guarda tu archivo `resultados_comparacion.md` y mantén actualizado tu diario de aprendizaje. Las reflexiones de esta práctica son insumo directo para las Prácticas 9 y 10, donde analizarás tu evolución como desarrollador en un entorno con IA generativa.
