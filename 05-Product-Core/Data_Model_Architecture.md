# Arquitectura del Modelo de Datos & Tablas (GastroTwin v0.1)

Este documento contiene el modelo analítico en estrella que unifica las lecturas de ventas de Skill POS junto con los registros de costos y gastos fijos en Excel.

## 1. Esquema del Modelo Estrella
```text
                  DimFecha
                     │
                     ▼
  ┌──────────────┬──────────────┬──────────────┐
  │              │              │              │
FactVentas   FactNomina    FactCostos   FactGastosFijos
  │              │              │              │
  └──────────────┴──────┬───────┴──────────────┘
                        ▼
                 DimCentroCosto
                        │
                  DimCategoria
                        │
                 DimArticulo
                
---

### Paso 2: Crear el Archivo de Fórmulas DAX y Alertas Tempranas

1. Haz clic derecho sobre `05-Product-Core`, selecciona **New File** y nómbralo: `DAX_Measures_Alerts.md`
2. Copia y pega las fórmulas oficiales y las reglas del semáforo, y guarda con `Ctrl + S`:

```markdown
# Medidas DAX Oficiales & Motor de Alertas (GastroTwin)

## 1. Medidas de Control Operativo e Insumos
* **Ventas Netas:** `Ventas = SUM(FactVentasPOS[VentasNetas])`
* **Food Cost:** `Food Cost = SUM(FactCostosVariables[FoodCost])`
* **Beverage Cost:** `Beverage Cost = SUM(FactCostosVariables[BeverageCost])`
* **Prime Cost:** `Prime Cost = [Food Cost] + [Beverage Cost] + [Nomina]`
* **Utilidad del Día:** `Utilidad Dia = [Ventas] - [Prime Cost] - [Gastos Variables] - [Gastos Fijos Prorrateados]`

## 2. Fórmulas del Punto de Equilibrio Dinámico
Implementado para sustituir el enfoque estático, calculándose de forma diaria mediante la venta y el gasto variable:

```dax
Margen Contribucion = 
DIVIDE(
    [Ventas] - [Costos Variables],
    [Ventas]
)

Punto Equilibrio Diario = 
DIVIDE(
    [Costos Fijos Dia],
    [Margen Contribucion]
)
---

### Paso 3: Subir la Documentación del Núcleo a GitHub

Abre tu terminal en VS Code o PowerShell y ejecuta estos comandos para consolidar tu avance:

```powershell
git add 05-Product-Core/Data_Model_Architecture.md 05-Product-Core/DAX_Measures_Alerts.md
git commit -m "Docs: complete data model spec, DAX measures, and alert thresholds"
git push origin main