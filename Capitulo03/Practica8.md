# Práctica 8: Desarrolla una funcionalidad que mejore un producto existente basándote en las sugerencias de Copilot Chat.

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

