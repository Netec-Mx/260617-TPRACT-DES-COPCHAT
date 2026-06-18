# Crea una función en un lenguaje de programación de tu elección utilizando Copilot Chat para autocompletar el código

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

---

---

# Escribe comentarios detallados sobre lo que debería hacer una función y utiliza Copilot Chat para generarla.

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

---
*Lab 02-00-02 — Práctica 5 | Módulo 2: Copilot Chat como Herramienta de Referencia*

---

# Práctica 6 — Mini Proyecto de Codificación con Diario de Intervenciones de Copilot Chat

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

---

*Lab 02-00-03 | Módulo 2 — Copilot Chat como Herramienta de Referencia | Práctica 6 de 10*
