# 📈Índice Compuesto Clave para Precios Diarios

Optimización de Consultas por Ticker y Fecha

## 📌Descripción

Este proyecto define un índice compuesto único sobre la tabla precios_diarios, utilizando las columnas ticker_id y fecha.

Su objetivo principal es garantizar integridad de datos y maximizar la eficiencia de las consultas temporales, que son la base de todos los análisis técnicos, eventos corporativos y estudios de mercado posteriores.

CREATE UNIQUE INDEX idx_ticker_fecha 
ON precios_diarios (ticker_id, fecha);

## 🎯Problema que resuelve

En sistemas de análisis financiero es extremadamente común:
- Consultar precios por ticker y por fecha
- Hacer JOIN con indicadores técnicos y eventos
- Usar funciones de ventana (LAG, LEAD, medias móviles, etc.)
- Asumir que existe un solo precio por ticker por día

Sin este índice:
- Las consultas escanean grandes volúmenes de datos
- Se corre el riesgo de duplicados silenciosos
- El rendimiento degrada exponencialmente a medida que crece el histórico

## 🚀Beneficios clave
1️⃣ Integridad de datos (crítico)

El índice es UNIQUE, lo que garantiza que:
- No puede existir más de un registro por (ticker_id, fecha)
- Se evita corrupción histórica de precios
- Los cálculos técnicos no se distorsionan

Esto es fundamental para:
- Backtesting
- Análisis estadístico
- Modelos cuantitativos

2️⃣ Rendimiento extremo en consultas financieras

Este índice acelera drásticamente consultas como:

WHERE ticker_id = 'AAPL'
  AND fecha BETWEEN '2024-01-01' AND '2024-06-30'


y todos los JOIN de este tipo:
- precios_diarios ↔ indicadores_tecnicos
- precios_diarios ↔ eventos_corporativos

3️⃣ Base para análisis avanzados

Este índice es estructural, no opcional. Es la base para:
- Medias móviles (SMA, EMA)
- RSI, ADX, volatilidad, kurtosis
- Detección de gaps
- Estudios pre y post evento
- Análisis sectorial y cross-asset

Sin él, los insights avanzados simplemente no escalan.

## 🧠Cuándo usar este índice

✔ Bases de datos financieras
✔ Series temporales de mercado
✔ Datos diarios o intradiarios
✔ Sistemas de análisis cuantitativo
✔ Dashboards y pipelines analíticos

## ⚠️Consideraciones

- El índice debe crearse después de limpiar duplicados
- Es ideal crearlo antes de cargar grandes volúmenes históricos
- Compatible con estrategias de particionado por fecha

## 📊Impacto esperado

⬇️ Reducción drástica del tiempo de consulta

⬆️ Mayor estabilidad en análisis históricos

🧱 Base sólida para insights complejos

🧠 Confianza total en los datos

## 👤Autora
Flavia Hepp Proyecto de SQL aplicó un análisis de riesgo basado en eventos.
