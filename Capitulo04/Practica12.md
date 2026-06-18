# Práctica 12: Reflexiona y documenta qué nuevas habilidades deberías aprender para adaptarte al uso de herramientas como Copilot Chat.

## 1. Metadatos

| Campo            | Detalle                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Duración**     | 9 minutos                                                               |
| **Complejidad**  | Media                                                                   |
| **Nivel Bloom**  | Crear (*Create*)                                                        |
| **Módulo**       | 4.0 — Evolución del Rol del Programador                                 |
| **Práctica**     | 12 de 12                                                                |

---

## 2. Descripción General

Esta práctica cierra el módulo 4.0 invitando a cada participante a sintetizar de forma personal lo aprendido sobre la evolución del rol del programador. A través de una reflexión guiada —apoyada opcionalmente en Copilot Chat como interlocutor— identificarás las habilidades técnicas y blandas que debes desarrollar o fortalecer para trabajar de manera efectiva en un entorno donde la IA generativa es una herramienta cotidiana. El entregable principal es un **Plan de Desarrollo Personal (PDP)** estructurado, concreto y directamente aplicable a tu trayectoria profesional.

> **Nota de tiempo:** Esta práctica está diseñada para completarse en 9 minutos en clase. Si la realizas de forma autónoma, puedes extender el tiempo para mayor profundidad. Conserva el documento generado, ya que puede servir como base para conversaciones de carrera y revisiones periódicas de progreso.

---

## 3. Objetivos de Aprendizaje

Al finalizar esta práctica serás capaz de:

- [ ] Reflexionar críticamente sobre cómo el uso de Copilot Chat transforma las competencias requeridas en el rol del programador moderno.
- [ ] Identificar al menos **cinco habilidades** (técnicas y blandas) necesarias para trabajar eficazmente con herramientas de IA generativa.
- [ ] Crear un **Plan de Desarrollo Personal** estructurado con habilidades priorizadas, recursos de aprendizaje y horizonte temporal estimado.
- [ ] Documentar el plan de manera clara y compartible, demostrando capacidad de autogestión del aprendizaje continuo.

---

## 4. Prerrequisitos

### Conocimiento previo

| Requisito | Descripción |
|-----------|-------------|
| Prácticas anteriores | Haber completado las Prácticas 1 a 11, especialmente la Práctica 11 (04-00-02) |
| Experiencia con Copilot Chat | Haber usado Copilot Chat durante el curso para tener una base experiencial de reflexión |
| Diario de aprendizaje | Tener disponible el archivo de notas o diario acumulado durante el curso |
| Disposición para autoevaluación | Apertura para identificar honestamente competencias actuales y áreas de mejora |

### Acceso y cuentas

| Recurso | Estado requerido |
|---------|-----------------|
| GitHub Copilot Chat | Suscripción activa y extensión instalada en VS Code |
| Procesador de texto | Google Docs, Microsoft Word, Notion o equivalente disponible |
| Conexión a internet | Activa (mínimo 10 Mbps) para consultar recursos de referencia |

---

## 5. Entorno de Laboratorio

### Hardware recomendado

| Componente | Mínimo | Recomendado |
|------------|--------|-------------|
| RAM | 8 GB | 16 GB |
| Procesador | Intel Core i5 / AMD Ryzen 5 (64 bits) | i7 / Ryzen 7 o superior |
| Espacio en disco | 10 GB libres | 20 GB libres |
| Pantalla | 1280×768 | 1920×1080 |
| Conexión | 10 Mbps | 25 Mbps o más |

### Software necesario

| Herramienta | Versión mínima | Uso en esta práctica |
|-------------|---------------|----------------------|
| Visual Studio Code | 1.90 | Abrir Copilot Chat como interlocutor opcional |
| GitHub Copilot Chat (extensión) | Última disponible | Reflexión guiada y consulta de habilidades |
| Procesador de texto | Cualquier versión reciente | Redactar el Plan de Desarrollo Personal |
| Navegador web | Chrome / Edge / Firefox (última versión) | Consultar roadmap.sh, Coursera, edX, GitHub Skills |

### Verificación rápida del entorno

Antes de comenzar, ejecuta los siguientes comandos para confirmar que tu entorno está listo:

```bash
# Verificar versión de VS Code desde terminal
code --version

# Verificar conexión a internet (debe responder con 200)
curl -o /dev/null -s -w "%{http_code}\n" https://github.com

# Verificar que Git está disponible (opcional, para guardar el PDP en un repo)
git --version
```

**Salida esperada:**

```
1.90.x (o superior)
200
git version 2.40.x (o superior)
```

> **Si Copilot Chat no responde:** Ten preparado el documento en blanco en tu procesador de texto; la reflexión puede completarse sin conexión usando las preguntas detonadoras de esta guía.

---

## 6. Instrucciones Paso a Paso

---

### Paso 1 — Prepara tu espacio de trabajo y activa Copilot Chat

**Objetivo:** Tener listo el entorno para la reflexión y el uso opcional de Copilot Chat como interlocutor.

**Instrucciones:**

1. Abre **Visual Studio Code**.
2. Presiona `Ctrl+Shift+P` (Windows/Linux) o `Cmd+Shift+P` (macOS) y escribe `GitHub Copilot Chat: Open`. Presiona `Enter`.
3. Abre tu **procesador de texto** preferido (Google Docs, Word, Notion, etc.) y crea un documento nuevo titulado:

   ```
   Plan de Desarrollo Personal — [Tu nombre] — [Fecha]
   ```

4. Abre también tu **diario de aprendizaje** o notas acumuladas del curso para tenerlas como referencia.
5. Opcional: abre una pestaña del navegador en [roadmap.sh](https://roadmap.sh) para consultar rutas de aprendizaje durante la actividad.

**Resultado esperado:**

- Panel de Copilot Chat visible en VS Code.
- Documento en blanco del PDP abierto en tu procesador de texto.
- Diario de aprendizaje disponible para consulta.

**Verificación:**

- El panel de Copilot Chat muestra el cuadro de texto de conversación activo (no muestra error de autenticación).
- El documento del PDP está creado y guardado con el nombre correcto.

---

### Paso 2 — Reflexión guiada con preguntas detonadoras

**Objetivo:** Activar el pensamiento crítico sobre cómo Copilot Chat ha cambiado (o podría cambiar) tu forma de programar, usando preguntas estructuradas como punto de partida.

**Instrucciones:**

1. Dedica **2 minutos** a responder mentalmente (o por escrito en tu diario) las siguientes **preguntas detonadoras**. No hay respuestas correctas o incorrectas; el objetivo es la honestidad reflexiva:

   **Bloque A — Lo que cambia:**
   - ¿Qué tareas que hacías manualmente (buscar sintaxis, escribir boilerplate, generar tests básicos) ahora puede hacer Copilot Chat por ti?
   - ¿En qué partes del ciclo *Enunciar–Especificar–Generar–Validar–Ajustar* te sientes más seguro/a? ¿En cuáles menos?
   - ¿Qué errores o limitaciones de Copilot Chat has detectado que requirieron tu criterio humano para corregir?

   **Bloque B — Lo que se potencia:**
   - ¿Qué habilidades humanas se vuelven *más valiosas* cuando la IA puede generar código? (Piensa en arquitectura, comunicación, juicio ético, revisión crítica.)
   - ¿Qué aspectos de tu trabajo como programador/a *no puede reemplazar* Copilot Chat?

   **Bloque C — Lo que falta:**
   - ¿Qué habilidades sientes que te faltan para sacar el máximo provecho de Copilot Chat?
   - ¿Qué conocimientos técnicos (seguridad, testing, arquitectura, prompting) querrías profundizar?
   - ¿Qué habilidades blandas (comunicación, ética, pensamiento crítico) reconoces que necesitas fortalecer?

2. **Opcional:** Usa Copilot Chat como interlocutor enviando el siguiente prompt para ampliar tu reflexión:

   ```
   Actúa como un coach de desarrollo profesional especializado en ingeniería de software
   y IA generativa. Quiero reflexionar sobre cómo herramientas como GitHub Copilot Chat
   están transformando el rol del programador.

   Por favor, ayúdame a explorar estas preguntas:
   1. ¿Qué habilidades técnicas se vuelven más importantes para un programador que usa
      IA generativa a diario?
   2. ¿Qué habilidades blandas (soft skills) son más críticas en este nuevo contexto?
   3. ¿Qué riesgos profesionales enfrenta un programador que NO desarrolla estas
      habilidades?
   4. Dame ejemplos concretos de cómo cada tipo de habilidad se manifiesta en el trabajo
      diario con Copilot Chat.

   Sé específico, práctico y honesto sobre tanto las oportunidades como los desafíos.
   ```

3. Lee la respuesta de Copilot Chat y anota en tu diario los puntos que resuenan con tu experiencia personal durante el curso.

**Resultado esperado:**

- Un conjunto de notas personales (escritas o mentales) sobre tus fortalezas actuales y áreas de crecimiento identificadas.
- Posiblemente, una respuesta de Copilot Chat con perspectivas adicionales sobre habilidades relevantes.

**Verificación:**

- Tienes al menos **3 ideas concretas** anotadas sobre habilidades que deseas desarrollar (aunque sea en borrador).
- Las ideas provienen de tu experiencia real con el curso, no solo de fuentes externas.

---

### Paso 3 — Clasifica las habilidades en tres categorías

**Objetivo:** Organizar las habilidades identificadas en la reflexión dentro de un marco de tres categorías para estructurar el Plan de Desarrollo Personal.

**Instrucciones:**

1. En tu documento del PDP, crea una sección titulada **"Inventario de Habilidades a Desarrollar"** con las siguientes tres subsecciones:

   ```
   ## Inventario de Habilidades a Desarrollar

   ### Categoría 1: Habilidades Técnicas de IA y Prompting
   (Prompt engineering, evaluación de outputs de IA, integración de herramientas,
   detección de alucinaciones, uso de contexto efectivo)

   ### Categoría 2: Habilidades de Ingeniería de Software Potenciadas por IA
   (Revisión de código, arquitectura de sistemas, testing automatizado,
   seguridad (SAST/DAST), documentación técnica, CI/CD)

   ### Categoría 3: Habilidades Blandas Críticas
   (Pensamiento crítico, comunicación técnica, ética en IA, aprendizaje continuo,
   colaboración, gestión de la incertidumbre)
   ```

2. Bajo cada categoría, lista las habilidades que identificaste en el Paso 2. Apunta al menos **2 habilidades por categoría** (mínimo 6 en total; el plan final requerirá al menos 5 priorizadas).

3. **Opcional:** Consulta a Copilot Chat para validar o ampliar tu lista:

   ```
   Tengo esta lista inicial de habilidades que quiero desarrollar como programador/a
   que usa IA generativa:

   [Pega aquí tu lista de habilidades]

   Por favor:
   1. ¿Hay habilidades importantes que me estén faltando en alguna categoría?
   2. ¿Cuáles de estas habilidades consideras más urgentes en 2024-2025?
   3. Para cada habilidad, sugiere UN recurso de aprendizaje concreto (curso, libro,
      comunidad o práctica).
   ```

4. Complementa tu lista con las sugerencias de Copilot Chat que consideres relevantes para tu contexto específico.

**Resultado esperado:**

- Una lista organizada de al menos 6 habilidades distribuidas en las tres categorías.
- Cada habilidad tiene una descripción breve de por qué es relevante para ti.

**Verificación:**

- Las tres categorías tienen al menos una habilidad cada una.
- Las habilidades listadas son específicas (no genéricas como "aprender más sobre IA"), sino concretas (por ejemplo: "aprender a escribir prompts con restricciones explícitas de seguridad").

---

### Paso 4 — Construye el Plan de Desarrollo Personal (PDP)

**Objetivo:** Transformar el inventario de habilidades en un plan estructurado, priorizado y con horizonte temporal, que sea accionable y compartible.

**Instrucciones:**

1. En tu documento del PDP, crea la sección principal **"Plan de Desarrollo Personal"** usando la siguiente estructura. Completa al menos **5 habilidades** con todos los campos:

   ```markdown
   # Plan de Desarrollo Personal
   ## Programador/a en la Era de la IA Generativa

   **Nombre:** [Tu nombre]
   **Fecha de creación:** [Fecha]
   **Versión:** 1.0

   ---

   ## Contexto y Motivación

   [2-3 oraciones describiendo tu situación actual y por qué este plan es importante
   para tu desarrollo profesional. Ejemplo: "Tras completar este curso, reconozco que
   el uso efectivo de Copilot Chat no es solo una habilidad técnica, sino un cambio
   de mentalidad que requiere fortalecer mi capacidad de especificación, revisión
   crítica y comunicación de decisiones técnicas..."]

   ---

   ## Habilidades Priorizadas

   ### Habilidad 1: [Nombre de la habilidad]
   - **Categoría:** [Técnica IA/Ingeniería de Software/Blanda]
   - **¿Por qué es relevante?** [1-2 oraciones desde tu perspectiva personal]
   - **Nivel actual (1-5):** [Tu autoevaluación honesta]
   - **Nivel objetivo (1-5):** [A dónde quieres llegar]
   - **Recursos de aprendizaje:**
     - [ ] [Recurso 1: nombre, plataforma, URL o referencia]
     - [ ] [Recurso 2: nombre, plataforma, URL o referencia]
   - **Plazo estimado:** [Ej: 1 mes / 3 meses / 6 meses]
   - **Indicador de logro:** [¿Cómo sabrás que alcanzaste el nivel objetivo?]

   ### Habilidad 2: [Nombre de la habilidad]
   [... mismo formato ...]

   ### Habilidad 3: [Nombre de la habilidad]
   [... mismo formato ...]

   ### Habilidad 4: [Nombre de la habilidad]
   [... mismo formato ...]

   ### Habilidad 5: [Nombre de la habilidad]
   [... mismo formato ...]

   ---

   ## Compromisos y Próximos Pasos

   - **Esta semana haré:** [Acción concreta y pequeña]
   - **Este mes completaré:** [Recurso o práctica específica]
   - **En 3 meses revisaré:** [Cómo evaluaré mi progreso]

   ---

   ## Reflexión Final

   [3-5 oraciones sobre cómo visualizas tu rol como programador/a en 2 años,
   integrando estas habilidades y trabajando con herramientas de IA generativa]
   ```

2. Completa cada campo con información real y específica. Evita respuestas genéricas; cuanto más personal y honesto sea el plan, más útil será.

3. Para los **recursos de aprendizaje**, puedes consultar las siguientes fuentes de referencia:

   | Recurso | URL | Útil para |
   |---------|-----|-----------|
   | roadmap.sh | https://roadmap.sh | Rutas de aprendizaje técnicas estructuradas |
   | GitHub Skills | https://skills.github.com | Habilidades prácticas con GitHub y Copilot |
   | Coursera | https://coursera.org | Cursos certificados de universidades |
   | edX | https://edx.org | Cursos de MIT, Harvard y otras instituciones |
   | OWASP | https://owasp.org | Seguridad en aplicaciones y LLMs |
   | Martin Fowler Blog | https://martinfowler.com | Arquitectura, TDD y buenas prácticas |
   | GitHub Blog | https://github.blog | Investigación sobre Copilot y productividad |
   | NIST AI RMF | https://nist.gov/itl/ai-risk-management-framework | Marco de gestión de riesgos de IA |

4. **Opcional:** Pide a Copilot Chat que revise y enriquezca tu plan:

   ```
   Revisa este borrador de mi Plan de Desarrollo Personal como programador/a que
   trabaja con IA generativa:

   [Pega aquí tu PDP en borrador]

   Por favor:
   1. ¿Las habilidades seleccionadas son coherentes entre sí y con el contexto actual
      del mercado laboral?
   2. ¿Los plazos son realistas?
   3. ¿Hay alguna habilidad crítica que me esté perdiendo?
   4. Sugiere 2-3 indicadores de logro más concretos y medibles para las habilidades
      que los tengan vagos.

   Sé constructivo y específico en tu retroalimentación.
   ```

**Resultado esperado:**

- Un documento PDP con al menos 5 habilidades completamente documentadas.
- Cada habilidad tiene: categoría, justificación personal, nivel actual/objetivo, al menos 2 recursos de aprendizaje, plazo estimado e indicador de logro.
- El documento incluye sección de contexto, compromisos próximos y reflexión final.

**Verificación:**

- El documento tiene al menos **5 habilidades** con todos los campos completados.
- Al menos **2 habilidades son técnicas** (Categorías 1 o 2) y al menos **1 es blanda** (Categoría 3).
- Cada habilidad tiene al menos **1 recurso de aprendizaje concreto** con nombre y referencia.
- Los indicadores de logro son medibles (no solo "saber más sobre X", sino "completar el curso Y" o "implementar Z en un proyecto real").

---

### Paso 5 — Guarda, comparte y cierra el ciclo de aprendizaje

**Objetivo:** Asegurar que el Plan de Desarrollo Personal esté guardado de forma accesible y, opcionalmente, compartido para recibir retroalimentación.

**Instrucciones:**

1. **Guarda el documento** en un formato compartible:
   - Google Docs: activa el acceso para comentarios con el instructor.
   - Word/Notion: exporta a PDF o comparte el enlace.
   - Opcionalmente, guarda el archivo en tu repositorio de notas del curso:

   ```bash
   # Si usas Git para gestionar tus notas del curso
   mkdir -p ~/curso-copilot/practica-12
   # Copia o crea el archivo PDP en esa carpeta
   # Ejemplo si usas un archivo markdown:
   touch ~/curso-copilot/practica-12/plan-desarrollo-personal.md
   # Abre el archivo en VS Code para editarlo
   code ~/curso-copilot/practica-12/plan-desarrollo-personal.md
   ```

2. **Nombra el archivo** siguiendo esta convención:

   ```
   PDP_[TuNombre]_[YYYYMMDD].md
   # Ejemplo:
   PDP_JuanPerez_20241215.md
   ```

3. Si el instructor lo solicita, **comparte el documento** en el canal del curso o plataforma LMS para recibir retroalimentación de pares.

4. Agrega una entrada final en tu **diario de aprendizaje** con la siguiente reflexión en 2-3 oraciones:

   ```
   Fecha: [hoy]
   Práctica 12 completada.

   Las 3 habilidades que más me urge desarrollar son:
   1. [Habilidad 1]
   2. [Habilidad 2]
   3. [Habilidad 3]

   El primer paso concreto que tomaré esta semana es:
   [Acción específica]
   ```

5. Cierra el panel de Copilot Chat en VS Code (puedes dejarlo abierto si lo necesitas para otras actividades).

**Resultado esperado:**

- Archivo PDP guardado con nombre correcto y accesible.
- Entrada final en el diario de aprendizaje completada.
- Documento listo para compartir con el instructor o pares si se requiere.

**Verificación:**

- El archivo existe en la ubicación indicada y se puede abrir correctamente.
- El nombre del archivo sigue la convención `PDP_[Nombre]_[Fecha].md` (o formato equivalente).
- La entrada del diario de aprendizaje está fechada y tiene las 3 habilidades prioritarias identificadas.

---

## 7. Validación y Pruebas

Usa esta lista de verificación para confirmar que completaste la práctica satisfactoriamente:

### Lista de verificación del entregable

| Criterio | ¿Cumplido? |
|----------|-----------|
| El documento PDP tiene título, nombre del autor y fecha | ☐ |
| Incluye una sección de contexto y motivación personal | ☐ |
| Contiene al menos **5 habilidades** documentadas | ☐ |
| Al menos 2 habilidades son de categorías técnicas (1 o 2) | ☐ |
| Al menos 1 habilidad es de la categoría blanda (3) | ☐ |
| Cada habilidad tiene justificación personal (no genérica) | ☐ |
| Cada habilidad tiene nivel actual y nivel objetivo (escala 1-5) | ☐ |
| Cada habilidad tiene al menos 1 recurso de aprendizaje concreto | ☐ |
| Cada habilidad tiene un plazo estimado | ☐ |
| Cada habilidad tiene un indicador de logro medible | ☐ |
| El documento incluye sección de compromisos y próximos pasos | ☐ |
| El documento incluye reflexión final sobre el rol futuro | ☐ |
| El archivo está guardado con la convención de nombre correcta | ☐ |
| El diario de aprendizaje tiene entrada final de la práctica | ☐ |

### Criterio de calidad del plan

Un PDP de calidad en esta práctica debe cumplir al menos **12 de los 14 criterios** de la lista anterior. Si cumples menos de 10, revisa los pasos 3 y 4 antes de considerar la práctica completa.

### Autoevaluación de profundidad

Responde estas preguntas para evaluar la calidad de tu reflexión:

1. ¿Las habilidades que listaste están directamente conectadas con experiencias específicas que tuviste durante el curso (no solo ideas abstractas)?
2. ¿Los indicadores de logro que definiste son lo suficientemente concretos como para que alguien más pueda verificar si los alcanzaste?
3. ¿El plazo que asignaste a cada habilidad es realista dado tu contexto actual (trabajo, tiempo disponible, recursos)?

Si alguna respuesta es "no", toma 1-2 minutos adicionales para ajustar esos elementos en tu PDP.

---

## 8. Solución de Problemas

### Problema 1: Copilot Chat no responde o muestra error de autenticación

**Síntomas:**
- El panel de Copilot Chat muestra el mensaje `"Sign in to use Copilot"` o `"GitHub Copilot could not connect to the server"`.
- Las consultas enviadas no reciben respuesta o muestran un error de red.

**Causa probable:**
- La sesión de GitHub expiró o la suscripción a Copilot no está activa.
- Problema temporal de conectividad a los servidores de GitHub.

**Solución:**
1. En VS Code, abre la paleta de comandos (`Ctrl+Shift+P`) y escribe `GitHub: Sign In`. Completa el flujo de autenticación.
2. Verifica que tu suscripción esté activa en [github.com/settings/copilot](https://github.com/settings/copilot).
3. Si el problema persiste, **continúa la práctica sin Copilot Chat**: todas las actividades de reflexión y construcción del PDP pueden completarse de forma autónoma usando las preguntas detonadoras del Paso 2 y los recursos de referencia listados en el Paso 4.
4. Usa el navegador para consultar recursos como roadmap.sh o GitHub Skills como alternativa a las consultas de Copilot.

---

### Problema 2: El Plan de Desarrollo Personal resulta demasiado genérico o superficial

**Síntomas:**
- Las habilidades listadas son vagas (por ejemplo: "aprender sobre IA", "mejorar en programación", "ser mejor comunicador").
- Los indicadores de logro no son medibles (por ejemplo: "saber más sobre seguridad").
- El plan se siente como una lista de deseos en lugar de un plan accionable.

**Causa probable:**
- La reflexión del Paso 2 fue demasiado rápida o superficial, sin conectar con experiencias concretas del curso.
- Las habilidades se tomaron de fuentes externas sin personalización al contexto propio.

**Solución:**
1. Regresa a tu diario de aprendizaje y busca **momentos específicos** del curso donde Copilot Chat te ayudó, te falló o te sorprendió. Usa esos momentos como base para habilidades concretas.
2. Para cada habilidad genérica, aplica el test de especificidad: reemplaza "aprender sobre X" por "ser capaz de hacer Y en el contexto Z". Ejemplo: en lugar de "aprender prompt engineering", escribe "escribir prompts con rol, restricciones y criterios de aceptación que generen código seguro en Python para APIs REST".
3. Para los indicadores de logro, usa el formato: "Habré logrado esta habilidad cuando [acción observable y verificable]". Ejemplo: "Habré logrado esta habilidad cuando complete el módulo de seguridad en OWASP Top 10 LLM y pueda identificar al menos 3 vulnerabilidades en código generado por IA en una revisión de código real".
4. Si usas Copilot Chat, envía el prompt del Paso 4, instrucción 4, para recibir retroalimentación específica sobre cómo hacer el plan más concreto.

---

## 9. Limpieza del Entorno

Esta práctica no genera archivos de código que deban eliminarse. Las acciones de limpieza son mínimas:

1. **Cierra el panel de Copilot Chat** en VS Code si ya no lo necesitas para otras actividades:
   - Haz clic en el ícono de Copilot en la barra lateral o cierra el panel desde la vista.

2. **Guarda y cierra** todos los documentos abiertos en tu procesador de texto, asegurándote de que el PDP esté guardado en la ubicación correcta.

3. **Actualiza tu diario de aprendizaje** con la entrada final si aún no lo has hecho (ver Paso 5, instrucción 4).

4. **Opcional:** Si guardaste el PDP en un repositorio Git, haz commit de los cambios:

   ```bash
   cd ~/curso-copilot
   git add practica-12/
   git commit -m "feat: agrega Plan de Desarrollo Personal - Práctica 12"
   # Si tienes un repositorio remoto configurado:
   git push origin main
   ```

5. No es necesario desinstalar ninguna herramienta ni eliminar configuraciones del sistema.

---

## 10. Resumen

### Lo que construiste en esta práctica

En esta práctica completaste el ciclo de aprendizaje del módulo 4.0 realizando tres actividades fundamentales:

1. **Reflexión crítica:** Usando preguntas detonadoras y opcionalmente Copilot Chat como interlocutor, activaste el pensamiento crítico sobre cómo la IA generativa transforma el rol del programador, conectando conceptos del curso con tu experiencia personal.

2. **Inventario de habilidades:** Clasificaste las habilidades identificadas en tres categorías (habilidades técnicas de IA/prompting, habilidades de ingeniería de software potenciadas, y habilidades blandas críticas), creando un mapa de tu situación actual y tus áreas de crecimiento.

3. **Plan de Desarrollo Personal:** Construiste un documento estructurado con al menos 5 habilidades priorizadas, cada una con justificación personal, recursos concretos de aprendizaje, plazo estimado e indicadores de logro medibles.

### Conexión con el contenido del módulo

Esta práctica materializa el ciclo **Enunciar–Especificar–Generar–Validar–Ajustar** del tema 4.1, pero aplicado a tu propio desarrollo profesional:

| Fase del ciclo | Aplicación en esta práctica |
|----------------|----------------------------|
| **Enunciar** | Identificar qué habilidades necesitas desarrollar |
| **Especificar** | Definir nivel actual, nivel objetivo e indicadores de logro |
| **Generar** | Construir el PDP con recursos y plazos concretos |
| **Validar** | Verificar con la lista de criterios y la autoevaluación |
| **Ajustar** | Refinar habilidades genéricas para hacerlas más específicas y accionables |

### Próximos pasos recomendados

- **Esta semana:** Ejecuta el primer paso concreto que definiste en la sección de compromisos de tu PDP.
- **En 30 días:** Revisa el PDP y marca el progreso en los recursos de aprendizaje iniciados.
- **En 90 días:** Realiza una revisión completa del PDP, actualiza los niveles de habilidad y ajusta prioridades según tu evolución.
- **Comparte tu plan:** Considera compartirlo con un colega o mentor para recibir retroalimentación externa y mantener la responsabilidad (*accountability*).

### Recursos de referencia adicionales

| Recurso | Descripción | URL |
|---------|-------------|-----|
| GitHub Copilot Docs | Documentación oficial de Copilot Chat | https://docs.github.com/en/copilot |
| roadmap.sh | Rutas de aprendizaje para roles de desarrollo | https://roadmap.sh |
| GitHub Skills | Cursos prácticos de GitHub | https://skills.github.com |
| OWASP Top 10 LLM | Riesgos de seguridad en aplicaciones con LLMs | https://owasp.org/www-project-top-10-for-large-language-model-applications/ |
| NIST AI RMF | Marco de gestión de riesgos de IA | https://www.nist.gov/itl/ai-risk-management-framework |
| Martin Fowler — TDD | Conceptos y prácticas de desarrollo guiado por pruebas | https://martinfowler.com/bliki/TestDrivenDevelopment.html |
| Stack Overflow Survey 2023 | Datos sobre uso de IA en desarrollo profesional | https://survey.stackoverflow.co/2023/#technology-ai |
| GitHub Research: Copilot Impact | Investigación sobre productividad con Copilot | https://github.blog/2022-09-07-research-quantifying-github-copilots-impact-on-developer-productivity-and-happiness/ |

---

> **Felicitaciones por completar el módulo 4.0.** Este Plan de Desarrollo Personal es un documento vivo: su valor real no está en haberlo creado, sino en revisarlo y actualizarlo regularmente a medida que tu experiencia con herramientas de IA generativa evoluciona. El programador del futuro no es el que más código escribe, sino el que mejor orquesta, valida y comunica soluciones en colaboración con la IA.

