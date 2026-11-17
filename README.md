# Análisis de Ventas y Retención - EcoShop
Este proyecto presenta un Análisis Exploratorio de Datos (EDA) sobre el comportamiento de compra de los usuarios de EcoShop durante el periodo *Enero 2025 - Diciembre 2025*, con el objetivo de identificar oportunidades para reducir la tasa de abandono.

![https://img.shields.io/badge/Python-3.11-blue](https://img.shields.io/badge/Python-3.11-blue)

![https://img.shields.io/badge/Estado-Completado-success](https://img.shields.io/badge/Estado-Completado-success)

- [Resumen Ejecutivo](#resumen-ejecutivo)

- [Tabla de KPIs](#tabla-de-kpis)

- [Metodologia](#metodologia)

- [Codigo Destacado](#codigo-destacado)


## Resumen Ejecutivo
> [!IMPORTANT]
>  *Los clientes que realizan una segunda compra dentro de los primeros 30 días tienen un LTV (Lifetime Value) 3 veces superior al resto.*

- Estacionalidad marcada: El pico de ventas ocurre en noviembre (+42%
respecto a la media anual) impulsado por el Black Friday.

- Fricción en móviles: La columna `device_type` reveló que el 70% del tráfico
viene de mobile, pero la conversión es un 1.8% menor que en desktop.

- Categoría estrella: Los productos de la categoría `Hogar_Sostenible`
concentran el mayor margen de beneficio neto.


## Tabla de KPIs


### Tabla comparativa 2024 vs 2025

| Métrica          | 2024    | 2025    | Variación     |
|:-----------------|:-------:|--------:|--------------:|
| Ingresos Totales | $450,000 | $585,000 | +30%     |
| Ticket Promedio  | $42.50  | $46.80   | +10.1%  |
| Tasa de Conversion | 2.4%   | 2.9%   | +0.5% |
| Tasa de Abandono (Churn)    | 18.0%  | 14.5%  | -3.5% |



## Metodologia

1. Extracción: Conexión a base de datos PostgreSQL mediante SQLAlchemy.
2. Limpieza: Tratamiento de valores nulos en fecha_entrega y
estandarización de categorías.
3. Análisis: Segmentación de clientes mediante análisis RFM (Recencia,
Frecuencia, Valor Monetario).
4. Visualización: Creación de dashboard interactivo en Power BI y gráficos
estáticos con Seaborn.

**Estado del proyecto**

- [x] Limpieza y validación del dataset 
- [x] Análisis exploratorio y pruebas de hipótesis 
- [ ] Automatización del pipeline semanal con Airflow
- [ ] Modelo predictivo de *churn*


## Codigo destacado

```sql
SELECT
categoria,
COUNT(DISTINCT order_id) AS total_pedidos,
ROUND(AVG(total_venta), 2) AS ticket_promedio
FROM ventas_2025
WHERE estado_pedido = 'Completado'
GROUP BY categoria
ORDER BY ticket_promedio DESC;
