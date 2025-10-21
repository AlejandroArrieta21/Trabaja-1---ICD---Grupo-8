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

# TRABAJO 2
Sentimiento en el mercado de criptomonedas y su relación con el tipo de cambio del sol peruano

Este proyecto analiza si existe una correlación significativa entre el sentimiento en el mercado de criptomonedas, medido por el Fear & Greed Index (FGI), y el tipo de cambio del sol peruano.
A través de modelos econométricos OLS (simples y complejos), se busca evaluar si el sentimiento financiero global influye en los retornos diarios del tipo de cambio.

# Estructura del proyecto
Feature Engineering, limpieza y preparación de datos
Se construyen las variables necesarias para el modelado:
Retorno logarítmico diario del tipo de cambio (ret_USD), definido como la variable objetivo.
Rezagos, promedios móviles y transformaciones cuadráticas del FGI.
Rezagos de variables de control: DXY, VIX, Bitcoin, Oro, T-Bills y Treasury 5y.
Interacción FGI × DXY para capturar efectos combinados.
Se eliminan valores infinitos y faltantes, aplicando forward-fill cuando corresponde. Finalmente, se divide la muestra en train y test, y se define un modelo base para referencia.

# Modelo base (Baseline)
El modelo base predice siempre el valor medio del retorno del tipo de cambio en el conjunto de entrenamiento.
Este modelo sirve como referencia para evaluar si los modelos econométricos logran mejorar la capacidad predictiva.
El desempeño se evalúa con el Mean Squared Error (MSE) en el conjunto de prueba.

# Modelo OLS simple
Se estima un modelo de regresión lineal en el que ret_USD depende del FGI rezagado (FGI_lag1).
Se utilizan errores robustos HAC (Newey-West) para corregir heterocedasticidad y autocorrelación.
Se reportan los coeficientes, el R², la significancia estadística y pruebas de diagnóstico (Durbin–Watson y Breusch–Pagan).
El desempeño se evalúa mediante el MSE en test.

# Modelo OLS complejo
Se amplía la especificación incluyendo:
Rezagos del FGI y su término cuadrático.
Promedios móviles e interacciones con el DXY.
Rezagos de las variables de control (VIX, Bitcoin, Oro, T-Bills y Treasury 5y).
Este modelo busca capturar relaciones no lineales y efectos conjuntos.
También se utilizan errores HAC y se evalúa el desempeño mediante el MSE y el R² ajustado.

# Validación cruzada temporal
Se emplea una validación cruzada que respeta la estructura temporal de los datos.
Se calculan el MSE promedio y su desviación estándar para cada modelo (baseline, simple y complejo), analizando la estabilidad y capacidad de generalización.

# Comparación de modelos
Se construye una tabla comparativa con los resultados de los tres modelos.
El OLS Simple (FGI) obtiene el menor error cuadrático medio (MSE = 0.1013) en el conjunto de prueba, mostrando un equilibrio óptimo entre simplicidad y rendimiento.
El modelo complejo, aunque más detallado, no mejora la capacidad predictiva y presenta mayor variabilidad.

# Evaluación final en el conjunto de prueba
El modelo ganador (OLS Simple) se reentrena con todo el conjunto de entrenamiento y se evalúa en los datos de prueba.
Los resultados confirman que el rendimiento fuera de muestra es consistente con la validación cruzada, lo que demuestra ausencia de sobreajuste y un desempeño estable.

# Conclusiones
Modelo ganador: OLS Simple con FGI rezagado (FGI_lag1).
Desempeño: MSE = 0.1013 y R² ≈ 0.001; bajo poder explicativo pero comportamiento estable.
Hallazgos clave: El coeficiente del FGI es negativo y no significativo, indicando una relación débil entre el sentimiento en criptomonedas y el tipo de cambio del sol peruano.
Consistencia teórica: Los resultados son coherentes con la literatura que señala que los movimientos cambiarios en economías emergentes responden más a factores macrofinancieros estructurales (Engel & West, 2005; Calvo & Reinhart, 2002).
Limitaciones: Forma funcional lineal, ruido en datos diarios y ausencia de variables de intervención o flujos de capital.
Próximos pasos: Probar modelos no lineales o dinámicos (VAR, GARCH), usar frecuencias semanales/mensuales e incorporar variables macroeconómicas adicionales.

# Referencias
- Calvo, G. A., & Reinhart, C. M. (2002). Fear of Floating. Quarterly Journal of Economics, 117(2), 379–408.
- Engel, C., & West, K. D. (2005). Exchange Rates and Fundamentals. Journal of Political Economy, 113(3), 485–517.
- Fama, E. F. (1970). Efficient Capital Markets: A Review of Theory and Empirical Work. Journal of Finance, 25(2), 383–417.
