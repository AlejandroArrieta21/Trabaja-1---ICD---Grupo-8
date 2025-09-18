# Proyecto: Análisis del Sentimiento en Criptomonedas y su Relación con el Tipo de Cambio
# Descripción general
Este trabajo busca evaluar la relación entre el sentimiento en el mercado de criptomonedas, medido a través del Fear & Greed Index (FGI) aplicado especialmente al Bitcoin, y el tipo de cambio de monedas emergentes, en particular el sol peruano.

El análisis incluye además variables de control relevantes como el DXY (Índice del dólar estadounidense), el VIX (Índice de volatilidad del mercado), el BTC (Precio histórico del Bitcoin), y tres nuevos activos financieros: el oro  (GC=F), las letras del Tesoro de 13 semanas (^IRX) y los bonos del Tesoro a 5 años (FVX).

# Fuentes de datos
Fear & Greed Index (FGI): datos obtenidos desde la API de Alternative.me
Tipo de cambio USD/PEN: series oficiales del Banco Central de Reserva del Perú (BCRP).
DXY, VIX, BTC, Gold, T-Bills 13w y Treasury 5y: información histórica descargada a través de yfinance desde Yahoo Finance.
Fecha de última actualización de los datos: Se consideraron observaciones hasta el 30 de junio de 2025, que corresponde al último registro disponible en la base de datos de Alternative.me.

# Variables principales
- FGI: Índice de "Miedo y Codicia" aplicado al Bitcoin, indicador de sentimiento en el mercado cripto. Está especialmente enfocado en el Bitcoin y combina diferentes indicadores (volatilidad, volumen, momentum, encuestas, etc.) para identificar si el mercado se encuentra en un estado de miedo (pesimismo, ventas masivas) o de codicia (optimismo, compras especulativas).

- USD_PEN_Venta: Representa el tipo de cambio nominal de venta del dólar estadounidense en el mercado peruano. Refleja el valor en soles peruanos que los agentes económicos deben pagar por adquirir un dólar. Esta variable es clave para analizar la estabilidad cambiaria del país y el impacto de factores externos sobre la economía local.

# Variables de Control
- BTC_USD: Precio diario de Bitcoin en dólares estadounidenses. El Bitcoin es el principal activo del mercado de criptomonedas y su precio refleja tanto movimientos especulativos como cambios en la confianza de los inversionistas.

- DXY: Índice que mide el valor del dólar frente a una cesta de monedas extranjeras (principalmente euro, yen japonés, libra esterlina, dólar canadiense, corona sueca y franco suizo). Es un indicador de la fortaleza del dólar en los mercados internacionales.

- VIX: Índice de volatilidad del mercado de opciones del S&P500. Valores altos del VIX suelen asociarse a periodos de incertidumbre o crisis financieras globales.

- Gold (GC=F): Precio spot del oro, considerado activo refugio en contextos de incertidumbre.

- TBills_13w (IRX): Rendimiento de las letras del Tesoro de EE. UU. a 13 semanas, indicador de la política monetaria de corto plazo.

- Treasury_5y (FVX): Rendimiento de los bonos del Tesoro de EE. UU. a 5 años, indicador de expectativas de tasas de interés de mediano plazo.

# Ejecución del Notebook
El notebook se organiza en las siguientes secciones:

1. Obtención de datos
- Se descargaron los datos del Fear & Greed Index (FGI) desde la API de Alternative.me.
- Se extrajeron series financieras desde distintas fuentes:
  - Tipo de cambio USD/PEN desde el BCRP.
  - Índice DXY y VIX desde Yahoo Finance.
  - Precio de Bitcoin (BTC/USD), Gold (GC=F), T-Bills 13w (^IRX) y Treasury 5y (^FVX) también desde Yahoo Finance.
    
2. Unificación de datos
- Conversión de etiquetas de fechas a formato datetime para unificar todas las series.
- Manejo de valores faltantes y estandarización de las frecuencias temporales.
- Consolidación de todas las fuentes en un único DataFrame para facilitar el análisis.

3. Análisis exploratorio
-Gráficos de series de tiempo para observar la evolución de cada variable.
- Boxplots de retornos diarios y variables a nivel para comparar dispersión y detectar valores atípicos.
- Histogramas para analizar la distribución de las variables.
- Gráficos de dispersión para evaluar relaciones entre el tipo de cambio USD/PEN y las demás variables.
- Visualización en un heatmap para identificar la fuerza y dirección de las relaciones.

4. Conclusiones
- Discusión sobre los hallazgos y su relevancia en el contexto del mercado cambiario.
  
# Conclusiones 
- El Fear & Greed Index (sentimiento cripto) no muestra relación estadísticamente significativa con el tipo de cambio USD/PEN (ρ ≈ 0.07). Esto indica que no es un determinante importante de la dinámica cambiaria peruana.
- Variables globales como el DXY y, en menor medida, el precio de Bitcoin, presentan correlaciones más relevantes con el tipo de cambio (ρDXY ≈ 0.31, ρBTC ≈ 0.52), mostrando que el sol responde principalmente a factores internacionales.
- El VIX y el FGI aportan información sobre percepción de riesgo y sentimiento especulativo, pero su influencia directa sobre el tipo de cambio en Perú es marginal (ρVIX ≈ 0.09).
- En términos generales, el tipo de cambio en Perú se encuentra más condicionado por variables externas tradicionales que por el sentimiento cripto.
- La correlación del Bitcoin con USD/PEN refleja más su propia volatilidad que un canal estable de transmisión hacia el mercado cambiario peruano.
- El oro muestra una correlación baja y estable con el USD/PEN, confirmando su rol de activo refugio más vinculado a la aversión global al riesgo que a los movimientos cambiarios locales.
- Los rendimientos de los bonos del Tesoro de EE. UU. (T-Bills 13w y Treasury 5y) evidencian una correlación positiva con el tipo de cambio peruano, lo que sugiere que las expectativas de tasas de interés en EE. UU. influyen directamente en la fortaleza del dólar frente al sol.
