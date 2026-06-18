# Práctica 1: Investiga y escribe un breve informe sobre cómo la IA ha impactado en una industria específica que te interese.

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

