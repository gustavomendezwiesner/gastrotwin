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