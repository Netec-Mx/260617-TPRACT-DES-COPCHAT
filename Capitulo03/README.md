# Identifica un problema común en el desarrollo y utiliza Copilot Chat para proponer varias soluciones

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

---

*Práctica 7 de 10 — Módulo 3: Resolución de Necesidades de Negocio*
*Conserva todos los archivos generados. La Práctica 8 continúa desde donde esta terminó.*

---

# Desarrolla una funcionalidad que mejore un producto existente basándote en las sugerencias de Copilot Chat.

## Metadatos

| Campo            | Detalle                                      |
|------------------|----------------------------------------------|
| **Duración**     | 10 minutos (clase) / hasta 30 minutos (autónomo) |
| **Complejidad**  | Alta                                         |
| **Nivel Bloom**  | Crear (*Create*)                             |
| **Módulo**       | 3 — Resolución de Necesidades de Negocio     |
| **Práctica**     | 8 de 10                                      |

---

## Descripción General

En esta práctica aplicarás el flujo **necesidad de negocio → artefactos técnicos** aprendido en la lección 3.1 para diseñar e implementar una funcionalidad nueva sobre un producto de software existente. Partirás del código base construido en la Práctica 6 (o un fragmento de gestión de inventario proporcionado), identificarás una oportunidad de mejora concreta, y usarás Copilot Chat para generar historias de usuario, criterios de aceptación (Gherkin), el código de la nueva funcionalidad y pruebas unitarias básicas. El ciclo cierra con una fase de refinamiento iterativo donde evaluarás la cohesión del código integrado y la calidad del resultado final.

---

## Objetivos de Aprendizaje

Al finalizar esta práctica serás capaz de:

- [ ] Analizar un producto de software existente para identificar oportunidades de mejora funcional alineadas a una necesidad de negocio real.
- [ ] Utilizar Copilot Chat con el patrón de prompt **contexto → restricciones → datos → definición de éxito → formato de salida** para diseñar e implementar una nueva funcionalidad.
- [ ] Integrar el código generado por Copilot Chat con código existente, evaluando la cohesión, calidad y trazabilidad del resultado.

---

## Prerrequisitos

### Conocimiento previo
- Haber completado la **Práctica 7** y conservar sus archivos de código.
- Contar con el código base del **mini proyecto de la Práctica 6** (sistema de inventario, carrito de compras o similar) en un repositorio Git local.
- Familiaridad con el patrón de prompt de negocio→técnico y con el formato Gherkin (lección 3.1).
- Conocimiento básico de Python (o el lenguaje elegido) y de escritura de pruebas unitarias con `unittest` o `pytest`.

### Acceso y herramientas
- Suscripción activa a **GitHub Copilot** (verificada por el instructor al inicio del curso).
- **VS Code 1.90+** con la extensión **GitHub Copilot Chat** instalada y autenticada.
- **Python 3.10+** instalado y accesible desde la terminal.
- **Git 2.40+** instalado.
- Archivo de **diario de aprendizaje** activo (requerido para Práctica 9).

---

## Entorno de Laboratorio

### Hardware recomendado

| Componente        | Mínimo                        | Recomendado                  |
|-------------------|-------------------------------|------------------------------|
| Procesador        | Intel Core i5 / AMD Ryzen 5   | Core i7 / Ryzen 7 (64-bit)   |
| RAM               | 8 GB                          | 16 GB                        |
| Espacio en disco  | 10 GB libres                  | 20 GB libres                 |
| Conectividad      | 10 Mbps estables              | 25 Mbps o superior           |
| Pantalla          | 1280 × 768                    | 1920 × 1080                  |

### Software requerido

| Herramienta                  | Versión mínima       | Verificación rápida              |
|------------------------------|----------------------|----------------------------------|
| Python                       | 3.10                 | `python --version`               |
| VS Code                      | 1.90                 | `code --version`                 |
| GitHub Copilot Chat (ext.)   | Última disponible    | Panel de extensiones en VS Code  |
| Git                          | 2.40                 | `git --version`                  |
| pytest                       | 7.x o superior       | `pytest --version`               |

### Configuración inicial del entorno

Ejecuta los siguientes comandos en tu terminal **antes de iniciar los pasos del laboratorio**:

```bash
# 1. Navega al directorio de trabajo del curso
cd ~/curso-copilot

# 2. Verifica que el repositorio de la Práctica 6 existe
ls practica-06/

# 3. Crea el directorio de trabajo para esta práctica
cp -r practica-06/ practica-08/
cd practica-08/

# 4. Inicializa entorno virtual e instala dependencias
python -m venv .venv
source .venv/bin/activate        # macOS / Linux
# .venv\Scripts\activate         # Windows PowerShell

pip install pytest

# 5. Confirma que el entorno está activo
python --version
pytest --version
```

> **Nota:** Si no cuentas con el código de la Práctica 6, el **Paso 1** incluye un fragmento base alternativo que puedes usar directamente.

---

## Pasos del Laboratorio

---

### Paso 1 — Preparar el código base y abrir VS Code

**Objetivo:** Establecer el punto de partida con el código existente abierto en VS Code y Copilot Chat disponible.

#### Instrucciones

1. Abre VS Code en el directorio de trabajo:

```bash
code .
```

2. Verifica que la extensión **GitHub Copilot Chat** aparece activa en la barra de estado inferior (ícono de Copilot sin símbolo de advertencia).

3. Si **no tienes el código de la Práctica 6**, crea el siguiente archivo base como punto de partida. En VS Code, crea `inventory.py` con este contenido:

```python
# inventory.py — Sistema de inventario básico (código base Práctica 6)
# Este módulo simula la gestión de productos en un almacén pequeño.

from dataclasses import dataclass, field
from typing import Optional


@dataclass
class Product:
    """Representa un producto en el inventario."""
    sku: str
    name: str
    price: float
    stock: int
    category: str = "general"


class Inventory:
    """Gestión básica de inventario."""

    def __init__(self):
        self._products: dict[str, Product] = {}

    def add_product(self, product: Product) -> None:
        """Agrega un producto al inventario."""
        if product.sku in self._products:
            raise ValueError(f"El SKU '{product.sku}' ya existe.")
        self._products[product.sku] = product

    def get_product(self, sku: str) -> Optional[Product]:
        """Retorna un producto por SKU o None si no existe."""
        return self._products.get(sku)

    def update_stock(self, sku: str, quantity: int) -> None:
        """Actualiza el stock de un producto (puede ser negativo para ventas)."""
        product = self.get_product(sku)
        if product is None:
            raise KeyError(f"Producto '{sku}' no encontrado.")
        if product.stock + quantity < 0:
            raise ValueError("Stock insuficiente.")
        product.stock += quantity

    def list_products(self) -> list[Product]:
        """Retorna todos los productos del inventario."""
        return list(self._products.values())
```

4. Crea también un archivo de pruebas existente `test_inventory.py`:

```python
# test_inventory.py — Pruebas existentes del sistema de inventario
import pytest
from inventory import Inventory, Product


@pytest.fixture
def sample_inventory():
    inv = Inventory()
    inv.add_product(Product("SKU-001", "Laptop", 1200.00, 10, "electronics"))
    inv.add_product(Product("SKU-002", "Mouse", 25.00, 100, "electronics"))
    inv.add_product(Product("SKU-003", "Desk", 350.00, 5, "furniture"))
    return inv


def test_add_product(sample_inventory):
    p = Product("SKU-004", "Chair", 200.00, 20, "furniture")
    sample_inventory.add_product(p)
    assert sample_inventory.get_product("SKU-004") is not None


def test_update_stock_reduces(sample_inventory):
    sample_inventory.update_stock("SKU-001", -3)
    assert sample_inventory.get_product("SKU-001").stock == 7


def test_update_stock_insufficient_raises(sample_inventory):
    with pytest.raises(ValueError, match="Stock insuficiente"):
        sample_inventory.update_stock("SKU-001", -999)
```

5. Ejecuta las pruebas existentes para confirmar que el código base funciona:

```bash
pytest test_inventory.py -v
```

#### Salida esperada

```
collected 3 items

test_inventory.py::test_add_product PASSED
test_inventory.py::test_update_stock_reduces PASSED
test_inventory.py::test_update_stock_insufficient_raises PASSED

3 passed in 0.XXs
```

#### Verificación

✅ Las 3 pruebas pasan sin errores antes de continuar al Paso 2.

---

### Paso 2 — Identificar la necesidad de negocio y formular el prompt inicial

**Objetivo:** Aplicar el patrón de prompt **contexto → restricciones → datos → definición de éxito → formato de salida** para que Copilot Chat genere los artefactos de diseño de la nueva funcionalidad.

#### Instrucciones

1. Abre el panel de **Copilot Chat** en VS Code:
   - Haz clic en el ícono de chat en la barra lateral izquierda, **o**
   - Usa el atajo: `Ctrl+Alt+I` (Windows/Linux) / `Cmd+Option+I` (macOS).

2. Asegúrate de que el archivo `inventory.py` está **abierto y activo** en el editor (esto provee contexto al modelo).

3. Copia y envía el siguiente prompt completo en el chat. Este prompt aplica directamente el patrón aprendido en la lección 3.1:

```text
Contexto: Tengo un sistema de inventario básico en Python (archivo inventory.py abierto).
El negocio necesita implementar un sistema de descuentos por volumen para incentivar
compras mayoristas y aumentar el ticket promedio por transacción.

Restricciones:
- El código debe integrarse con las clases Product e Inventory existentes sin romper
  las pruebas actuales.
- Sin dependencias externas adicionales (solo stdlib de Python).
- Los descuentos deben ser configurables (no hardcodeados).
- La lógica de descuentos debe ser testeable de forma aislada.

Datos disponibles:
- Cada producto tiene: sku, name, price, stock, category.
- Los descuentos se aplican por rangos de cantidad (ej: 5-9 unidades → 5%, 10+ → 10%).

Definición de éxito:
- Un cliente puede calcular el precio total con descuento para una lista de ítems.
- El sistema soporta múltiples reglas de descuento configurables por producto o categoría.
- Se puede consultar qué descuento aplica para una cantidad dada.

Solicita:
1) 2 historias de usuario con IDs (US-001, US-002) y criterios de aceptación en Gherkin.
2) Diseño de la clase o función en Python (nombres, métodos públicos, tipos).
3) Código de implementación completo listo para integrar con inventory.py.
4) 4 casos de prueba con pytest que cubran: caso feliz, descuento no aplica, límite exacto
   de rango, y categoría sin regla definida.

Incluye: supuestos que estás haciendo y riesgos identificados.
Formatea con encabezados claros.
```

4. **Espera la respuesta completa** de Copilot Chat. No interrumpas el stream.

5. Lee la respuesta completa antes de copiar cualquier código. Presta atención especial a:
   - Los supuestos que Copilot declara explícitamente.
   - Si el diseño propuesto es compatible con las clases existentes.
   - Si los criterios de aceptación son verificables.

#### Salida esperada

Copilot Chat debe generar una respuesta estructurada similar a:

```
## Historias de Usuario

**US-001**: Como comprador mayorista, quiero ver el precio con descuento al comprar
por volumen, para reducir mi costo unitario.

**US-002**: Como administrador, quiero configurar reglas de descuento por producto
o categoría, para adaptar la estrategia comercial sin cambiar código.

## Criterios de Aceptación (Gherkin)

Feature: Descuentos por volumen
  Scenario: Descuento aplicado por cantidad en rango
    Given existe una regla de descuento del 10% para qty >= 10
    When calculo el precio de 10 unidades de "Laptop" a $1200
    Then el precio total es $10800 (descuento aplicado)

  Scenario: Sin descuento cuando la cantidad es menor al umbral mínimo
    Given la regla mínima de descuento es para qty >= 5
    When calculo el precio de 3 unidades de "Mouse"
    Then el precio total es $75 (precio regular)

## Diseño Propuesto
class DiscountRule: ...
class DiscountEngine: ...

## Código de Implementación
[código Python completo]

## Pruebas
[4 casos de prueba con pytest]

## Supuestos y Riesgos
- Supuesto: las reglas se almacenan en memoria (sin persistencia)...
- Riesgo: colisión entre regla por producto y por categoría...
```

#### Verificación

✅ La respuesta incluye al menos: historias de usuario con IDs, criterios Gherkin, código Python, pruebas y una sección de supuestos/riesgos.

---

### Paso 3 — Integrar el código generado con el sistema existente

**Objetivo:** Crear el archivo de la nueva funcionalidad, integrarlo con `inventory.py` y verificar que no rompe el código existente.

#### Instrucciones

1. Crea un nuevo archivo llamado `discount_engine.py` en el mismo directorio:

```bash
touch discount_engine.py
```

2. Copia el código de implementación generado por Copilot Chat en `discount_engine.py`. Si la respuesta de Copilot fue incompleta o imprecisa, usa esta implementación de referencia como base:

```python
# discount_engine.py — Sistema de descuentos por volumen
# Generado con asistencia de GitHub Copilot Chat e integrado manualmente.

from dataclasses import dataclass, field
from typing import Optional


@dataclass
class DiscountRule:
    """
    Define una regla de descuento por volumen.

    Atributos:
        min_qty: Cantidad mínima para activar el descuento.
        max_qty: Cantidad máxima del rango (None = sin límite superior).
        discount_pct: Porcentaje de descuento (0.0 a 1.0, ej: 0.10 = 10%).
    """
    min_qty: int
    discount_pct: float
    max_qty: Optional[int] = None

    def __post_init__(self):
        if not (0.0 <= self.discount_pct <= 1.0):
            raise ValueError("discount_pct debe estar entre 0.0 y 1.0")
        if self.min_qty < 1:
            raise ValueError("min_qty debe ser al menos 1")
        if self.max_qty is not None and self.max_qty < self.min_qty:
            raise ValueError("max_qty no puede ser menor que min_qty")

    def applies_to(self, qty: int) -> bool:
        """Retorna True si la regla aplica para la cantidad dada."""
        if qty < self.min_qty:
            return False
        if self.max_qty is not None and qty > self.max_qty:
            return False
        return True


class DiscountEngine:
    """
    Motor de descuentos por volumen.

    Permite registrar reglas de descuento por SKU o por categoría,
    y calcular precios con descuento para una lista de ítems.
    Prioridad: regla por SKU > regla por categoría > sin descuento.
    """

    def __init__(self):
        # Clave: sku o category_name → lista de reglas ordenadas por min_qty
        self._rules_by_sku: dict[str, list[DiscountRule]] = {}
        self._rules_by_category: dict[str, list[DiscountRule]] = {}

    def add_rule_for_sku(self, sku: str, rule: DiscountRule) -> None:
        """Registra una regla de descuento para un SKU específico."""
        self._rules_by_sku.setdefault(sku, [])
        self._rules_by_sku[sku].append(rule)
        self._rules_by_sku[sku].sort(key=lambda r: r.min_qty)

    def add_rule_for_category(self, category: str, rule: DiscountRule) -> None:
        """Registra una regla de descuento para toda una categoría."""
        self._rules_by_category.setdefault(category, [])
        self._rules_by_category[category].append(rule)
        self._rules_by_category[category].sort(key=lambda r: r.min_qty)

    def get_discount_pct(self, sku: str, category: str, qty: int) -> float:
        """
        Retorna el porcentaje de descuento aplicable (0.0 si ninguno aplica).
        Prioriza reglas por SKU sobre reglas por categoría.
        """
        # Buscar regla por SKU (más específica)
        for rule in reversed(self._rules_by_sku.get(sku, [])):
            if rule.applies_to(qty):
                return rule.discount_pct

        # Buscar regla por categoría (más general)
        for rule in reversed(self._rules_by_category.get(category, [])):
            if rule.applies_to(qty):
                return rule.discount_pct

        return 0.0

    def calculate_total(
        self,
        sku: str,
        category: str,
        unit_price: float,
        qty: int
    ) -> dict:
        """
        Calcula el precio total con descuento para un ítem.

        Retorna un diccionario con:
        - subtotal_before: precio sin descuento
        - discount_pct: porcentaje aplicado
        - discount_amount: monto descontado
        - total: precio final
        """
        if qty < 0:
            raise ValueError("La cantidad no puede ser negativa.")
        if unit_price < 0:
            raise ValueError("El precio unitario no puede ser negativo.")

        subtotal_before = unit_price * qty
        discount_pct = self.get_discount_pct(sku, category, qty)
        discount_amount = round(subtotal_before * discount_pct, 2)
        total = round(subtotal_before - discount_amount, 2)

        return {
            "sku": sku,
            "qty": qty,
            "unit_price": unit_price,
            "subtotal_before": round(subtotal_before, 2),
            "discount_pct": discount_pct,
            "discount_amount": discount_amount,
            "total": total,
        }
```

3. Ahora crea el archivo de pruebas de la nueva funcionalidad. Crea `test_discount_engine.py`:

> **Instrucción:** Antes de copiar manualmente, intenta generar estas pruebas con Copilot Chat usando el prompt del Paso 2 o el siguiente prompt de refinamiento:

```text
Basándote en la clase DiscountEngine que acabamos de crear en discount_engine.py,
genera pruebas pytest para estos 4 casos:
1) Caso feliz: descuento del 10% para qty=10 con regla configurada.
2) Sin descuento cuando qty=3 y la regla mínima es qty=5.
3) Límite exacto: qty=5 activa exactamente la regla de min_qty=5.
4) Categoría sin regla definida retorna 0.0 de descuento.
Usa fixtures de pytest. Incluye docstrings en cada test.
```

Si Copilot Chat genera el código, cópialo en `test_discount_engine.py`. Como referencia:

```python
# test_discount_engine.py — Pruebas del sistema de descuentos por volumen
import pytest
from discount_engine import DiscountEngine, DiscountRule


@pytest.fixture
def engine_with_rules():
    """Motor con reglas típicas de negocio para pruebas."""
    engine = DiscountEngine()
    # Reglas por SKU: Laptop tiene descuentos escalonados
    engine.add_rule_for_sku("SKU-001", DiscountRule(min_qty=5, max_qty=9, discount_pct=0.05))
    engine.add_rule_for_sku("SKU-001", DiscountRule(min_qty=10, discount_pct=0.10))
    # Regla por categoría: electronics tiene 3% desde qty=3
    engine.add_rule_for_category("electronics", DiscountRule(min_qty=3, discount_pct=0.03))
    return engine


def test_discount_applied_for_qty_in_range(engine_with_rules):
    """Caso feliz: descuento del 10% para qty=10 en SKU-001."""
    result = engine_with_rules.calculate_total(
        sku="SKU-001", category="electronics", unit_price=1200.0, qty=10
    )
    assert result["discount_pct"] == 0.10
    assert result["total"] == 10800.0
    assert result["discount_amount"] == 1200.0


def test_no_discount_below_minimum_qty(engine_with_rules):
    """Sin descuento cuando qty=3 no alcanza el mínimo de SKU-001 (min=5),
    pero sí aplica la regla de categoría electronics (min=3)."""
    # qty=3: no aplica SKU rule (min=5), pero sí categoría (min=3, 3%)
    result = engine_with_rules.calculate_total(
        sku="SKU-001", category="electronics", unit_price=1200.0, qty=3
    )
    # La regla de categoría aplica (prioridad: SKU > categoría, pero SKU no aplica)
    assert result["discount_pct"] == 0.03

    # Para qty=2: ninguna regla aplica
    result_no_discount = engine_with_rules.calculate_total(
        sku="SKU-001", category="electronics", unit_price=1200.0, qty=2
    )
    assert result_no_discount["discount_pct"] == 0.0
    assert result_no_discount["total"] == 2400.0


def test_exact_boundary_qty_activates_rule(engine_with_rules):
    """Límite exacto: qty=5 debe activar exactamente la regla min_qty=5 (5%)."""
    result = engine_with_rules.calculate_total(
        sku="SKU-001", category="electronics", unit_price=1200.0, qty=5
    )
    assert result["discount_pct"] == 0.05
    assert result["total"] == 5700.0


def test_category_without_rule_returns_zero_discount(engine_with_rules):
    """Categoría sin regla definida retorna 0.0 de descuento."""
    result = engine_with_rules.calculate_total(
        sku="SKU-003", category="furniture", unit_price=350.0, qty=20
    )
    assert result["discount_pct"] == 0.0
    assert result["total"] == 7000.0
```

4. Ejecuta **todas** las pruebas (existentes + nuevas) para verificar que la integración no rompe nada:

```bash
pytest test_inventory.py test_discount_engine.py -v
```

#### Salida esperada

```
collected 7 items

test_inventory.py::test_add_product PASSED
test_inventory.py::test_update_stock_reduces PASSED
test_inventory.py::test_update_stock_insufficient_raises PASSED
test_discount_engine.py::test_discount_applied_for_qty_in_range PASSED
test_discount_engine.py::test_no_discount_below_minimum_qty PASSED
test_discount_engine.py::test_exact_boundary_qty_activates_rule PASSED
test_discount_engine.py::test_category_without_rule_returns_zero_discount PASSED

7 passed in 0.XXs
```

#### Verificación

✅ Las 7 pruebas pasan. ✅ No hay errores de importación entre módulos. ✅ El código existente de `inventory.py` no fue modificado.

---

### Paso 4 — Iterar y refinar con Copilot Chat

**Objetivo:** Aplicar al menos una iteración de refinamiento para mejorar la implementación inicial, identificando una limitación real y solicitando a Copilot Chat una mejora concreta.

#### Instrucciones

1. Selecciona **todo el contenido de `discount_engine.py`** en VS Code (`Ctrl+A`).

2. Con el texto seleccionado, abre Copilot Chat y envía el siguiente prompt de refinamiento:

```text
Revisa la implementación de DiscountEngine seleccionada. Identifica:
1) Al menos 2 limitaciones o áreas de mejora en la implementación actual.
2) Sugiere cómo manejar el caso donde un mismo SKU tiene reglas con rangos
   solapados (ej: regla A: 5-10 uds, regla B: 8-15 uds). ¿Cómo debería
   resolverse la ambigüedad?
3) Propón un método `get_all_rules_summary()` que retorne un resumen legible
   de todas las reglas registradas, útil para auditoría.
Devuelve solo el código del método nuevo y la explicación de las mejoras.
No reescribas toda la clase.
```

3. Analiza la respuesta de Copilot Chat. Evalúa críticamente:
   - ¿La solución propuesta para rangos solapados es razonable para el negocio?
   - ¿El método de auditoría es útil y tiene el formato correcto?

4. Agrega el método `get_all_rules_summary()` sugerido por Copilot Chat a la clase `DiscountEngine` en `discount_engine.py`. Si la sugerencia es razonable, intégrala directamente. Si no lo es, usa esta versión de referencia y documenta en tu diario por qué rechazaste la sugerencia de Copilot:

```python
    def get_all_rules_summary(self) -> list[dict]:
        """
        Retorna un resumen de todas las reglas registradas para auditoría.
        Útil para logs, dashboards de configuración y debugging.
        """
        summary = []

        for sku, rules in self._rules_by_sku.items():
            for rule in rules:
                summary.append({
                    "scope": "sku",
                    "key": sku,
                    "min_qty": rule.min_qty,
                    "max_qty": rule.max_qty if rule.max_qty is not None else "∞",
                    "discount_pct": f"{rule.discount_pct * 100:.1f}%",
                })

        for category, rules in self._rules_by_category.items():
            for rule in rules:
                summary.append({
                    "scope": "category",
                    "key": category,
                    "min_qty": rule.min_qty,
                    "max_qty": rule.max_qty if rule.max_qty is not None else "∞",
                    "discount_pct": f"{rule.discount_pct * 100:.1f}%",
                })

        return summary
```

5. Agrega una prueba rápida para el nuevo método al final de `test_discount_engine.py`:

```python
def test_get_all_rules_summary_returns_all_entries(engine_with_rules):
    """El resumen debe contener todas las reglas registradas (3 en el fixture)."""
    summary = engine_with_rules.get_all_rules_summary()
    assert len(summary) == 3  # 2 reglas SKU-001 + 1 regla categoría electronics
    scopes = {entry["scope"] for entry in summary}
    assert "sku" in scopes
    assert "category" in scopes
```

6. Ejecuta el conjunto completo de pruebas nuevamente:

```bash
pytest test_inventory.py test_discount_engine.py -v --tb=short
```

7. Registra en tu **diario de aprendizaje** las siguientes observaciones:
   - ¿Qué limitaciones identificó Copilot Chat que tú no habías considerado?
   - ¿Aceptaste o rechazaste alguna sugerencia? ¿Por qué?
   - ¿El código generado siguió las convenciones de `inventory.py` (nombres, estilo)?

#### Salida esperada

```
collected 8 items

test_inventory.py::test_add_product PASSED
test_inventory.py::test_update_stock_reduces PASSED
test_inventory.py::test_update_stock_insufficient_raises PASSED
test_discount_engine.py::test_discount_applied_for_qty_in_range PASSED
test_discount_engine.py::test_no_discount_below_minimum_qty PASSED
test_discount_engine.py::test_exact_boundary_qty_activates_rule PASSED
test_discount_engine.py::test_category_without_rule_returns_zero_discount PASSED
test_discount_engine.py::test_get_all_rules_summary_returns_all_entries PASSED

8 passed in 0.XXs
```

#### Verificación

✅ Las 8 pruebas pasan. ✅ El método de auditoría está integrado y probado. ✅ Se registraron observaciones en el diario de aprendizaje.

---

### Paso 5 — Confirmar cambios en Git

**Objetivo:** Guardar el trabajo realizado con un mensaje de commit descriptivo que refleje la trazabilidad entre la necesidad de negocio y el código entregado.

#### Instrucciones

1. Desde la terminal, en el directorio `practica-08/`:

```bash
# Verifica el estado del repositorio
git status
```

2. Agrega todos los archivos nuevos y modificados:

```bash
git add discount_engine.py test_discount_engine.py
```

3. Crea el commit con un mensaje estructurado que incluya referencia a la historia de usuario:

```bash
git commit -m "feat(US-001/US-002): implementa sistema de descuentos por volumen

- Agrega DiscountRule y DiscountEngine para descuentos configurables
- Soporta reglas por SKU y por categoría con prioridad SKU > categoría
- Agrega método get_all_rules_summary() para auditoría de reglas
- 8 pruebas pytest pasan (inventory + discount_engine)
- Generado con GitHub Copilot Chat + revisión manual

Resolves: necesidad de negocio - incrementar ticket promedio mayorista"
```

4. Verifica el log del commit:

```bash
git log --oneline -3
```

#### Salida esperada

```
a1b2c3d feat(US-001/US-002): implementa sistema de descuentos por volumen
[commits anteriores de prácticas previas...]
```

#### Verificación

✅ El commit existe en el log. ✅ El mensaje incluye referencia a las historias de usuario. ✅ No hay archivos sin trackear relacionados con la práctica.

---

## Validación y Pruebas

Ejecuta la siguiente secuencia de validación final para confirmar que todos los entregables de la práctica están completos:

```bash
# 1. Ejecutar suite completa con reporte de cobertura conceptual
pytest test_inventory.py test_discount_engine.py -v --tb=long

# 2. Verificar que no hay errores de sintaxis en los módulos principales
python -c "from inventory import Inventory, Product; from discount_engine import DiscountEngine, DiscountRule; print('Importaciones OK')"

# 3. Smoke test manual: simular un flujo de negocio completo
python -c "
from inventory import Inventory, Product
from discount_engine import DiscountEngine, DiscountRule

# Setup
inv = Inventory()
inv.add_product(Product('SKU-001', 'Laptop', 1200.0, 50, 'electronics'))

engine = DiscountEngine()
engine.add_rule_for_sku('SKU-001', DiscountRule(min_qty=10, discount_pct=0.10))

# Simular compra mayorista
product = inv.get_product('SKU-001')
result = engine.calculate_total(
    sku=product.sku,
    category=product.category,
    unit_price=product.price,
    qty=10
)

print(f'Producto: {product.name}')
print(f'Cantidad: {result[\"qty\"]} unidades')
print(f'Subtotal sin descuento: \${result[\"subtotal_before\"]:,.2f}')
print(f'Descuento aplicado: {result[\"discount_pct\"]*100:.0f}% (\${result[\"discount_amount\"]:,.2f})')
print(f'Total final: \${result[\"total\"]:,.2f}')
print()
print('Resumen de reglas:', engine.get_all_rules_summary())
"
```

#### Salida esperada del smoke test

```
Producto: Laptop
Cantidad: 10 unidades
Subtotal sin descuento: $12,000.00
Descuento aplicado: 10% ($1,200.00)
Total final: $10,800.00

Resumen de reglas: [{'scope': 'sku', 'key': 'SKU-001', 'min_qty': 10, 'max_qty': '∞', 'discount_pct': '10.0%'}]
```

### Lista de verificación de entregables

| Entregable | Criterio de aceptación | ¿Completado? |
|---|---|---|
| `discount_engine.py` | Contiene `DiscountRule`, `DiscountEngine` y `get_all_rules_summary()` | ☐ |
| `test_discount_engine.py` | 5 pruebas pytest (4 originales + 1 de auditoría) | ☐ |
| Suite completa | 8 pruebas pasan sin errores | ☐ |
| Commit en Git | Mensaje incluye referencia a US-001/US-002 | ☐ |
| Diario de aprendizaje | Registra observaciones del refinamiento con Copilot Chat | ☐ |
| Prompt de negocio→técnico | Aplicado con los 5 elementos del patrón de la lección 3.1 | ☐ |

---

## Solución de Problemas

### Problema 1: Copilot Chat genera código incompatible con las clases existentes

**Síntomas:**
- Al ejecutar `pytest`, aparece `ImportError`, `AttributeError` o `TypeError` en `test_discount_engine.py`.
- El código generado referencia métodos o atributos que no existen en `inventory.py` (por ejemplo: `product.id` en lugar de `product.sku`).
- La clase generada hereda de `Inventory` cuando debería ser independiente.

**Causa probable:**
Copilot Chat no tuvo suficiente contexto del código existente al momento de generar la respuesta. Esto ocurre cuando `inventory.py` no estaba abierto y activo en el editor, o cuando el prompt no especificó explícitamente los nombres de clases y atributos existentes.

**Solución:**
1. Asegúrate de que `inventory.py` está **abierto y visible** en VS Code antes de enviar el prompt.
2. Agrega al inicio del prompt una referencia explícita: `"El archivo inventory.py tiene las clases Product (atributos: sku, name, price, stock, category) e Inventory (métodos: add_product, get_product, update_stock, list_products)."`.
3. Si el código ya fue generado con errores, selecciónalo en el editor y usa: `"Corrige este código para que sea compatible con las clases Product e Inventory tal como están definidas en inventory.py"`.
4. Ejecuta `python -c "from discount_engine import DiscountEngine"` para aislar errores de importación antes de correr pytest.

---

### Problema 2: Las pruebas de límites de rango fallan con resultados inesperados

**Síntomas:**
- `test_exact_boundary_qty_activates_rule` falla con `AssertionError`: el descuento retornado es `0.0` cuando debería ser `0.05`.
- `test_no_discount_below_minimum_qty` falla porque aplica un descuento cuando no debería, o viceversa.
- El método `get_discount_pct` retorna el porcentaje de una regla incorrecta cuando hay múltiples reglas para el mismo SKU.

**Causa probable:**
La lógica de iteración sobre las reglas ordenadas tiene un error en la dirección de la búsqueda (`reversed` vs. orden directo). Cuando hay múltiples reglas para un SKU, el algoritmo puede encontrar primero la regla de mayor `min_qty` (que no aplica para cantidades intermedias) y nunca evaluar la regla correcta. También puede ocurrir si `DiscountRule.applies_to()` tiene un error en la comparación de `max_qty`.

**Solución:**
1. Verifica la lógica de `applies_to()` manualmente en la terminal:
```python
python -c "
from discount_engine import DiscountRule
r = DiscountRule(min_qty=5, max_qty=9, discount_pct=0.05)
print('qty=5:', r.applies_to(5))   # debe ser True
print('qty=9:', r.applies_to(9))   # debe ser True
print('qty=4:', r.applies_to(4))   # debe ser False
print('qty=10:', r.applies_to(10)) # debe ser False
"
```
2. Si hay errores, pide a Copilot Chat: `"El método applies_to() retorna resultados incorrectos en los límites. Revisa la condición de max_qty: ¿debería ser > o >= ?"`.
3. Para el problema de múltiples reglas, verifica que la lista esté ordenada por `min_qty` ascendente y que la iteración con `reversed()` recorra desde el `min_qty` más alto al más bajo, seleccionando la primera regla que aplique (la más específica para la cantidad dada).
4. Usa `pytest -v --tb=long` para ver el valor exacto retornado vs. el esperado en cada assertion.

---

## Limpieza

Al finalizar la práctica, ejecuta los siguientes pasos para dejar el entorno ordenado:

```bash
# 1. Desactiva el entorno virtual
deactivate

# 2. Verifica que todos los cambios están commiteados (no debe haber archivos pendientes)
git status
# Salida esperada: "nothing to commit, working tree clean"

# 3. (Opcional) Lista los archivos generados en esta práctica para confirmar
ls -la practica-08/
# Debe mostrar: inventory.py, test_inventory.py, discount_engine.py, test_discount_engine.py
```

> **Importante — No elimines los archivos de esta práctica.** Los archivos `discount_engine.py` y `test_discount_engine.py` son necesarios como insumo para la **Práctica 9**, que tiene dependencia directa con el código generado aquí. Conserva también las notas en tu diario de aprendizaje.

---

## Resumen

En esta práctica aplicaste el flujo completo de **resolución de necesidades de negocio con Copilot Chat**:

| Fase | Lo que hiciste |
|---|---|
| **Análisis** | Identificaste la necesidad de negocio (descuentos por volumen) y la tradujiste en restricciones, datos y métricas de éxito. |
| **Diseño con IA** | Aplicaste el patrón de prompt de 5 elementos para obtener historias de usuario, criterios Gherkin, diseño de clases y pruebas. |
| **Implementación** | Integraste `DiscountEngine` y `DiscountRule` con el inventario existente sin romper el código previo. |
| **Refinamiento** | Iteraste con Copilot Chat para identificar limitaciones y agregar funcionalidad de auditoría. |
| **Validación** | Ejecutaste 8 pruebas pytest y un smoke test de flujo completo de negocio. |
| **Trazabilidad** | Commiteaste con mensajes que referencian las historias de usuario (US-001/US-002). |

### Puntos clave para recordar

- **El contexto es crítico:** Copilot Chat genera código de mayor calidad cuando el archivo relevante está abierto y los nombres de clases/atributos se mencionan explícitamente en el prompt.
- **El patrón de prompt estructura la conversación:** Contexto → Restricciones → Datos → Definición de éxito → Formato de salida produce respuestas más completas y alineadas al negocio que prompts libres.
- **La revisión humana es obligatoria:** Copilot Chat puede generar código funcionalmente correcto pero con supuestos implícitos (como la prioridad SKU > categoría) que deben ser validados contra las reglas reales del negocio.
- **La trazabilidad es un hábito profesional:** Vincular commits, pruebas y código a IDs de historias de usuario facilita el mantenimiento y la comunicación con stakeholders no técnicos.

### Recursos adicionales

- [Documentación oficial de GitHub Copilot Chat](https://docs.github.com/es/copilot/copilot-chat/using-github-copilot-chat)
- [Referencia de Gherkin — Cucumber](https://cucumber.io/docs/gherkin/reference/)
- [Guía de pytest — Fixtures y parametrización](https://docs.pytest.org/en/stable/how-to/fixtures.html)
- [Historias de usuario — Agile Alliance](https://www.agilealliance.org/glossary/user-stories/)
- [Buenas prácticas de diseño de APIs REST — Microsoft](https://learn.microsoft.com/es-es/azure/architecture/best-practices/api-design)
- [Python dataclasses — Documentación oficial](https://docs.python.org/3/library/dataclasses.html)

---
*Lab 03-00-02 | Módulo 3: Resolución de Necesidades de Negocio | GitHub Copilot Chat para Desarrolladores*

---

# Realiza un caso de estudio sobre un proyecto en donde puedas utilizar Copilot Chat, analizando sus aportes y resultados.

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

---
