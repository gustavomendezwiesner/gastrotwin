# Motor de Simulación & Recuperación de Utilidad (Digital Twin)

Este componente actúa como el "Digital Twin" financiero de la operación, modelando el impacto completo en el P&G ante cambios en las variables operativas intra-mes.

## 1. Algoritmo del Simulador (Capa 4)

El motor procesa los escenarios "What-if" recalculando de forma secuencial la estructura financiera mediante la siguiente lógica:

```text
[Ingresar Escenario] 
       │
       ▼
[Recalcular Ventas Proyectadas] (Clientes × Ticket Promedio)
       │
       ▼
[Ajustar Costos Variables] (Food Cost % / Beverage Cost % / Extras)
       │
       ▼
[Calcular Nuevo Prime Cost] (Nómina Ajustada + Nuevos Costos Variables)
       │
       ▼
[Determinar Margen y Punto de Equilibrio]
       │
       ▼
[Resultado: Comparación de Nueva Utilidad vs. Escenario Actual]