# Práctica 11: Compara un código generado por Copilot Chat con buenas prácticas recomendadas y valida si cumple con ellas.

## Metadatos

| Campo            | Detalle                                                                 |
|------------------|-------------------------------------------------------------------------|
| **Duración**     | 9 minutos                                                               |
| **Complejidad**  | Media                                                                   |
| **Nivel Bloom**  | Aplicar                                                                 |
| **Módulo**       | 4 — Evolución del Rol del Programador                                   |
| **Tema**         | 4.1 Evolución del Rol del Programador                                   |
| **Lenguaje**     | Python 3.10+ (adaptable a JavaScript, Java, TypeScript, C#)             |

---

## Descripción General

En esta práctica actuarás como **curador de calidad** —uno de los nuevos roles del programador moderno descritos en el tema 4.1— al evaluar críticamente un fragmento de código generado por Copilot Chat. Utilizarás un prompt estructurado para obtener una función de complejidad media, luego la contrastarás sistemáticamente contra al menos cinco buenas prácticas provenientes de guías reconocidas (PEP 8, principios SOLID, *Clean Code*). El resultado será una **rúbrica de evaluación** documentada que evidencia que la responsabilidad de la calidad del código sigue residiendo en el programador, no en la IA.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Generar un fragmento de código funcional de complejidad media utilizando un prompt estructurado en Copilot Chat.
- [ ] Identificar y aplicar al menos cinco buenas prácticas de programación como criterios de evaluación (nomenclatura, modularidad, manejo de errores, legibilidad, documentación).
- [ ] Comparar sistemáticamente el código generado contra las buenas prácticas seleccionadas, documentando hallazgos en una rúbrica.
- [ ] Determinar si el código **cumple**, **cumple parcialmente** o **no cumple** con cada práctica, justificando la evaluación con evidencia concreta del código.

---

## Prerrequisitos

### Conocimiento previo
- Conocimiento básico de al menos un lenguaje de programación (Python recomendado).
- Familiaridad con el uso básico de Copilot Chat para generación de código (Prácticas 1–10 del curso).
- Noción general de qué son las buenas prácticas de programación (PEP 8, Clean Code, SOLID).

### Acceso y herramientas
- Suscripción activa a **GitHub Copilot** (verificada antes de iniciar).
- **Visual Studio Code 1.90+** con la extensión **GitHub Copilot Chat** instalada y autenticada.
- **Python 3.10+** instalado y accesible desde la terminal.
- Herramienta de linting: **pylint** o **flake8** instalada (`pip install pylint` o `pip install flake8`).
- Procesador de texto (Word, Google Docs, Notion o un archivo `.md`) para registrar la rúbrica.
- Diario de aprendizaje del curso activo y disponible.

---

## Entorno de Laboratorio

### Tabla de hardware requerido

| Componente        | Mínimo recomendado                              |
|-------------------|-------------------------------------------------|
| Procesador        | Intel Core i5 / AMD Ryzen 5 de 64 bits          |
| RAM               | 8 GB (16 GB recomendado)                        |
| Espacio en disco  | 10 GB libres                                    |
| Resolución        | 1280 × 768 o superior                           |
| Conectividad      | Internet estable ≥ 10 Mbps                      |

### Tabla de software requerido

| Herramienta                  | Versión mínima          | Rol en la práctica                          |
|------------------------------|-------------------------|---------------------------------------------|
| Visual Studio Code           | 1.90                    | IDE principal                               |
| GitHub Copilot Chat (ext.)   | Última disponible       | Generación del código a evaluar             |
| Python                       | 3.10                    | Lenguaje del fragmento generado             |
| pylint / flake8              | pylint 3.x / flake8 7.x | Validación automática de estilo             |
| Procesador de texto / `.md`  | Cualquier versión       | Registro de la rúbrica de evaluación        |

### Comandos de configuración del entorno

Abre una terminal en VS Code (`Ctrl+`` ` `` `) y ejecuta lo siguiente para verificar que todo está en orden:

```bash
# Verificar versión de Python
python --version

# Verificar pip
pip --version

# Instalar pylint y flake8 si no están disponibles
pip install pylint flake8

# Verificar instalación
pylint --version
flake8 --version
```

Crea la carpeta de trabajo para esta práctica:

```bash
mkdir lab-practica-11
cd lab-practica-11
```

Abre la carpeta en VS Code:

```bash
code .
```

> **Nota:** Asegúrate de que la extensión GitHub Copilot Chat muestre el ícono activo (sin advertencias de autenticación) en la barra lateral de VS Code antes de continuar.

---

## Pasos del Laboratorio

---

### Paso 1 — Preparar el archivo de trabajo y el documento de rúbrica

**Objetivo:** Establecer los archivos donde se registrará el código generado y la evaluación, siguiendo el ciclo *Enunciar* del tema 4.1.

**Instrucciones:**

1. Dentro de la carpeta `lab-practica-11`, crea el archivo Python que recibirá el código generado:

    ```bash
    # En la terminal integrada de VS Code
    touch procesador_csv.py
    ```

2. Crea también el archivo de rúbrica en Markdown:

    ```bash
    touch rubrica_evaluacion.md
    ```

3. Abre `rubrica_evaluacion.md` y añade la siguiente estructura inicial (puedes copiar y pegar):

    ```markdown
    # Rúbrica de Evaluación — Práctica 11
    ## Código evaluado: `procesador_csv.py`
    ## Fecha: [COMPLETAR]
    ## Lenguaje: Python 3.10+
    ## Guías de referencia: PEP 8, Clean Code (R. C. Martin), Principios SOLID

    ---

    | # | Buena Práctica            | Criterio de evaluación                                     | Nivel de cumplimiento | Evidencia / Comentario |
    |---|---------------------------|------------------------------------------------------------|-----------------------|------------------------|
    | 1 | Nomenclatura clara        | Nombres de variables, funciones y clases son descriptivos  |                       |                        |
    | 2 | Modularidad               | Funciones con responsabilidad única (SRP)                  |                       |                        |
    | 3 | Manejo de errores         | Uso de try/except con excepciones específicas              |                       |                        |
    | 4 | Legibilidad               | Código legible sin comentarios; estructura clara           |                       |                        |
    | 5 | Documentación (docstrings)| Funciones documentadas con parámetros y retorno            |                       |                        |
    | 6 | Validación de entradas    | Se verifican tipos y valores antes de procesar             |                       |                        |
    | 7 | Ausencia de números mágicos| Constantes con nombre en lugar de literales                |                       |                        |

    ---

    ## Reflexión Final
    [COMPLETAR AL FINAL DE LA PRÁCTICA]
    ```

4. Guarda el archivo (`Ctrl+S`).

**Resultado esperado:** La carpeta `lab-practica-11` contiene dos archivos: `procesador_csv.py` (vacío) y `rubrica_evaluacion.md` (con la estructura de la rúbrica).

**Verificación:**

```bash
ls -la lab-practica-11/
# Debe mostrar: procesador_csv.py  rubrica_evaluacion.md
```

---

### Paso 2 — Construir y ejecutar el prompt estructurado en Copilot Chat

**Objetivo:** Aplicar el ciclo *Especificar → Generar* del tema 4.1 mediante un prompt con rol, restricciones y criterios de aceptación explícitos para obtener código de complejidad media.

**Instrucciones:**

1. Abre el panel de **Copilot Chat** en VS Code:
   - Haz clic en el ícono de Copilot Chat en la barra lateral izquierda, **o**
   - Usa el atajo `Ctrl+Alt+I` (Windows/Linux) / `Cmd+Option+I` (macOS).

2. Asegúrate de que el archivo `procesador_csv.py` esté abierto y activo en el editor (esto proporciona contexto a Copilot Chat).

3. Escribe el siguiente prompt en el campo de chat. Cópialo **exactamente** para garantizar la calidad del código generado:

    ```
    Actúa como desarrollador senior de Python con experiencia en Clean Code y PEP 8.

    Escribe una función llamada `filter_csv_records` en Python 3.10 que:
    1. Reciba como parámetros: la ruta de un archivo CSV (string), el nombre de una columna (string) y un valor de filtro (string).
    2. Lea el archivo CSV usando el módulo `csv` de la biblioteca estándar (sin pandas).
    3. Retorne una lista de diccionarios con las filas donde el valor de la columna indicada coincida exactamente con el valor de filtro.
    4. Maneje los siguientes errores: archivo no encontrado, columna inexistente en el CSV, y archivo con formato inválido.
    5. Incluya docstring completo con descripción, parámetros (Args), retorno (Returns) y excepciones (Raises).
    6. Defina constantes con nombre para cualquier valor literal relevante.
    7. Siga estrictamente PEP 8: nombres en snake_case, máximo 79 caracteres por línea, espacios alrededor de operadores.

    Restricciones:
    - Solo usa módulos de la biblioteca estándar de Python 3.10.
    - No uses variables de una sola letra excepto en comprensiones de lista donde sea convencional.
    - Separa la lógica de lectura del CSV de la lógica de filtrado en funciones auxiliares.
    - Incluye al menos un ejemplo de uso en un bloque `if __name__ == "__main__":`.

    Entrega únicamente el código Python, sin explicaciones adicionales fuera del código.
    ```

4. Envía el prompt presionando `Enter` o haciendo clic en el botón de enviar.

5. Espera a que Copilot Chat genere la respuesta completa.

6. Cuando aparezca el código generado, haz clic en el botón **"Insert into Editor"** (o copia y pega manualmente) para insertar el código en `procesador_csv.py`.

7. Guarda el archivo (`Ctrl+S`).

**Resultado esperado:** El archivo `procesador_csv.py` contiene código Python funcional con al menos dos funciones (`filter_csv_records` y al menos una función auxiliar), docstrings, manejo de errores con `try/except`, constantes definidas y un bloque `if __name__ == "__main__":`.

> **Nota para el instructor:** Si hay problemas de conectividad, el siguiente código de referencia puede usarse como respaldo. Los participantes deben evaluarlo igualmente con la rúbrica.

**Código de referencia (respaldo en caso de problemas de conectividad):**

```python
"""
Módulo para lectura y filtrado de archivos CSV.
Generado con asistencia de GitHub Copilot Chat.
"""

import csv
from pathlib import Path

# Constantes
ENCODING = "utf-8"
NEWLINE = ""


def read_csv_file(file_path: str) -> list[dict]:
    """
    Lee un archivo CSV y retorna su contenido como lista de diccionarios.

    Args:
        file_path (str): Ruta al archivo CSV.

    Returns:
        list[dict]: Lista de filas como diccionarios {columna: valor}.

    Raises:
        FileNotFoundError: Si el archivo no existe en la ruta indicada.
        ValueError: Si el archivo está vacío o tiene formato inválido.
    """
    path = Path(file_path)

    if not path.exists():
        raise FileNotFoundError(f"Archivo no encontrado: {file_path}")

    try:
        with open(path, encoding=ENCODING, newline=NEWLINE) as csv_file:
            reader = csv.DictReader(csv_file)
            rows = list(reader)
    except csv.Error as error:
        raise ValueError(f"Formato CSV inválido: {error}") from error

    if not rows:
        raise ValueError(f"El archivo CSV está vacío: {file_path}")

    return rows


def filter_records(
    rows: list[dict], column: str, filter_value: str
) -> list[dict]:
    """
    Filtra una lista de diccionarios por el valor de una columna.

    Args:
        rows (list[dict]): Lista de filas como diccionarios.
        column (str): Nombre de la columna a evaluar.
        filter_value (str): Valor exacto que debe coincidir.

    Returns:
        list[dict]: Filas donde column == filter_value.

    Raises:
        KeyError: Si la columna indicada no existe en el CSV.
    """
    if rows and column not in rows[0]:
        raise KeyError(f"Columna '{column}' no encontrada en el CSV.")

    return [row for row in rows if row.get(column) == filter_value]


def filter_csv_records(
    file_path: str, column: str, filter_value: str
) -> list[dict]:
    """
    Lee un archivo CSV y retorna las filas que coincidan con el filtro.

    Args:
        file_path (str): Ruta al archivo CSV.
        column (str): Nombre de la columna por la que filtrar.
        filter_value (str): Valor exacto que debe tener la columna.

    Returns:
        list[dict]: Lista de diccionarios con las filas filtradas.

    Raises:
        FileNotFoundError: Si el archivo no existe.
        ValueError: Si el CSV está vacío o tiene formato inválido.
        KeyError: Si la columna no existe en el CSV.
    """
    rows = read_csv_file(file_path)
    return filter_records(rows, column, filter_value)


if __name__ == "__main__":
    # Ejemplo de uso: filtrar empleados del departamento "Ventas"
    resultado = filter_csv_records(
        file_path="empleados.csv",
        column="departamento",
        filter_value="Ventas",
    )
    print(f"Registros encontrados: {len(resultado)}")
    for registro in resultado:
        print(registro)
```

**Verificación:**

```bash
# Verificar que el archivo tiene contenido
cat procesador_csv.py | head -30
# Debe mostrar al menos el encabezado del módulo y la primera función
```

---

### Paso 3 — Ejecutar el linter para obtener evidencia objetiva

**Objetivo:** Aplicar herramientas de validación automática (*guardrails*) como parte del ciclo *Validar* del tema 4.1, generando evidencia objetiva para la rúbrica.

**Instrucciones:**

1. Desde la terminal integrada de VS Code, asegúrate de estar en la carpeta `lab-practica-11`:

    ```bash
    cd lab-practica-11
    ```

2. Ejecuta **flake8** sobre el archivo generado:

    ```bash
    flake8 procesador_csv.py --max-line-length=79 --statistics
    ```

3. Anota los resultados. Cada línea de salida indica una violación con el formato:
   `procesador_csv.py:LÍNEA:COLUMNA: CÓDIGO Descripción`

   Ejemplos de códigos comunes:
   - `E501` — Línea demasiado larga (> 79 caracteres)
   - `E302` — Falta línea en blanco antes de función
   - `W291` — Espacio en blanco al final de línea
   - `E711` — Comparación con `None` usando `==` en lugar de `is`

4. Ejecuta también **pylint** para un análisis más profundo:

    ```bash
    pylint procesador_csv.py --output-format=text
    ```

5. Anota la **puntuación final** de pylint (línea al final: `Your code has been rated at X.XX/10`).

6. Guarda la salida de ambas herramientas en un archivo de texto para referencia:

    ```bash
    flake8 procesador_csv.py --max-line-length=79 --statistics > reporte_linting.txt 2>&1
    pylint procesador_csv.py --output-format=text >> reporte_linting.txt 2>&1
    cat reporte_linting.txt
    ```

**Resultado esperado:**
- `flake8` produce cero advertencias **o** lista específica de violaciones de estilo.
- `pylint` muestra una puntuación numérica y una lista categorizada de mensajes (Convención, Advertencia, Error, Refactorización).
- El archivo `reporte_linting.txt` contiene ambos reportes para consulta posterior.

**Verificación:**

```bash
# Verificar que el reporte existe y tiene contenido
wc -l reporte_linting.txt
# Debe mostrar al menos 1 línea
```

> **Interpretación rápida de la puntuación pylint:**
> - **9.0–10.0**: Código de alta calidad, sigue buenas prácticas.
> - **7.0–8.9**: Calidad aceptable con áreas de mejora menores.
> - **5.0–6.9**: Problemas moderados que requieren atención.
> - **< 5.0**: Problemas significativos de calidad.

---

### Paso 4 — Revisar el código manualmente e identificar evidencias

**Objetivo:** Realizar la inspección humana del código generado, identificando evidencias concretas (líneas específicas) que respalden la evaluación de cada buena práctica. Este paso representa el rol de **curador de calidad** del programador moderno.

**Instrucciones:**

1. Abre `procesador_csv.py` en el editor de VS Code y léelo completo.

2. Para cada una de las siete buenas prácticas de la rúbrica, busca evidencias concretas en el código. Usa la siguiente guía de inspección:

    **BP1 — Nomenclatura clara (PEP 8 / Clean Code Cap. 2)**
    Revisa: ¿Los nombres de funciones, variables y parámetros son descriptivos y en `snake_case`? ¿Evitan abreviaciones crípticas?
    - ✅ Ejemplo de cumplimiento: `filter_csv_records`, `file_path`, `filter_value`
    - ❌ Ejemplo de incumplimiento: `f`, `fp`, `fv`, `proc`

    **BP2 — Modularidad / Principio de Responsabilidad Única (SOLID — SRP)**
    Revisa: ¿Cada función hace **una sola cosa**? ¿La lectura del CSV está separada del filtrado?
    - ✅ Cumplimiento: funciones `read_csv_file` y `filter_records` separadas
    - ❌ Incumplimiento: una sola función que lee, filtra y formatea el resultado

    **BP3 — Manejo de errores (Clean Code Cap. 7)**
    Revisa: ¿Se usan `try/except` con excepciones **específicas** (no `except Exception` genérico)? ¿Los mensajes de error son informativos?
    - ✅ Cumplimiento: `except FileNotFoundError`, `except csv.Error`
    - ❌ Incumplimiento: `except:` desnudo o `except Exception as e: pass`

    **BP4 — Legibilidad (Clean Code Cap. 4 — Comentarios)**
    Revisa: ¿El código se entiende sin necesidad de comentarios explicativos inline excesivos? ¿Las líneas tienen longitud razonable (≤ 79 chars)?
    - ✅ Cumplimiento: código autoexplicativo, sin comentarios redundantes como `# incrementa i en 1`
    - ❌ Incumplimiento: lógica oscura con comentarios que "explican lo que hace" en lugar de "por qué"

    **BP5 — Documentación / Docstrings (PEP 257)**
    Revisa: ¿Cada función tiene docstring? ¿Documenta `Args`, `Returns` y `Raises`?
    - ✅ Cumplimiento: docstring con las tres secciones presentes
    - ❌ Incumplimiento: docstring ausente o incompleto (solo descripción, sin Args/Returns)

    **BP6 — Validación de entradas**
    Revisa: ¿El código verifica que los parámetros son válidos antes de procesarlos? ¿Se valida que la columna existe antes de filtrar?
    - ✅ Cumplimiento: verificación de existencia del archivo y de la columna antes de procesar
    - ❌ Incumplimiento: asumir que los parámetros siempre son válidos, sin ninguna verificación

    **BP7 — Ausencia de números mágicos (Clean Code Cap. 17)**
    Revisa: ¿Los valores literales con significado están definidos como constantes con nombre?
    - ✅ Cumplimiento: `ENCODING = "utf-8"`, `MAX_RETRIES = 3`
    - ❌ Incumplimiento: `open(path, encoding="utf-8")` con el literal directamente sin constante

3. Para cada buena práctica, localiza la **línea o líneas específicas** del código que respaldan tu evaluación. Anota el número de línea.

4. Asigna un nivel de cumplimiento a cada práctica:
   - **✅ Cumple**: La práctica se aplica correctamente y de forma consistente en todo el código.
   - **⚠️ Cumple parcialmente**: La práctica se aplica en algunos casos pero no en todos, o se aplica de forma incompleta.
   - **❌ No cumple**: La práctica está ausente o se viola de forma clara.

**Resultado esperado:** Para cada una de las siete buenas prácticas tienes identificadas al menos una evidencia concreta (número de línea o fragmento de código) y un nivel de cumplimiento asignado.

**Verificación:** Abre `procesador_csv.py` y confirma que puedes señalar con el cursor al menos una línea específica que respalde cada evaluación antes de continuar al siguiente paso.

---

### Paso 5 — Completar la rúbrica de evaluación

**Objetivo:** Documentar formalmente los hallazgos del paso anterior en la rúbrica, completando el ciclo *Validar* del tema 4.1 con evidencia estructurada.

**Instrucciones:**

1. Abre `rubrica_evaluacion.md` en VS Code.

2. Completa la fecha en el encabezado.

3. Para cada fila de la tabla, rellena las columnas **"Nivel de cumplimiento"** y **"Evidencia / Comentario"** con base en tu inspección del Paso 4.

    Usa el siguiente formato de ejemplo como guía (tus resultados pueden diferir según el código que generó Copilot Chat en tu sesión):

    ```markdown
    | # | Buena Práctica            | Criterio de evaluación                                     | Nivel de cumplimiento | Evidencia / Comentario |
    |---|---------------------------|------------------------------------------------------------|-----------------------|------------------------|
    | 1 | Nomenclatura clara        | Nombres de variables, funciones y clases son descriptivos  | ✅ Cumple             | `filter_csv_records`, `file_path`, `filter_value` son descriptivos. Sin abreviaciones. Líneas 12, 28, 45. |
    | 2 | Modularidad (SRP)         | Funciones con responsabilidad única                        | ✅ Cumple             | Lectura separada en `read_csv_file` (L.18) y filtrado en `filter_records` (L.35). Cada función hace una cosa. |
    | 3 | Manejo de errores         | try/except con excepciones específicas                     | ⚠️ Cumple parcialmente | Captura `FileNotFoundError` y `csv.Error` (L.24-27), pero el bloque `__main__` no tiene manejo de errores. |
    | 4 | Legibilidad               | Código legible; líneas ≤ 79 chars                          | ✅ Cumple             | flake8 reportó 0 errores E501. Estructura clara y sin comentarios redundantes. |
    | 5 | Docstrings (PEP 257)      | Funciones documentadas con Args, Returns, Raises           | ✅ Cumple             | Las tres funciones tienen docstring completo con las tres secciones. Líneas 6, 20, 37, 52. |
    | 6 | Validación de entradas    | Se verifican tipos y valores antes de procesar             | ⚠️ Cumple parcialmente | Se valida existencia del archivo y de la columna, pero no se valida que `file_path`, `column` y `filter_value` sean strings no vacíos. |
    | 7 | Ausencia de números mágicos | Constantes con nombre para literales relevantes           | ✅ Cumple             | `ENCODING = "utf-8"` y `NEWLINE = ""` definidas como constantes (L.8-9). |
    ```

4. Al final de la tabla, añade un **resumen cuantitativo**:

    ```markdown
    ## Resumen de Evaluación

    | Nivel             | Cantidad | Prácticas                        |
    |-------------------|----------|----------------------------------|
    | ✅ Cumple         |    X     | [listar números]                 |
    | ⚠️ Parcialmente   |    X     | [listar números]                 |
    | ❌ No cumple      |    X     | [listar números]                 |
    | **Total**         |  **7**   |                                  |
    ```

5. Guarda el archivo (`Ctrl+S`).

**Resultado esperado:** La rúbrica está completamente llena con niveles de cumplimiento y evidencias concretas para las siete buenas prácticas evaluadas.

**Verificación:**

```bash
# Verificar que la rúbrica tiene contenido sustancial
wc -l rubrica_evaluacion.md
# Debe mostrar al menos 30 líneas
grep -c "Cumple" rubrica_evaluacion.md
# Debe mostrar al menos 7 (una por práctica)
```

---

### Paso 6 — Reflexión crítica y registro en el diario de aprendizaje

**Objetivo:** Sintetizar los hallazgos de la evaluación en una reflexión que responda a la pregunta central del tema 4.1: ¿qué responsabilidades permanecen en el programador cuando se usa IA generativa?

**Instrucciones:**

1. Abre tu **diario de aprendizaje** del curso (archivo `.md`, Word, Google Docs o Notion).

2. Crea una nueva entrada con el título: **"Práctica 11 — Reflexión: ¿Puede confiarse ciegamente en el código de Copilot Chat?"**

3. Responde las siguientes tres preguntas en no más de 3–5 oraciones cada una. Basa tus respuestas en la evidencia de tu rúbrica:

    **Pregunta A — Hallazgos principales:**
    > ¿Qué buenas prácticas cumplió el código generado por Copilot Chat? ¿Cuáles no cumplió o cumplió solo parcialmente? ¿Te sorprendió algún resultado?

    **Pregunta B — Implicaciones para la confianza:**
    > Con base en tu evaluación, ¿puede un equipo de desarrollo usar el código de Copilot Chat directamente en producción sin revisión? Justifica con al menos un hallazgo concreto de tu rúbrica.

    **Pregunta C — Responsabilidades del programador moderno:**
    > Según el ciclo *Enunciar–Especificar–Generar–Validar–Ajustar* del tema 4.1, ¿en qué pasos del ciclo la intervención humana fue más importante en esta práctica? ¿Qué habilidades del programador son irreemplazables aún con IA?

4. Añade también una **acción concreta de mejora**: ¿Qué cambiarías en el prompt original para obtener código que cumpla mejor con las prácticas donde encontraste deficiencias?

5. Guarda el diario.

6. Opcionalmente, regresa a Copilot Chat y ejecuta el siguiente prompt de ajuste (*Ajustar* del ciclo 4.1) para mejorar el código en las áreas deficientes identificadas:

    ```
    Revisa el código en procesador_csv.py y aplica las siguientes mejoras:
    1. Añade validación de que `file_path`, `column` y `filter_value` sean strings no vacíos al inicio de `filter_csv_records`, lanzando `ValueError` con mensaje descriptivo si no lo son.
    2. Añade manejo de errores en el bloque `if __name__ == "__main__":` para capturar FileNotFoundError, KeyError y ValueError con mensajes de error claros al usuario.
    3. Mantén estrictamente PEP 8 y todos los docstrings existentes.
    Entrega únicamente el código Python modificado.
    ```

7. Si ejecutas el prompt de mejora, guarda el código mejorado como `procesador_csv_v2.py` y anota en tu diario si las deficiencias identificadas fueron corregidas.

**Resultado esperado:**
- El diario de aprendizaje contiene una entrada con respuestas a las tres preguntas y una acción de mejora concreta.
- (Opcional) El archivo `procesador_csv_v2.py` contiene una versión mejorada del código con las deficiencias corregidas.

**Verificación:**
- Lee tu reflexión y confirma que cada respuesta hace referencia a al menos un hallazgo específico de la rúbrica (número de práctica o número de línea de código).
- Si completaste el paso opcional, vuelve a ejecutar el linter sobre `procesador_csv_v2.py` y compara la puntuación con la versión original.

---

## Validación y Pruebas

Al completar todos los pasos, verifica que los entregables de la práctica estén completos ejecutando el siguiente checklist:

```bash
# Desde la carpeta lab-practica-11
echo "=== Verificación de entregables ==="

echo "1. Archivo de código generado:"
ls -la procesador_csv.py && echo "   ✅ procesador_csv.py existe" || echo "   ❌ FALTA procesador_csv.py"

echo "2. Reporte de linting:"
ls -la reporte_linting.txt && echo "   ✅ reporte_linting.txt existe" || echo "   ❌ FALTA reporte_linting.txt"

echo "3. Rúbrica de evaluación:"
ls -la rubrica_evaluacion.md && echo "   ✅ rubrica_evaluacion.md existe" || echo "   ❌ FALTA rubrica_evaluacion.md"

echo "4. Contenido de la rúbrica (mínimo 30 líneas):"
LINE_COUNT=$(wc -l < rubrica_evaluacion.md)
[ "$LINE_COUNT" -ge 30 ] && echo "   ✅ $LINE_COUNT líneas" || echo "   ⚠️ Solo $LINE_COUNT líneas — revisar si está completa"

echo "5. Puntuación pylint del código:"
pylint procesador_csv.py --score=y 2>/dev/null | grep "rated at"
```

### Criterios de éxito de la práctica

| Criterio | Indicador de éxito |
|----------|--------------------|
| Código generado | `procesador_csv.py` contiene al menos 2 funciones y manejo de errores |
| Linting ejecutado | `reporte_linting.txt` existe con resultados de flake8 y pylint |
| Rúbrica completada | Todas las 7 filas tienen nivel de cumplimiento y evidencia |
| Reflexión documentada | Diario de aprendizaje contiene respuestas a las 3 preguntas |
| Evaluación justificada | Cada nivel de cumplimiento tiene evidencia con número de línea o fragmento de código |

---

## Resolución de Problemas

### Problema 1 — Copilot Chat genera código que no sigue el prompt o ignora restricciones

**Síntoma:** El código generado por Copilot Chat es una función simple sin funciones auxiliares, sin docstrings, o usa `pandas` a pesar de haber indicado "solo biblioteca estándar". La respuesta no refleja las restricciones del prompt.

**Causa:** Copilot Chat puede no haber tomado en cuenta todo el contexto del prompt si este fue muy largo, si el archivo activo en el editor no estaba abierto, o si el historial de la conversación anterior influyó en la respuesta. También puede ocurrir cuando el modelo interpreta restricciones de forma laxa.

**Solución:**
1. Inicia una **nueva conversación** en Copilot Chat (botón "+" o "New Chat") para limpiar el historial.
2. Asegúrate de que `procesador_csv.py` esté abierto y activo en el editor antes de enviar el prompt.
3. Divide el prompt en dos partes: primero envía el requerimiento funcional, luego envía las restricciones de estilo en un segundo mensaje.
4. Si el problema persiste, usa el código de referencia provisto en el Paso 2 y evalúalo con la rúbrica normalmente; el objetivo de la práctica es la evaluación, no la generación perfecta.

```
# Prompt alternativo más corto y directo:
Escribe en Python 3.10 una función `filter_csv_records(file_path, column, filter_value)` 
que lea un CSV con el módulo `csv` estándar y retorne filas filtradas. 
Separa la lectura del filtrado en funciones auxiliares. 
Incluye docstrings PEP 257 y manejo de errores con excepciones específicas.
```

---

### Problema 2 — pylint o flake8 no están instalados o no se reconocen en la terminal

**Síntoma:** Al ejecutar `pylint procesador_csv.py` o `flake8 procesador_csv.py`, la terminal muestra `command not found`, `'pylint' is not recognized as an internal or external command`, o un error similar. El Paso 3 no puede completarse.

**Causa:** Las herramientas de linting no están instaladas en el entorno Python activo, o están instaladas en un entorno virtual diferente al que está activo en la terminal de VS Code. En Windows, puede ocurrir que el directorio de scripts de pip no esté en el `PATH`.

**Solución:**

```bash
# Paso 1: Verificar qué Python está activo
python --version
which python   # macOS/Linux
where python   # Windows

# Paso 2: Instalar en el Python activo
python -m pip install pylint flake8

# Paso 3: Ejecutar usando el módulo de Python directamente (evita problemas de PATH)
python -m pylint procesador_csv.py
python -m flake8 procesador_csv.py --max-line-length=79

# Paso 4 (si usas entorno virtual): activar el entorno primero
# macOS/Linux:
source venv/bin/activate
# Windows:
venv\Scripts\activate
# Luego reinstalar:
pip install pylint flake8
```

Si el problema persiste en un entorno corporativo con restricciones de red, puedes usar la extensión **Pylance** de VS Code como alternativa visual: abre el archivo, observa los subrayados de advertencia y haz clic en ellos para ver la descripción del problema. Documenta los hallazgos manualmente en la rúbrica.

---

## Limpieza

Al finalizar la práctica, los archivos generados son parte de tu portafolio del curso y **no deben eliminarse**. Sin embargo, puedes organizar tu espacio de trabajo:

```bash
# Desde la carpeta padre de lab-practica-11
# Comprimir los archivos de la práctica para archivar
zip -r lab-practica-11-backup.zip lab-practica-11/

# Verificar el contenido del archivo comprimido
unzip -l lab-practica-11-backup.zip
```

> **Importante:** Conserva `procesador_csv.py` y `rubrica_evaluacion.md` ya que las Prácticas 9 y 10 del curso requieren reflexionar sobre experiencias acumuladas, y esta evaluación puede ser referenciada en esas prácticas.

Si deseas limpiar archivos temporales sin eliminar los entregables principales:

```bash
# Eliminar solo el reporte de linting (puede regenerarse)
rm lab-practica-11/reporte_linting.txt

# Verificar que los entregables principales permanecen
ls lab-practica-11/
# Debe mostrar: procesador_csv.py  rubrica_evaluacion.md
```

---

## Resumen

En esta práctica actuaste como **curador de calidad** del código asistido por IA, uno de los roles centrales del programador moderno descritos en el tema 4.1. Recorriste el ciclo completo **Enunciar → Especificar → Generar → Validar → Ajustar**:

1. **Enunciaste** la necesidad de negocio (filtrar registros de un CSV).
2. **Especificaste** los criterios de calidad mediante un prompt estructurado con rol, restricciones y criterios de aceptación.
3. **Generaste** código de complejidad media con Copilot Chat.
4. **Validaste** el código con herramientas automáticas (flake8, pylint) y con inspección humana estructurada en una rúbrica de siete buenas prácticas.
5. **Ajustaste** el prompt para corregir deficiencias identificadas (paso opcional).

### Conclusión clave

El código generado por Copilot Chat puede cumplir con muchas buenas prácticas cuando se le provee un prompt bien estructurado, pero **la responsabilidad de verificar la calidad, la seguridad y la adecuación al contexto permanece en el programador**. La IA es un acelerador poderoso; la juicio crítico y el conocimiento de estándares son las habilidades que el programador moderno debe cultivar activamente.

### Puntos clave de la práctica

- Un prompt con **rol + restricciones + criterios de aceptación** produce código de mayor calidad que un prompt genérico.
- Las herramientas de linting (flake8, pylint) proveen evidencia **objetiva y reproducible** para la evaluación de estilo.
- La inspección humana es necesaria para evaluar prácticas que las herramientas automáticas no detectan: modularidad, semántica de nombres, adecuación de la lógica de negocio.
- La rúbrica de evaluación es un artefacto profesional que puede formalizarse en procesos de **code review** en equipos reales.
- El ciclo *Generar → Validar → Ajustar* es iterativo: las deficiencias encontradas en la validación se convierten en insumos para prompts de refinamiento.

### Recursos adicionales

| Recurso | URL |
|---------|-----|
| PEP 8 — Guía de estilo para Python | https://peps.python.org/pep-0008/ |
| PEP 257 — Convenciones de docstrings | https://peps.python.org/pep-0257/ |
| Clean Code — Resumen de principios | https://gist.github.com/wojteklu/73c6914cc446146b8b533c0988cf8d29 |
| Principios SOLID explicados | https://realpython.com/solid-principles-python/ |
| Documentación oficial Copilot Chat | https://docs.github.com/en/copilot/copilot-chat/copilot-chat-in-the-editor |
| flake8 — Documentación oficial | https://flake8.pycqa.org/en/latest/ |
| pylint — Documentación oficial | https://pylint.readthedocs.io/en/stable/ |


