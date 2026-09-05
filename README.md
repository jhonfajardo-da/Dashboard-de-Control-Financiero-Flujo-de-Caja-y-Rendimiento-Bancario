# 📊 Dashboard de Control Financiero, Flujo de Caja y Rendimiento Bancario

![Power BI](https://img.shields.io/badge/Power_BI-F2C94C?style=for-the-badge&logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-1D6F42?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)

## 📌 Descripción del Proyecto

Este repositorio contiene la solución analítica integral enfocada en la gestión de **Flujo de Caja, Tesorería y Rendimiento Bancario**. El proyecto consolida y procesa los movimientos de tesorería, concilia estados de cuenta bancarios y evalúa la salud financiera operativa para optimizar la toma de decisiones ejecutivas en capital de trabajo.

La solución permite auditar ingresos, egresos, saldos consolidados y rendimiento por entidad bancaria en tiempo real, garantizando un control estricto sobre la liquidez de la organización.

---

## 🎯 Objetivos Analíticos

* **Monitorear la Liquidez Neta:** Evaluar la evolución del flujo de caja operativo y la disponibilidad de caja en tiempo real.
* **Analizar la Concentración Bancaria:** Medir la distribución de saldos y volumen de transacciones por entidad bancaria y tipo de cuenta.
* **Auditar Flujos de Ingresos y Egresos:** Mapear las entradas y salidas operacionales para detectar patrones de gasto y optimizar el fondo de maniobra.
* **Evaluar Gastos Operativos y Financieros:** Identificar comisiones, costos bancarios e impactos por tipo de cambio.

---

## 📈 Indicadores Clave de Rendimiento (KPIs Globales)

| Métrica KPI | Valor Absoluto | Descripción |
| :--- | :--- | :--- |
| **Ingresos Totales (Inflow)** | **$0,00 USD** | Total de recursos monetarios percibidos en el periodo. |
| **Egresos Totales (Outflow)** | **$0,00 USD** | Total de desembolsos y pagos operativos realizados. |
| **Flujo de Caja Neto** | **$0,00 USD** | Diferencia neta entre ingresos acumulados y egresos. |
| **Saldo Disponible en Bancos** | **$0,00 USD** | Balance consolidado en las cuentas de tesorería. |
| **Costo por Comisiones** | **$0,00 USD** | Impacto acumulado de tarifas e intereses bancarios. |

---

## 🔍 Análisis de Resultados y Hallazgos Clave

### 🏦 1. Rendimiento y Distribución por Entidad Bancaria

* **Concentración de Liquidez:** Evaluación del porcentaje de capital distribuido entre los principales bancos aliados.
* **Cobertura de Operaciones:** Análisis de disponibilidad inmediata frente a compromisos de corto plazo.

| Banco / Entidad | Saldo Actual (USD) | Ingresos (USD) | Egresos (USD) | Participación (%) |
| :--- | :--- | :--- | :--- | :--- |
| **Banco A** | $0,00 | $0,00 | $0,00 | 0,00% |
| **Banco B** | $0,00 | $0,00 | $0,00 | 0,00% |
| **Banco C** | $0,00 | $0,00 | $0,00 | 0,00% |

---

### 💸 2. Estructura de Ingresos y Egresos Operativos

* **Categorización de Gastos:** Clasificación detallada de desembolsos (proveedores, nómina, servicios y gastos financieros).
* **Rendimiento de Cobranza:** Seguimiento a la efectividad en el ingreso de fondos según condiciones de pago.

| Categoría de Flujo | Monto (USD) | % del Total | Tendencia |
| :--- | :--- | :--- | :--- |
| **Cobros a Clientes** | $0,00 | 0,00% | Estable |
| **Pago a Proveedores** | $0,00 | 0,00% | Controlado |
| **Nómina y Gastos Operativos**| $0,00 | 0,00% | Programado |
| **Comisiones Bancarias** | $0,00 | 0,00% | A Optimizar |

---

## 🖼️ Evidencias / Dashboard

![Dashboard de Control Financiero](Finanzas.pdf)[cite: 10]

---

## 📐 Medidas DAX Utilizadas

El modelo analítico en Power BI incorpora lógica de cálculo financiera mediante medidas DAX avanzadas:

```dax
// 1. Total Ingresos (Inflow)
Total_Ingresos = 
SUMX(
    FILTER('Movimientos', 'Movimientos'[Tipo] = "Ingreso"),
    'Movimientos'[Monto]
)

// 2. Total Egresos (Outflow)
Total_Egresos = 
SUMX(
    FILTER('Movimientos', 'Movimientos'[Tipo] = "Egreso"),
    'Movimientos'[Monto]
)

// 3. Flujo de Caja Neto
Flujo_Caja_Neto = [Total_Ingresos] - [Total_Egresos]

// 4. Saldo Disponible Consolidado
Saldo_Disponible = 
CALCULATE(
    SUM('Cuentas_Bancarias'[Saldo_Inicial]) + [Flujo_Caja_Neto]
)

// 5. Ratio de Cobertura de Liquidez
Ratio_Cobertura = 
DIVIDE([Total_Ingresos], [Total_Egresos], 0)
