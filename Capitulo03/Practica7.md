#  Práctica 7: Identifica un problema común en el desarrollo y utiliza Copilot Chat para proponer varias soluciones.

## Metadatos

| Campo            | Detalle                                      |
|------------------|----------------------------------------------|
| **Duración**     | 10 minutos (extensible a 25 min de forma autónoma) |
| **Complejidad**  | Media                                        |
| **Nivel Bloom**  | Aplicar (*Apply*)                            |
| **Módulo**       | 3 — Resolución de Necesidades de Negocio     |
| **Práctica**     | 7 de 10                                      |

---

## Descripción General

En esta práctica aplicarás el flujo **necesidad de negocio → artefactos técnicos** aprendido en la lección 3.1. Seleccionarás un problema técnico con impacto real en el negocio, lo formularás como un prompt estructurado para Copilot Chat y solicitarás **al menos tres soluciones alternativas**. Luego documentarás cada propuesta con sus ventajas, desventajas y escenario de aplicación ideal, para finalmente seleccionar y justificar la más adecuada para un contexto de negocio que tú mismo definirás.

Esta práctica es la base de las Prácticas 8 y 9; conserva todos los archivos generados.

---

## Objetivos de Aprendizaje

Al finalizar esta práctica serás capaz de:

- [ ] Formular un problema técnico de negocio con el patrón de prompt recomendado (contexto, restricciones, datos, criterios de éxito, formato de salida)
- [ ] Utilizar Copilot Chat para obtener múltiples soluciones alternativas a un mismo problema, evaluando la diversidad de enfoques propuestos
- [ ] Comparar las soluciones generadas según criterios de calidad: rendimiento, mantenibilidad, complejidad y adecuación al contexto de negocio
- [ ] Seleccionar y justificar la solución más apropiada para un escenario de negocio específico previamente definido
- [ ] Documentar el proceso de decisión como artefacto técnico reutilizable para las prácticas siguientes

---

## Prerrequisitos

### Conocimiento previo
- Haber completado las prácticas de los Módulos 1 y 2 (configuración de Copilot Chat, prompts básicos y evaluación de código)
- Comprensión básica de conceptos como rendimiento algorítmico, manejo de errores y buenas prácticas de código limpio
- Familiaridad con el patrón de prompt estructurado presentado en la lección 3.1

### Acceso y herramientas
- Suscripción activa a **GitHub Copilot** (verificada por el instructor al inicio del módulo)
- **VS Code 1.90+** con la extensión **GitHub Copilot Chat** instalada y autenticada
- **Python 3.10+** instalado y accesible desde la terminal integrada de VS Code
- Conexión a internet estable (mínimo 10 Mbps)
- Archivo de **diario de aprendizaje** iniciado en prácticas anteriores (Word, Google Docs, Notion u otro procesador de texto)

---

## Entorno de Laboratorio

### Requisitos de hardware

| Componente       | Mínimo                              | Recomendado                         |
|------------------|-------------------------------------|-------------------------------------|
| Procesador       | Intel Core i5 / AMD Ryzen 5 (64-bit)| Intel Core i7 / AMD Ryzen 7         |
| RAM              | 8 GB                                | 16 GB                               |
| Disco libre      | 2 GB                                | 10 GB                               |
| Pantalla         | 1280 × 768                          | 1920 × 1080                         |
| Red              | 10 Mbps                             | 25 Mbps o superior                  |

### Requisitos de software

| Software                        | Versión mínima          |
|---------------------------------|-------------------------|
| Visual Studio Code              | 1.90                    |
| GitHub Copilot Chat (extensión) | Última disponible       |
| Python                          | 3.10                    |
| Git                             | 2.40                    |
| pylint o flake8                 | pylint 3.x / flake8 7.x |
| Navegador web                   | Chrome / Edge / Firefox (última versión estable) |

### Configuración inicial del entorno

Ejecuta los siguientes comandos en la terminal integrada de VS Code para preparar el espacio de trabajo antes de comenzar los pasos del laboratorio:

```bash
# 1. Crear y navegar al directorio de trabajo del Módulo 3
mkdir -p ~/curso-copilot/modulo3/practica7
cd ~/curso-copilot/modulo3/practica7

# 2. Inicializar repositorio Git (si aún no existe)
git init
git config user.name "Tu Nombre"
git config user.email "tu@email.com"

# 3. Crear entorno virtual de Python
python -m venv .venv

# 4. Activar el entorno virtual
# En macOS/Linux:
source .venv/bin/activate
# En Windows (PowerShell):
# .venv\Scripts\Activate.ps1

# 5. Instalar herramienta de linting
pip install flake8

# 6. Crear estructura de archivos del laboratorio
touch problema_negocio.md
touch soluciones_comparadas.md
touch solucion_elegida.py

# 7. Abrir el directorio en VS Code
code .
```

**Verificación rápida del entorno:**

```bash
# Confirmar versión de Python
python --version          # Esperado: Python 3.10.x o superior

# Confirmar que Copilot Chat está activo
# En VS Code: Ctrl+Shift+P → "GitHub Copilot Chat: Open Chat"
# Debe abrirse el panel de chat sin errores de autenticación
```

---

## Procedimiento Paso a Paso

---

### Paso 1: Definir el contexto de negocio y seleccionar el problema

**Objetivo:** Establecer el escenario de negocio y formular el problema técnico de forma clara antes de interactuar con Copilot Chat.

#### Instrucciones

1. Abre el archivo `problema_negocio.md` en VS Code.

2. Elige **uno** de los siguientes problemas técnicos con impacto de negocio (o propón el tuyo propio si tienes un caso real de tu organización):

   | Opción | Problema técnico               | Contexto de negocio sugerido                                      |
   |--------|-------------------------------|-------------------------------------------------------------------|
   | A      | Búsqueda lenta en lista grande | E-commerce: filtrar catálogo de 50,000 productos por categoría    |
   | B      | Manejo de errores de BD        | Sistema bancario: transacciones que deben ser resilientes a fallos |
   | C      | Validación de entradas de usuario | Plataforma SaaS: formulario de registro con datos sensibles    |
   | D      | Caché simple para datos frecuentes | App de delivery: menús de restaurantes consultados miles de veces por hora |

3. Documenta el contexto en `problema_negocio.md` usando la siguiente plantilla:

```markdown
# Definición del Problema de Negocio

## Contexto
- **Empresa/Sector:** [Ej: E-commerce de moda con 200,000 usuarios activos]
- **Problema técnico seleccionado:** [Ej: Opción A — Búsqueda lenta en lista grande]
- **Impacto en el negocio:** [Ej: El tiempo de respuesta del filtro de productos supera 3s,
  causando una tasa de abandono del 40% en la página de catálogo]

## Objetivo y Métrica de Éxito
- **Objetivo:** [Ej: Reducir el tiempo de búsqueda a menos de 200ms para el percentil 95]
- **Métrica:** [Ej: Latencia p95 del endpoint de búsqueda, medida con logs de producción]

## Restricciones
- [Ej: El dataset actual está en memoria (lista Python), migración a BD no es posible en este sprint]
- [Ej: Compatibilidad con Python 3.10+, sin dependencias externas de pago]
- [Ej: El equipo tiene 1 sprint (2 semanas) para implementar]

## Criterios de Aceptación Preliminares
- [ ] La búsqueda retorna resultados correctos para todos los casos de prueba existentes
- [ ] El tiempo de respuesta mejora al menos un 70% respecto a la implementación actual
- [ ] El código es legible y documentado para el equipo de mantenimiento
```

4. Guarda el archivo con `Ctrl+S`.

#### Resultado Esperado

El archivo `problema_negocio.md` contiene una descripción clara y estructurada del problema, con contexto de negocio, métricas de éxito y restricciones definidas. Este documento será la base del prompt que usarás en el siguiente paso.

#### Verificación

```bash
# Confirmar que el archivo tiene contenido
cat problema_negocio.md | head -20
# Debe mostrar las primeras líneas del documento con el contexto definido
```

---

### Paso 2: Formular el prompt estructurado y solicitar múltiples soluciones a Copilot Chat

**Objetivo:** Aplicar el patrón de prompt **negocio → técnico** de la lección 3.1 para obtener al menos tres soluciones alternativas con código funcional.

#### Instrucciones

1. Abre el panel de **Copilot Chat** en VS Code:
   - Atajo: `Ctrl+Shift+I` (Windows/Linux) o `Cmd+Shift+I` (macOS)
   - O desde el menú: `View → GitHub Copilot Chat`

2. Asegúrate de que el archivo `problema_negocio.md` está abierto y visible en el editor (Copilot Chat puede usar el contexto del archivo activo).

3. Copia y adapta el siguiente prompt en el campo de chat. **Personaliza los corchetes `[ ]` con los valores que definiste en el Paso 1:**

```text
Actúa como un ingeniero de software senior con experiencia en Python y optimización de sistemas.

CONTEXTO DE NEGOCIO:
[Pega aquí el contenido de tu sección "Contexto" del archivo problema_negocio.md]

PROBLEMA TÉCNICO:
[Describe el problema técnico en 2-3 oraciones. Ej: "Tenemos una función Python que busca
productos por nombre en una lista de 50,000 diccionarios. Actualmente usa búsqueda lineal
y tarda entre 2-4 segundos. Necesitamos reducir este tiempo a menos de 200ms."]

RESTRICCIONES:
[Lista tus restricciones del archivo problema_negocio.md]

CRITERIOS DE ÉXITO:
[Pega tus criterios de aceptación]

SOLICITUD:
Proporciona EXACTAMENTE 3 soluciones alternativas en Python para este problema.
Para cada solución incluye:
1. Nombre del enfoque (ej: "Enfoque 1: Índice con diccionario hash")
2. Descripción en 2-3 oraciones de la estrategia
3. Código Python completo y funcional con comentarios explicativos
4. Ventajas (mínimo 2)
5. Desventajas (mínimo 2)
6. Escenario de negocio ideal donde este enfoque sería la mejor elección
7. Estimación de complejidad: tiempo O(?) y espacio O(?)

Al final, agrega una tabla comparativa de las 3 soluciones con columnas:
Enfoque | Complejidad Tiempo | Complejidad Espacio | Facilidad de Implementación | Mantenibilidad

Incluye también: supuestos que estás haciendo y riesgos a considerar.
```

4. Envía el prompt y **espera la respuesta completa** de Copilot Chat.

5. Si la respuesta es incompleta o falta alguna solución, usa este prompt de seguimiento:

```text
La solución [número] está incompleta. Por favor, proporciona el código Python completo
para ese enfoque, incluyendo una función de prueba con datos de ejemplo que demuestre
su funcionamiento.
```

#### Resultado Esperado

Copilot Chat debe responder con tres bloques claramente diferenciados, cada uno con código Python funcional, análisis de complejidad y contexto de aplicación. La respuesta debe incluir una tabla comparativa al final.

**Ejemplo de estructura de respuesta esperada (fragmento ilustrativo):**

```
## Enfoque 1: Búsqueda Lineal Optimizada con Early Exit
**Descripción:** Mejora la búsqueda lineal actual añadiendo...

**Código:**
```python
def buscar_producto_lineal(productos: list[dict], nombre: str) -> dict | None:
    """
    Búsqueda lineal con early exit y comparación case-insensitive.
    Complejidad: O(n) tiempo, O(1) espacio.
    """
    nombre_lower = nombre.lower().strip()
    for producto in productos:
        if producto.get("nombre", "").lower() == nombre_lower:
            return producto
    return None
```

**Ventajas:** ...
**Desventajas:** ...
```

#### Verificación

- La respuesta contiene exactamente 3 (o más) enfoques diferenciados
- Cada enfoque tiene código Python que se puede copiar y ejecutar
- Existe una tabla comparativa al final de la respuesta
- Se mencionan supuestos y riesgos

---

### Paso 3: Documentar y ejecutar las soluciones propuestas

**Objetivo:** Capturar las soluciones en archivos de código ejecutables y verificar que funcionan correctamente antes de compararlas.

#### Instrucciones

1. Crea un archivo Python para cada solución. En la terminal integrada:

```bash
touch solucion_1.py
touch solucion_2.py
touch solucion_3.py
touch datos_prueba.py
```

2. Abre `datos_prueba.py` y crea un dataset de prueba representativo. Puedes pedirle a Copilot Chat que lo genere con este prompt:

```text
Genera un script Python llamado datos_prueba.py que cree una lista de 50,000 diccionarios
simulando un catálogo de productos de e-commerce. Cada diccionario debe tener los campos:
id (int), nombre (str), categoria (str), precio (float), stock (int).
Usa nombres de productos realistas y variados. Incluye al menos 5 productos con nombres
que contengan la palabra "camiseta" para facilitar las pruebas de búsqueda.
Exporta la lista como la variable CATALOGO.
```

3. Copia el código de **cada solución** desde la respuesta de Copilot Chat a su archivo correspondiente (`solucion_1.py`, `solucion_2.py`, `solucion_3.py`).

4. Agrega al final de cada archivo de solución un bloque de prueba con medición de tiempo. Pide a Copilot Chat:

```text
Agrega al final de [solucion_1.py / solucion_2.py / solucion_3.py] un bloque
if __name__ == "__main__": que:
1. Importe CATALOGO desde datos_prueba.py
2. Ejecute la función de búsqueda 100 veces buscando "camiseta azul"
3. Mida el tiempo promedio usando el módulo timeit
4. Imprima: "Tiempo promedio: X.XXX ms" y el primer resultado encontrado
```

5. Ejecuta cada solución y captura los resultados:

```bash
# Ejecutar cada solución
python datos_prueba.py      # Verificar que genera datos sin errores
python solucion_1.py
python solucion_2.py
python solucion_3.py
```

6. Ejecuta el linter sobre cada archivo:

```bash
flake8 solucion_1.py solucion_2.py solucion_3.py --max-line-length=100
```

7. Si el linter reporta errores, pide a Copilot Chat que los corrija:

```text
El linter flake8 reporta los siguientes errores en solucion_1.py:
[pega los errores aquí]
Por favor, corrige el código manteniendo la misma lógica funcional.
```

#### Resultado Esperado

```
# Ejemplo de salida esperada al ejecutar solucion_1.py:
Tiempo promedio: 45.230 ms
Resultado encontrado: {'id': 1042, 'nombre': 'Camiseta Azul Marino', 'categoria': 'Ropa', 'precio': 29.99, 'stock': 150}

# Ejemplo de salida esperada al ejecutar solucion_2.py:
Tiempo promedio: 0.082 ms
Resultado encontrado: {'id': 1042, 'nombre': 'Camiseta Azul Marino', 'categoria': 'Ropa', 'precio': 29.99, 'stock': 150}

# Ejemplo de salida esperada al ejecutar solucion_3.py:
Tiempo promedio: 0.195 ms
Resultado encontrado: {'id': 1042, 'nombre': 'Camiseta Azul Marino', 'categoria': 'Ropa', 'precio': 29.99, 'stock': 150}
```

#### Verificación

```bash
# Confirmar que los tres archivos de solución existen y tienen contenido
wc -l solucion_1.py solucion_2.py solucion_3.py
# Cada archivo debe tener al menos 15 líneas de código

# Confirmar que no hay errores de sintaxis Python
python -m py_compile solucion_1.py && echo "solucion_1: OK"
python -m py_compile solucion_2.py && echo "solucion_2: OK"
python -m py_compile solucion_3.py && echo "solucion_3: OK"
```

---

### Paso 4: Comparar las soluciones y documentar el análisis

**Objetivo:** Construir el documento de comparación estructurado que servirá como artefacto técnico para la toma de decisiones.

#### Instrucciones

1. Abre el archivo `soluciones_comparadas.md`.

2. Usa el siguiente prompt en Copilot Chat para enriquecer tu análisis con perspectiva de negocio:

```text
Basándote en las 3 soluciones que propusiste anteriormente para [describe tu problema],
y considerando los siguientes resultados de rendimiento medidos:

- Solución 1 ([nombre del enfoque]): [X] ms promedio
- Solución 2 ([nombre del enfoque]): [X] ms promedio
- Solución 3 ([nombre del enfoque]): [X] ms promedio

Proporciona un análisis comparativo desde la perspectiva de un equipo de desarrollo que debe:
1. Entregar en 2 semanas
2. Mantener el código durante 2 años
3. Escalar de 50,000 a 500,000 productos en los próximos 6 meses

Para cada solución evalúa (escala 1-5):
- Rendimiento actual
- Escalabilidad futura
- Facilidad de implementación
- Facilidad de mantenimiento
- Riesgo de introducir bugs

¿Cuál recomiendas y por qué? Incluye advertencias sobre lo que podría salir mal con cada opción.
```

3. Documenta el análisis en `soluciones_comparadas.md` con esta estructura:

```markdown
# Comparación de Soluciones — Práctica 7

## Problema: [Nombre del problema seleccionado]
## Contexto de negocio: [Descripción breve]
## Fecha: [Fecha actual]

---

## Solución 1: [Nombre del Enfoque]

### Descripción del Enfoque
[2-3 oraciones describiendo la estrategia]

### Código Implementado
[Referencia al archivo: ver solucion_1.py]

### Resultados de Rendimiento
- Tiempo promedio medido: [X] ms
- Mejora respecto a baseline: [X]%

### Ventajas
- [Ventaja 1]
- [Ventaja 2]

### Desventajas
- [Desventaja 1]
- [Desventaja 2]

### Escenario de Negocio Ideal
[Describe en qué contexto de negocio esta solución sería la más apropiada]

### Puntuación (1-5)
| Criterio                    | Puntuación |
|-----------------------------|-----------|
| Rendimiento actual          | [1-5]     |
| Escalabilidad futura        | [1-5]     |
| Facilidad de implementación | [1-5]     |
| Facilidad de mantenimiento  | [1-5]     |
| Riesgo de bugs              | [1-5]     |
| **TOTAL**                   | **[suma]**|

---

## Solución 2: [Nombre del Enfoque]
[Misma estructura que Solución 1]

---

## Solución 3: [Nombre del Enfoque]
[Misma estructura que Solución 1]

---

## Tabla Comparativa Resumen

| Criterio                    | Solución 1 | Solución 2 | Solución 3 |
|-----------------------------|-----------|-----------|-----------|
| Rendimiento actual (ms)     |           |           |           |
| Escalabilidad futura        |           |           |           |
| Facilidad de implementación |           |           |           |
| Facilidad de mantenimiento  |           |           |           |
| Riesgo de bugs              |           |           |           |
| **Puntuación Total**        |           |           |           |

---

## Supuestos y Riesgos Identificados por Copilot Chat
[Lista los supuestos y riesgos que Copilot Chat identificó]

## Reflexión Personal
[2-3 oraciones sobre lo que observaste en las diferencias entre las soluciones]
```

4. Guarda el documento con `Ctrl+S`.

#### Resultado Esperado

El archivo `soluciones_comparadas.md` contiene el análisis completo de las tres soluciones con puntuaciones, tabla comparativa y reflexión personal. Este documento debe tener al menos 60 líneas de contenido significativo.

#### Verificación

```bash
# Contar líneas del documento de comparación
wc -l soluciones_comparadas.md
# Debe tener al menos 60 líneas

# Verificar que el archivo no está vacío
head -5 soluciones_comparadas.md
```

---

### Paso 5: Seleccionar la solución final y construir el artefacto de entrega

**Objetivo:** Tomar una decisión justificada y producir el código final de la solución elegida, listo para revisión de equipo.

#### Instrucciones

1. Con base en tu análisis del Paso 4, selecciona la solución más adecuada para tu contexto de negocio específico.

2. Abre el archivo `solucion_elegida.py` y usa Copilot Chat para refinar la solución seleccionada:

```text
Basándome en mi análisis, he elegido [Solución X: nombre del enfoque] para mi contexto de
[describe tu contexto de negocio en 1 oración].

Por favor, refina el código de esta solución para que sea production-ready:
1. Agrega docstrings completos en formato Google Style
2. Añade type hints en todas las funciones
3. Incluye manejo de errores apropiado (ValueError, TypeError, casos edge)
4. Agrega logging básico usando el módulo logging de Python
5. Incluye al menos 3 funciones de prueba unitaria usando unittest
6. Agrega un comentario de encabezado con: fecha, autor (Estudiante), versión, descripción

El código debe pasar flake8 sin errores con --max-line-length=100.
```

3. Copia el código refinado a `solucion_elegida.py` y ejecuta las verificaciones:

```bash
# Ejecutar la solución final
python solucion_elegida.py

# Verificar con linter
flake8 solucion_elegida.py --max-line-length=100

# Ejecutar las pruebas unitarias incluidas
python -m unittest solucion_elegida -v
```

4. Agrega al inicio del archivo `solucion_elegida.py` el siguiente bloque de decisión como comentario:

```python
"""
DECISIÓN TÉCNICA — Práctica 7
==============================
Problema: [Nombre del problema]
Solución elegida: [Nombre del enfoque]
Razón principal: [1-2 oraciones justificando la elección]
Contexto de negocio: [Descripción del escenario]
Alternativas consideradas: [Lista de las otras 2 soluciones]
Compromisos aceptados (trade-offs): [Qué se sacrifica con esta elección]
Fecha de decisión: [Fecha actual]
Autor: Estudiante
"""
```

5. Realiza el commit final del laboratorio:

```bash
# Agregar todos los archivos al staging
git add .

# Commit con mensaje descriptivo
git commit -m "practica7: analisis de 3 soluciones para [nombre-del-problema]

- Problema seleccionado: [nombre]
- Soluciones comparadas: [enfoque1], [enfoque2], [enfoque3]
- Solución elegida: [enfoque elegido]
- Documentación: problema_negocio.md, soluciones_comparadas.md"
```

#### Resultado Esperado

```
# Salida esperada de python solucion_elegida.py:
INFO:root:Iniciando búsqueda de productos...
INFO:root:Índice construido con 50000 productos
Tiempo promedio: 0.082 ms
Resultado: {'id': 1042, 'nombre': 'Camiseta Azul Marino', ...}
INFO:root:Búsqueda completada exitosamente

# Salida esperada de unittest:
test_busqueda_exitosa ... ok
test_busqueda_no_encontrada ... ok
test_busqueda_entrada_vacia ... ok
----------------------------------------------------------------------
Ran 3 tests in 0.003s
OK

# Salida esperada de flake8:
(sin salida = sin errores)
```

#### Verificación

```bash
# Verificar el commit en el historial de Git
git log --oneline -3
# Debe mostrar el commit de la práctica 7 como el más reciente

# Listar todos los archivos del laboratorio
ls -la ~/curso-copilot/modulo3/practica7/
# Debe mostrar: problema_negocio.md, soluciones_comparadas.md,
#               solucion_1.py, solucion_2.py, solucion_3.py,
#               solucion_elegida.py, datos_prueba.py
```

---

## Validación y Pruebas

Antes de dar por completada la práctica, verifica que se cumplen todos los criterios de la siguiente lista:

### Lista de Verificación Final

```bash
# === VERIFICACIÓN AUTOMATIZADA ===

echo "=== Verificando archivos del laboratorio ==="
for f in problema_negocio.md soluciones_comparadas.md solucion_1.py solucion_2.py solucion_3.py solucion_elegida.py datos_prueba.py; do
    if [ -f "$f" ]; then
        echo "✓ $f existe"
    else
        echo "✗ FALTA: $f"
    fi
done

echo ""
echo "=== Verificando sintaxis Python ==="
for f in solucion_1.py solucion_2.py solucion_3.py solucion_elegida.py; do
    python -m py_compile "$f" && echo "✓ $f: sintaxis OK" || echo "✗ $f: ERROR de sintaxis"
done

echo ""
echo "=== Verificando linting ==="
flake8 solucion_elegida.py --max-line-length=100 && echo "✓ solucion_elegida.py: linting OK"

echo ""
echo "=== Ejecutando pruebas unitarias ==="
python -m unittest solucion_elegida -v

echo ""
echo "=== Verificando commit Git ==="
git log --oneline -1
```

### Criterios de Aceptación del Laboratorio

| Criterio | Descripción | Estado |
|----------|-------------|--------|
| Problema documentado | `problema_negocio.md` con contexto, métricas y restricciones | ☐ |
| 3 soluciones generadas | Código funcional para cada alternativa | ☐ |
| Medición de rendimiento | Tiempo promedio medido para las 3 soluciones | ☐ |
| Análisis documentado | `soluciones_comparadas.md` con tabla comparativa y puntuaciones | ☐ |
| Solución final refinada | `solucion_elegida.py` con docstrings, type hints y pruebas | ☐ |
| Linting sin errores | `flake8` pasa en `solucion_elegida.py` | ☐ |
| Pruebas unitarias pasan | Mínimo 3 pruebas con `unittest` | ☐ |
| Decisión justificada | Bloque de decisión técnica en el encabezado del archivo | ☐ |
| Commit realizado | Historial Git con mensaje descriptivo | ☐ |
| Diario actualizado | Reflexión agregada al diario de aprendizaje personal | ☐ |

### Actualización del Diario de Aprendizaje

Antes de cerrar la práctica, agrega la siguiente reflexión a tu diario personal:

```markdown
## Práctica 7 — Fecha: [fecha]

**Problema trabajado:** [nombre del problema]
**Solución elegida:** [nombre del enfoque]

**¿Qué me sorprendió de las soluciones que propuso Copilot Chat?**
[Tu respuesta]

**¿En qué momento tuve que corregir o guiar a Copilot Chat?**
[Tu respuesta]

**¿Cómo cambió mi comprensión del problema al tener que comparar 3 alternativas?**
[Tu respuesta]

**Trade-off más importante que identifiqué:**
[Tu respuesta]

**¿Qué llevaré a la Práctica 8?**
[Archivos conservados, aprendizajes clave]
```

---

## Solución de Problemas

### Problema 1: Copilot Chat devuelve menos de 3 soluciones o las soluciones son muy similares entre sí

**Síntoma:** La respuesta de Copilot Chat contiene solo 1 o 2 soluciones, o las tres propuestas usan esencialmente el mismo algoritmo con variaciones menores sin valor diferenciador.

**Causa probable:** El prompt no fue suficientemente explícito en pedir enfoques *estructuralmente diferentes*, o el contexto del problema fue demasiado restrictivo, lo que llevó al modelo a convergir en una sola familia de soluciones.

**Solución:**

Envía el siguiente prompt de seguimiento en la misma conversación de Copilot Chat:

```text
Las soluciones anteriores son demasiado similares entre sí. Necesito 3 enfoques
que sean fundamentalmente diferentes en su estrategia algorítmica o arquitectónica.

Por ejemplo, para un problema de búsqueda podrías proponer:
- Un enfoque basado en estructura de datos (índice/hash)
- Un enfoque basado en algoritmo de búsqueda diferente (binaria, Trie, etc.)
- Un enfoque basado en preprocesamiento o caché

Por favor, regenera las 3 soluciones asegurándote de que cada una use una
estrategia DIFERENTE. Indica explícitamente en qué se diferencia cada enfoque
del anterior antes de mostrar el código.
```

Si el problema persiste, reformula el problema con más contexto o elige un problema diferente de la tabla del Paso 1.

---

### Problema 2: El código generado por Copilot Chat falla al ejecutarse con errores de importación o de sintaxis

**Síntoma:** Al ejecutar `python solucion_1.py` (o cualquier archivo de solución), aparece un `ImportError`, `ModuleNotFoundError`, `SyntaxError` o `IndentationError`. El código se ve correcto visualmente pero no se puede ejecutar.

**Causa probable:** Copilot Chat puede generar código que asume la existencia de librerías de terceros no instaladas (ej. `numpy`, `pandas`, `sortedcontainers`), usa sintaxis de una versión de Python diferente a la instalada, o genera código con indentación mezclada (tabs y espacios).

**Solución:**

```bash
# Paso 1: Identificar el error específico
python solucion_1.py 2>&1 | head -20

# Paso 2a: Si es ModuleNotFoundError, instalar la dependencia
# (solo si es una librería estándar o de uso común y confiable)
pip install [nombre-del-modulo]

# Paso 2b: Si prefieres no instalar dependencias externas,
# pide a Copilot Chat una versión sin dependencias externas:
```

```text
El código de la Solución [X] usa [nombre_librería] que no está disponible
en mi entorno. Por favor, reescribe la misma solución usando únicamente
la biblioteca estándar de Python 3.10 (sin pip install).
Mantén la misma estrategia algorítmica.
```

```bash
# Paso 3: Si es un error de indentación, usar autopep8 para corregir
pip install autopep8
autopep8 --in-place solucion_1.py

# Paso 4: Verificar que el error se resolvió
python -m py_compile solucion_1.py && echo "OK"
python solucion_1.py
```

---

## Limpieza del Entorno

Al finalizar la práctica, **no elimines** los archivos generados, ya que son necesarios para las Prácticas 8 y 9. Solo realiza la siguiente limpieza de archivos temporales:

```bash
# Navegar al directorio del laboratorio
cd ~/curso-copilot/modulo3/practica7

# Eliminar archivos de caché de Python (no son necesarios para las prácticas siguientes)
find . -type d -name "__pycache__" -exec rm -rf {} + 2>/dev/null
find . -name "*.pyc" -delete 2>/dev/null

# Verificar que los archivos importantes están intactos
ls -la
# Deben estar presentes: problema_negocio.md, soluciones_comparadas.md,
# solucion_1.py, solucion_2.py, solucion_3.py, solucion_elegida.py, datos_prueba.py

# Desactivar el entorno virtual si ya no lo necesitas en esta sesión
# (NO lo elimines; lo necesitarás en las Prácticas 8 y 9)
deactivate

# Confirmar el estado limpio del repositorio Git
git status
# Debe mostrar: "nothing to commit, working tree clean"

echo "Práctica 7 completada. Archivos conservados para Prácticas 8 y 9."
```

> ⚠️ **Importante:** El directorio `~/curso-copilot/modulo3/practica7/` y su entorno virtual `.venv` deben mantenerse intactos. Las Prácticas 8 y 9 del Módulo 3 dependen directamente de los archivos generados en esta práctica.

---

## Resumen

### Lo que Lograste en Esta Práctica

En esta práctica aplicaste el flujo completo de **resolución de necesidades de negocio con Copilot Chat**, tal como se presentó en la lección 3.1:

1. **Tradujiste una necesidad de negocio** en un prompt estructurado usando el patrón: contexto → restricciones → datos → criterios de éxito → formato de salida
2. **Obtuviste múltiples soluciones alternativas** de Copilot Chat, experimentando cómo la especificidad del prompt influye directamente en la diversidad y calidad de las respuestas
3. **Ejecutaste y mediste** cada solución con datos reales, obteniendo evidencia empírica para la toma de decisiones
4. **Evaluaste críticamente** las propuestas según criterios de rendimiento, mantenibilidad, escalabilidad y riesgo — no solo aceptando la primera respuesta de la IA
5. **Documentaste la decisión técnica** como artefacto reutilizable, estableciendo trazabilidad entre el problema de negocio y el código producido

### Conceptos Clave Reforzados

| Concepto | Aplicación en esta práctica |
|----------|----------------------------|
| Patrón de prompt negocio→técnico | Usado para formular el problema inicial |
| Criterios de aceptación | Definidos antes de generar código, usados para evaluar soluciones |
| Trazabilidad | Documentos vinculan problema → análisis → código → decisión |
| Evaluación crítica de IA | Comparación objetiva con métricas medidas, no solo opinión |
| Trade-offs de ingeniería | Explicitados en el bloque de decisión técnica del archivo final |

### Conexión con las Prácticas Siguientes

- **Práctica 8:** Tomará la `solucion_elegida.py` de esta práctica y la extenderá con funcionalidades adicionales usando Copilot Chat como herramienta de autocompletado y refactorización
- **Práctica 9:** Usará el `soluciones_comparadas.md` y el diario de aprendizaje para una reflexión estructurada sobre el rol evolutivo del programador en entornos con IA generativa

### Recursos Adicionales

| Recurso | URL |
|---------|-----|
| Documentación oficial de GitHub Copilot Chat | https://docs.github.com/es/copilot/copilot-chat/using-github-copilot-chat |
| Complejidad algorítmica — Big O Notation (referencia) | https://wiki.python.org/moin/TimeComplexity |
| Google Style Python Docstrings | https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings |
| Módulo `timeit` de Python (para medición de rendimiento) | https://docs.python.org/3/library/timeit.html |
| Módulo `unittest` de Python | https://docs.python.org/3/library/unittest.html |
| Buenas prácticas de toma de decisiones técnicas (Architecture Decision Records) | https://adr.github.io/ |




