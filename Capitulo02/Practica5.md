# Práctica 5: Escribe comentarios detallados sobre lo que debería hacer una función y utiliza Caht  Copilot para generarla.

## 1. Metadatos

| Campo            | Detalle                                      |
|------------------|----------------------------------------------|
| **Duración**     | 10 minutos (hasta 25 min en modo autónomo)   |
| **Complejidad**  | Media                                        |
| **Nivel Bloom**  | Aplicar (*Apply*)                            |
| **Módulo**       | 2 — Copilot Chat como Herramienta de Referencia |
| **Práctica**     | 5 de 10                                      |

---

## 2. Descripción General

En esta práctica explorarás la técnica de **"comment-driven development"**: escribir comentarios de código precisos y estructurados que sirvan como instrucciones explícitas para que Copilot Chat genere el cuerpo completo de una función. Trabajarás con tres funciones de complejidad comparable pero con niveles de detalle en los comentarios muy distintos — detallado, moderado y mínimo — para descubrir de forma empírica cómo la calidad del comentario/prompt impacta directamente la calidad del código generado. Este ejercicio refuerza el concepto central de la lección 2.1: Copilot Chat actúa como una herramienta de referencia contextual que responde a la intención del desarrollador.

---

## 3. Objetivos de Aprendizaje

Al finalizar esta práctica, serás capaz de:

- [ ] Redactar comentarios de código precisos y estructurados (propósito, parámetros, retorno, casos especiales, ejemplo de uso) que actúen como prompts efectivos para Copilot Chat.
- [ ] Generar funciones completas utilizando únicamente comentarios en lenguaje natural como guía para Copilot Chat, sin escribir el cuerpo de la función manualmente.
- [ ] Comparar la calidad del código generado a partir de comentarios detallados versus comentarios vagos, identificando diferencias concretas en manejo de errores, legibilidad y corrección.
- [ ] Aplicar buenas prácticas de consulta (objetivo, alcance, formato) aprendidas en la lección 2.1 para refinar el código generado cuando el primer resultado no sea satisfactorio.

---

## 4. Prerrequisitos

### Conocimientos previos
- Haber completado la **Práctica 4** del curso.
- Saber escribir comentarios de código en el lenguaje elegido (Python recomendado; también válido JavaScript, TypeScript, Java, C#).
- Comprender los conceptos de función, parámetros, valor de retorno y manejo de excepciones en el lenguaje elegido.
- Haber leído o asistido a la lección **2.1: Uso de Copilot Chat como Herramienta de Referencia**.

### Acceso y cuentas
- Cuenta de GitHub con **suscripción activa a GitHub Copilot** (Individual, Team o Enterprise).
- Extensión **GitHub Copilot Chat** instalada y autenticada en VS Code.
- Conexión a internet estable (mínimo 10 Mbps).

---

## 5. Entorno de Laboratorio

### Hardware mínimo recomendado

| Componente       | Mínimo                          | Recomendado                    |
|------------------|---------------------------------|--------------------------------|
| Procesador       | Intel Core i5 / AMD Ryzen 5 x64 | Intel Core i7 / AMD Ryzen 7    |
| RAM              | 8 GB                            | 16 GB                          |
| Disco libre      | 2 GB                            | 10 GB                          |
| Pantalla         | 1280 × 768                      | 1920 × 1080                    |
| Red              | 10 Mbps                         | 25 Mbps o más                  |

### Software requerido

| Software                        | Versión mínima          |
|---------------------------------|-------------------------|
| Visual Studio Code              | 1.90 o superior         |
| Extensión GitHub Copilot Chat   | Última del Marketplace  |
| Python                          | 3.10 o superior         |
| Git                             | 2.40 o superior         |
| pylint o flake8 (opcional)      | pylint 3.x / flake8 7.x |

### Verificación del entorno (ejecutar antes de iniciar)

Abre una terminal en VS Code (`Ctrl+`` ` ``) y ejecuta los siguientes comandos para confirmar que todo está disponible:

```bash
# Verificar Python
python --version
# Resultado esperado: Python 3.10.x o superior

# Verificar Git
git --version
# Resultado esperado: git version 2.40.x o superior

# Verificar pylint (opcional pero recomendado)
pylint --version
# Resultado esperado: pylint 3.x.x
```

### Preparación del proyecto

```bash
# 1. Crear carpeta de trabajo para esta práctica
mkdir practica-05-comment-driven
cd practica-05-comment-driven

# 2. Inicializar repositorio Git (para que Copilot tenga contexto de workspace)
git init

# 3. Crear el archivo principal de trabajo
touch funciones_comentadas.py

# 4. Abrir la carpeta en VS Code
code .
```

> **Nota:** Abrir la carpeta completa en VS Code (no solo el archivo) permite que Copilot Chat aproveche el contexto del workspace, tal como se describió en la lección 2.1.

---

## 6. Instrucciones Paso a Paso

---

### Paso 1 — Preparar el archivo de trabajo y entender la estructura de un comentario efectivo

**Objetivo:** Establecer la plantilla de comentarios que usarás como base para los tres niveles de detalle, siguiendo las buenas prácticas de la lección 2.1.

#### Instrucciones

1. Abre el archivo `funciones_comentadas.py` en VS Code.

2. Escribe el siguiente encabezado en el archivo para establecer el contexto del módulo:

```python
"""
Módulo: funciones_comentadas.py
Propósito: Exploración de 'comment-driven development' con GitHub Copilot Chat.
Práctica 5 — Módulo 2: Copilot Chat como Herramienta de Referencia
"""
```

3. Revisa la siguiente plantilla de comentario estructurado. Esta es la **estructura de referencia** para un comentario de nivel detallado:

```python
# FUNCIÓN: <nombre_descriptivo>
#
# PROPÓSITO:
#   <Descripción clara y completa de qué hace la función, por qué existe
#    y qué problema resuelve. 2-4 oraciones.>
#
# PARÁMETROS:
#   <nombre_param> (<tipo>): <descripción> — restricciones: <rango, formato, etc.>
#
# RETORNO:
#   <tipo>: <descripción del valor retornado y su significado>
#
# CASOS ESPECIALES / ERRORES:
#   - <caso 1>: <qué debe ocurrir>
#   - <caso 2>: <qué debe ocurrir>
#
# EJEMPLO DE USO:
#   >>> <llamada de ejemplo>
#   <resultado esperado>
```

4. Guarda el archivo (`Ctrl+S`).

#### Resultado esperado
El archivo `funciones_comentadas.py` contiene el encabezado del módulo y tienes clara la estructura de comentario que usarás. VS Code muestra el archivo sin errores de sintaxis.

#### Verificación
- El archivo se guarda sin advertencias.
- La extensión de Copilot Chat aparece activa en la barra lateral izquierda de VS Code (ícono de chat).

---

### Paso 2 — Función 1: Comentario detallado → Generar con Copilot Chat

**Objetivo:** Escribir un comentario de máximo detalle y observar cómo Copilot Chat genera una función completa, robusta y bien manejada.

#### Instrucciones

1. Debajo del encabezado del módulo, escribe **exactamente** el siguiente bloque de comentarios en `funciones_comentadas.py`. **No escribas el cuerpo de la función** — eso lo hará Copilot Chat:

```python
# FUNCIÓN: calcular_descuento
#
# PROPÓSITO:
#   Calcula el precio final de un producto después de aplicar un porcentaje
#   de descuento. Se utiliza en el módulo de facturación para mostrar el
#   precio con descuento al cliente antes de confirmar la compra.
#   El resultado se redondea a dos decimales para representar moneda.
#
# PARÁMETROS:
#   precio_original (float): Precio del producto antes del descuento.
#                            Debe ser un número positivo mayor a 0.
#   porcentaje_descuento (float): Porcentaje de descuento a aplicar (0 a 100).
#                                 Ejemplo: 20 representa un 20% de descuento.
#
# RETORNO:
#   float: Precio final después de aplicar el descuento, redondeado a 2
#          decimales. Siempre será un valor positivo mayor o igual a 0.
#
# CASOS ESPECIALES / ERRORES:
#   - Si precio_original <= 0: lanzar ValueError con mensaje descriptivo.
#   - Si porcentaje_descuento < 0 o > 100: lanzar ValueError con mensaje.
#   - Si algún parámetro no es numérico (int o float): lanzar TypeError.
#   - Si porcentaje_descuento == 100: retornar 0.0 (producto gratuito).
#
# EJEMPLO DE USO:
#   >>> calcular_descuento(100.0, 20)
#   80.0
#   >>> calcular_descuento(250.50, 15)
#   212.93
```

2. Coloca el cursor en la línea inmediatamente debajo del último comentario (línea en blanco después del ejemplo de uso).

3. Escribe la firma de la función y detente **antes** de los dos puntos o el cuerpo:

```python
def calcular_descuento(precio_original: float, porcentaje_descuento: float) -> float:
```

4. Presiona `Enter`. Copilot Chat (modo autocompletado inline) debería comenzar a sugerir el cuerpo. Si la sugerencia aparece en gris, presiona `Tab` para aceptarla. Si no aparece automáticamente, continúa con el paso 5.

5. **Alternativa con el panel de chat:** Si el autocompletado no generó el cuerpo completo, selecciona **todo el bloque** (comentarios + firma) con `Ctrl+Shift+K` para seleccionar o arrastrando el cursor. Luego abre el panel de Copilot Chat (`Ctrl+Alt+I` o clic en el ícono del chat) y envía el siguiente prompt:

```
Basándote estrictamente en los comentarios seleccionados, genera el cuerpo 
completo de la función calcular_descuento en Python. Incluye validaciones de 
tipo y valor, manejo de todos los casos especiales descritos, y docstring 
estilo Google. No omitas ningún caso de error mencionado.
```

6. Copia el cuerpo generado y pégalo en el archivo debajo de la firma.

7. El resultado debería verse similar a esto (el código exacto puede variar):

```python
def calcular_descuento(precio_original: float, porcentaje_descuento: float) -> float:
    """Calcula el precio final después de aplicar un descuento.

    Args:
        precio_original (float): Precio del producto antes del descuento. Debe ser > 0.
        porcentaje_descuento (float): Porcentaje de descuento (0 a 100).

    Returns:
        float: Precio final redondeado a 2 decimales.

    Raises:
        TypeError: Si algún parámetro no es numérico.
        ValueError: Si precio_original <= 0 o porcentaje_descuento fuera de [0, 100].
    """
    if not isinstance(precio_original, (int, float)):
        raise TypeError("precio_original debe ser un número (int o float).")
    if not isinstance(porcentaje_descuento, (int, float)):
        raise TypeError("porcentaje_descuento debe ser un número (int o float).")
    if precio_original <= 0:
        raise ValueError("precio_original debe ser mayor que 0.")
    if not (0 <= porcentaje_descuento <= 100):
        raise ValueError("porcentaje_descuento debe estar entre 0 y 100.")

    precio_final = precio_original * (1 - porcentaje_descuento / 100)
    return round(precio_final, 2)
```

8. Guarda el archivo.

#### Resultado esperado
La función `calcular_descuento` está completamente implementada con validaciones de tipo, validaciones de rango, manejo de todos los casos especiales descritos en los comentarios y un docstring completo.

#### Verificación
Ejecuta en la terminal integrada de VS Code:

```bash
python -c "
from funciones_comentadas import calcular_descuento
print(calcular_descuento(100.0, 20))      # Esperado: 80.0
print(calcular_descuento(250.50, 15))     # Esperado: 212.93
print(calcular_descuento(100.0, 100))     # Esperado: 0.0

try:
    calcular_descuento(-50, 10)
except ValueError as e:
    print(f'ValueError capturado: {e}')

try:
    calcular_descuento(100, 110)
except ValueError as e:
    print(f'ValueError capturado: {e}')

try:
    calcular_descuento('cien', 10)
except TypeError as e:
    print(f'TypeError capturado: {e}')
"
```

**Salida esperada:**
```
80.0
212.93
0.0
ValueError capturado: precio_original debe ser mayor que 0.
ValueError capturado: porcentaje_descuento debe estar entre 0 y 100.
TypeError capturado: precio_original debe ser un número (int o float).
```

> **Anota en tu diario de aprendizaje:** ¿Cuántos de los casos especiales que describiste en los comentarios fueron correctamente implementados por Copilot? ¿Hubo alguno que se omitió o se implementó de forma diferente a lo esperado?

---

### Paso 3 — Función 2: Comentario moderado → Generar y comparar

**Objetivo:** Escribir un comentario de nivel moderado (propósito y parámetros básicos, sin casos de error ni ejemplo) y observar cómo cambia la calidad del código generado.

#### Instrucciones

1. Debajo de la función `calcular_descuento`, agrega el siguiente bloque de comentarios moderados:

```python
# FUNCIÓN: buscar_elemento
#
# PROPÓSITO:
#   Busca un elemento en una lista y retorna su índice.
#   Si el elemento no existe, retorna -1.
#
# PARÁMETROS:
#   lista (list): La lista donde buscar.
#   elemento: El elemento a buscar en la lista.
#
# RETORNO:
#   int: El índice del elemento encontrado, o -1 si no existe.
```

2. Escribe la firma de la función y deja que Copilot genere el cuerpo (igual que en el Paso 2):

```python
def buscar_elemento(lista: list, elemento) -> int:
```

3. Si el autocompletado no aparece, usa el panel de Copilot Chat con el prompt:

```
Genera el cuerpo de la función buscar_elemento basándote en los comentarios 
que la preceden. Usa Python idiomático.
```

4. Acepta o copia el código generado. Un ejemplo típico de lo que Copilot generará con comentarios moderados:

```python
def buscar_elemento(lista: list, elemento) -> int:
    """Busca un elemento en una lista y retorna su índice."""
    for i, item in enumerate(lista):
        if item == elemento:
            return i
    return -1
```

5. **Análisis crítico:** Observa qué falta en comparación con la Función 1. Abre el panel de Copilot Chat y pregunta:

```
Revisa la función buscar_elemento que acabo de generar. 
¿Qué validaciones o casos especiales debería manejar que no están 
implementados actualmente? Lista al menos 3 mejoras concretas.
```

6. Anota la respuesta de Copilot. Luego pregunta:

```
Basándote en las mejoras que identificaste, muéstrame una versión mejorada 
de buscar_elemento que maneje esos casos especiales. Incluye docstring.
```

7. Compara la versión original generada con la versión mejorada. Guarda el archivo con la versión mejorada.

#### Resultado esperado
Tienes dos versiones de `buscar_elemento`: la generada a partir del comentario moderado (simple, sin validaciones) y la versión mejorada sugerida por Copilot al hacer una consulta de refinamiento. La diferencia entre ambas ilustra el valor de los comentarios detallados.

#### Verificación

```bash
python -c "
from funciones_comentadas import buscar_elemento
print(buscar_elemento([1, 2, 3, 4], 3))      # Esperado: 2
print(buscar_elemento(['a', 'b', 'c'], 'b')) # Esperado: 1
print(buscar_elemento([10, 20, 30], 99))     # Esperado: -1
print(buscar_elemento([], 5))                # Esperado: -1
"
```

**Salida esperada:**
```
2
1
-1
-1
```

> **Anota en tu diario de aprendizaje:** ¿Qué diferencias concretas encontraste entre el código generado con comentario detallado (Función 1) y el generado con comentario moderado (Función 2)? ¿Copilot incluyó manejo de errores para lista vacía o para parámetros no válidos sin que se lo indicaras?

---

### Paso 4 — Función 3: Comentario mínimo → Generar, evaluar y reflexionar

**Objetivo:** Escribir un comentario mínimo (solo una línea) y observar las limitaciones del código generado, cerrando el ciclo de comparación entre los tres niveles.

#### Instrucciones

1. Debajo de la función `buscar_elemento`, agrega el siguiente comentario mínimo:

```python
# Convierte temperatura de Celsius a Fahrenheit
```

2. Escribe la firma de la función:

```python
def convertir_temperatura(celsius):
```

3. Deja que Copilot genere el cuerpo. Con un comentario tan escaso, Copilot probablemente generará algo como:

```python
def convertir_temperatura(celsius):
    return celsius * 9/5 + 32
```

4. Acepta el código generado **sin modificarlo todavía**. Guarda el archivo.

5. Ahora abre el panel de Copilot Chat, selecciona la función generada, y realiza las siguientes consultas para evaluar su calidad (envía cada pregunta por separado):

   **Consulta A — Evaluación de robustez:**
   ```
   Evalúa la función convertir_temperatura que tengo seleccionada. 
   ¿Qué casos especiales no maneja? ¿Qué pasaría si se pasa un string, 
   None, o un valor por debajo del cero absoluto (-273.15°C)?
   ```

   **Consulta B — Solicitud de versión completa:**
   ```
   Reescribe convertir_temperatura con: validación de tipo, validación de 
   rango (no menor a -273.15°C que es el cero absoluto), docstring estilo 
   Google, type hints, y un ejemplo de uso en el docstring. 
   Retorna el resultado redondeado a 2 decimales.
   ```

6. Copia la versión mejorada generada por Copilot y reemplaza la versión mínima en el archivo. Debería verse similar a:

```python
def convertir_temperatura(celsius: float) -> float:
    """Convierte una temperatura de grados Celsius a Fahrenheit.

    Args:
        celsius (float): Temperatura en grados Celsius. No puede ser menor
                         al cero absoluto (-273.15°C).

    Returns:
        float: Temperatura equivalente en grados Fahrenheit, redondeada
               a 2 decimales.

    Raises:
        TypeError: Si celsius no es un número (int o float).
        ValueError: Si celsius es menor al cero absoluto (-273.15°C).

    Example:
        >>> convertir_temperatura(0)
        32.0
        >>> convertir_temperatura(100)
        212.0
    """
    if not isinstance(celsius, (int, float)):
        raise TypeError("celsius debe ser un número (int o float).")
    if celsius < -273.15:
        raise ValueError("La temperatura no puede ser menor al cero absoluto (-273.15°C).")
    return round(celsius * 9 / 5 + 32, 2)
```

7. Guarda el archivo.

#### Resultado esperado
Tienes la función `convertir_temperatura` en su versión mejorada, generada iterativamente a través de consultas de refinamiento a Copilot Chat. Puedes ver claramente cómo partiste de una implementación de una sola línea y llegaste a una función robusta.

#### Verificación

```bash
python -c "
from funciones_comentadas import convertir_temperatura
print(convertir_temperatura(0))       # Esperado: 32.0
print(convertir_temperatura(100))     # Esperado: 212.0
print(convertir_temperatura(-40))     # Esperado: -40.0

try:
    convertir_temperatura('caliente')
except TypeError as e:
    print(f'TypeError: {e}')

try:
    convertir_temperatura(-300)
except ValueError as e:
    print(f'ValueError: {e}')
"
```

**Salida esperada:**
```
32.0
212.0
-40.0
TypeError: celsius debe ser un número (int o float).
ValueError: La temperatura no puede ser menor al cero absoluto (-273.15°C).
```

> **Anota en tu diario de aprendizaje:** ¿Cuántas iteraciones de consulta necesitaste para llevar el comentario mínimo a una función de calidad comparable a la Función 1? ¿Qué conclusión sacas sobre la relación entre la calidad del comentario inicial y el esfuerzo de refinamiento posterior?

---

### Paso 5 — Reflexión comparativa con Copilot Chat

**Objetivo:** Usar Copilot Chat como herramienta de referencia para sintetizar las diferencias entre los tres enfoques y generar una guía personal de buenas prácticas.

#### Instrucciones

1. Abre el panel de Copilot Chat (`Ctrl+Alt+I`).

2. Envía el siguiente prompt de análisis comparativo:

```
Tengo el archivo funciones_comentadas.py abierto con tres funciones:
calcular_descuento (comentario muy detallado), buscar_elemento (comentario 
moderado) y convertir_temperatura (empezó con comentario mínimo).

Basándote en el código actual del archivo, genera una tabla comparativa 
en Markdown con las siguientes columnas:
- Función
- Nivel de detalle del comentario original
- ¿Incluyó validaciones de tipo? (Sí/No/Parcial)
- ¿Incluyó manejo de errores? (Sí/No/Parcial)
- ¿Incluyó docstring? (Sí/No)
- Iteraciones de refinamiento necesarias (estimado)
- Calidad del primer resultado (Alta/Media/Baja)
```

3. Copia la tabla generada y guárdala en un nuevo archivo llamado `reflexion_practica5.md`.

4. Envía un segundo prompt para generar tu guía personal:

```
Basándote en las diferencias observadas entre los tres niveles de comentario, 
genera una lista de 5 reglas prácticas para escribir comentarios efectivos 
que sirvan como prompts para Copilot Chat. Escríbelas en español, en formato 
de lista numerada, con una oración de justificación para cada regla.
```

5. Agrega las 5 reglas al archivo `reflexion_practica5.md` bajo un encabezado `## Mis Reglas de Comment-Driven Development`.

6. Guarda ambos archivos y haz un commit:

```bash
git add funciones_comentadas.py reflexion_practica5.md
git commit -m "practica-05: comment-driven development con tres niveles de detalle"
```

#### Resultado esperado
Tienes un archivo `reflexion_practica5.md` con una tabla comparativa de las tres funciones y tus 5 reglas personales de comment-driven development, respaldadas por la experiencia práctica de esta sesión.

#### Verificación
- El comando `git log --oneline` muestra el commit recién creado.
- El archivo `reflexion_practica5.md` contiene tanto la tabla como las 5 reglas.

```bash
git log --oneline
# Resultado esperado: algo como → a1b2c3d practica-05: comment-driven development con tres niveles de detalle
```

---

## 7. Validación y Pruebas Finales

Ejecuta la siguiente verificación integral para confirmar que las tres funciones están correctamente implementadas:

```bash
python -c "
print('=== VALIDACIÓN INTEGRAL - PRÁCTICA 5 ===')
print()

from funciones_comentadas import calcular_descuento, buscar_elemento, convertir_temperatura

# --- Función 1: calcular_descuento ---
print('--- calcular_descuento (comentario detallado) ---')
assert calcular_descuento(100.0, 20) == 80.0, 'Error en descuento básico'
assert calcular_descuento(250.50, 15) == 212.93, 'Error en descuento con decimales'
assert calcular_descuento(100.0, 100) == 0.0, 'Error en descuento 100%'
assert calcular_descuento(100.0, 0) == 100.0, 'Error en descuento 0%'
try:
    calcular_descuento(-10, 20)
    print('FALLO: debió lanzar ValueError para precio negativo')
except ValueError:
    pass
try:
    calcular_descuento(100, 110)
    print('FALLO: debió lanzar ValueError para porcentaje > 100')
except ValueError:
    pass
print('calcular_descuento: TODAS LAS PRUEBAS PASARON ✓')
print()

# --- Función 2: buscar_elemento ---
print('--- buscar_elemento (comentario moderado) ---')
assert buscar_elemento([1, 2, 3], 2) == 1, 'Error en búsqueda básica'
assert buscar_elemento([1, 2, 3], 99) == -1, 'Error en elemento no encontrado'
assert buscar_elemento([], 5) == -1, 'Error en lista vacía'
assert buscar_elemento(['a', 'b', 'c'], 'c') == 2, 'Error en lista de strings'
print('buscar_elemento: TODAS LAS PRUEBAS PASARON ✓')
print()

# --- Función 3: convertir_temperatura ---
print('--- convertir_temperatura (comentario mínimo → mejorado) ---')
assert convertir_temperatura(0) == 32.0, 'Error en 0°C'
assert convertir_temperatura(100) == 212.0, 'Error en 100°C'
assert convertir_temperatura(-40) == -40.0, 'Error en -40°C'
try:
    convertir_temperatura('caliente')
    print('FALLO: debió lanzar TypeError')
except TypeError:
    pass
try:
    convertir_temperatura(-300)
    print('FALLO: debió lanzar ValueError para bajo cero absoluto')
except ValueError:
    pass
print('convertir_temperatura: TODAS LAS PRUEBAS PASARON ✓')
print()

print('=== VALIDACIÓN COMPLETA: TODAS LAS FUNCIONES CORRECTAS ✓ ===')
"
```

**Salida esperada:**
```
=== VALIDACIÓN INTEGRAL - PRÁCTICA 5 ===

--- calcular_descuento (comentario detallado) ---
calcular_descuento: TODAS LAS PRUEBAS PASARON ✓

--- buscar_elemento (comentario moderado) ---
buscar_elemento: TODAS LAS PRUEBAS PASARON ✓

--- convertir_temperatura (comentario mínimo → mejorado) ---
convertir_temperatura: TODAS LAS PRUEBAS PASARON ✓

=== VALIDACIÓN COMPLETA: TODAS LAS FUNCIONES CORRECTAS ✓ ===
```

### Verificación opcional con linting

Si tienes `pylint` o `flake8` instalado, ejecuta:

```bash
# Con pylint
pylint funciones_comentadas.py

# Con flake8
flake8 funciones_comentadas.py --max-line-length=100
```

Un puntaje de pylint de **8.0/10 o superior** indica buena calidad de código. Si el puntaje es inferior, usa Copilot Chat para identificar y corregir los problemas reportados:

```
pylint reporta los siguientes problemas en mi archivo: [pega aquí la salida].
¿Cuáles son los más importantes de corregir y cómo los soluciono?
```

---

## 8. Solución de Problemas

---

### Problema 1: Copilot Chat no genera sugerencias inline al escribir la firma de la función

**Síntoma:** Después de escribir `def nombre_funcion(...):` y presionar `Enter`, no aparece ninguna sugerencia en gris (ghost text). El autocompletado parece inactivo.

**Causa probable:** La extensión de GitHub Copilot puede estar en pausa, el archivo puede no tener suficiente contexto cargado, o la conexión a internet fue interrumpida momentáneamente al momento de la solicitud.

**Solución:**
1. Verifica el estado de Copilot en la barra de estado inferior de VS Code. Busca el ícono de Copilot (puede mostrar un ícono de pausa o error). Haz clic en él y selecciona **"Enable Completions"** si está desactivado.
2. Asegúrate de que el archivo esté guardado (`Ctrl+S`) antes de esperar sugerencias.
3. Espera 3-5 segundos después de escribir la firma; a veces hay latencia de red.
4. Si el problema persiste, usa el **panel de chat** como alternativa: selecciona los comentarios + la firma, abre Copilot Chat (`Ctrl+Alt+I`) y envía el prompt descrito en el Paso 2, instrucción 5.
5. Como última alternativa, recarga VS Code: `Ctrl+Shift+P` → "Developer: Reload Window".

---

### Problema 2: El código generado no maneja todos los casos especiales descritos en los comentarios

**Síntoma:** Copilot generó el cuerpo de la función pero omitió una o más validaciones que estaban explícitamente descritas en los comentarios (por ejemplo, no lanza `TypeError` para parámetros no numéricos, o no maneja el caso de lista vacía).

**Causa probable:** Los comentarios, aunque detallados, pueden estar redactados de forma ambigua para el modelo, o Copilot priorizó la implementación más común y simple, ignorando casos de borde menos frecuentes. También puede ocurrir si el comentario mezcla varios casos en una sola línea sin suficiente separación visual.

**Solución:**
1. Selecciona el código generado y abre el panel de Copilot Chat.
2. Envía un prompt de refinamiento específico:
   ```
   La función generada no maneja el caso donde [describe el caso omitido].
   Agrega esa validación manteniendo el resto del código igual. 
   Muéstrame solo la sección modificada.
   ```
3. Si el problema es sistemático (varios casos omitidos), reformula el comentario separando cada caso especial en su propia línea con un guion, como se muestra en la plantilla del Paso 1.
4. Usa el comando `/fix` de Copilot Chat con la función seleccionada para pedir una revisión general:
   ```
   /fix Agrega todas las validaciones de tipo y valor descritas en los 
   comentarios que preceden a esta función.
   ```

---

## 9. Limpieza del Entorno

Al finalizar la práctica, los archivos generados son parte de tu portafolio de aprendizaje y **no deben eliminarse** — serán referenciados en prácticas posteriores (especialmente la Práctica 9 y 10).

Realiza las siguientes acciones de cierre:

```bash
# 1. Confirmar que todos los cambios están commiteados
git status
# Resultado esperado: "nothing to commit, working tree clean"

# 2. Si hay cambios pendientes, hacer commit final
git add .
git commit -m "practica-05: cierre - validacion completa y reflexion"

# 3. Verificar el historial de commits de la práctica
git log --oneline
```

### Archivos generados en esta práctica

| Archivo                    | Descripción                                               | ¿Conservar? |
|----------------------------|-----------------------------------------------------------|-------------|
| `funciones_comentadas.py`  | Tres funciones generadas con comment-driven development   | ✅ Sí       |
| `reflexion_practica5.md`   | Tabla comparativa y reglas personales de buenas prácticas | ✅ Sí       |

> **Importante:** Guarda la carpeta `practica-05-comment-driven/` en tu diario de aprendizaje o repositorio personal del curso. Las reflexiones documentadas en `reflexion_practica5.md` serán insumo directo para las actividades de evaluación del Módulo 3.

---

## 10. Resumen

### Lo que aprendiste en esta práctica

En esta práctica aplicaste la técnica de **comment-driven development** con GitHub Copilot Chat, experimentando de forma directa cómo la calidad del comentario/prompt determina la calidad del código generado:

| Nivel de comentario | Resultado típico del primer intento | Iteraciones necesarias |
|---------------------|-------------------------------------|------------------------|
| **Detallado** (propósito + parámetros + retorno + casos especiales + ejemplo) | Función completa, con validaciones y docstring | 0-1 |
| **Moderado** (propósito + parámetros básicos) | Función funcional pero sin validaciones robustas | 1-2 |
| **Mínimo** (una sola línea) | Implementación básica, sin manejo de errores | 2-4 |

### Conceptos clave reforzados

- **Copilot Chat como referencia contextual:** Tal como aprendiste en la lección 2.1, Copilot responde mejor cuando el contexto es explícito y bien estructurado. Los comentarios detallados son, en esencia, prompts de alta calidad anclados al código.
- **Iteración como parte del flujo:** Incluso con comentarios mínimos puedes llegar a código de calidad usando consultas de refinamiento sucesivas — pero a un costo mayor de tiempo y esfuerzo.
- **Validación crítica es obligatoria:** Ninguna de las tres funciones debe usarse en producción sin revisión manual. Copilot puede omitir casos de borde, generar lógica incorrecta o no seguir las convenciones específicas de tu equipo.
- **El desarrollador sigue siendo responsable:** Copilot es una herramienta de referencia y asistencia, no un reemplazo del criterio del programador.

### Conexión con las siguientes prácticas

- La técnica de comment-driven development que practicaste aquí es la base para las prácticas del **Módulo 3**, donde aplicarás Copilot Chat a necesidades de negocio concretas.
- Las reflexiones en `reflexion_practica5.md` serán retomadas en la **Práctica 9** para evaluar tu evolución como desarrollador en el contexto de la IA generativa.

### Recursos adicionales

- [Documentación oficial: GitHub Copilot Chat en VS Code](https://code.visualstudio.com/docs/copilot/copilot-chat)
- [Guía de prompting efectivo para Copilot (GitHub Blog)](https://github.blog/news-insights/product-news/getting-the-most-out-of-github-copilot-tips-tricks-hacks/)
- [Acerca de GitHub Copilot Chat](https://docs.github.com/en/copilot/copilot-chat/about-github-copilot-chat)
- [PEP 257 — Convenciones de Docstrings en Python](https://peps.python.org/pep-0257/)
- [Guía de estilo de docstrings Google para Python](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings)


