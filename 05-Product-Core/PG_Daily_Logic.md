# Especificación Lógica: Capa 1 - P&G Diario

Este documento define el modelo conceptual, las variables y las fuentes de datos (ERP Skill y estructuras en Excel) para el cálculo de la utilidad operativa diaria estimada.

## 1. Estructura de Ingresos Diarios (Efectivo + Devengado)
El sistema consolida los ingresos del día a partir de los cierres de caja y facturación del ERP Skill, categorizados así:
* **Venta Restaurante (POS):** Ingresos por cubiertos, mesas y rotación diaria regular.
* **Venta Eventos:** Facturación de banquetes, alquiler de espacios y servicios corporativos integrados.
* **Servicios Adicionales:** Otros ingresos operativos directos.

## 2. Estructura de Costos Variables y Prime Cost
Para calcular el **Prime Cost** diario (indicador clave de eficiencia en alimentos y mano de obra), agrupamos los costos controlables:

### A. Costo de Alimentos y Bebidas (Food & Beverage Cost)
* **Food Cost:** Insumos perecederos y no perecederos despachados/consumidos en el día.
* **Beverage Cost:** Costo de licores, bebidas y cafetería.
* *Nota de control:* Las variaciones de precios en facturas de proveedores son notificadas por el Agente de IA para ajustar este impacto de forma inmediata.

### B. Costo de Mano de Obra Operativa (Labor Cost)
* **Nómina Fija Diaria:** Costo diario prorrateado del personal de planta.
* **Personal Extra:** Costo variable del personal de refuerzo contratado según el volumen de operación o eventos del día.

### C. Otros Costos Variables
* Lavandería variable, suministros de mesa y otros gastos directamente proporcionales a la venta del día.

## 3. Costos Fijos Prorrateados
Para que la utilidad estimada del día sea realista, los costos fijos mensuales se dividen de manera lineal o ponderada por día:
* Gastos administrativos fijos.
* Servicios públicos (estimado diario).
* Depreciaciones y otros costos fijos estructurales.

## 4. Ecuación de la Utilidad Operativa Diaria

La utilidad operativa estimada del día se calcula mediante la siguiente relación:

$$\text{Utilidad Operativa Diaria} = \text{Ingresos Totales} - \text{Prime Cost} - \text{Otros Costos Variables} - \text{Costos Fijos Prorrateados}$$

Donde el Prime Cost se define como:

$$\text{Prime Cost} = \text{Costo de Alimentos y Bebidas} + \text{Costo de Mano de Obra Total}$$