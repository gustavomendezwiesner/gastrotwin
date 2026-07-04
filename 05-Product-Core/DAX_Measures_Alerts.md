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
## 3. Umbrales del Semáforo de Alertas Tempranas
* 🔴 **Rojo (Riesgo Alto):** `Ventas < [Punto Equilibrio Diario]`
* 🟡 **Amarillo (Precaución):** `Ventas` entre el 100% y el 110% del punto de equilibrio.
* 🟢 **Verde (Zona Segura):** `Ventas > 110%` del punto de equilibrio.

### Reglas de Disparo de Alertas Diarias:
1. **Nómina:** `Nomina > Presupuesto + 5%`
2. **Food Cost:** `Food Cost > Objetivo + 2%`
3. **Personal Extra:** `Horas extra > Objetivo semanal`
4. **Compras:** `Compra extraordinaria` -> Dispara alerta inmediata.