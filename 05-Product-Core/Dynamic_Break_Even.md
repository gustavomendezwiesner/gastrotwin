# Metodología: Capa 2 - Punto de Equilibrio Dinámico

Este documento detalla el modelo matemático para calcular el punto de equilibrio diario en función de las fluctuaciones de costos de la operación y el margen de contribución real.

## 1. El Concepto Dinámico
El punto de equilibrio diario no es fijo. Varía cada día debido a:
* **Estructura de Turnos:** Ajustes programados en la nómina según el día de la semana (ej. menos personal los miércoles vs. fines de semana).
* **Costos fijos ponderados:** Prorrateo de los costos fijos mensuales sobre una base operativa diaria.
* **Margen de Contribución Real ($M_c$):** Cambia según el mix de venta del día (el margen de la venta de alimentos es distinto al de bebidas o banquetes de eventos).

## 2. Formulación Matemática

El Margen de Contribución Porcentual ($M_c$) se determina a partir de la relación entre las Ventas Totales y los Costos Variables Totales (Food Cost + Beverage Cost + Personal Extra + Lavandería Variable):

$$M_c = \frac{\text{Ventas Totales} - \text{Costos Variables Totales}}{\text{Ventas Totales}}$$

Una vez obtenido el margen de contribución del día, el **Punto de Equilibrio Dinámico ($PE_d$)** —que representa la venta mínima requerida para que la utilidad operativa sea exactamente cero— se calcula dividiendo los costos fijos del día entre dicho margen:

$$PE_d = \frac{\text{Costos Fijos Prorrateados Diarios}}{M_c}$$

## 3. Lógica de Alerta de Desviación Intra-Día
Para mitigar el riesgo de pérdida antes del cierre del turno, el sistema cruza el avance de facturación en tiempo real proveniente del ERP Skill contra el $PE_d$ calculado para ese día específico:

* **Monitoreo de Horas Críticas:** Si a un corte intermedio (ej. 2:00 PM después del servicio de almuerzo) la venta ejecutada está significativamente por debajo de la curva histórica para alcanzar el punto de equilibrio, el modelo activa un estado de riesgo alto.
* **Acción Gerencial:** Permite al administrador tomar decisiones logísticas inmediatas, como optimizar el despacho de personal extra de pasantía o controlar mermas en tiempo real.