# Proyecto: 

## 1. Objetivo

El objetivo de este proyecto es realizar un Análisis Exploratorio de Datos (EDA) y construir un dashboard interactivo que permita comprender el comportamiento de las ventas, clientes, productos y países entre los años 2009 y 2011.
El análisis incluye:

Limpieza y transformación profunda de los datos.

Análisis descriptivo y estadístico.

Visualización de patrones temporales, geográficos y macroeconómicos.

Creación de un dashboard profesional en Power BI.

Conclusiones basadas en los hallazgos del análisis.

## 2. Dataset

### 📌 Fuente  

Los datos provienen del dataset de ventas de Online Retail II, disponible en [Dataset en Kaggle](https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci)
El resto de datos son datos que hemos scrapeado de la página: [Dataset scrapeado](https://datosmacro.expansion.com/)

---

### 📊 Descripción de los datasets  

Este conjunto de datos Online Retail II contiene todas las transacciones realizadas por una empresa minorista online del Reino Unido (sin tienda física) entre el 01/12/2009 y el 09/12/2011.
La empresa vende principalmente artículos de regalo únicos para todo tipo de ocasiones.
Muchos de sus clientes son mayoristas.

- InvoiceNo: Número de factura. Es un identificador nominal. Un número entero de 6 dígitos asignado de forma única a cada transacción. Si comienza con la letra "C", indica una cancelación.

- StockCode: Código del producto. Nominal. Un número entero de 5 dígitos asignado de forma única a cada producto.

- Description: Nombre del producto. Nominal.

- Quantity: Cantidad de unidades del producto por transacción. Numérico.

- InvoiceDate: Fecha y hora de la factura. Numérico. Indica el momento en que se generó la transacción.

- UnitPrice: Precio unitario. Numérico. Precio por unidad en libras esterlinas (£).

- CustomerID: Número de cliente. Nominal. Un número entero de 5 dígitos asignado de forma única a cada cliente.

- Country: País. Nominal. Nombre del país donde reside el cliente.

El resto de datasets son datasets con datos macroeconómicos que hemos scrapeado como: la deuda, paro, pib per capita, pib y la poblacion

### 🔄 Transformación de los datos  

Tras la limpieza, transformación y unión de los datasets, se obtuvo un dataset final con:

- **794.754 filas**
- **23 columnas** 

## 3. Tecnologías utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Visual Studio Code
- Microsoft Power BI Desktop

## 4. Estructura del proyecto

```
proyecto-final
│
├── README.md                         # Documentación del proyecto
│
├── Dashboard/
│   └── dashboard.pbix                # Archivo del dashboard en Power BI
│
└── ecommerce-sales-analysis/
    │
    ├── Data/
    │   ├── 0_raw/                        # Datos originales
    │   │   ├── deuda2009.csv
    │   │   ├── deuda2010.csv
    │   │   ├── deuda2011.csv
    │   │   ├── online_retail_II.csv
    │   │   ├── paro2009.csv
    │   │   ├── paro2010.csv
    │   │   ├── paro2011.csv
    │   │   ├── pib_per_capita2009.csv
    │   │   ├── pib_per_capita2010.csv
    │   │   ├── pib_per_capita2011.csv
    │   │   ├── pib2009.csv
    │   │   ├── pib2010.csv
    │   │   ├── pib2011.csv
    │   │   ├── poblacion2009.csv
    │   │   ├── poblacion2010.csv
    │   │   ├── poblacion2011.csv
    │   │
    │   ├── 1_interim/                    # Datos tras una primera limpieza
    │   │   ├── deuda.csv
    │   │   ├── paro.csv
    │   │   ├── pib.csv
    │   │   ├── poblacion.csv
    │   │   ├── ppcapita.csv
    │   │   ├── retail.csv
    │   │
    │   ├── 2_cleaned/                    # Datos completamente limpios
    │   │   ├── deuda.csv
    │   │   ├── paro.csv
    │   │   ├── pib.csv
    │   │   ├── poblacion.csv
    │   │   ├── ppcapita.csv
    │   │   ├── ventas.csv
    │   │
    │   └── 3_processed/                  # Dataset final después del análisis
    │       ├── ventas.csv
    │
    ├── notebooks/
    │   ├── 0_adquisicion_datos.ipynb     # Scrapeo de datos
    │   ├── 1_exploracion.ipynb           # Análisis exploratorio
    │   ├── 2_limpieza.ipynb              # Limpieza y transformación
    │   ├── 3_analisis.ipynb              # Análisis y visualizaciones
    │
    ├── requirements.txt                  # Dependencias del proyecto
    │
    └── images/
        ├── img1.png  
        ├── img2.png            
        ├── img3.png               
        ├── img4.png
        ├── img5.png  
        ├── img6.png
             
```

## 5. Cómo ejecutar el proyecto

1. Crear el entorno virtual
2. Instalar dependencias
3. Ejecutar el notebook

## 6. Limpieza y transformación de los datos

Durante el proceso de preparación de los datasets se realizaron múltiples tareas de depuración, estandarización y creación de nuevas variables con el objetivo de dejar los datos listos para el análisis y el posterior merge entre tablas.

### 🧹 Eliminación de columnas innecesarias  
Se eliminaron columnas redundantes o irrelevantes para el análisis:

- **Deuda**: `Deuda total (M.€).1`, `Deuda total (M.$)`, `Deuda total (M.$).1`, `Deuda Per Cápita.1`  
- **Paro**: `Tasa de desempleo.1`, `Var.`, `Var. Año`  
- **PIB**: `PIB anual.1`, `PIB anual.2`, `PIB anual.3`, `Var. PIB (%)`, `Var. PIB (%).1`  
- **Población**: `Densidad`, `Población.1`, `Var.`  
- **PIB Per Capita**: `PIB Per Capita.1`, `PIB Per Capita.2`, `PIB Per Capita.3`, `Var. anual PIB Per Capita`, `Var. anual PIB Per Capita.1`, `Var. anual PIB Per Capita.2`, `Var. anual PIB Per Capita.3`

---

### 🔧 Renombrado y estandarización de columnas  
- Se renombró la columna **fecha** a **Año**.  
- Se renombró la columna **Países** a **Country**.  
- En el dataset retail, se estandarizó **Description** a minúsculas y se limpiaron espacios.

---

### 🩹 Imputación y corrección de valores  
- En los datasets macroeconómicos, se imputaron valores **NaN** en la columna Año con **2009**, ya que el scrapeo de ese año no incluía dicha columna.  
- En retail, las descripciones vacías (`NaN`) se rellenaron con **"No description"**.  
- Se corrigieron valores incorrectos en la columna Country, eliminando textos añadidos por error durante el scrapeo.  
- Se eliminaron filas incorrectas generadas durante el proceso de extracción.

---

### 🔢 Conversión de tipos de datos  
Se ajustaron los tipos de datos para garantizar coherencia:

- **Deuda**:  
  - `Año` → entero  
  - `Deuda total (M.€)` → entero  
  - `Deuda Per Cápita` → entero  
  - `Deuda (%PIB)` → float  

- **Paro**:  
  - `Tasa de desempleo` → float  

- **PIB**:  
  - `PIB anual (M€)` → entero  

- **PIB Per Capita**:  
  - `Year` → entero  
  - `PIB Per Capita (€)` → entero  

- **Retail**:  
  - `CustomerID` → entero  

---

### 🌍 Traducción de países  
Para poder realizar un merge correcto entre los datasets, se tradujeron los nombres de los países mediante un diccionario, asegurando que todos coincidieran con los valores del dataset retail.

---

### 📅 Transformación de fechas en retail  
La columna `InvoiceDate` se convirtió a formato **datetime** y se generaron nuevas variables temporales:

- `Year`  
- `Month`  
- `Day`  
- `Hour`  
- `Week`  
- `YearMonth`

---

### 🔁 Eliminación de duplicados  
Se eliminaron los registros duplicados del dataset retail para evitar distorsiones en el análisis.

---

### 🚫 Filtrado de movimientos internos  
Dentro del dataset retail se identificaron movimientos internos del almacén.  
Como solo interesan ventas y cancelaciones, se eliminaron todas las filas con:

- `Price = 0`  
- `Quantity = 0`  

Estas no representan ventas ni devoluciones reales.

---

### ❌ Identificación de cancelaciones  
Se creó la columna **isCancelled**, basada en el prefijo de `InvoiceNo` (facturas que comienzan con “C”).

## 7. 📈 Análisis descriptivo

### ⭐ Variables más importantes
- **Quantity**
- **Price**
- **PIB Per Capita**
- **Line Total**
- **Customer ID**
- **Country**
- **Description**
- **InvoiceDate**

---

### 🔥 Correlaciones
- Correlación PIB ↔ ventas:
  - Con UK: correlación débil (~0.298).  
  - Sin UK: correlación fuertemente negativa (~ -0.875).  
- El negocio no depende del tamaño económico del país, sino de factores culturales, nichos o clientes estratégicos.  
- UK actuaba como outlier y ocultaba la relación real.

- PIB per cápita ↔ ticket medio
  - La regresión muestra una tendencia al alza débil: mayor PIB per cápita → ticket medio ligeramente mayor.  
  - La dispersión es alta → relación poco determinante.   

- Desempleo ↔ ventas
  - Correlación prácticamente nula (-0.05).  
  - El desempleo no influye en el volumen de ventas.

- Deuda pública ↔ ventas
  - Correlación nula (0.04).  
  - La deuda pública no explica el comportamiento de compra.

- Población ↔ ventas
  - Con UK: correlación ligeramente positiva (0.05).  
  - Sin UK: correlación negativa (-0.08).  
  - La población no explica el volumen de ventas.

- PIB per cápita ↔ ventas totales
  - Con UK: correlación nula (0.04).  
  - Sin UK: correlación débil positiva (0.30).  
  - El PIB per cápita no es un factor explicativo sólido del volumen de ventas.  
  - Otros factores (hábitos de consumo, cultura de compra, tipo de cliente, penetración del producto) tienen más peso.

---

### 🔍 Patrones encontrados
- Las ventas presentan un patrón estacional muy marcado.  
- Los meses con mayor volumen de ventas son septiembre, octubre y especialmente noviembre.  
- Tras noviembre, las ventas caen en diciembre y se mantienen bajas durante los primeros meses del año.  
- El negocio muestra un pico fuerte en otoño, probablemente vinculado a compras previas a Navidad.
- **Reino Unido** domina el mercado con +80% de las ventas

### Productos equilibrados (alto volumen + alto valor)
- **white hanging heart t-light holder**  
- **paper craft, little birdie**  
Ambos aparecen en el top de cantidad y en el top de ingresos → buena rotación y buen rendimiento económico.

### Producto muy vendido pero barato
- **world war 2 gliders asstd designs**  
Es el nº1 en cantidad vendida, pero no aparece en ingresos → producto de bajo precio y bajo impacto económico.

### Producto poco vendido pero caro
- **regency cakestand 3 tier**  
No está en el top de cantidad, pero es el nº1 en dinero generado → producto premium.

### ❌ Cancelaciones
- El porcentaje total de cancelaciones es muy bajo (~2.2%).  
- El porcentaje mensual es estable entre 1.5% y 3%.  
- Los meses con menos ventas (enero, diciembre, mayo) presentan más cancelaciones, posiblemente por devoluciones post-navidad.  
- Los meses de mayor actividad (septiembre–noviembre) tienen menos cancelaciones → mejor rendimiento operativo en picos de demanda.

### 🌍 Análisis por países (incluyendo UK)
- **United Kingdom** domina en volumen y valor → fuerte dependencia geográfica.  
- **France** actúa como mercado premium: genera mucho dinero con menos unidades.  
- **Netherlands, EIRE y Germany** son mercados secundarios pero estables.  
- Se identifican mercados de volumen, premium y equilibrados.

---

### 🌍 Análisis por países (sin UK)
- **EIRE y Netherlands** son los mercados más fuertes sin UK.  
- **France** sigue siendo mercado premium.  
- **Germany y Denmark** son mercados equilibrados.  
- **Australia, Sweden, Switzerland, Belgium y Spain** muestran bajo volumen y valor → mercados marginales.  
- Sin UK, los países que sostienen el negocio son EIRE, Netherlands, France y Germany.


### 👥 Mejores clientes
- 6 de los 10 mejores clientes son de **United Kingdom**, confirmando la dependencia geográfica.  
- Netherlands aporta un cliente muy potente (521k).  
- EIRE aporta dos clientes fuertes (300k y 265k).  


## 8. Visualización de los datos

En esta sección se presentan las principales visualizaciones obtenidas durante el análisis exploratorio, con el objetivo de identificar patrones relevantes en los datos.


### 📊 Grafico temporal de ventas

![analisis temporal de ventas](../proyecto-final/ecommerce-sales-analysis/images/img1.png)

---

### Productos mas vendidos y que más dinero generan

![productos](../proyecto-final/ecommerce-sales-analysis/images/img2.png)

---

### Cancelaciones en el tiempo

![Cancelaciones](../proyecto-final/ecommerce-sales-analysis/images/img3.png)

---

### Cantidad vendida y dinero generado por cada pais

![Paises](../proyecto-final/ecommerce-sales-analysis/images/img4.png)

---

### Facturacion por cliente

![clientes](../proyecto-final/ecommerce-sales-analysis/images/img5.png)

#### Relacion ticket medio con pib per capita

![relacion](../proyecto-final/ecommerce-sales-analysis/images/img6.png)

---


## 9. Conclusiones

El análisis permitió identificar los patrones clave del comportamiento de ventas entre 2009 y 2011, destacando la fuerte estacionalidad, la concentración del negocio en Reino Unido y la relevancia de ciertos productos en la demanda global. La integración con indicadores macroeconómicos mostró que los países con mayor PIB per cápita tienden a presentar tickets medios más altos, reforzando la relación entre capacidad económica y gasto.
En conjunto, el proyecto cumple su objetivo: ofrecer una visión completa, limpia y estructurada del negocio, apoyada en un dashboard interactivo que facilita la toma de decisiones basada en datos.

## 10. Autor

Alejandro Gálvez Beneroso