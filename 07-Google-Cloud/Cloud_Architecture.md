# Arquitectura de Infraestructura en Google Cloud (GastroTwin)

Este documento detalla el flujo de datos y los servicios de Google Cloud Platform (GCP) requeridos para soportar la ingesta y procesamiento automatizado de los costos operativos.

## 1. Diagrama del Pipeline de Datos

```text
 ┌─────────────────┐       ┌──────────────────────┐       ┌──────────────────────┐
 │  Fuentes Datos  │       │     Almacenamiento   │       │ Capa de Inteligencia │
 │ (Skill / Excel) │──────>│ Google Cloud Storage │──────>│    Agentes Gemini    │
 └─────────────────┘       └──────────────────────┘       └──────────────────────┘
                                                                     │
                                                                     ▼
 ┌─────────────────┐       ┌──────────────────────┐       ┌──────────────────────┐
 │  Visualización  │       │    Modelo Canónico   │       │   Motor GastroTwin   │
 │   (Power BI)    │<──────│ (BigQuery / Excel)   │<──────│   (Cálculo Costos)   │
 └─────────────────┘       └──────────────────────┘       └──────────────────────┘
 ## 2. Componentes e Integración de Servicios

### A. Capa de Almacenamiento (Google Cloud Storage)
* **Bucket Principal:** `gs://gastrotwin-core-prod-data-lake/`
* **Estructura de Carpetas:**
  - `/raw-pos/`: Archivos planos diarios con las ventas brutas, netas e impuestos extraídos del sistema POS.
  - `/raw-invoices/`: Imágenes (`.png`, `.jpg`) o PDFs de las facturas físicas de proveedores cargadas desde dispositivos móviles o escáneres.
  - `/processed-json/`: Resultados estructurados limpios ya validados por la IA.

### B. Capa de Cómputo e IA (Vertex AI & Gemini Pro)
* Cuando un nuevo archivo ingresa a `/raw-invoices/`, una función sin servidor o trigger despierta el **Invoice Parser Agent**.
* Usando las capacidades multimodales de **Gemini Pro**, se lee la imagen de la factura y se extraen los costos de insumos mapeados al catálogo de alimentos, bebidas o suministros.
* El resultado se consolida en BigQuery o tablas maestras en Excel para actualizar de forma inmediata las medidas DAX de **Prime Cost** y **Punto de Equilibrio Diario** en el Dashboard de Power BI.