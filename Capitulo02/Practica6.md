# Práctica 6: Realiza un pequeño proyecto de codificación donde documentes cada vez que Chat  Copilot te ayude, evaluando su efectividad.

## Metadatos

| Campo            | Detalle                                      |
|------------------|----------------------------------------------|
| **Duración**     | 10 minutos (extensible en modo autónomo)     |
| **Complejidad**  | Alta                                         |
| **Nivel Bloom**  | Crear (*Create*)                             |
| **Módulo**       | 2 — Copilot Chat como Herramienta de Referencia |
| **Práctica**     | 6 de 10                                      |

---

## Descripción General

En esta práctica construirás un mini proyecto de software funcional —una **calculadora de IMC con validaciones**— utilizando GitHub Copilot Chat como herramienta de referencia continua a lo largo de todo el desarrollo. Mientras codificas, llevarás un **diario de intervenciones** donde registrarás cada vez que consultes a Copilot Chat: qué pediste, qué obtuvo, si aceptaste o modificaste la sugerencia y qué tan efectiva fue. Al finalizar, redactarás un análisis crítico de 3 a 5 párrafos reflexionando sobre los escenarios donde Copilot Chat aportó mayor y menor valor. Esta práctica integra directamente los conceptos de la lección 2.1: prompts claros con objetivo, alcance y formato; uso de `/explain`, `/fix` y solicitudes ancladas al código; y verificación crítica de las respuestas.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Desarrollar un proyecto de software funcional utilizando Copilot Chat como referencia técnica continua en cada fase del desarrollo.
- [ ] Documentar sistemáticamente cada intervención de Copilot Chat en un diario estructurado, evaluando su efectividad con criterios definidos.
- [ ] Aplicar buenas prácticas de prompting (objetivo + alcance + formato de salida) para obtener respuestas más precisas y útiles de Copilot Chat.
- [ ] Evaluar críticamente las sugerencias de Copilot Chat, aceptando, modificando o rechazando código según su calidad y adecuación al contexto.
- [ ] Crear un análisis reflexivo sobre el rol de Copilot Chat como herramienta de referencia en un proyecto real de codificación.

---

## Prerrequisitos

### Conocimientos previos
- Haber completado las **Prácticas 4 y 5** del curso.
- Conocimiento básico de estructuras de control (`if/else`, bucles) y funciones en Python (u otro lenguaje elegido).
- Comprensión de los conceptos de la lección 2.1: prompts claros, comandos `/explain`, `/fix`, contexto anclado al código.
- Familiaridad básica con Git para inicializar un repositorio y hacer commits.

### Acceso y herramientas
- Cuenta de GitHub con **suscripción activa a GitHub Copilot** (verificada por el instructor).
- Visual Studio Code 1.90 o superior instalado y funcional.
- Extensión **GitHub Copilot Chat** instalada y autenticada en VS Code.
- Python 3.10 o superior disponible en el sistema (`python --version`).
- Git 2.40 o superior (`git --version`).
- Herramienta de linting instalada (`pylint` o `flake8`).
- Archivo de notas o diario de aprendizaje del curso (iniciado desde la Práctica 1).

---

## Entorno del Laboratorio

### Hardware recomendado

| Componente       | Mínimo                          | Recomendado                      |
|------------------|---------------------------------|----------------------------------|
| Procesador       | Intel Core i5 / AMD Ryzen 5 64-bit | Intel Core i7 / AMD Ryzen 7    |
| RAM              | 8 GB                            | 16 GB                            |
| Espacio en disco | 10 GB libres                    | 15 GB libres                     |
| Conectividad     | 10 Mbps estable                 | 25 Mbps o superior               |
| Resolución       | 1280 × 768                      | 1920 × 1080                      |

### Software requerido

| Herramienta                   | Versión mínima         | Verificación                        |
|-------------------------------|------------------------|-------------------------------------|
| Visual Studio Code            | 1.90                   | `code --version`                    |
| GitHub Copilot Chat (extensión)| Última del marketplace | Panel de extensiones en VS Code     |
| Python                        | 3.10                   | `python --version`                  |
| Git                           | 2.40                   | `git --version`                     |
| pylint o flake8               | pylint 3.x / flake8 7.x| `pylint --version` / `flake8 --version` |

### Configuración inicial del entorno

Ejecuta los siguientes comandos en tu terminal para preparar el entorno del proyecto antes de iniciar la práctica:

```bash
# 1. Crear y navegar al directorio del proyecto
mkdir practica6-imc-calculator
cd practica6-imc-calculator

# 2. Inicializar repositorio Git
git init
git config user.name "Tu Nombre"
git config user.email "tu@email.com"

# 3. Crear entorno virtual de Python
python -m venv .venv

# En macOS/Linux:
source .venv/bin/activate

# En Windows (PowerShell):
.venv\Scripts\Activate.ps1

# 4. Instalar herramienta de linting
pip install pylint

# 5. Abrir el proyecto en VS Code
code .
```

> **Nota:** Si VS Code no abre automáticamente con `code .`, ábrelo manualmente y selecciona la carpeta `practica6-imc-calculator` con **File → Open Folder**.

---

## Pasos del Laboratorio

---

### Paso 1: Preparar el Diario de Intervenciones y la Estructura del Proyecto

**Objetivo:** Crear la estructura de archivos del proyecto y el plantilla del diario de intervenciones antes de comenzar a codificar, para poder documentar cada consulta a Copilot Chat de manera sistemática desde el inicio.

#### Instrucciones

1. En VS Code, crea los siguientes archivos en la raíz del proyecto usando el explorador de archivos lateral o la terminal integrada:

```bash
# Desde la terminal integrada de VS Code (Ctrl+` / Cmd+`)
touch imc_calculator.py
touch diario_intervenciones.md
touch README.md
```

2. Abre `diario_intervenciones.md` y copia la siguiente plantilla completa. Este archivo es el núcleo de la práctica:

```markdown
# Diario de Intervenciones — Copilot Chat
## Proyecto: Calculadora de IMC con Validaciones
## Fecha: [FECHA DE HOY]
## Participante: [TU NOMBRE]

---

## Plantilla de Registro (copiar para cada intervención)

| Campo                  | Detalle |
|------------------------|---------|
| **# Intervención**     | N       |
| **Fase del proyecto**  | [Estructura / Lógica / Validaciones / Documentación / Refactor] |
| **Tipo de ayuda**      | [Autocompletado / Generación desde comentario / /explain / /fix / Consulta de referencia] |
| **Prompt utilizado**   | [Texto exacto del prompt enviado a Copilot Chat] |
| **Código sugerido**    | [Fragmento sugerido por Copilot Chat, o "No código / solo explicación"] |
| **Decisión tomada**    | [Aceptado sin cambios / Modificado (describir qué) / Rechazado (describir por qué)] |
| **Efectividad (1-5)**  | [1=Inútil, 2=Poco útil, 3=Útil con ajustes, 4=Muy útil, 5=Excelente] |
| **Observaciones**      | [Reflexión breve: ¿por qué fue o no fue efectivo?] |

---

## Registro de Intervenciones

<!-- Aquí irás agregando cada intervención numerada -->

---

## Análisis Final (completar al terminar el proyecto)

### Párrafo 1 — Resumen del proyecto y uso general de Copilot Chat

### Párrafo 2 — Escenarios de mayor valor

### Párrafo 3 — Escenarios de menor valor o limitaciones encontradas

### Párrafo 4 — Impacto en productividad y calidad del código

### Párrafo 5 — Reflexión personal sobre el rol de Copilot Chat como referencia
```

3. Guarda el archivo (`Ctrl+S` / `Cmd+S`).

4. Abre `README.md` y escribe una descripción mínima del proyecto:

```markdown
# Calculadora de IMC con Validaciones

Mini proyecto desarrollado en la Práctica 6 del curso.

## Descripción
Script en Python que calcula el Índice de Masa Corporal (IMC) de una persona,
con validaciones de entrada y clasificación del resultado según estándares de la OMS.

## Ejecución
```bash
python imc_calculator.py
```

## Autor
[Tu nombre] — [Fecha]
```

5. Haz un primer commit para registrar la estructura inicial:

```bash
git add .
git commit -m "chore: estructura inicial del proyecto y plantilla del diario"
```

#### Salida esperada

```
[main (root-commit) abc1234] chore: estructura inicial del proyecto y plantilla del diario
 3 files changed, 60 insertions(+)
 create mode 100644 README.md
 create mode 100644 diario_intervenciones.md
 create mode 100644 imc_calculator.py
```

#### Verificación

- [ ] Los tres archivos aparecen en el explorador de VS Code.
- [ ] El diario contiene la plantilla completa con todos los campos.
- [ ] El commit inicial aparece en `git log --oneline`.

---

### Paso 2: Generar la Estructura Base del Proyecto con Copilot Chat

**Objetivo:** Usar Copilot Chat como herramienta de referencia para generar la estructura base del script, documentando esta primera intervención en el diario.

#### Instrucciones

1. Abre `imc_calculator.py` en el editor. El archivo está vacío.

2. Abre el panel de Copilot Chat con `Ctrl+Alt+I` (Windows/Linux) o `Cmd+Alt+I` (macOS), o haz clic en el ícono de Copilot Chat en la barra lateral.

3. Envía el siguiente prompt a Copilot Chat (aplica las buenas prácticas de la lección 2.1: especifica objetivo, alcance y formato):

```
Dame la estructura base de un script Python para una calculadora de IMC.
El script debe incluir:
- Una función para calcular el IMC dado peso (kg) y altura (m)
- Una función para clasificar el IMC según estándares OMS (bajo peso, normal, sobrepeso, obesidad)
- Una función main() con un menú de consola simple
- Docstrings en cada función
- Manejo básico de errores de entrada

Formato: código Python comentado, con type hints. Solo la estructura con funciones vacías o con lógica mínima, sin implementación completa todavía.
```

4. Revisa la respuesta de Copilot Chat. Observa si:
   - Incluye type hints
   - Incluye docstrings
   - La estructura es coherente con lo solicitado

5. Copia el código sugerido a `imc_calculator.py`. Si necesitas modificaciones menores (nombres de funciones, estructura del menú), aplícalas ahora.

6. **Registra esta intervención en `diario_intervenciones.md`** usando la plantilla. Ejemplo de cómo debería verse:

```markdown
## Intervención #1

| Campo                  | Detalle |
|------------------------|---------|
| **# Intervención**     | 1       |
| **Fase del proyecto**  | Estructura |
| **Tipo de ayuda**      | Generación desde prompt de referencia |
| **Prompt utilizado**   | "Dame la estructura base de un script Python..." [texto completo] |
| **Código sugerido**    | [Pega aquí el fragmento principal sugerido] |
| **Decisión tomada**    | Aceptado con modificación menor: renombré `classify_bmi` a `clasificar_imc` |
| **Efectividad (1-5)**  | 4 |
| **Observaciones**      | La estructura fue coherente y ahorró ~3 minutos de diseño inicial. Faltaron type hints en un parámetro. |
```

7. Guarda ambos archivos y haz un commit:

```bash
git add .
git commit -m "feat: estructura base del script de IMC (generada con Copilot Chat)"
```

#### Salida esperada

Tu `imc_calculator.py` debe verse similar a esto (la estructura exacta puede variar según lo que Copilot Chat genere):

```python
"""
Calculadora de IMC con validaciones.
Proyecto: Práctica 6 — Uso de Copilot Chat como herramienta de referencia.
"""

def calcular_imc(peso_kg: float, altura_m: float) -> float:
    """
    Calcula el Índice de Masa Corporal (IMC).

    Args:
        peso_kg: Peso de la persona en kilogramos.
        altura_m: Altura de la persona en metros.

    Returns:
        Valor del IMC como número de punto flotante.
    """
    pass  # Implementación pendiente


def clasificar_imc(imc: float) -> str:
    """
    Clasifica el IMC según los estándares de la OMS.

    Args:
        imc: Valor del IMC calculado.

    Returns:
        Clasificación como cadena de texto.
    """
    pass  # Implementación pendiente


def solicitar_dato(mensaje: str, tipo: type):
    """
    Solicita un dato al usuario con validación de tipo.

    Args:
        mensaje: Texto del prompt para el usuario.
        tipo: Tipo de dato esperado (float, int, etc.).

    Returns:
        El dato ingresado convertido al tipo especificado.
    """
    pass  # Implementación pendiente


def main() -> None:
    """Función principal: menú de consola para la calculadora de IMC."""
    pass  # Implementación pendiente


if __name__ == "__main__":
    main()
```

#### Verificación

- [ ] El archivo `imc_calculator.py` tiene al menos 3 funciones con docstrings.
- [ ] La Intervención #1 está registrada en el diario con todos los campos completados.
- [ ] El commit fue creado exitosamente.

---

### Paso 3: Implementar la Lógica Principal con Copilot Chat como Referencia

**Objetivo:** Implementar las funciones `calcular_imc` y `clasificar_imc` utilizando Copilot Chat para consultas específicas de referencia, documentando al menos 2 intervenciones adicionales.

#### Instrucciones

1. Posiciona el cursor dentro del cuerpo de la función `calcular_imc` (sobre el `pass`).

2. Selecciona la función completa (incluyendo docstring) y abre Copilot Chat con la selección activa.

3. Envía este prompt anclado al código seleccionado:

```
/explain Explica qué validaciones debo agregar a esta función para que sea robusta.
Específicamente: ¿qué valores de peso y altura son inválidos?
¿Debo lanzar excepciones o retornar valores especiales?
Dame la implementación completa con las validaciones, usando ValueError con mensajes descriptivos.
```

4. Revisa la respuesta. Copilot Chat debería sugerir validaciones como:
   - `peso_kg <= 0` → `ValueError`
   - `altura_m <= 0` o `altura_m > 3` → `ValueError`
   - División por `altura_m ** 2`

5. Implementa `calcular_imc` con las validaciones sugeridas (acepta, modifica o rechaza según tu criterio). **Registra como Intervención #2.**

6. Ahora escribe el siguiente comentario directamente en el cuerpo de `clasificar_imc` (autocompletado desde comentario):

```python
def clasificar_imc(imc: float) -> str:
    # Clasificar según rangos OMS:
    # < 18.5: Bajo peso
    # 18.5 - 24.9: Normal
    # 25.0 - 29.9: Sobrepeso
    # >= 30.0: Obesidad
```

7. Presiona `Enter` después del último comentario y observa si Copilot (autocompletado inline) sugiere la implementación. Acepta con `Tab` si la sugerencia es correcta.

8. Si el autocompletado no aparece o es incompleto, usa Copilot Chat con:

```
Implementa la función clasificar_imc() usando los rangos de los comentarios.
Devuelve strings en español. Incluye el rango numérico en el string de retorno.
Ejemplo de formato: "Normal (IMC: 22.5 — Rango: 18.5–24.9)"
```

9. **Registra como Intervención #3** (ya sea el autocompletado inline o la consulta al chat).

10. Verifica que el código funcione ejecutando una prueba rápida en la terminal:

```bash
python -c "
from imc_calculator import calcular_imc, clasificar_imc
imc = calcular_imc(70, 1.75)
print(f'IMC: {imc:.2f}')
print(clasificar_imc(imc))
"
```

11. Haz commit:

```bash
git add imc_calculator.py diario_intervenciones.md
git commit -m "feat: implementación de calcular_imc y clasificar_imc con validaciones"
```

#### Salida esperada

```
IMC: 22.86
Normal (IMC: 22.86 — Rango: 18.5–24.9)
```

La implementación de `calcular_imc` debe incluir validaciones similares a:

```python
def calcular_imc(peso_kg: float, altura_m: float) -> float:
    if peso_kg <= 0:
        raise ValueError(f"El peso debe ser mayor a 0. Recibido: {peso_kg}")
    if altura_m <= 0 or altura_m > 3.0:
        raise ValueError(f"La altura debe estar entre 0 y 3 metros. Recibida: {altura_m}")
    return peso_kg / (altura_m ** 2)
```

#### Verificación

- [ ] `calcular_imc(70, 1.75)` retorna aproximadamente `22.86`.
- [ ] `clasificar_imc(22.86)` retorna una cadena que incluye "Normal".
- [ ] `calcular_imc(-5, 1.70)` lanza `ValueError`.
- [ ] Las Intervenciones #2 y #3 están registradas en el diario.

---

### Paso 4: Implementar la Función de Entrada con Validación Robusta

**Objetivo:** Implementar `solicitar_dato()` con manejo de errores, usando Copilot Chat específicamente para pedir referencia sobre patrones idiomáticos de validación de entrada en Python, y documentar la intervención evaluando la calidad del patrón sugerido.

#### Instrucciones

1. Selecciona la función `solicitar_dato` completa en el editor.

2. Con la selección activa, abre Copilot Chat y envía:

```
/explain Muéstrame el patrón idiomático en Python para solicitar un dato numérico al usuario
con reintentos en caso de entrada inválida (bucle while + try/except).
La función debe:
- Aceptar un parámetro `intentos_max` (default: 3)
- Lanzar un RuntimeError si se agotan los intentos
- Mostrar mensajes de error claros al usuario
- Funcionar con float e int según el parámetro `tipo`
Dame el código completo con type hints y docstring actualizado.
```

3. Analiza críticamente la respuesta:
   - ¿El bucle `while` está bien estructurado?
   - ¿El manejo de `ValueError` es apropiado?
   - ¿Los mensajes de error son claros para el usuario?
   - ¿Hay algún edge case no cubierto?

4. Implementa la función. Si modificas algo del código sugerido, anota exactamente qué y por qué en el diario.

5. **Registra como Intervención #4.** En las observaciones, sé específico sobre la calidad del patrón sugerido.

6. Ahora implementa la función `main()`. Escribe primero estos comentarios en su cuerpo y observa el autocompletado:

```python
def main() -> None:
    """Función principal: menú de consola para la calculadora de IMC."""
    print("=== Calculadora de IMC ===")
    # Solicitar nombre del usuario
    # Solicitar peso en kg usando solicitar_dato
    # Solicitar altura en metros usando solicitar_dato
    # Calcular IMC y manejar posibles ValueError
    # Mostrar resultado con clasificación
    # Preguntar si desea calcular otro IMC
```

7. Deja que Copilot Chat (autocompletado inline) sugiera la implementación a partir de los comentarios. Acepta las sugerencias que sean correctas con `Tab`.

8. Si el autocompletado no genera la implementación completa, consulta a Copilot Chat:

```
Implementa la función main() según los comentarios del cuerpo.
Incluye un bucle que permita calcular el IMC de múltiples personas.
Usa un bloque try/except para manejar ValueError de calcular_imc.
Muestra el resultado con 2 decimales.
```

9. **Registra como Intervención #5.**

10. Ejecuta el script completo para verificar el flujo:

```bash
python imc_calculator.py
```

11. Haz commit:

```bash
git add imc_calculator.py diario_intervenciones.md
git commit -m "feat: implementación de solicitar_dato y main() con manejo de errores"
```

#### Salida esperada al ejecutar el script

```
=== Calculadora de IMC ===
Ingresa tu nombre: Ana
Ingresa tu peso en kg: 65
Ingresa tu altura en metros: 1.68

=== Resultado para Ana ===
IMC: 23.03
Clasificación: Normal (IMC: 23.03 — Rango: 18.5–24.9)

¿Deseas calcular otro IMC? (s/n): n
¡Hasta luego!
```

#### Verificación

- [ ] El script ejecuta sin errores con entradas válidas.
- [ ] Al ingresar texto donde se espera un número, muestra un mensaje de error y reintenta.
- [ ] Al agotar los intentos máximos, el programa termina con un mensaje apropiado.
- [ ] Las Intervenciones #4 y #5 están registradas con observaciones detalladas.

---

### Paso 5: Usar `/fix` para Mejorar el Código y Detectar Pitfalls

**Objetivo:** Aplicar el comando `/fix` y consultas de detección de problemas de Copilot Chat para mejorar la calidad del código, documentando si las sugerencias son valiosas o superficiales.

#### Instrucciones

1. Selecciona todo el contenido de `imc_calculator.py` (Ctrl+A / Cmd+A).

2. Abre Copilot Chat y envía:

```
/fix Revisa este código e identifica:
1. Posibles condiciones de error no manejadas
2. Problemas de usabilidad (mensajes poco claros para el usuario)
3. Violaciones de PEP 8 o malas prácticas de Python
4. Cualquier edge case no cubierto en las validaciones

Para cada problema encontrado, muestra el código actual y el código corregido.
Sé específico con los números de línea si es posible.
```

3. Revisa cada sugerencia de `/fix` críticamente:
   - ¿Identificó problemas reales o falsos positivos?
   - ¿Las correcciones son mejoras genuinas?
   - ¿Hay sugerencias que no aplican a este contexto?

4. Aplica únicamente las correcciones que consideres válidas. Rechaza o ignora las que no aporten valor real.

5. **Registra como Intervención #6.** Esta intervención es especialmente importante para el análisis final: documenta con detalle qué sugerencias aceptaste, cuáles rechazaste y por qué.

6. Ejecuta el linter para validar la calidad del código de forma independiente:

```bash
# Con pylint
pylint imc_calculator.py

# O con flake8
flake8 imc_calculator.py
```

7. Si el linter reporta problemas que Copilot Chat no detectó, anota esta discrepancia en las observaciones de la Intervención #6.

8. Selecciona la función `calcular_imc` y pide una consulta de referencia adicional:

```
Explica si hay algún pitfall de precisión numérica al calcular IMC con punto flotante en Python.
¿Debo usar round() en el retorno o en la presentación? ¿Por qué?
```

9. **Registra como Intervención #7** (consulta de referencia pura, sin código).

10. Aplica los ajustes finales y haz commit:

```bash
git add imc_calculator.py diario_intervenciones.md
git commit -m "refactor: mejoras de calidad aplicadas tras /fix y revisión de linting"
```

#### Salida esperada del linter

Idealmente deberías ver una puntuación de pylint de **8.0/10 o superior**, o cero errores en flake8. Ejemplo:

```
--------------------------------------------------------------------
Your code has been rated at 9.20/10 (previous run: 8.50/10, +0.70)
```

#### Verificación

- [ ] El linter reporta 0 errores críticos (pueden quedar advertencias menores).
- [ ] La Intervención #6 documenta explícitamente qué sugerencias de `/fix` fueron aceptadas y cuáles rechazadas.
- [ ] La Intervención #7 está registrada como consulta de referencia (sin código).
- [ ] El commit fue creado.

---

### Paso 6: Documentar el Proyecto y Redactar el Análisis Final

**Objetivo:** Usar Copilot Chat para generar documentación del proyecto y, a continuación, redactar el análisis crítico final en el diario de intervenciones, sintetizando las lecciones aprendidas sobre el uso de Copilot Chat como herramienta de referencia.

#### Instrucciones

1. Abre `README.md`. Selecciona todo su contenido.

2. Consulta a Copilot Chat:

```
Basándote en el archivo imc_calculator.py de este proyecto,
genera un README.md completo que incluya:
- Descripción del proyecto
- Requisitos (Python 3.10+)
- Instrucciones de instalación y ejecución
- Ejemplos de uso con salida esperada
- Descripción de las funciones principales
- Notas sobre validaciones implementadas

Formato: Markdown limpio con secciones bien definidas.
```

3. Revisa y adapta el README generado. Acepta lo que sea correcto, modifica lo que necesite ajuste.

4. **Registra como Intervención #8.**

5. Ahora cierra el editor de código y abre únicamente `diario_intervenciones.md`.

6. Redacta el **Análisis Final** en la sección correspondiente del diario. Este análisis debe ser personal y reflexivo. Usa las siguientes guías para cada párrafo (escribe entre 80 y 150 palabras por párrafo):

   **Párrafo 1 — Resumen del proyecto y uso general:**
   Describe brevemente el proyecto construido, cuántas intervenciones de Copilot Chat realizaste en total, y una impresión general de la experiencia.

   **Párrafo 2 — Escenarios de mayor valor:**
   Identifica 2 o 3 intervenciones específicas (cítalas por número) donde Copilot Chat fue más efectivo. ¿Por qué funcionó bien? ¿Qué características del prompt o del contexto contribuyeron?

   **Párrafo 3 — Escenarios de menor valor o limitaciones:**
   Identifica 1 o 2 intervenciones donde Copilot Chat fue menos útil o donde tuviste que rechazar/modificar significativamente el código. ¿Qué falló? ¿Fue el prompt, el contexto, o una limitación del modelo?

   **Párrafo 4 — Impacto en productividad:**
   Estima cuánto tiempo ahorraste (o perdiste) usando Copilot Chat comparado con escribir el código sin asistencia. ¿El tiempo de revisión y corrección fue significativo?

   **Párrafo 5 — Reflexión sobre el rol de Copilot Chat como referencia:**
   Conecta tu experiencia con los conceptos de la lección 2.1. ¿Copilot Chat actuó como un "manual de bolsillo" efectivo? ¿En qué se diferencia de buscar en Google o en la documentación oficial?

7. Haz el commit final del proyecto:

```bash
git add .
git commit -m "docs: README completo y análisis final del diario de intervenciones"
```

8. Verifica el historial completo de commits:

```bash
git log --oneline
```

#### Salida esperada de `git log --oneline`

```
f3e9a12 docs: README completo y análisis final del diario de intervenciones
b2c7d45 refactor: mejoras de calidad aplicadas tras /fix y revisión de linting
9a1e823 feat: implementación de solicitar_dato y main() con manejo de errores
7f4c210 feat: implementación de calcular_imc y clasificar_imc con validaciones
3d8b091 feat: estructura base del script de IMC (generada con Copilot Chat)
1a2b3c4 chore: estructura inicial del proyecto y plantilla del diario
```

#### Verificación

- [ ] El `README.md` tiene todas las secciones solicitadas y es coherente con el código real.
- [ ] El análisis final tiene los 5 párrafos completos con reflexiones específicas.
- [ ] El historial de Git muestra al menos 5 commits que documentan la evolución del proyecto.
- [ ] La Intervención #8 está registrada en el diario.

---

## Validación y Pruebas

### Prueba de Funcionalidad Completa

Ejecuta la siguiente secuencia de pruebas para validar que el proyecto está completo y funcional:

```bash
# Prueba 1: Ejecución normal con valores válidos
echo "Prueba 1: IMC normal"
python -c "
from imc_calculator import calcular_imc, clasificar_imc
imc = calcular_imc(70, 1.75)
assert 22.0 < imc < 23.0, f'IMC inesperado: {imc}'
clasificacion = clasificar_imc(imc)
assert 'Normal' in clasificacion, f'Clasificación inesperada: {clasificacion}'
print(f'✓ IMC: {imc:.2f} — {clasificacion}')
"

# Prueba 2: Validación de entradas inválidas
echo "Prueba 2: Entradas inválidas"
python -c "
from imc_calculator import calcular_imc
import sys

try:
    calcular_imc(-10, 1.70)
    print('✗ ERROR: Debería haber lanzado ValueError para peso negativo')
    sys.exit(1)
except ValueError as e:
    print(f'✓ ValueError capturado correctamente: {e}')

try:
    calcular_imc(70, 0)
    print('✗ ERROR: Debería haber lanzado ValueError para altura cero')
    sys.exit(1)
except ValueError as e:
    print(f'✓ ValueError capturado correctamente: {e}')
"

# Prueba 3: Clasificaciones en los límites de rangos OMS
echo "Prueba 3: Clasificaciones en límites de rangos"
python -c "
from imc_calculator import clasificar_imc
casos = [
    (17.0, 'Bajo peso'),
    (18.5, 'Normal'),
    (24.9, 'Normal'),
    (25.0, 'Sobrepeso'),
    (29.9, 'Sobrepeso'),
    (30.0, 'Obesidad'),
    (35.0, 'Obesidad'),
]
for imc_val, esperado in casos:
    resultado = clasificar_imc(imc_val)
    assert esperado in resultado, f'Para IMC {imc_val}: esperado \"{esperado}\", obtenido \"{resultado}\"'
    print(f'✓ IMC {imc_val}: {resultado}')
"

# Prueba 4: Verificación de linting
echo "Prueba 4: Calidad de código"
pylint imc_calculator.py --fail-under=7.0
echo "✓ Linting superado con puntuación >= 7.0"
```

### Lista de Verificación Final del Diario

Antes de dar por completada la práctica, verifica que tu `diario_intervenciones.md` cumpla con:

- [ ] **Mínimo 6 intervenciones registradas** (se recomiendan 8).
- [ ] Cada intervención tiene **todos los campos completados** (ningún campo vacío o con "[pendiente]").
- [ ] Las calificaciones de efectividad (1-5) son **variadas y justificadas** (no todas son 5).
- [ ] Al menos **una intervención fue rechazada o modificada significativamente** (decisión ≠ "Aceptado sin cambios").
- [ ] El **análisis final tiene los 5 párrafos** completos.
- [ ] Los párrafos del análisis **citan intervenciones específicas** por número.

---

## Solución de Problemas

### Problema 1: Copilot Chat no genera código en Python sino en otro lenguaje

**Síntomas:** Las sugerencias de Copilot Chat vienen en JavaScript, TypeScript u otro lenguaje, aunque el archivo activo es `.py`.

**Causa probable:** El archivo `imc_calculator.py` no estaba abierto o activo como contexto cuando se envió el prompt. Copilot Chat infiere el lenguaje del archivo activo; si el foco estaba en `diario_intervenciones.md` (archivo Markdown), el chat puede perder el contexto del lenguaje.

**Solución:**
1. Asegúrate de que `imc_calculator.py` esté abierto y sea la pestaña activa en el editor antes de abrir Copilot Chat.
2. Especifica explícitamente el lenguaje en el prompt: *"En Python 3.10, dame..."*
3. Si el chat ya estaba abierto, ciérralo y ábrelo nuevamente con `imc_calculator.py` como archivo activo.
4. Cuando selecciones código antes de abrir el chat, el contexto se ancla automáticamente al fragmento seleccionado, lo que fuerza el lenguaje correcto.

```
# Ejemplo de prompt con lenguaje explícito:
"En Python 3.10, implementa la función calcular_imc con las siguientes validaciones..."
```

---

### Problema 2: El script falla con `RecursionError` o `ZeroDivisionError` en casos edge

**Síntomas:** Al ejecutar las pruebas de validación, el script lanza `ZeroDivisionError` en lugar de `ValueError` para altura = 0, o falla inesperadamente con valores muy pequeños de altura.

**Causa probable:** La validación de `altura_m` en `calcular_imc` verifica `altura_m <= 0` pero la división `peso_kg / (altura_m ** 2)` puede ocurrir antes de que se evalúe la condición, o la condición está mal ordenada en el código (la división se ejecuta antes del `if`).

**Solución:**
1. Verifica que las validaciones estén **antes** de la operación de cálculo:

```python
def calcular_imc(peso_kg: float, altura_m: float) -> float:
    # ✅ CORRECTO: validaciones PRIMERO
    if peso_kg <= 0:
        raise ValueError(f"El peso debe ser mayor a 0. Recibido: {peso_kg}")
    if altura_m <= 0 or altura_m > 3.0:
        raise ValueError(f"La altura debe estar entre 0 y 3 metros. Recibida: {altura_m}")
    # La división ocurre DESPUÉS de las validaciones
    return peso_kg / (altura_m ** 2)
```

2. Si el código generado por Copilot Chat tenía el orden incorrecto, selecciona la función, abre el chat y envía:

```
/fix Esta función lanza ZeroDivisionError en lugar de ValueError cuando altura_m=0.
Las validaciones deben ejecutarse antes del cálculo. Corrige el orden.
```

3. Anota este caso en tu diario como un ejemplo de código generado que requirió corrección, con la causa y la solución aplicada.

---

## Limpieza del Entorno

Al finalizar la práctica, realiza los siguientes pasos de limpieza:

```bash
# 1. Desactivar el entorno virtual
deactivate

# 2. Verificar que todos los cambios están commiteados
git status
# Debe mostrar: "nothing to commit, working tree clean"

# 3. (Opcional) Ver el resumen completo del proyecto
git log --oneline --all
```

> **⚠️ Importante — NO elimines el proyecto:** Los archivos de esta práctica (especialmente `diario_intervenciones.md` y `imc_calculator.py`) son necesarios para las **Prácticas 7, 8 y 9** del Módulo 3, que tienen dependencias directas con este trabajo. Conserva la carpeta `practica6-imc-calculator` en tu disco local.

```bash
# 4. (Opcional) Crear un archivo ZIP de respaldo si lo deseas
cd ..
zip -r practica6-imc-calculator-backup.zip practica6-imc-calculator/
```

---

## Resumen

### Lo que construiste y documentaste

En esta práctica desarrollaste un **mini proyecto de software funcional** — una calculadora de IMC con validaciones en Python — y simultáneamente mantuviste un **diario de intervenciones** que registró sistemáticamente cada consulta realizada a GitHub Copilot Chat. A través de 8 intervenciones documentadas, practicaste los flujos de trabajo centrales de la lección 2.1:

| Concepto de la Lección 2.1          | Aplicación en la Práctica                                          |
|--------------------------------------|--------------------------------------------------------------------|
| Prompts con objetivo + alcance + formato | Cada consulta especificó qué generar, para qué y en qué formato |
| Contexto anclado al código           | Seleccionar funciones antes de abrir el chat                       |
| Comandos `/explain` y `/fix`         | Usados en Pasos 3 y 5 respectivamente                              |
| Validación crítica de respuestas     | Aceptar, modificar o rechazar según calidad real                   |
| Copilot Chat como "manual de bolsillo"| Consultas de referencia sobre patrones idiomáticos y pitfalls     |

### Lecciones clave para llevar

- **El contexto importa más que el prompt:** Las intervenciones más efectivas fueron aquellas donde el código relevante estaba seleccionado al abrir el chat.
- **Copilot Chat no reemplaza el juicio crítico:** El valor real está en saber cuándo aceptar, modificar o rechazar una sugerencia.
- **El diario de intervenciones es una herramienta de metacognición:** Documentar en tiempo real revela patrones de uso que no serían visibles al final.
- **`/fix` es más útil como punto de partida que como solución definitiva:** Sus sugerencias deben complementarse con linting y revisión manual.

### Próximos pasos

- **Práctica 7 (Módulo 3):** Extenderás el proyecto de esta práctica agregando nuevas funcionalidades, donde el diario de intervenciones será el punto de partida para medir mejoras en tu estrategia de prompting.
- **Práctica 9:** Usarás el análisis final de este diario como insumo para una reflexión más amplia sobre la evolución del rol del programador.
- **Hábito recomendado:** Mantén el diario de intervenciones activo en tus proyectos personales durante al menos dos semanas para acumular datos suficientes para una reflexión significativa.

### Recursos adicionales

- [Copilot Chat en Visual Studio Code — Documentación oficial](https://code.visualstudio.com/docs/copilot/copilot-chat)
- [Acerca de GitHub Copilot Chat](https://docs.github.com/en/copilot/copilot-chat/about-github-copilot-chat)
- [Guía de inicio de GitHub Copilot en VS Code](https://code.visualstudio.com/docs/copilot/getting-started)
- [Consejos prácticos para aprovechar GitHub Copilot (GitHub Blog)](https://github.blog/news-insights/product-news/getting-the-most-out-of-github-copilot-tips-tricks-hacks/)
- [Clasificación de IMC — Organización Mundial de la Salud](https://www.who.int/es/news-room/fact-sheets/detail/obesity-and-overweight)
