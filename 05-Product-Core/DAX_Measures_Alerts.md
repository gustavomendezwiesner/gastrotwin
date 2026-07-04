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