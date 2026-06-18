# Práctica 2: Utiliza Copilot Chat para automatizar una tarea repetitiva en tu código. Documenta el proceso y los resultados.

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