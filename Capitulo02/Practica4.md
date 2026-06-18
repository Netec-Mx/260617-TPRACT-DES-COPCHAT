# Práctica 4: Crea una función en un lenguaje de programación de tu elección utilizando Copilot Chat para autocompletar el código.

## Metadatos

| Campo            | Detalle                                      |
|------------------|----------------------------------------------|
| **Duración**     | 10 minutos (hasta 20 min en modo autónomo)   |
| **Complejidad**  | Fácil                                        |
| **Nivel Bloom**  | Aplicar (Apply)                              |
| **Módulo**       | 2 — Copilot Chat como Herramienta de Referencia y Autocompletado |
| **Práctica**     | 4 de 10                                      |

---

## Descripción General

En esta práctica aplicarás las capacidades de **autocompletado contextual** de GitHub Copilot Chat para crear al menos dos funciones con lógica de negocio real en el lenguaje de tu preferencia. Observarás cómo Copilot Chat infiere la intención del programador a partir del nombre de la función, los comentarios previos y el contexto del archivo, y evaluarás la precisión de sus sugerencias comparándolas con buenas prácticas. Al finalizar, habrás documentado qué sugirió Copilot Chat en cada caso y verificado el comportamiento de las funciones con casos de prueba concretos.

---

## Objetivos de Aprendizaje

Al completar esta práctica serás capaz de:

- [ ] Utilizar las capacidades de autocompletado de Copilot Chat para generar funciones completas a partir de una firma o un comentario descriptivo.
- [ ] Comprender cómo el contexto del archivo (imports, comentarios, otras funciones) influye en la calidad y relevancia de las sugerencias de autocompletado.
- [ ] Evaluar la precisión y utilidad de las sugerencias de Copilot Chat en un escenario de desarrollo real con lógica de negocio moderadamente compleja.
- [ ] Documentar y reflexionar sobre el proceso de aceptación, modificación o rechazo de sugerencias generadas por IA.

---

## Prerrequisitos

### Conocimiento previo

| Requisito | Descripción |
|-----------|-------------|
| Prácticas anteriores | Haber completado las Prácticas 1, 2 y 3 del Módulo 1 |
| Funciones | Conocimiento básico de cómo declarar y llamar funciones en al menos un lenguaje de programación |
| VS Code | Saber abrir, editar y guardar archivos en Visual Studio Code |
| Copilot Chat | Haber activado la extensión y verificado que la suscripción a GitHub Copilot está activa |

### Acceso y cuentas

| Recurso | Estado requerido |
|---------|-----------------|
| Cuenta GitHub con Copilot activo | ✅ Activo y verificado |
| Extensión GitHub Copilot Chat en VS Code | ✅ Instalada y autenticada |
| Conexión a internet | ✅ Estable (mínimo 10 Mbps) |

> **⚠️ Nota importante:** Si tu suscripción a Copilot no está activa, el autocompletado no funcionará. Verifica en [github.com/settings/copilot](https://github.com/settings/copilot) antes de comenzar.

---

## Entorno de Laboratorio

### Hardware mínimo recomendado

| Componente | Mínimo | Recomendado |
|------------|--------|-------------|
| RAM | 8 GB | 16 GB |
| Procesador | Intel Core i5 / AMD Ryzen 5 (64-bit) | i7 / Ryzen 7 |
| Espacio en disco | 2 GB libres | 10 GB libres |
| Resolución de pantalla | 1280×768 | 1920×1080 |

### Software requerido

| Herramienta | Versión mínima | Verificación |
|-------------|----------------|--------------|
| Visual Studio Code | 1.90 | `code --version` |
| Extensión GitHub Copilot Chat | Última disponible | Panel de extensiones VS Code |
| Python | 3.10+ | `python --version` |
| Node.js (opcional) | 20 LTS | `node --version` |
| Git | 2.40+ | `git --version` |

### Verificación rápida del entorno

Abre una terminal y ejecuta los siguientes comandos para confirmar que el entorno está listo:

```bash
# Verificar Python
python --version
# Salida esperada: Python 3.10.x o superior

# Verificar VS Code
code --version
# Salida esperada: 1.90.x o superior

# Verificar Git
git --version
# Salida esperada: git version 2.40.x o superior
```

### Configuración inicial del proyecto

```bash
# Crear el directorio de trabajo para esta práctica
mkdir practica-04-autocompletado
cd practica-04-autocompletado

# Inicializar repositorio Git (buena práctica para rastrear cambios)
git init

# Crear el archivo principal (Python como lenguaje sugerido)
touch funciones_negocio.py

# Abrir el proyecto en VS Code
code .
```

> **🌐 Lenguaje alternativo:** Si prefieres JavaScript, crea `funciones_negocio.js`; para TypeScript, `funciones_negocio.ts`; para Java, `FuncionesNegocio.java`. Los pasos son equivalentes; los ejemplos de esta práctica usan Python como referencia principal.

---

## Pasos del Laboratorio

---

### Paso 1: Preparar el archivo con contexto inicial

**Objetivo:** Establecer el contexto del archivo (imports, comentarios de módulo y constantes) para que Copilot Chat tenga información suficiente para generar sugerencias relevantes y precisas.

#### Instrucciones

1. Abre el archivo `funciones_negocio.py` en VS Code (debe estar vacío).

2. Escribe **manualmente** el siguiente bloque de contexto inicial. No copies y pegues; escríbelo tú mismo para que Copilot Chat pueda observar tu intención en tiempo real:

```python
"""
Módulo: funciones_negocio.py
Descripción: Funciones de lógica de negocio para una tienda en línea.
Incluye cálculo de precios con descuento y validación de pedidos.
Autor: [Tu nombre]
Fecha: [Fecha actual]
"""

# Constantes de negocio
DESCUENTO_CLIENTE_VIP = 0.20      # 20% de descuento para clientes VIP
DESCUENTO_TEMPORADA = 0.10        # 10% de descuento por temporada
PRECIO_MINIMO = 0.01              # Precio mínimo permitido después del descuento
CANTIDAD_MAXIMA_PEDIDO = 100      # Cantidad máxima de unidades por pedido
```

3. Guarda el archivo con `Ctrl+S` (Windows/Linux) o `Cmd+S` (macOS).

4. Observa que VS Code muestra el archivo activo en la barra de título. Copilot Chat ahora tiene acceso a este contexto.

#### Salida esperada

El archivo debe verse así en VS Code, sin errores de sintaxis (sin subrayados rojos):

```
funciones_negocio.py  ×
─────────────────────────────────────────
"""
Módulo: funciones_negocio.py
...
"""
# Constantes de negocio
DESCUENTO_CLIENTE_VIP = 0.20
...
```

#### Verificación

- [ ] El archivo está guardado (sin el punto de cambios pendientes `●` en la pestaña).
- [ ] No hay errores de sintaxis visibles en el editor.
- [ ] Las constantes están definidas con nombres descriptivos en mayúsculas.

> **💡 Por qué importa el contexto:** Como aprendiste en la lección 2.1, Copilot Chat utiliza el archivo activo y la selección como **contexto primario**. Los comentarios descriptivos y las constantes con nombres claros le indican al modelo el dominio del problema, lo que mejora significativamente la calidad del autocompletado.

---

### Paso 2: Crear la primera función — Cálculo de precio con descuento

**Objetivo:** Utilizar el autocompletado de Copilot Chat para generar una función con lógica de negocio moderadamente compleja, observando cómo infiere las reglas a partir del nombre y el contexto.

#### Instrucciones

1. Posiciona el cursor al final del archivo (después de las constantes), presiona `Enter` dos veces para dejar una línea en blanco, y escribe **solo la firma de la función con su docstring inicial**:

```python
def calcular_precio_final(precio_base: float, es_cliente_vip: bool, es_temporada_descuento: bool) -> float:
    """
    Calcula el precio final de un producto aplicando reglas de descuento de negocio.
```

2. Después de escribir la línea del docstring, presiona `Enter`. Copilot Chat debería comenzar a sugerir el resto del docstring y la implementación. Observa el texto gris semitransparente que aparece (sugerencia inline).

3. **Antes de aceptar**, lee cuidadosamente la sugerencia completa. Puedes ver la sugerencia completa con `Alt+]` (siguiente sugerencia) o `Alt+[` (sugerencia anterior) si hay múltiples opciones.

4. Si la sugerencia es razonable, acéptala presionando `Tab`. Si no, escribe la siguiente línea del docstring para guiar mejor a Copilot:

```python
    Args:
        precio_base: Precio original del producto (debe ser mayor que PRECIO_MINIMO).
        es_cliente_vip: True si el cliente tiene membresía VIP.
        es_temporada_descuento: True si hay promoción de temporada activa.
    Returns:
        Precio final después de aplicar todos los descuentos aplicables.
    Raises:
        ValueError: Si precio_base es menor o igual a cero.
    """
```

5. Presiona `Enter` después del cierre del docstring (`"""`). Copilot Chat debería sugerir el cuerpo completo de la función. Acepta la sugerencia con `Tab` o modifícala según sea necesario.

6. Si Copilot no genera automáticamente una implementación completa, puedes escribir el comentario guía `# Validar precio base` y presionar `Enter` para provocar una nueva sugerencia.

7. **Documenta en tu diario de aprendizaje:** ¿Qué sugirió Copilot Chat exactamente? ¿Aplicó las constantes definidas al inicio del archivo? ¿La lógica de negocio fue correcta?

#### Ejemplo de implementación que Copilot Chat podría generar (referencia)

La función generada debería ser similar a esta. Si Copilot generó algo diferente, compáralo con esta referencia:

```python
def calcular_precio_final(precio_base: float, es_cliente_vip: bool, es_temporada_descuento: bool) -> float:
    """
    Calcula el precio final de un producto aplicando reglas de descuento de negocio.

    Args:
        precio_base: Precio original del producto (debe ser mayor que PRECIO_MINIMO).
        es_cliente_vip: True si el cliente tiene membresía VIP.
        es_temporada_descuento: True si hay promoción de temporada activa.
    Returns:
        Precio final después de aplicar todos los descuentos aplicables.
    Raises:
        ValueError: Si precio_base es menor o igual a cero.
    """
    if precio_base <= 0:
        raise ValueError(f"El precio base debe ser mayor que cero. Recibido: {precio_base}")

    descuento_total = 0.0

    if es_cliente_vip:
        descuento_total += DESCUENTO_CLIENTE_VIP

    if es_temporada_descuento:
        descuento_total += DESCUENTO_TEMPORADA

    precio_final = precio_base * (1 - descuento_total)

    # Garantizar que el precio nunca sea menor al mínimo permitido
    return max(precio_final, PRECIO_MINIMO)
```

#### Salida esperada

- La función completa aparece en el archivo sin errores de sintaxis.
- La función utiliza las constantes definidas en el Paso 1 (`DESCUENTO_CLIENTE_VIP`, `DESCUENTO_TEMPORADA`, `PRECIO_MINIMO`).
- Incluye validación de entrada y manejo del caso borde (precio mínimo).

#### Verificación

- [ ] La función está definida correctamente (sin errores de indentación ni sintaxis).
- [ ] Copilot Chat utilizó al menos una de las constantes del archivo en su sugerencia.
- [ ] Has documentado en tu diario qué sugirió Copilot y si fue necesario modificarlo.

---

### Paso 3: Crear la segunda función — Validación de pedido

**Objetivo:** Crear una segunda función usando autocompletado, esta vez observando cómo el contexto de la primera función influye en las nuevas sugerencias.

#### Instrucciones

1. Deja dos líneas en blanco después de la primera función y escribe el siguiente comentario descriptivo **antes** de la firma:

```python
# Valida que un pedido sea procesable según las reglas de negocio de la tienda
```

2. Inmediatamente después del comentario, en la siguiente línea, escribe solo el nombre y los parámetros de la función:

```python
def validar_pedido(producto_id: str, cantidad: int, precio_unitario: float) -> dict:
```

3. Presiona `Enter` y observa la sugerencia de Copilot Chat. Esta vez, el modelo tiene más contexto: conoce las constantes, la primera función y el comentario descriptivo.

4. Acepta o modifica la sugerencia. Si Copilot no genera el docstring automáticamente, escríbelo tú:

```python
    """
    Valida si un pedido puede ser procesado según las reglas de negocio.
    Retorna un diccionario con el resultado de la validación.
    """
```

5. Continúa aceptando sugerencias de Copilot para el cuerpo de la función. Presta atención a si Copilot utiliza `CANTIDAD_MAXIMA_PEDIDO` del contexto inicial.

6. **Documenta en tu diario:** ¿Las sugerencias de la segunda función fueron más relevantes que las de la primera? ¿Por qué crees que ocurre esto?

#### Ejemplo de implementación de referencia

```python
# Valida que un pedido sea procesable según las reglas de negocio de la tienda
def validar_pedido(producto_id: str, cantidad: int, precio_unitario: float) -> dict:
    """
    Valida si un pedido puede ser procesado según las reglas de negocio.
    Retorna un diccionario con el resultado de la validación.

    Args:
        producto_id: Identificador único del producto (no puede estar vacío).
        cantidad: Número de unidades solicitadas (entre 1 y CANTIDAD_MAXIMA_PEDIDO).
        precio_unitario: Precio por unidad (debe ser mayor que PRECIO_MINIMO).
    Returns:
        dict con claves 'valido' (bool), 'mensaje' (str) y 'total' (float o None).
    """
    # Validar producto_id
    if not producto_id or not producto_id.strip():
        return {"valido": False, "mensaje": "El ID del producto no puede estar vacío.", "total": None}

    # Validar cantidad
    if cantidad <= 0:
        return {"valido": False, "mensaje": "La cantidad debe ser mayor que cero.", "total": None}

    if cantidad > CANTIDAD_MAXIMA_PEDIDO:
        return {
            "valido": False,
            "mensaje": f"La cantidad {cantidad} supera el máximo permitido de {CANTIDAD_MAXIMA_PEDIDO} unidades.",
            "total": None
        }

    # Validar precio unitario
    if precio_unitario <= PRECIO_MINIMO:
        return {"valido": False, "mensaje": f"El precio unitario debe ser mayor que {PRECIO_MINIMO}.", "total": None}

    total = cantidad * precio_unitario
    return {
        "valido": True,
        "mensaje": "Pedido válido y listo para procesar.",
        "total": round(total, 2)
    }
```

#### Salida esperada

- La segunda función está definida correctamente.
- Utiliza `CANTIDAD_MAXIMA_PEDIDO` y/o `PRECIO_MINIMO` del contexto del archivo.
- Retorna un diccionario estructurado con información de validación.

#### Verificación

- [ ] La segunda función está completa y sin errores de sintaxis.
- [ ] Has comparado si las sugerencias de la segunda función fueron más contextuales que las de la primera.
- [ ] Tienes anotado en tu diario las diferencias observadas entre ambas experiencias de autocompletado.

---

### Paso 4: Escribir casos de prueba con ayuda de Copilot Chat

**Objetivo:** Usar el comando `/tests` de Copilot Chat para generar casos de prueba y verificar el comportamiento de las funciones creadas.

#### Instrucciones

1. Crea un nuevo archivo de pruebas en el mismo directorio:

```bash
touch test_funciones_negocio.py
```

2. Abre `test_funciones_negocio.py` en VS Code.

3. Abre el panel de Copilot Chat con `Ctrl+Alt+I` (Windows/Linux) o `Cmd+Alt+I` (macOS), o haz clic en el ícono de Copilot Chat en la barra lateral izquierda.

4. En el panel de chat, escribe el siguiente prompt:

```
/tests Genera casos de prueba para las funciones calcular_precio_final y validar_pedido 
definidas en funciones_negocio.py. Incluye al menos 2 casos por función: 
uno con entradas válidas y uno con entradas inválidas o casos borde. 
Usa el módulo unittest de Python estándar.
```

5. Observa la respuesta de Copilot Chat. Copia el código sugerido en `test_funciones_negocio.py`.

6. Asegúrate de que el archivo de pruebas incluya el import correcto al inicio:

```python
import unittest
from funciones_negocio import calcular_precio_final, validar_pedido
```

7. Si Copilot generó los imports automáticamente, verifica que sean correctos.

#### Ejemplo de casos de prueba de referencia

Si Copilot Chat no genera pruebas suficientes, complementa con las siguientes:

```python
import unittest
from funciones_negocio import calcular_precio_final, validar_pedido


class TestCalcularPrecioFinal(unittest.TestCase):

    def test_precio_sin_descuentos(self):
        """Cliente normal, sin temporada: precio base sin cambios."""
        resultado = calcular_precio_final(100.0, False, False)
        self.assertAlmostEqual(resultado, 100.0)

    def test_precio_cliente_vip(self):
        """Cliente VIP recibe 20% de descuento."""
        resultado = calcular_precio_final(100.0, True, False)
        self.assertAlmostEqual(resultado, 80.0)

    def test_precio_temporada_descuento(self):
        """Temporada de descuento aplica 10% adicional."""
        resultado = calcular_precio_final(100.0, False, True)
        self.assertAlmostEqual(resultado, 90.0)

    def test_precio_vip_y_temporada(self):
        """VIP + temporada: descuento acumulado del 30%."""
        resultado = calcular_precio_final(100.0, True, True)
        self.assertAlmostEqual(resultado, 70.0)

    def test_precio_invalido_cero(self):
        """Precio base de cero debe lanzar ValueError."""
        with self.assertRaises(ValueError):
            calcular_precio_final(0.0, False, False)

    def test_precio_invalido_negativo(self):
        """Precio base negativo debe lanzar ValueError."""
        with self.assertRaises(ValueError):
            calcular_precio_final(-50.0, True, True)


class TestValidarPedido(unittest.TestCase):

    def test_pedido_valido(self):
        """Pedido con datos correctos debe ser válido."""
        resultado = validar_pedido("PROD-001", 5, 25.0)
        self.assertTrue(resultado["valido"])
        self.assertAlmostEqual(resultado["total"], 125.0)

    def test_pedido_cantidad_maxima(self):
        """Cantidad igual al máximo debe ser válida."""
        resultado = validar_pedido("PROD-002", 100, 10.0)
        self.assertTrue(resultado["valido"])

    def test_pedido_cantidad_excede_maximo(self):
        """Cantidad mayor al máximo debe ser inválida."""
        resultado = validar_pedido("PROD-003", 101, 10.0)
        self.assertFalse(resultado["valido"])
        self.assertIsNone(resultado["total"])

    def test_pedido_producto_id_vacio(self):
        """ID de producto vacío debe ser inválido."""
        resultado = validar_pedido("", 5, 25.0)
        self.assertFalse(resultado["valido"])

    def test_pedido_cantidad_cero(self):
        """Cantidad de cero unidades debe ser inválida."""
        resultado = validar_pedido("PROD-004", 0, 25.0)
        self.assertFalse(resultado["valido"])


if __name__ == "__main__":
    unittest.main()
```

8. Guarda el archivo con `Ctrl+S`.

#### Salida esperada

- El archivo `test_funciones_negocio.py` contiene al menos 4 casos de prueba (2 por función).
- Los imports son correctos y apuntan al módulo creado en el Paso 1.

#### Verificación

- [ ] El archivo de pruebas está guardado sin errores de sintaxis.
- [ ] Hay al menos 2 casos de prueba para `calcular_precio_final`.
- [ ] Hay al menos 2 casos de prueba para `validar_pedido`.
- [ ] Has documentado qué generó Copilot Chat con `/tests` vs. lo que escribiste manualmente.

---

### Paso 5: Ejecutar las pruebas y analizar resultados

**Objetivo:** Verificar que las funciones generadas con autocompletado funcionan correctamente ejecutando los casos de prueba.

#### Instrucciones

1. Abre la terminal integrada de VS Code con `` Ctrl+` `` y navega al directorio del proyecto si no estás en él:

```bash
cd practica-04-autocompletado
```

2. Ejecuta las pruebas con el siguiente comando:

```bash
python -m unittest test_funciones_negocio.py -v
```

3. Observa la salida. Cada prueba debe mostrar `OK` o `FAIL`/`ERROR`.

4. Si alguna prueba falla, identifica el motivo. Puede ser que:
   - La función generada por Copilot tiene un error lógico.
   - La prueba asume un comportamiento diferente al implementado.
   - Hay un error de importación.

5. Si hay fallos, abre el panel de Copilot Chat y usa el siguiente prompt para obtener ayuda de diagnóstico:

```
Tengo este error al ejecutar mis pruebas unitarias: [pega aquí el mensaje de error]
La función afectada es [nombre de la función]. 
Explícame la causa probable y sugiere una corrección.
```

6. Aplica las correcciones sugeridas y vuelve a ejecutar las pruebas hasta que todas pasen.

#### Salida esperada

```bash
python -m unittest test_funciones_negocio.py -v
```

```
test_pedido_cantidad_cero (test_funciones_negocio.TestValidarPedido) ... ok
test_pedido_cantidad_excede_maximo (test_funciones_negocio.TestValidarPedido) ... ok
test_pedido_cantidad_maxima (test_funciones_negocio.TestValidarPedido) ... ok
test_pedido_producto_id_vacio (test_funciones_negocio.TestValidarPedido) ... ok
test_pedido_valido (test_funciones_negocio.TestValidarPedido) ... ok
test_precio_cliente_vip (test_funciones_negocio.TestCalcularPrecioFinal) ... ok
test_precio_invalido_cero (test_funciones_negocio.TestCalcularPrecioFinal) ... ok
test_precio_invalido_negativo (test_funciones_negocio.TestCalcularPrecioFinal) ... ok
test_precio_sin_descuentos (test_funciones_negocio.TestCalcularPrecioFinal) ... ok
test_precio_temporada_descuento (test_funciones_negocio.TestCalcularPrecioFinal) ... ok
test_precio_vip_y_temporada (test_funciones_negocio.TestCalcularPrecioFinal) ... ok

----------------------------------------------------------------------
Ran 11 tests in 0.002s

OK
```

#### Verificación

- [ ] Todas las pruebas pasan (`OK`).
- [ ] No hay errores de importación (`ImportError` o `ModuleNotFoundError`).
- [ ] La salida muestra el número total de pruebas ejecutadas.

---

### Paso 6: Usar Copilot Chat como referencia para evaluar el código generado

**Objetivo:** Aplicar Copilot Chat como herramienta de referencia (según la lección 2.1) para evaluar críticamente el código generado por autocompletado e identificar posibles mejoras.

#### Instrucciones

1. Selecciona **toda la función `calcular_precio_final`** en el editor (incluyendo el docstring).

2. Con el código seleccionado, abre el panel de Copilot Chat y escribe el siguiente prompt:

```
/explain Evalúa esta función considerando:
1. ¿Sigue buenas prácticas de Python (PEP 8, type hints, manejo de errores)?
2. ¿Hay casos borde no contemplados?
3. ¿La lógica de negocio es correcta para un sistema de descuentos?
4. Señala pitfalls frecuentes en funciones de cálculo de precios.
Dame la respuesta en formato de lista con 4 viñetas máximo.
```

3. Lee la respuesta de Copilot Chat. Anota en tu diario de aprendizaje:
   - ¿Identificó algún problema que no habías notado?
   - ¿Las sugerencias son válidas o son genéricas?

4. Ahora selecciona la función `validar_pedido` y usa este segundo prompt:

```
Basándote estrictamente en el código seleccionado, responde:
- ¿El tipo de retorno (dict) es la mejor opción para una función de validación en Python moderno?
- ¿Qué alternativa más robusta podrías sugerir (por ejemplo, dataclass o TypedDict)?
- Dame un ejemplo mínimo de la alternativa sugerida.
```

5. Evalúa si la sugerencia de Copilot Chat es aplicable a tu contexto y anota tu conclusión.

6. **Opcional (si tienes tiempo):** Implementa una de las mejoras sugeridas por Copilot Chat y vuelve a ejecutar las pruebas para confirmar que siguen pasando.

#### Salida esperada

Copilot Chat debería responder con observaciones específicas al código seleccionado, no respuestas genéricas. Por ejemplo, podría mencionar:

- El uso de `round()` para evitar errores de punto flotante en precios.
- Considerar el uso de `Decimal` para cálculos monetarios precisos.
- Sugerir `TypedDict` o `dataclass` para el retorno de `validar_pedido`.
- Señalar que la acumulación de descuentos podría necesitar un tope máximo de descuento.

#### Verificación

- [ ] Has enviado al menos 2 prompts de evaluación a Copilot Chat con código seleccionado.
- [ ] Has documentado las observaciones de Copilot Chat en tu diario.
- [ ] Has identificado al menos una fortaleza y una área de mejora en el código generado.

---

## Validación y Pruebas Finales

Una vez completados todos los pasos, realiza esta validación integral:

### Lista de verificación final

```bash
# 1. Verificar que ambos archivos existen
ls -la practica-04-autocompletado/
# Salida esperada: funciones_negocio.py y test_funciones_negocio.py

# 2. Ejecutar todas las pruebas una última vez
cd practica-04-autocompletado
python -m unittest test_funciones_negocio.py -v

# 3. Verificar que no hay errores de sintaxis en el módulo principal
python -c "import funciones_negocio; print('Módulo importado correctamente')"

# 4. Prueba rápida en la terminal interactiva (opcional)
python -c "
from funciones_negocio import calcular_precio_final, validar_pedido

# Prueba 1: Cliente VIP en temporada
precio = calcular_precio_final(200.0, True, True)
print(f'Precio VIP + temporada: \${precio:.2f}')  # Esperado: 140.00

# Prueba 2: Pedido válido
pedido = validar_pedido('LAPTOP-01', 3, 999.99)
print(f'Pedido válido: {pedido[\"valido\"]}, Total: \${pedido[\"total\"]:.2f}')  # Esperado: True, 2999.97

# Prueba 3: Pedido inválido
pedido_inv = validar_pedido('', 0, -5.0)
print(f'Pedido inválido: {pedido_inv[\"valido\"]}')  # Esperado: False
"
```

### Criterios de éxito

| Criterio | Estado esperado |
|----------|----------------|
| Todas las pruebas unitarias pasan | ✅ `Ran N tests... OK` |
| Ambas funciones usan constantes del módulo | ✅ Verificado en el código |
| Copilot Chat fue consultado al menos 3 veces | ✅ Documentado en el diario |
| El diario de aprendizaje tiene notas de esta práctica | ✅ Completado |

---

## Solución de Problemas

### Problema 1: Las sugerencias de Copilot Chat no aparecen o aparecen vacías

**Síntoma:** Al escribir la firma de la función y presionar `Enter`, no aparece ninguna sugerencia gris de autocompletado. El editor no muestra el texto semitransparente característico de Copilot.

**Causa probable:** La extensión de GitHub Copilot no está autenticada o la suscripción venció. También puede ocurrir si el autocompletado inline está desactivado en la configuración de VS Code, o si hay un problema de conectividad con los servidores de GitHub.

**Solución:**

1. Verifica el estado de la extensión en la barra de estado inferior de VS Code. Busca el ícono de Copilot (un círculo con punto); si tiene una `X` o una advertencia, haz clic en él.

2. Comprueba la autenticación:
   - Abre la paleta de comandos: `Ctrl+Shift+P` (Windows/Linux) o `Cmd+Shift+P` (macOS).
   - Escribe `GitHub Copilot: Sign In` y selecciona la opción.
   - Sigue el flujo de autenticación en el navegador.

3. Verifica que el autocompletado inline esté habilitado:
   - Ve a `File > Preferences > Settings` (o `Ctrl+,`).
   - Busca `editor.inlineSuggest.enabled` y asegúrate de que esté en `true`.

4. Prueba la conectividad:
   ```bash
   # Verificar acceso a GitHub
   curl -I https://github.com
   # Debe retornar HTTP/2 200 o HTTP/1.1 200
   ```

5. Si el problema persiste, reinicia VS Code completamente y vuelve a intentarlo.

---

### Problema 2: Error `ModuleNotFoundError` al ejecutar las pruebas

**Síntoma:** Al ejecutar `python -m unittest test_funciones_negocio.py -v`, aparece el siguiente error:

```
ModuleNotFoundError: No module named 'funciones_negocio'
```

**Causa probable:** El archivo `test_funciones_negocio.py` está buscando el módulo `funciones_negocio` pero Python no puede encontrarlo. Esto ocurre cuando la terminal no está posicionada en el directorio correcto (`practica-04-autocompletado`), o cuando los archivos tienen nombres con errores tipográficos.

**Solución:**

1. Verifica que estás en el directorio correcto:
   ```bash
   pwd
   # Debe mostrar: .../practica-04-autocompletado
   
   ls *.py
   # Debe mostrar: funciones_negocio.py  test_funciones_negocio.py
   ```

2. Si no estás en el directorio correcto, navega a él:
   ```bash
   cd practica-04-autocompletado
   python -m unittest test_funciones_negocio.py -v
   ```

3. Verifica que el nombre del archivo es exactamente `funciones_negocio.py` (sin espacios, sin mayúsculas):
   ```bash
   ls -la | grep funciones
   ```

4. Si el nombre del archivo en el import no coincide, edita `test_funciones_negocio.py` y corrige la línea de import para que coincida exactamente con el nombre del archivo:
   ```python
   # Asegúrate de que esta línea coincida con el nombre real del archivo
   from funciones_negocio import calcular_precio_final, validar_pedido
   ```

5. Como alternativa, ejecuta las pruebas especificando el directorio explícitamente:
   ```bash
   python -m pytest test_funciones_negocio.py -v
   # (requiere pytest: pip install pytest)
   ```

---

## Limpieza

Al finalizar la práctica, realiza las siguientes acciones para mantener tu entorno organizado:

### Guardar el trabajo

```bash
# Asegúrate de estar en el directorio del proyecto
cd practica-04-autocompletado

# Hacer commit del trabajo realizado (importante para prácticas futuras)
git add funciones_negocio.py test_funciones_negocio.py
git commit -m "Practica 04: Funciones de negocio creadas con autocompletado de Copilot Chat"

# Verificar el estado del repositorio
git log --oneline
git status
```

### Notas para prácticas futuras

> **⚠️ Importante:** Conserva el directorio `practica-04-autocompletado` y sus archivos. Las Prácticas 7, 8 y 9 del Módulo 3 tienen dependencias con el código generado en prácticas anteriores. **No elimines estos archivos.**

### Cerrar recursos (opcional)

Si necesitas liberar memoria, puedes cerrar las pestañas del panel de Copilot Chat en VS Code, pero mantén VS Code abierto si continuarás con la siguiente práctica en la misma sesión.

---

## Resumen

En esta práctica aplicaste las capacidades de **autocompletado contextual** de GitHub Copilot Chat para crear dos funciones con lógica de negocio real: `calcular_precio_final` y `validar_pedido`. A lo largo del ejercicio experimentaste de primera mano cómo:

- El **contexto del archivo** (constantes, comentarios, imports y funciones previas) influye directamente en la calidad y relevancia de las sugerencias de Copilot Chat.
- Los **comentarios descriptivos y nombres de función claros** actúan como señales de intención que guían al modelo hacia sugerencias más precisas.
- El comando `/tests` permite generar casos de prueba rápidamente, y el comando `/explain` con código seleccionado sirve como herramienta de referencia para evaluar críticamente el código generado.
- Las sugerencias de Copilot Chat deben ser **revisadas y validadas**, no aceptadas ciegamente; el programador sigue siendo responsable de la calidad y corrección del código final.

### Puntos clave de esta práctica

| Concepto | Lo que aprendiste |
|----------|-------------------|
| Autocompletado contextual | Copilot usa el archivo activo completo como contexto |
| Calidad del prompt | Comentarios claros + tipo de retorno = mejores sugerencias |
| Evaluación crítica | `/explain` con selección ancla la respuesta al código real |
| Ciclo completo | Autocompletar → Revisar → Probar → Evaluar con Copilot |

### Recursos adicionales

- [Documentación oficial de GitHub Copilot en VS Code](https://code.visualstudio.com/docs/copilot/copilot-chat)
- [Mejores prácticas para prompts en GitHub Copilot](https://github.blog/news-insights/product-news/getting-the-most-out-of-github-copilot-tips-tricks-hacks/)
- [Guía de type hints en Python (PEP 484)](https://peps.python.org/pep-0484/)
- [Documentación de unittest en Python](https://docs.python.org/3/library/unittest.html)

> **📓 Recuerda:** Actualiza tu diario de aprendizaje con las observaciones de esta práctica. Las Prácticas 9 y 10 requerirán que reflexiones sobre experiencias acumuladas, incluyendo lo que aprendiste hoy sobre el comportamiento del autocompletado y la evaluación crítica del código generado por IA.





