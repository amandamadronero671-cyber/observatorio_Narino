# 🇨🇴 Observatorio Departamental de Actividad Económica y Social

Aplicación interactiva construida con **Gradio** y **Plotly** que permite explorar indicadores oficiales de los departamentos de Colombia a partir de fuentes públicas de datos.gov.co.

## Características

- Carga automática de datos oficiales desde APIs SODA de datos.gov.co
- Normalización robusta de nombres de departamentos (sin tildes, mayúsculas/minúsculas)
- Filtros por departamento(s), indicador y rango de años
- Estadísticas descriptivas (media, mediana, desviación, min, max)
- Gráfico de tendencias (líneas)
- Gráfico de barras comparativas (Top 15)
- Tabla de datos filtrados

## Indicadores disponibles

| Indicador | Fuente | Descripción |
|-----------|--------|-------------|
| **PIB (miles de millones, constantes 2015)** | datos.gov.co/kgyi-qc7j | PIB total por departamento (precios constantes 2015) |
| **Homicidios (víctimas)** | MinDefensa / m8fd-ahd9 | Número de víctimas de homicidio |
| **Recursos públicos DNP (COP)** | DNP / wc86-9j4a | Recursos públicos asignados |

## Requisitos

- Python 3.9 o superior
- Conexión a internet (para descargar los datos en tiempo de ejecución)

## Instalación

```bash
# 1. Clonar o descargar el repositorio
# 2. Crear entorno virtual (recomendado)
python -m venv venv
source venv/bin/activate        # Linux/Mac
# venv\Scripts\activate         # Windows

# 3. Instalar dependencias
pip install -r requirements.txt
```

## Uso

```bash
python observatorio_nariñoipynb.py
```

La aplicación se abrirá en el navegador (por defecto en `http://127.0.0.1:7860`) y generará un enlace público (`share=True`) si se desea compartir.

### Interfaz

1. Selecciona uno o varios **departamentos** (o "Todos").
2. Elige el **indicador** de interés.
3. Ajusta el **rango de años**.
4. Selecciona el **año** para el gráfico de barras.
5. Haz clic en **Actualizar análisis**.

## Estructura del código

```
observatorio_nariñoipynb.py
├── Normalización de departamentos (quitar_tildes + diccionario canónico)
├── Carga de datos
│   ├── cargar_pib()
│   ├── cargar_homicidios()
│   └── cargar_dnp()
├── construir_maestro()          # Une todas las fuentes
├── Funciones de análisis
│   ├── filtrar()
│   ├── stats()
│   ├── tendencia()
│   └── barras()
└── Interfaz Gradio (Blocks)
```

## Fuentes de datos

Todos los datos se obtienen en tiempo real desde:

- [PIB por departamento](https://www.datos.gov.co/resource/kgyi-qc7j.json)
- [Homicidios](https://www.datos.gov.co/resource/m8fd-ahd9.json)
- [Recursos DNP](https://www.datos.gov.co/resource/wc86-9j4a.json)

> **Nota:** Los datos no se inventan ni se modifican. Solo se normalizan nombres de departamentos y se agregan por año.

## Dependencias principales

Ver archivo `requirements.txt`:

- `gradio` – Interfaz web
- `plotly` – Visualizaciones interactivas
- `pandas` / `numpy` – Manipulación de datos
- `requests` – Consumo de APIs

## Licencia

Código de ejemplo para uso educativo y de análisis. Los datos pertenecen a las entidades oficiales de Colombia (DANE, MinDefensa, DNP).
