# 📊 Dashboard de Control Financiero, Flujo de Caja y Rendimiento Bancario

[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)](https://learn.microsoft.com/en-us/dax/)

## 📌 Descripción del Proyecto
Este proyecto consiste en el desarrollo de un **Dashboard de Control Financiero y Flujo de Caja** diseñado para proveer visibilidad consolidad a la dirección de tesorería y finanzas. Permite monitorear la captación de ingresos por entidad bancaria, analizar la variabilidad mensual del flujo de caja mediante un gráfico de cascada (*Waterfall Chart*) y supervisar la utilidad neta real descontando automáticamente el impacto tributario.

---

## 🎯 Problema de Negocio
La organización requería resolver tres retos analíticos clave:
1. **Dispersión de transacciones:** Monitorear el rendimiento operativo distribuido en 5 bancos (*Chase Bank, Bank of America, BBVA Bancomer, Santander y Citigroup*).
2. **Cálculo impositivo en tiempo real:** Descontar automáticamente la retención fiscal obligatoria del 15% sobre ingresos para reflejar la utilidad neta real.
3. **Control de variaciones de caja:** Detectar los meses con caídas operativas para ajustar presupuestos y evitar falta de liquidez.

---

## 🗃️ Dataset / Fuente de Datos
* **Archivo:** `Base Financiero.xlsx` (Hoja: *Finanzas*).
* **Volumen:** 2,725 registros transaccionales del periodo 2020.
* **Atributos clave:** `Número Movimiento`, `Nombre`, `Ciudad`, `Fecha de movimiento`, `Valor de movimiento`, `Tipo` (*Recibido / Pagado*), `Banco`, `Imagen`, `Forma de pago`.

---

## 📐 Metodología y Modelado

### 1. Limpieza y Transformación en Power Query
* Estandarización de signos en transacciones de egreso (`Pagado`).
* Creación de catálogo de bancos e integración de identidades visuales para optimizar la experiencia UX/UI.
* Conexión con tabla de calendario dimensional para análisis temporal.

## 🖼️ Evidencias / Dashboard

![Dashboard de Productividad y Piezas Fabricadas](screenshots/overview.png)[cite: 10]

---

### 2. Medidas DAX Implementadas
```dax
// 1. Total Pagos Recibidos (Ingresos Brutos)
Pagos_Recibidos = 
CALCULATE(
    SUM('Finanzas'[Valor de movimiento]),
    'Finanzas'[Tipo] = "Recibido"
)

// 2. Total Pagos Hechos (Egresos Operativos)
Pagos_Hechos = 
ABS(
    CALCULATE(
        SUM('Finanzas'[Valor de movimiento]),
        'Finanzas'[Tipo] = "Pagado"
    )
)

// 3. Retención de Impuestos (TAX 15%)
Impuestos_TAX = [Pagos_Recibidos] * 0.15

// 4. Utilidad Neta Consolidada
Utilidad_Neta = [Pagos_Recibidos] - [Pagos_Hechos] - [Impuestos_TAX]

// 5. Porcentaje de Utilidad Neta
Porcentaje_Utilidad = DIVIDE([Utilidad_Neta], [Pagos_Recibidos], 0)
