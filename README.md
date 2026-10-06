# Resumen_Ejecutivo_Ventas_Walmart
Sprint 2 | Proyecto 2: Resumen Ejecutivo de Ventas Walmart

## 📊 Introducción

En este proyecto asumí el rol de analista de datos para Walmart. El objetivo fue preparar un resumen ejecutivo que ayudara a la Dirección Comercial a evaluar posibles ajustes de presupuesto e inventario.

Trabajé con datos de ventas semanales correspondientes a 2012. Mi propósito fue limpiar, organizar y analizar la información para responder preguntas de negocio mediante indicadores clave, tablas dinámicas, visualizaciones y un dashboard interactivo.

El proyecto integró las siguientes capacidades:

- Limpieza y preparación de datos.
- Integración de tablas mediante funciones de búsqueda.
- Creación de indicadores de negocio.
- Construcción de tablas dinámicas.
- Diseño de un dashboard interactivo.
- Validación de calidad de datos.
- Comunicación ejecutiva mediante el método Contexto → Hallazgo → Implicación.

## 🎯 Preguntas de negocio

Durante el análisis busqué responder las siguientes preguntas:

1. ¿Qué departamentos fueron más eficientes para generar ventas durante 2012?
2. ¿Qué departamentos aportaron una mayor proporción de las ventas totales?
3. ¿Qué departamentos estuvieron por debajo de su potencial comercial?
4. ¿Dónde conviene priorizar inventario y presupuesto?

## 🗂️ Datasets utilizados

Trabajé con una tabla transaccional y dos tablas de referencia.

| Dataset | Tipo | Información principal |
| --- | --- | --- |
| `raw_ventas` | Tabla transaccional | Ventas semanales por tienda, departamento, fecha y condición de feriado. |
| `raw_departamento` | Tabla de referencia | Relación entre el código del departamento y su nombre. |
| `raw_tiendas` | Tabla de referencia | Tipo de tienda y tamaño en metros cuadrados. |

### Columnas principales

| Tabla | Columnas |
| --- | --- |
| `raw_ventas` | `tienda`, `dept`, `fecha`, `ventas_semanales`, `esferiado` |
| `raw_departamento` | `dept`, `nombre_dept` |
| `raw_tiendas` | `tienda`, `tipo`, `tamaño` |

## 🧮 KPIs del proyecto

Definí dos indicadores principales para evaluar la eficiencia y la participación de cada departamento.

### KPI 1: Ventas por metro cuadrado

Este indicador mide la eficiencia comercial del espacio físico:

```text
Ventas por m² = Ventas semanales / Tamaño de la tienda
```

Para construirlo, agrupé las ventas por departamento, calculé el promedio del tamaño y relacioné ambos valores.

Este KPI permite identificar qué departamentos generan más ventas en relación con el espacio que ocupan.

### KPI 2: Participación por departamento

Este indicador muestra qué proporción de las ventas totales representa cada departamento:

```text
Participación del departamento =
Ventas del departamento / Ventas totales
```

Este KPI permite identificar cuáles son los departamentos que más aportan al resultado general del negocio.

### Interpretación de los KPIs

| KPI | Qué mide | Utilidad para el negocio |
| --- | --- | --- |
| Ventas por m² | Eficiencia del espacio comercial. | Ayuda a evaluar inventario, distribución y productividad del espacio. |
| Participación por departamento | Peso relativo de cada departamento en las ventas. | Permite identificar los departamentos que más contribuyen al resultado total. |

## 🔄 Proceso de trabajo

Organicé el análisis en seis etapas principales:

| Etapa | Qué hice | Resultado |
| :---: | --- | --- |
| 1 | Limpié los datos. | Preparé una base consistente para el análisis. |
| 2 | Enriquecí la tabla de ventas. | Incorporé el nombre del departamento, tipo de tienda y tamaño. |
| 3 | Construí tablas dinámicas. | Calculé los dos KPIs por departamento. |
| 4 | Diseñé el dashboard. | Creé filtros, indicadores y gráficos interactivos. |
| 5 | Elaboré el resumen ejecutivo. | Organicé los hallazgos mediante el modelo C → F → I. |
| 6 | Realicé validaciones de calidad. | Documenté controles sobre ventas, tamaños y categorías. |

## 🧹 Paso 1: Limpieza de datos

Creé una copia de la tabla `raw_ventas` y la preparé en una hoja denominada `clean_ventas`.

Durante esta etapa:

- Revisé el formato de la columna `fecha`.
- Validé el formato monetario de `ventas_semanales`.
- Confirmé la consistencia de `tienda` y `dept`.
- Conservé la condición de feriado en `esferiado`.
- Creé la columna `semana_limpia` para facilitar el filtrado temporal.
- Enfocqué el análisis en los registros de 2012.

### Resultado esperado

La tabla limpia quedó organizada con las siguientes columnas:

| Columna |
| --- |
| `tienda` |
| `dept` |
| `fecha` |
| `ventas_semanales` |
| `esferiado` |
| `semana_limpia` |

## 🔗 Paso 2: Enriquecimiento de datos

Para poder calcular la eficiencia y generar reportes legibles, incorporé información de las tablas de referencia a `clean_ventas`.

Añadí las siguientes columnas:

- `tipo`
- `tamaño`
- `nombre_dept`

La tabla consolidada quedó estructurada así:

| `tienda` | `dept` | `fecha` | `ventas_semanales` | `esferiado` | `semana_limpia` | `tipo` | `tamaño` | `nombre_dept` |
| --- | --- | --- | ---: | --- | --- | --- | ---: | --- |

Utilicé funciones de búsqueda para relacionar las tablas:

### En inglés

```excel
=VLOOKUP(valor_buscado, rango_tabla, índice_columna, FALSE)
```

### En español

```excel
=BUSCARV(valor_buscado; rango_tabla; índice_columna; FALSO)
```

La clave fue conservar una relación correcta entre:

- `dept` y `nombre_dept`.
- `tienda` y sus características físicas.
- Las ventas y el tamaño de cada tienda.

## 📌 Paso 3: Tablas dinámicas

Construí tablas dinámicas para calcular cada KPI utilizando únicamente las ventas correspondientes a 2012.

### KPI 1: Ventas por metro cuadrado

Agrupé la información por `nombre_dept` y calculé:

- Suma de `ventas_semanales`.
- Promedio de `tamaño`.
- Ventas por metro cuadrado.

La tabla resultante contiene:

| `nombre_dept` | Ventas semanales | Tamaño promedio | Ventas por m² |
| --- | ---: | ---: | ---: |
| Departamento 1 | Monto | Monto | Monto |
| Departamento 2 | Monto | Monto | Monto |
| Departamento 3 | Monto | Monto | Monto |

La fórmula utilizada conceptualmente fue:

```text
Ventas por m² =
Suma de ventas_semanales / Promedio de tamaño
```

Filtré la columna `semana_limpia` para trabajar únicamente con el año 2012.

### KPI 2: Participación por departamento

Construí una tabla dinámica con las ventas de cada departamento expresadas como porcentaje del total.

| `nombre_dept` | Participación de ventas |
| --- | ---: |
| Despensa y Básicos | 15,23 % |
| Comida Fresca | 10,66 % |
| Otros departamentos | Porcentaje correspondiente |

La lógica utilizada fue:

```text
Participación =
Ventas del departamento / Ventas totales de 2012
```

## 📊 Paso 4: Dashboard

Construí un dashboard interactivo en una hoja independiente llamada `Dashboard`.

### Selector de departamento

Incorporé un menú desplegable para que el usuario pudiera seleccionar un departamento y consultar sus indicadores de manera dinámica.

La selección actualiza:

- Ventas por metro cuadrado.
- Participación del departamento.
- Gráficos relacionados con el departamento seleccionado.

### Fórmulas de búsqueda

Para traer los valores desde las tablas dinámicas utilicé:

```excel
=VLOOKUP(valor_buscado, rango_tabla, índice_columna, FALSE)
```

En español:

```excel
=BUSCARV(valor_buscado; rango_tabla; índice_columna; FALSO)
```

### Visualizaciones construidas

#### Ventas por metro cuadrado

Utilicé un gráfico de barras para comparar la eficiencia de los departamentos.

La lectura recomendada es ordenar los departamentos de mayor a menor para identificar rápidamente:

- Los departamentos con mayor eficiencia.
- Los departamentos que ocupan espacio, pero generan menos ventas por metro cuadrado.
- Las posibles oportunidades de reorganización de inventario.

#### Participación por departamento

Utilicé un gráfico de barras apiladas para visualizar la proporción que aporta cada departamento al total de ventas.

Este gráfico permite:

- Comparar la contribución relativa.
- Identificar los departamentos dominantes.
- Reconocer aquellos con baja participación.
- Analizar la composición general de las ventas.

### Formato condicional

Apliqué formato condicional para facilitar la lectura de los resultados.

Por ejemplo:

- Participaciones menores al 5 % pueden resaltarse en rojo.
- Valores intermedios pueden mostrarse en amarillo.
- Valores altos pueden resaltarse en verde.

El formato semáforo ayuda a que los stakeholders interpreten los resultados con rapidez.

## 📝 Paso 5: Resumen ejecutivo C → F → I

Organicé el resumen ejecutivo mediante el modelo:

- **Contexto**
- **Hallazgo**
- **Implicación**

### Pregunta 1: ¿Qué departamentos fueron más eficientes?

#### Contexto

Analicé las ventas semanales de 2012 y las relacioné con el tamaño promedio de las tiendas para calcular las ventas por metro cuadrado.

#### Hallazgo

Los departamentos con mayores ventas por metro cuadrado son los más eficientes en el uso del espacio comercial. El indicador permite comparar departamentos sin depender únicamente de sus ventas absolutas.

#### Implicación

La dirección puede priorizar inventario, visibilidad y espacio para los departamentos que produzcan más ventas por metro cuadrado, siempre contrastando el resultado con disponibilidad, rotación y margen.

### Pregunta 2: ¿Qué departamentos aportaron más al negocio?

#### Contexto

Calculé la participación porcentual de cada departamento sobre las ventas totales de 2012.

#### Hallazgo

Los departamentos con mayor participación representan una parte importante del resultado comercial. Sin embargo, una alta participación no significa automáticamente una mayor eficiencia por metro cuadrado.

#### Implicación

La dirección puede proteger la disponibilidad de los departamentos con mayor participación y, al mismo tiempo, investigar si los departamentos con menor participación tienen oportunidades de crecimiento.

## ✅ Paso 6: Validación de calidad

Documenté controles de calidad para comprobar que los resultados fueran confiables.

| Validación | Pregunta |
| --- | --- |
| Departamentos sin asignar | ¿Existen tiendas o registros sin departamento identificado? |
| Ventas inválidas | ¿Hay ventas negativas o nulas? |
| Tamaño de tienda | ¿Existen tiendas con tamaño igual a cero? |
| Fechas | ¿Todas las fechas tienen formato válido? |
| Periodo | ¿El dashboard está filtrado correctamente para 2012? |
| Relaciones | ¿Las búsquedas incorporaron correctamente tipo, tamaño y nombre de departamento? |
| KPIs | ¿Las fórmulas coinciden con las tablas dinámicas? |
| Dashboard | ¿Los filtros actualizan los indicadores y los gráficos? |

### Importancia de QA

La validación fue necesaria para asegurar que:

- Las ventas por metro cuadrado no utilizaran tamaños iguales a cero.
- La participación departamental tuviera un denominador consistente.
- Los nombres de departamentos fueran comparables.
- Las fechas no mezclaran periodos distintos.
- Las tablas dinámicas alimentaran correctamente el dashboard.
- Los resultados pudieran rastrearse hasta la tabla consolidada.

## 📁 Estructura final del archivo

El archivo de trabajo quedó organizado con las siguientes hojas:

| Hoja | Propósito |
| --- | --- |
| `README` | Documentación, objetivo, KPIs y validaciones. |
| `raw_ventas` | Datos originales de ventas semanales. |
| `raw_departamento` | Catálogo original de departamentos. |
| `raw_tiendas` | Información original de tiendas y tamaños. |
| `clean_ventas` | Tabla limpia y enriquecida. |
| `Pivot` | Cálculo de los dos KPIs por departamento. |
| `Dashboard` | Visualizaciones, filtros e indicadores dinámicos. |
| `Resumen` | Hallazgos y recomendaciones mediante C → F → I. |

## 📦 Lista de comprobación final

Antes de entregar el proyecto, verifiqué que el archivo incluyera:

- [x] Hoja `README` completa.
- [x] Objetivo y contexto del negocio.
- [x] Tablas originales.
- [x] Tabla `clean_ventas` consolidada.
- [x] Tabla dinámica de ventas por metro cuadrado.
- [x] Tabla dinámica de participación por departamento.
- [x] Dashboard con filtro por departamento.
- [x] KPI dinámico de ventas por metro cuadrado.
- [x] KPI dinámico de participación.
- [x] Gráfico de barras de eficiencia.
- [x] Gráfico de participación departamental.
- [x] Resumen ejecutivo C → F → I.
- [x] Validaciones de calidad documentadas.
- [x] Copia de seguridad del archivo final.

## 💭 Reflexión final

Este proyecto me permitió integrar habilidades esenciales de análisis de datos:

- Preparé datos desde las tablas originales.
- Enriquecí la información mediante relaciones entre fuentes.
- Construí KPIs para evaluar eficiencia y participación.
- Diseñé un dashboard interactivo.
- Utilicé tablas dinámicas como fuente de los indicadores.
- Apliqué validaciones de calidad.
- Tradují los resultados en recomendaciones ejecutivas.

La principal enseñanza fue que una buena decisión comercial no depende de un único indicador. Las ventas totales muestran la magnitud del negocio, mientras que las ventas por metro cuadrado permiten evaluar la eficiencia del espacio y la participación por departamento ayuda a comprender la contribución relativa.

Con este proyecto fortalecí mi capacidad para transformar datos operativos en información útil para la asignación de inventario, presupuesto y espacio comercial.
