# Práctica 9: Realiza un caso de estudio sobre un proyecto en donde puedas utilizar Copilot Chat, analizando sus aportes y resultados.

## Metadatos

| Campo            | Detalle                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Duración**     | 10 minutos (clase) / 30–45 minutos (exploración autónoma)              |
| **Complejidad**  | Alta                                                                    |
| **Nivel Bloom**  | Crear — el participante sintetiza experiencias, analiza evidencia y produce un documento estructurado original |
| **Módulo**       | 3 — Resolución de Necesidades de Negocio                               |
| **Práctica**     | 9 de 10                                                                 |

---

## Descripción General

En esta práctica construirás un **caso de estudio formal** que documente el uso de GitHub Copilot Chat en un proyecto de desarrollo real o simulado, tomando como base las experiencias acumuladas en las Prácticas 7 y 8 del Módulo 3. Aplicarás el patrón de negocio→técnico aprendido en la lección 3.1 para estructurar el análisis: desde las necesidades de negocio originales hasta los artefactos técnicos generados, pasando por métricas cuantitativas y observaciones cualitativas. El objetivo final es producir un documento reutilizable que sirva como referencia de buenas prácticas y como insumo reflexivo para la Práctica 10.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Construir un caso de estudio estructurado que documente el uso de Copilot Chat en un proyecto de desarrollo completo, siguiendo una metodología formal de cinco secciones.
- [ ] Analizar cuantitativamente (tiempo estimado, líneas generadas, número de interacciones) y cualitativamente (calidad del código, casos de fallo, satisfacción) los aportes de Copilot Chat.
- [ ] Utilizar Copilot Chat de forma meta-cognitiva para ayudar a redactar y estructurar el propio caso de estudio, documentando esa experiencia reflexiva.
- [ ] Sintetizar lecciones aprendidas y formular al menos tres recomendaciones prácticas para el uso efectivo de Copilot Chat en proyectos futuros.

---

## Prerrequisitos

### Conocimiento previo
- Haber completado las **Prácticas 7 y 8** del Módulo 3 y conservar los archivos de código generados.
- Comprender el patrón de prompt negocio→técnico (lección 3.1): contexto, restricciones, datos, criterios de éxito, formato de salida.
- Familiaridad con historias de usuario, criterios de aceptación en Gherkin y diseño básico de APIs REST.
- Tener notas o un diario de aprendizaje con observaciones de prácticas anteriores.

### Acceso y cuentas
- Cuenta de GitHub con suscripción activa a **GitHub Copilot** (Individual, Business o Enterprise).
- VS Code con la extensión **GitHub Copilot Chat** instalada y autenticada.
- Acceso a una herramienta de procesamiento de texto (VS Code, Word, Google Docs o Notion).

---

## Entorno de Laboratorio

### Hardware mínimo recomendado

| Recurso         | Mínimo              | Recomendado          |
|-----------------|---------------------|----------------------|
| Procesador      | Intel Core i5 / AMD Ryzen 5 (64 bits) | Core i7 / Ryzen 7 |
| RAM             | 8 GB                | 16 GB                |
| Disco libre     | 2 GB                | 10 GB                |
| Resolución      | 1280 × 768          | 1920 × 1080          |
| Conectividad    | 10 Mbps             | 25 Mbps              |

### Software requerido

| Herramienta                    | Versión mínima        | Propósito                                    |
|--------------------------------|-----------------------|----------------------------------------------|
| Visual Studio Code             | 1.90                  | IDE principal y edición del caso de estudio  |
| GitHub Copilot Chat (extensión)| Última disponible     | Asistente de IA para generación y redacción  |
| Python                         | 3.10                  | Lenguaje de referencia para ejemplos de código (opcional: JS/TS, Java, C#) |
| Git                            | 2.40                  | Control de versiones del proyecto            |
| pylint / flake8                | pylint 3.x / flake8 7.x | Verificación de calidad del código generado |
| Procesador de texto            | Cualquier versión reciente | Redacción del documento final            |

### Configuración inicial (verificación rápida)

Ejecuta los siguientes comandos en la terminal integrada de VS Code para confirmar que el entorno está listo antes de comenzar:

```bash
# Verificar versión de Python
python --version

# Verificar Git
git --version

# Verificar pylint (o flake8)
pylint --version
# o bien:
flake8 --version
```

Confirma también que Copilot Chat está activo abriendo el panel lateral con el ícono de chat en VS Code. Si aparece el prompt de autenticación, ingresa con tu cuenta de GitHub antes de continuar.

---

## Pasos del Laboratorio

---

### Paso 1 — Preparar el contexto del proyecto base

**Objetivo:** Reunir y organizar la evidencia de las Prácticas 7 y 8 que servirá como insumo del caso de estudio. Si no tienes esas prácticas completadas, se usará el escenario de referencia provisto.

#### Instrucciones

1. Abre VS Code y crea una carpeta de trabajo para esta práctica:

```bash
mkdir caso-estudio-copilot
cd caso-estudio-copilot
git init
```

2. Dentro de la carpeta, crea la siguiente estructura de archivos:

```bash
mkdir -p docs codigo evidencia
touch docs/caso_estudio.md
touch evidencia/registro_interacciones.md
touch evidencia/metricas.md
```

3. Si tienes archivos de las Prácticas 7 y 8, cópialos dentro de la carpeta `codigo/`. Si no los tienes disponibles, utilizarás el **escenario de referencia** del sistema Click & Collect de la lección 3.1.

4. Abre `evidencia/registro_interacciones.md` y completa la siguiente tabla con tus notas de prácticas anteriores (o estima los valores si trabajas con el escenario de referencia):

```markdown
# Registro de Interacciones con Copilot Chat

| # | Prompt resumido                             | Tipo de artefacto generado | ¿Fue útil? (1-5) | Requirió corrección |
|---|---------------------------------------------|----------------------------|------------------|---------------------|
| 1 |                                             |                            |                  |                     |
| 2 |                                             |                            |                  |                     |
| 3 |                                             |                            |                  |                     |
```

5. Abre `evidencia/metricas.md` y prepara la tabla de métricas cuantitativas:

```markdown
# Métricas Cuantitativas del Proyecto

| Métrica                                  | Valor estimado | Notas                       |
|------------------------------------------|----------------|-----------------------------|
| Tiempo total de desarrollo (min)         |                |                             |
| Tiempo estimado sin Copilot Chat (min)   |                |                             |
| Ahorro estimado (%)                      |                |                             |
| Número total de interacciones con Copilot|                |                             |
| Líneas de código generadas por Copilot   |                |                             |
| Líneas de código escritas manualmente    |                |                             |
| Número de artefactos generados           |                |                             |
| Interacciones que requirieron corrección |                |                             |
```

**Salida esperada:** Carpeta `caso-estudio-copilot/` inicializada con Git, archivos de documentación creados y tablas de evidencia listas para completar.

**Verificación:**

```bash
# Confirmar estructura de archivos
find . -type f | sort
```

La salida debe mostrar al menos:
```
./docs/caso_estudio.md
./evidencia/metricas.md
./evidencia/registro_interacciones.md
```

---

### Paso 2 — Generar la estructura del caso de estudio con Copilot Chat

**Objetivo:** Usar Copilot Chat de forma meta-cognitiva para obtener una plantilla formal del caso de estudio, documentando esta interacción como parte del propio análisis.

#### Instrucciones

1. Abre el panel de **Copilot Chat** en VS Code (`Ctrl+Alt+I` o clic en el ícono de chat).

2. Escribe el siguiente prompt completo en el chat. Observa cómo aplica el patrón negocio→técnico de la lección 3.1:

```text
Contexto: Soy un desarrollador que acaba de completar un proyecto de desarrollo asistido 
por IA usando GitHub Copilot Chat. El proyecto involucró la construcción de funcionalidades 
para un sistema [describe brevemente: ej. "de gestión de inventario" o "Click & Collect 
para retail"].

Necesito elaborar un caso de estudio formal de 5 secciones para documentar esta experiencia:
1. Contexto del proyecto y necesidades de negocio
2. Metodología de uso de Copilot Chat
3. Resultados cuantitativos (tiempo, líneas de código, interacciones)
4. Resultados cualitativos (calidad, satisfacción, fallos)
5. Lecciones aprendidas y recomendaciones

Genera:
a) Una plantilla detallada en Markdown para cada sección con subsecciones específicas 
   y preguntas guía que debo responder.
b) Una tabla de métricas sugeridas para la sección cuantitativa.
c) Un checklist de calidad para evaluar el código generado por Copilot.
d) Tres preguntas de reflexión para la sección de lecciones aprendidas.

Formato: Markdown con encabezados claros (##, ###). Incluye ejemplos breves de cómo 
completar cada sección.
```

3. Cuando Copilot Chat responda, **copia la plantilla generada** y pégala en `docs/caso_estudio.md`.

4. En `evidencia/registro_interacciones.md`, registra esta primera interacción meta-cognitiva:

```markdown
## Interacción Meta-Cognitiva #1

**Prompt:** Solicitud de plantilla para caso de estudio formal
**Artefacto generado:** Plantilla Markdown con 5 secciones
**Utilidad (1-5):** [tu evaluación]
**Observaciones:** [¿La plantilla fue completa? ¿Requirió ajustes?]
**Tiempo de respuesta estimado:** [segundos]
```

5. Haz un commit con el progreso:

```bash
git add .
git commit -m "feat: estructura inicial del caso de estudio generada con Copilot Chat"
```

**Salida esperada:** El archivo `docs/caso_estudio.md` contiene una plantilla estructurada con al menos 5 secciones, preguntas guía y ejemplos. El registro de interacciones tiene la primera entrada meta-cognitiva.

**Verificación:** Abre `docs/caso_estudio.md` en la vista previa de VS Code (`Ctrl+Shift+V`) y confirma que los encabezados de las 5 secciones son visibles y el documento tiene al menos 40 líneas de contenido.

---

### Paso 3 — Completar la Sección 1: Contexto y necesidades de negocio

**Objetivo:** Documentar el proyecto base con el patrón negocio→técnico aprendido en la lección 3.1, traduciendo necesidades de negocio en artefactos técnicos trazables.

#### Instrucciones

1. Abre `docs/caso_estudio.md` y localiza la **Sección 1**. Complétala con la información de tu proyecto de las Prácticas 7 y 8, o usa el escenario de referencia Click & Collect. El contenido mínimo debe incluir:

```markdown
## Sección 1: Contexto del Proyecto y Necesidades de Negocio

### 1.1 Descripción del Proyecto
- **Nombre del proyecto:** [ej. Sistema Click & Collect para Retail]
- **Dominio de negocio:** [ej. Comercio electrónico / Retail omnicanal]
- **Duración del desarrollo:** [ej. Prácticas 7, 8 y 9 del Módulo 3]
- **Lenguaje/tecnología principal:** [Python / TypeScript / Java]

### 1.2 Necesidad de Negocio Original
<!-- Describe el "por qué" estratégico. ¿Qué problema resuelve? -->
[Tu descripción aquí]

### 1.3 Objetivo y Métricas de Éxito
| Objetivo               | Métrica KPI                  | Meta          |
|------------------------|------------------------------|---------------|
| [ej. Aumentar conversión] | [ej. Tasa de conversión (%)] | [ej. +3%]   |

### 1.4 Restricciones Identificadas
- **Técnicas:** [ej. SLO p95 < 300ms, compatibilidad con Python 3.10+]
- **Normativas:** [ej. PCI-DSS para pagos, GDPR para datos personales]
- **Presupuesto/Tiempo:** [ej. Desarrollo en 3 sesiones de práctica]

### 1.5 Artefactos Técnicos Generados
| ID     | Tipo de Artefacto          | Descripción breve                    |
|--------|----------------------------|--------------------------------------|
| US-001 | Historia de usuario        | [descripción]                        |
| AC-001 | Criterio de aceptación     | [descripción]                        |
| API-01 | Endpoint REST              | [descripción]                        |
```

2. Usa Copilot Chat para enriquecer esta sección. Prueba el siguiente prompt:

```text
Tengo el siguiente contexto de proyecto: [pega tu Sección 1.2 y 1.3].

Ayúdame a:
1. Identificar 3 riesgos técnicos o de negocio que no haya considerado.
2. Sugerir 2 métricas adicionales relevantes para medir el éxito del proyecto.
3. Redactar un párrafo ejecutivo de 3 oraciones que resuma la necesidad de negocio 
   para una audiencia no técnica.
```

3. Registra esta interacción en `evidencia/registro_interacciones.md` con el formato del Paso 2.

**Salida esperada:** La Sección 1 del caso de estudio está completa con tablas de métricas, restricciones documentadas y al menos 3 artefactos técnicos identificados con sus IDs de trazabilidad.

**Verificación:** La sección debe contener al menos una tabla de métricas KPI, una lista de restricciones y una tabla de artefactos técnicos con identificadores únicos (US-XXX, AC-XXX, API-XX).

---

### Paso 4 — Completar las Secciones 2, 3 y 4: Metodología y resultados

**Objetivo:** Documentar el proceso de uso de Copilot Chat y analizar los resultados cuantitativos y cualitativos con datos reales o estimados.

#### Instrucciones

1. Completa la **Sección 2 — Metodología** en `docs/caso_estudio.md`:

```markdown
## Sección 2: Metodología de Uso de Copilot Chat

### 2.1 Flujo de Trabajo Aplicado
<!-- Describe cómo integraste Copilot Chat en tu proceso de desarrollo -->
1. [Paso 1: ej. Definición de necesidad de negocio con prompt de contexto]
2. [Paso 2: ej. Generación de historias de usuario y criterios Gherkin]
3. [Paso 3: ej. Diseño de API con OpenAPI]
4. [Paso 4: ej. Generación de código esqueleto]
5. [Paso 5: ej. Generación de pruebas unitarias]
6. [Paso 6: ej. Revisión y corrección de código generado]

### 2.2 Tipos de Prompts Utilizados
| Categoría de Prompt        | Ejemplo resumido                          | Frecuencia |
|----------------------------|-------------------------------------------|------------|
| Negocio → Artefactos       | "Genera historias de usuario para..."     | Alta       |
| Generación de código       | "Escribe un endpoint que..."              | Alta       |
| Revisión y mejora          | "Revisa este código y sugiere mejoras..." | Media      |
| Explicación                | "Explica qué hace esta función..."        | Media      |
| Pruebas                    | "Genera 5 casos de prueba para..."        | Media      |
| Documentación              | "Documenta esta función con docstring..." | Baja       |

### 2.3 Herramientas y Comandos Clave de Copilot Chat
- `/explain` — para entender código existente
- `/tests` — para generar casos de prueba
- `/fix` — para corregir errores detectados
- `/doc` — para generar documentación inline
- Chat libre con contexto de archivo abierto
```

2. Completa la **Sección 3 — Resultados Cuantitativos** usando los datos de `evidencia/metricas.md`:

```markdown
## Sección 3: Resultados Cuantitativos

### 3.1 Tabla de Métricas de Productividad
[Copia y completa la tabla de evidencia/metricas.md]

### 3.2 Análisis del Ahorro de Tiempo
<!-- Fórmula: Ahorro (%) = ((Tiempo sin Copilot - Tiempo con Copilot) / Tiempo sin Copilot) × 100 -->
- Tiempo estimado de desarrollo **sin** Copilot Chat: ___ minutos
- Tiempo real de desarrollo **con** Copilot Chat: ___ minutos
- **Ahorro estimado:** ___% 

### 3.3 Distribución de Código Generado vs. Manual
| Componente               | Líneas generadas por Copilot | Líneas escritas manualmente | % Copilot |
|--------------------------|------------------------------|-----------------------------|-----------|
| Modelos / Esquemas       |                              |                             |           |
| Lógica de negocio        |                              |                             |           |
| Pruebas                  |                              |                             |           |
| Documentación / Comentarios |                           |                             |           |
| **Total**                |                              |                             |           |
```

3. Usa Copilot Chat para generar un análisis automático de las métricas. Escribe el siguiente prompt:

```text
Tengo las siguientes métricas de un proyecto desarrollado con GitHub Copilot Chat:
- Tiempo total con Copilot: [X] minutos
- Tiempo estimado sin Copilot: [Y] minutos  
- Interacciones totales: [N]
- Líneas generadas por Copilot: [L]
- Interacciones que requirieron corrección: [C]

Genera:
1. Un párrafo de análisis ejecutivo de los resultados cuantitativos.
2. Una interpretación del porcentaje de correcciones sobre el total de interacciones.
3. Dos conclusiones sobre la relación entre productividad y calidad observada.
Sé objetivo: incluye tanto aspectos positivos como limitaciones evidentes en los datos.
```

4. Completa la **Sección 4 — Resultados Cualitativos**:

```markdown
## Sección 4: Resultados Cualitativos

### 4.1 Calidad del Código Generado
<!-- Evalúa usando el checklist generado en el Paso 2 -->

| Criterio de Calidad                          | Observación                          | Puntuación (1-5) |
|----------------------------------------------|--------------------------------------|------------------|
| Legibilidad y nomenclatura                   |                                      |                  |
| Manejo de errores y casos borde              |                                      |                  |
| Seguridad (validación de entradas, secretos) |                                      |                  |
| Cobertura de pruebas generadas               |                                      |                  |
| Adherencia a estándares del proyecto         |                                      |                  |
| Documentación inline (docstrings/comentarios)|                                      |                  |

### 4.2 Casos en que Copilot Chat Fue Impreciso o Falló
| # | Descripción del fallo                    | Causa probable               | Cómo se resolvió           |
|---|------------------------------------------|------------------------------|----------------------------|
| 1 | [ej. Generó código con dependencia no disponible] | Contexto de repo insuficiente | Se especificó la versión en el prompt |
| 2 |                                          |                              |                            |
| 3 |                                          |                              |                            |

### 4.3 Satisfacción del Desarrollador
- **Facilidad de uso de Copilot Chat (1-10):** ___
- **Confianza en el código generado sin revisión (1-10):** ___
- **Impacto percibido en productividad (1-10):** ___
- **Comentario libre:** [Tu observación más importante]

### 4.4 Impacto en la Calidad del Producto Final
<!-- ¿El código generado por Copilot pasó las pruebas de linting sin modificaciones? -->
[Descripción breve]
```

5. Ejecuta el linter sobre el código generado en prácticas anteriores y registra los resultados:

```bash
# Para Python
pylint codigo/*.py --output-format=text 2>&1 | tee evidencia/linting_report.txt

# O con flake8
flake8 codigo/ --statistics 2>&1 | tee evidencia/linting_report.txt
```

6. Registra todas las interacciones de Copilot Chat de este paso en `evidencia/registro_interacciones.md`.

**Salida esperada:** Las Secciones 2, 3 y 4 están completas con datos reales o estimados, incluyendo al menos un análisis de texto generado por Copilot Chat y un reporte de linting documentado.

**Verificación:** El archivo `evidencia/linting_report.txt` existe y el caso de estudio tiene las tres secciones con tablas completas. Verifica con:

```bash
wc -l docs/caso_estudio.md
# Debe tener al menos 80 líneas
```

---

### Paso 5 — Completar la Sección 5: Lecciones aprendidas y recomendaciones

**Objetivo:** Sintetizar el aprendizaje acumulado y formular recomendaciones prácticas, usando Copilot Chat para estructurar la reflexión final.

#### Instrucciones

1. Antes de redactar, usa Copilot Chat para detonar la reflexión. Escribe el siguiente prompt:

```text
Soy un desarrollador que ha completado un proyecto usando GitHub Copilot Chat como 
asistente principal. He documentado las siguientes observaciones clave:

Positivas:
- [Lista 2-3 cosas que funcionaron bien, de tus notas]

Negativas / Limitaciones:
- [Lista 2-3 cosas que no funcionaron o requirieron corrección]

Con base en esto, ayúdame a:
1. Formular 5 lecciones aprendidas en formato "Aprendí que... porque... En el futuro haré..."
2. Generar 3 recomendaciones prácticas para equipos que quieran adoptar Copilot Chat 
   en proyectos similares, ordenadas por impacto esperado.
3. Identificar 2 escenarios donde Copilot Chat NO sería la herramienta adecuada 
   o requeriría supervisión especialmente cuidadosa.
4. Proponer un "checklist de adopción" de 7 puntos para usar Copilot Chat efectivamente 
   en un proyecto de negocio real.

Formato: Markdown con listas numeradas y viñetas. Sé específico y evita generalidades.
```

2. Incorpora la respuesta de Copilot Chat en la **Sección 5** del caso de estudio, adaptando el contenido a tu experiencia real:

```markdown
## Sección 5: Lecciones Aprendidas y Recomendaciones

### 5.1 Lecciones Aprendidas
1. **Aprendí que** [lección 1]... **porque** [evidencia]... **En el futuro haré** [acción]
2. **Aprendí que** [lección 2]...
3. **Aprendí que** [lección 3]...
4. **Aprendí que** [lección 4]...
5. **Aprendí que** [lección 5]...

### 5.2 Recomendaciones para Equipos de Desarrollo
| Prioridad | Recomendación                                          | Impacto esperado |
|-----------|--------------------------------------------------------|------------------|
| Alta      | [Recomendación 1]                                      | [descripción]    |
| Alta      | [Recomendación 2]                                      | [descripción]    |
| Media     | [Recomendación 3]                                      | [descripción]    |

### 5.3 Escenarios de Uso con Supervisión Especial
- **Escenario 1:** [ej. Código de autenticación y manejo de secretos] — Razón: [...]
- **Escenario 2:** [ej. Lógica de negocio crítica sin pruebas de integración] — Razón: [...]

### 5.4 Checklist de Adopción de Copilot Chat
- [ ] Definir contexto claro del proyecto antes de iniciar prompts
- [ ] Especificar restricciones técnicas y normativas en el primer prompt
- [ ] Exigir siempre supuestos y riesgos en las respuestas
- [ ] Revisar todo código generado con linter antes de integrar
- [ ] Mantener trazabilidad entre prompts y artefactos generados
- [ ] Documentar fallos e imprecisiones para mejorar prompts futuros
- [ ] [Punto adicional de tu experiencia]

### 5.5 Reflexión Meta-Cognitiva: Usar Copilot Chat para Documentar
<!-- ¿Cómo fue la experiencia de usar Copilot Chat para ayudar a redactar este caso de estudio? -->
[Tu reflexión en 3-5 oraciones]
```

3. Registra la interacción de este paso en `evidencia/registro_interacciones.md`.

4. Haz el commit final del documento completo:

```bash
git add .
git commit -m "feat: caso de estudio completo con 5 secciones y evidencia documentada"
```

**Salida esperada:** La Sección 5 contiene al menos 5 lecciones aprendidas, 3 recomendaciones priorizadas, 2 escenarios de supervisión especial y el checklist de adopción. La reflexión meta-cognitiva está presente.

**Verificación:** El documento debe tener las 5 secciones completas. Verifica el historial de commits:

```bash
git log --oneline
# Debe mostrar al menos 2 commits
```

---

### Paso 6 — Revisión final y consolidación de evidencia

**Objetivo:** Revisar la coherencia del caso de estudio, consolidar toda la evidencia y preparar el documento para presentación.

#### Instrucciones

1. Usa Copilot Chat para hacer una revisión editorial del documento completo. Selecciona todo el contenido de `docs/caso_estudio.md` y escribe en el chat:

```text
Revisa el siguiente caso de estudio y proporciona:
1. Una evaluación de coherencia: ¿las secciones están bien conectadas entre sí?
2. Tres sugerencias de mejora en claridad o completitud.
3. Un resumen ejecutivo de 5 oraciones que capture los hallazgos principales.
4. Una puntuación global del documento (1-10) con justificación.

[Pega el contenido del caso de estudio aquí o usa @workspace si tienes el archivo abierto]
```

2. Agrega el **resumen ejecutivo** generado al inicio del documento, antes de la Sección 1:

```markdown
## Resumen Ejecutivo

[Pega aquí el resumen de 5 oraciones generado por Copilot Chat]

**Puntuación de Copilot Chat para este caso de estudio:** [X]/10
**Fecha de elaboración:** [fecha]
**Autor:** [tu nombre o alias]
```

3. Consolida el registro de interacciones con un conteo final en `evidencia/registro_interacciones.md`:

```markdown
## Resumen de Interacciones

| Categoría                          | Cantidad |
|------------------------------------|----------|
| Prompts de generación de artefactos|          |
| Prompts de análisis y revisión     |          |
| Prompts meta-cognitivos (este doc) |          |
| Total de interacciones             |          |
| Interacciones con alta utilidad (4-5/5) |     |
| Interacciones que requirieron corrección |    |
```

4. Realiza el commit final:

```bash
git add .
git commit -m "docs: caso de estudio finalizado con resumen ejecutivo y evidencia consolidada"
git log --oneline
```

5. Exporta o guarda el documento final en el formato que uses (PDF, Word, Google Docs) para tenerlo disponible en la Práctica 10.

**Salida esperada:** El documento `docs/caso_estudio.md` está completo con resumen ejecutivo, 5 secciones desarrolladas y metadatos de autoría. La carpeta `evidencia/` contiene el registro de interacciones consolidado y el reporte de linting.

**Verificación:**

```bash
# Verificar estructura completa del proyecto
find . -type f | sort

# Verificar longitud del caso de estudio
wc -l docs/caso_estudio.md
# Debe tener al menos 100 líneas

# Verificar historial completo
git log --oneline
```

---

## Validación y Pruebas

Usa la siguiente rúbrica para autoevaluar tu caso de estudio antes de darlo por completado:

### Lista de verificación del caso de estudio

| Criterio                                                                 | ✓ / ✗ |
|--------------------------------------------------------------------------|--------|
| El documento tiene las 5 secciones con contenido sustantivo              |        |
| La Sección 1 incluye tabla de KPIs y tabla de artefactos con IDs         |        |
| La Sección 2 describe el flujo de trabajo real aplicado con Copilot Chat |        |
| La Sección 3 tiene datos numéricos (estimados o reales) con fórmulas     |        |
| La Sección 4 documenta al menos 2 casos donde Copilot fue impreciso      |        |
| La Sección 5 tiene al menos 5 lecciones en formato estructurado          |        |
| El registro de interacciones tiene al menos 5 entradas documentadas      |        |
| Se ejecutó el linter y el reporte está guardado en `evidencia/`          |        |
| El repositorio tiene al menos 3 commits con mensajes descriptivos        |        |
| La reflexión meta-cognitiva (usar Copilot para documentar) está presente |        |

### Prueba de coherencia del documento

Ejecuta el siguiente prompt final en Copilot Chat como prueba de coherencia:

```text
Lee el caso de estudio en @docs/caso_estudio.md y responde:
1. ¿Están alineados los KPIs de la Sección 1 con las métricas de la Sección 3?
2. ¿Las lecciones aprendidas (Sección 5) están respaldadas por evidencia en las 
   Secciones 3 y 4?
3. ¿Hay contradicciones o afirmaciones sin soporte entre secciones?
```

Si Copilot identifica inconsistencias, corrígelas antes de finalizar.

---

## Solución de Problemas

### Problema 1: Copilot Chat genera un caso de estudio genérico sin adaptarse al contexto del proyecto

**Síntomas:** Las respuestas de Copilot Chat son plantillas genéricas que no reflejan el proyecto específico (ej. menciona industrias o tecnologías que no corresponden, usa ejemplos de otros dominios).

**Causa probable:** El prompt no incluye suficiente contexto específico del proyecto. Copilot Chat no puede inferir el dominio, tecnología o métricas si no se le proporcionan explícitamente. Esto ocurre especialmente cuando el panel de chat se abre sin ningún archivo del proyecto activo.

**Solución:**
1. Asegúrate de tener el archivo de código relevante de las Prácticas 7/8 abierto en el editor antes de escribir en el chat.
2. Usa la referencia `@workspace` o selecciona el código relevante antes de enviar el prompt.
3. Enriquece el prompt con datos específicos:

```text
# Antes (genérico):
"Genera lecciones aprendidas de usar Copilot Chat"

# Después (específico):
"En mi proyecto de [nombre], usando Python 3.11 y FastAPI, usé Copilot Chat 
para generar [X] endpoints REST. Tuve [N] interacciones, de las cuales [C] 
requirieron corrección, principalmente por [razón específica]. 
Con este contexto, genera 5 lecciones aprendidas..."
```

---

### Problema 2: El linter reporta muchos errores en el código generado por Copilot Chat en prácticas anteriores

**Síntomas:** Al ejecutar `pylint` o `flake8` sobre los archivos de código de las Prácticas 7/8, aparecen más de 10 advertencias o errores (imports no usados, nombres de variables, líneas muy largas, falta de docstrings).

**Causa probable:** Copilot Chat genera código funcional pero no siempre sigue las convenciones de estilo del proyecto (PEP 8 para Python). Esto es un comportamiento esperado y documentable como hallazgo cualitativo del caso de estudio.

**Solución:**
1. No corrijas todos los errores manualmente. Primero **documéntalos** como evidencia en la Sección 4 del caso de estudio.
2. Luego usa Copilot Chat para corregirlos automáticamente como ejercicio adicional:

```text
# Selecciona el código con errores de linting y escribe en el chat:
"Este código tiene los siguientes errores de pylint: [pega los errores].
Corrígelos siguiendo PEP 8, sin cambiar la lógica de negocio. 
Explica brevemente cada cambio realizado."
```

3. Registra cuántos errores existían antes y después de la corrección asistida por Copilot como métrica adicional en la Sección 3.

```bash
# Antes de corrección
pylint codigo/*.py --score=y 2>&1 | grep "Your code"

# Después de corrección asistida
pylint codigo/*.py --score=y 2>&1 | grep "Your code"
```

---

## Limpieza

Esta práctica genera archivos de documentación y código que debes **conservar** para la Práctica 10. No elimines nada de la carpeta `caso-estudio-copilot/`.

Acciones de limpieza opcionales:

```bash
# Eliminar archivos temporales de Python si los hay
find . -name "*.pyc" -delete
find . -name "__pycache__" -type d -exec rm -rf {} + 2>/dev/null || true

# Verificar que el repositorio está limpio
git status
# Debe mostrar "nothing to commit, working tree clean"
```

Si usaste un entorno virtual de Python durante las prácticas anteriores, puedes desactivarlo:

```bash
deactivate  # Si usabas venv
```

> ⚠️ **Importante:** Guarda una copia del archivo `docs/caso_estudio.md` en tu herramienta de procesamiento de texto favorita (Word, Google Docs, Notion). Este documento es el insumo principal de la **Práctica 10** y deberás reflexionar sobre él en la sesión final del curso.

---

## Resumen

En esta práctica construiste un **caso de estudio formal de cinco secciones** que documenta el uso de GitHub Copilot Chat en un proyecto de desarrollo real. Aplicaste el patrón negocio→técnico de la lección 3.1 para estructurar el análisis, desde las necesidades de negocio originales hasta los artefactos técnicos generados. Lo más significativo fue la dimensión **meta-cognitiva**: usaste Copilot Chat no solo para desarrollar software, sino para ayudarte a documentar, analizar y reflexionar sobre su propio uso.

### Puntos clave de esta práctica

- Un caso de estudio efectivo combina **métricas cuantitativas** (tiempo, líneas de código, interacciones) con **observaciones cualitativas** (calidad, fallos, satisfacción) para dar una imagen completa del impacto de Copilot Chat.
- La **trazabilidad** entre necesidades de negocio, artefactos técnicos y resultados es fundamental para evaluar el valor real de cualquier herramienta de IA generativa.
- Copilot Chat puede actuar como asistente en tareas de **documentación y análisis**, no solo de codificación, ampliando su utilidad más allá del desarrollo técnico puro.
- Los **fallos e imprecisiones** de Copilot Chat son tan valiosos como sus aciertos: documentarlos permite mejorar los prompts y establecer prácticas de supervisión adecuadas.
- El rol del programador evoluciona hacia la **revisión crítica, contextualización y validación** del trabajo generado por IA, habilidades que este caso de estudio ejercita directamente.

### Recursos adicionales

- [Documentación oficial de GitHub Copilot Chat](https://docs.github.com/es/copilot/copilot-chat/using-github-copilot-chat)
- [Guía de escritura de casos de estudio técnicos — IEEE](https://www.ieee.org/publications/authors/write-for-us/write-a-case-study.html)
- [Métricas de productividad en desarrollo de software (DORA Metrics)](https://dora.dev/research/)
- [Gherkin Reference — Cucumber](https://cucumber.io/docs/gherkin/reference/)
- [PEP 8 — Guía de estilo para Python](https://peps.python.org/pep-0008/)
- [Buenas prácticas de APIs REST — Microsoft Azure](https://learn.microsoft.com/es-es/azure/architecture/best-practices/api-design)


