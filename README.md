# Análisis de Delitos en la Ciudad de México (CDMX)

Un proyecto de análisis de datos centrado en examinar la incidencia delictiva en la capital mexicana durante el año 2024. Este repositorio contiene el proceso de integración, limpieza y transformación de datos públicos para extraer *insights* valiosos sobre patrones criminales y seguridad urbana.

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)

---

## 📋 Tabla de Contenidos
1. [Descripción del Proyecto](#-descripción-del-proyecto)
2. [Datos](#-datos)
3. [Flujo de Trabajo (Data Pipeline)](#-flujo-de-trabajo-data-pipeline)
4. [Estructura del Proyecto](#-estructura-del-proyecto)
5. [Autores](#-autores)

---

## Descripción del Proyecto

La CDMX enfrenta desafíos significativos en materia de seguridad pública. Este estudio cuantitativo busca transformar datos crudos en información accionable para entender patrones temporales, identificar zonas de mayor riesgo y evaluar los tipos de delitos predominantes. 

El objetivo de este preprocesamiento es preparar un conjunto de datos robusto que permita aportar a la toma de decisiones informada, contribuyendo al debate sobre cómo reducir la criminalidad.

---

## Datos

Los datos utilizados corresponden al año **2024** y fueron obtenidos del portal de transparencia de la **Fiscalía General de Justicia de la CDMX** (FGJCDMX).

Se utilizan dos conjuntos de datos principales:
- `delitos.csv`: Contiene información sobre las carpetas de investigación, ubicación geoespacial (coordenadas), fecha, hora, tipo y modalidad del delito.
- `victimas.csv`: Aporta información demográfica clave, como el sexo y la edad de las personas afectadas por los ilícitos.

---

## Flujo de Trabajo (Data Pipeline)

El *notebook* documenta un proceso exhaustivo de limpieza y manipulación de datos utilizando **Pandas**:

1. **Integración de Datos:** - Fusión (*Inner Join*) de los registros de delitos y víctimas mediante sus identificadores únicos (`ID_CI` y `ID_AP`).
2. **Limpieza y Estandarización:**
   - Eliminación de miles de registros completamente duplicados.
   - Filtrado de registros sin información geoespacial válida (`COORD X` y `COORD Y`) para garantizar un correcto análisis espacial futuro.
   - Normalización de las variables `SEXO` y `EDAD` (unificando categorías redundantes y valores nulos bajo la etiqueta "No Especificado").
3. **Ingeniería de Características (Feature Engineering):**
   - Extracción de componentes temporales a partir de la fecha del siniestro: `DIA` de la semana, `DIA_NUM` y `MES`.
   - Discretización de la variable numérica `EDAD` en una nueva columna categórica llamada `EDAD_Rango`, segmentando a las víctimas por etapas de desarrollo (Primeros años, Niñez, Adolescencia, Juventud, Adulto, Adulto mayor).
4. **Exportación:**
   - El resultado final se exporta como un archivo consolidado (`delitos_cdmx_limpio.xlsx`), listo para ser consumido en herramientas de *Business Intelligence* (Power BI/Tableau) o modelos predictivos.

---

## Uso y Requisitos

Para reproducir este análisis, necesitas tener instalado Python y las siguientes librerías:

```bash
pip install pandas numpy matplotlib openpyxl
