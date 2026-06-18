# Práctica 3: Realiza una comparación de tiempo entre escribir un fragmento de código manualmente y utilizar Copilot Chat para completarlo.

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
