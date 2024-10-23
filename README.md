<h1 align='center'>
<b>Proyecto Individual 2 - Análisis y Visualización de Datos </b>
</h1>

![Portada](img/portada.png)

## Descripcion General
A contInuación se presenta un proyecto de análisis de datos desarrollado a partir de un dataset sobre homicidios en siniestros viales que tuvieron lugar en la Ciudad Autónoma de Buenos Aires durante el periodo 2016-2021. Para este llevó a cabo un proceso de limpieza, transformación y normalización de datos para proceder a realizar un analisis exploratorio de datos y posteriormente un analisis exhaustivo de la problematica. Para finalizar, se realizó un dashboard explicativo en PowerBI en el cual se presentaron las conclusiones que se lograron extraer.

## Tabla de Contenido
1. Descripción de la Estructura de Datos<br>
    1.1. Datos en bruto <br>
    1.2. Datos finales<br>
2. Estructura del Proyecto<br>
    2.1. Carpetas <br>
    2.2. Notebooks<br>
    2.3. Archivos adicionales <br>
3. Contexto del Problema <br>
4. Objetivos <br>
5. Metodología<br>
6. Resultados <br>
    6.1. KPI's <br>
7. Conclusiones <br>
8. Recomendacciones <br>
9. Herramientas implementadas <br>
10. Uso y Ejecucion <br>
11. Disclaimer <br>


## Descripción de la Estructura de Datos

### Datos en bruto

Para este analisis se contó con 2 archivos que se encuentraban en formato xlsx: 
- [**homicidios.xlsx:**](Archivos%20Origen/homicidios.xlsx) El archivo con los datos a tratar, contiene dos hojas llamadas: hechos y víctimas.
- [**Diccionario de datos Siniestros viales.xlsx:**](Archivos%20Origen/Diccionario%20de%20datos%20Siniestros%20viales.xlsx) Es un archivo con el diccionario de datos para las dos tablas que se van a trabajar que sirve de guía para un mayor entendimiento de la data.

Las dos tablas con las que se inició el proyecto con las siguientes.

#### Hechos
Esta tabla contiene la informacion correspondiente a cada siniestro vial: fecha, ubicacion, numerode victimas y tipo de victima y acusado.

![hechos_in](img/hechos_in.png)
#### Victimas
Contiene la informacion de cada victima mortal (sexo, edad, tipo de victima, etc) y un indice que indica el siniestro en el cual falleció.

![victimas_in](img/victimas_in.png)
### Datos procesados
Una vez se realizó todo el proceso de ETL el analisis exploratorio de datos se realizó con las tablas que se explican a continuacion.

#### Hechos
![hechos_a](img/hechos_a.png)

1. **ID** - string <br> &emsp; Identificador unico del siniestro
2. **N_VICTIMAS** - int <br> &emsp; Cantidad de victimas mortales
3. **AÑO** - int <br> &emsp; Año del siniestro
4. **MES** - int <br> &emsp; Mes del siniestro
5. **DIA_SEMANA** - int <br> &emsp; Dia de la semana del siniestro
6. **DIA_SEMANA_NOM** - string <br> &emsp; Nombre del dia de la semana del siniestro
7. **HORA** - float <br> &emsp; Hora del siniestro
8. **TIPO_CALLE** - string <br> &emsp; Tipo de arteria (en el caso de intersecciones a nivel se clasifica según la de mayor jerarquía)
9. **VIAS_INVOL** - list <br> &emsp; Vias involucradas en el siniestro (la principal y el cruce en el caso de intersecciones a nivel)
10. **INTERSECCION** - int <br> &emsp; Indicador de si el siniestro ocurrió en una interseccion a nivel (1: Si, 0: No)
11. **COMUNA** - int <br> &emsp; Comuna de la ciudad en la que ocurrió el siniestro (1 a 15)
12. **PARTICIPANTES** - string <br> &emsp; Conjunción de víctima y acusado
13. **VICTIMA** - string <br> &emsp; Vehículo que ocupaba quien haya fallecido a se haya lastimado a raíz del hecho, o bien peatón/a. Clasificación agregada del tipo de vehículos. <br>
    - PEATON: Víctima distinta de cualquier ocupante de un vehículo, ya sea un conductor/a o un pasajero/a. Se incluyen los ocupantes o personas que empujan o arrastran un coche de bebé o una silla de ruedas o cualquier otro vehículo sin motor de pequeñas dimensiones. Se incluyen también las personas que caminan empujando una bicicleta o un ciclomotor.
    - MOTO: Vehículo a motor no carrozado que incluye motocicleta, ciclomotor y cuatriciclo.
    - AUTO: Vehículo a motor destinado al transporte de personas, diferente de los motovehículos, y que tenga hasta nueve plazas (incluyendo al asiento del conductor) (Sedan, SUV, coupe, etc)
    - CARGAS: Vehículo a motor destiando al transporte de cargas, incluye camiones pesados (con o sin acoplado o semirremolque, etc., camión de recolección de residuos) y livianos (utilitarios, furgonetas, pick-ups, camioneta con caja de carga).
    - BICICLETA: Vehículo con al menos dos ruedas, que generalmente es accionado por el esfuerzo muscular de las personas que lo ocupan, en particular mediante pedales o manivelas. Incluye bicicletas de pedaleo asistido y/o con motor
    - PASAJEROS: Personas lesionadas que se encuentran dentro, descendiendo o ascendiendo de las unidades de autotrasporte público de pasajeros/as y ómnibus de larga distancia
    - MOVIL: Vehículos de emergencia: móviles policiales, ambulancias, autobombas. 
    - OTRO: Otros vehículos
14. **ACUSADO** - string <br> &emsp; Vehículo que ocupaba quien resultó acusado/a del hecho, sin implicar culpabilidad legal <br>
    - AUTO: Vehículo a motor destinado al transporte de personas, diferente de los motovehículos, y que tenga hasta nueve plazas (incluyendo al asiento del conductor) (Sedan, SUV, coupe, etc)
    - BICICLETA: Vehículo con al menos dos ruedas, que generalmente es accionado por el esfuerzo muscular de las personas que lo ocupan, en particular mediante pedales o manivelas. Incluye bicicletas de pedaleo asistido y/o con motor
    - CARGAS: Vehículo a motor destiando al transporte de cargas, incluye camiones pesados (con o sin acoplado o semirremolque, etc., camión de recolección de residuos) y livianos (utilitarios, furgonetas, pick-ups, camioneta con caja de carga).
    - MOTO: Vehículo a motor no carrozado que incluye motocicleta, ciclomotor y cuatriciclo.
    - OBJETO FIJO: Colisión contra objetos inmóviles fijados de manera permanente o semipermanente (columna, árbol, semáforo, etc.) o pérdidas de equilibrio de vehículos de dos ruedas que desencadenen la caída de sus ocupantes.
    - PASAJEROS: Personas lesionadas que se encuentran dentro, descendiendo o ascendiendo de las unidades de autotrasporte público de pasajeros/as y ómnibus de larga distancia
    - TREN: Equipo móvil que se desplaza exclusivamente sobre rieles
    - OTRO: Otros vehículos
15. **LONGITUD** - float <br> &emsp; Longitud del lugar donde ocurrió el siniestro
16. **LATITUD** - float <br> &emsp; Latitud del lugar donde ocurrió el siniestro

#### Victimas
![victimas_a](img/victimas_a.png)

1. **ID** - string <br> &emsp; Identificador unico del siniestro
2. **AÑO** - string <br> &emsp; Año del siniestro
3. **MES** - string <br> &emsp; Mes del siniestro
4. **DIA_SEMANA** - string <br> &emsp; Dia de la semana del siniestro
5. **ROL** - string <br> &emsp; Posición relativa al vehículo que presentaba la víctima en el momento del siniestro <br>
    - CONDUCTOR
    - PEATON
    - PASAJERO_ACOMPAÑANTE
    - CICLISTA
6. **VICTIMA** - string <br> &emsp; Vehículo que ocupaba quien haya fallecido a se haya lastimado a raíz del hecho, o bien peatón/a. Clasificación agregada del tipo de vehículos. <br>
    - MOTO: Vehículo a motor no carrozado que incluye motocicleta, ciclomotor y cuatriciclo.
    - PEATON: Víctima distinta de cualquier ocupante de un vehículo, ya sea un conductor/a o un pasajero/a. Se incluyen los ocupantes o personas que empujan o arrastran un coche de bebé o una silla de ruedas o cualquier otro vehículo sin motor de pequeñas dimensiones. Se incluyen también las personas que caminan empujando una bicicleta o un ciclomotor.
    - AUTO: Vehículo a motor destinado al transporte de personas, diferente de los motovehículos, y que tenga hasta nueve plazas (incluyendo al asiento del conductor) (Sedan, SUV, coupe, etc)
    - BICICLETA: Vehículo con al menos dos ruedas, que generalmente es accionado por el esfuerzo muscular de las personas que lo ocupan, en particular mediante pedales o manivelas. Incluye bicicletas de pedaleo asistido y/o con motor
    - CARGAS: Vehículo a motor destiando al transporte de cargas, incluye camiones pesados (con o sin acoplado o semirremolque, etc., camión de recolección de residuos) y livianos (utilitarios, furgonetas, pick-ups, camioneta con caja de carga).
    - PASAJEROS: Personas lesionadas que se encuentran dentro, descendiendo o ascendiendo de las unidades de autotrasporte público de pasajeros/as y ómnibus de larga distancia
    - MOVIL: Vehículos de emergencia: móviles policiales, ambulancias, autobombas. 
8. **SEXO** - string <br> &emsp; Sexo informado por fuente policial de la víctima
9. **EDAD** - string <br> &emsp; Edad de la víctima al momento del siniestro

## Estructura del Proyecto

### Carpetas
- **[Archivos Finales:](Archivos%20Finales)** Contiene los archivos procesados que se cargaron en PowerBI
- **[Archivos Origen:](Archivos%20Origen)** Contiene los archivos originales que fueron dados para realizar el proyecto y el archivo con la iformacion poblacional de la ciudad.
### Notebooks
- **[ETL_EDA_hechos:](ETL_EDA_hechos.ipynb)** Contiene toda la parte de extraccion, transformacion de los datos y el Analisis Exploratorio de Datos de la tabla *HECHOS*
- **[ETL_EDA_victimas:](ETL_EDA_victimas.ipynb)** Contiene toda la parte de extraccion, transformacion de los datos y el Analisis Exploratorio de Datos de la tabla *VICTIMAS*
- **[tablas_KPIs:](tablas_KPIs.ipynb)** En este notebook se realizó la sintesis de la informacion de las tablas y la union con la informacion poblacional para crear dataset que hicieran mas sencillo el calculo del los KPIs
### Archivos adicionales
- **[Dashboard:](Dashboard.pbix)** Contiene el dashboard explicativo con las conclusiones e informacion importante del analisis
- **[requirements.txt:](requirements.txt)** Es el archivo donde se encuentran todas las librerias y versiones necesarias para ejecuar el proyecto desde un entorno virtual

## Contexto del Problema

## Objetivos
   - Generar información que le permita a las autoridades locales tomar medidas para disminuir la cantidad de víctimas fatales de los siniestros viales

## Metodologia

## Resultados

### KPI's
   - **Tasa de homicidios en siniestros viales:** Número de víctimas fatales en accidentes de tránsito por cada 100,000 habitantes en un área geográfica
       durante un período de tiempo específico.<br>
   - **Cantidad de accidentes mortales de motociclistas en siniestros viales:** Número absoluto de accidentes fatales en los que estuvieron involucradas
   víctimas que viajaban en moto en un determinado periodo temporal.<br>

## Conclusiones

## Recomendaciones

## Herramientas empleadas

### Python

#### Librerias instaladas

### PowerBI

## Uso y Ejecucion

## Disclaimer
Este proyecto se realizó como parte del metodo educativo propuesto por la academia de educación en tecnología **Soy Henry** en la carrera de **Data Science**. 
Se quiere aclarar y remarcar que el proyecto se desarrollo con el objetivo de realizar proyectos que simulen un entorno laboral, en el cual se trabajen diversas 
temáticas ajustadas a la realidad. Henry no alienta ni tampoco recomienda a los alumnos y/o cualquier persona leyendo los repositorios (y entregas de proyectos) 
que tomen acciones en base a los datos que pudieran o no haber recabado. Toda la información expuesta y resultados obtenidos en los proyectos nunca deben ser 
tomados en cuenta para la toma real de decisiones (especialmente en la temática de finanzas, salud, política, etc.).

## Autor

Carolina Cardenas - Contacto: [LinkedIn](https://www.linkedin.com/in/carolina-cardenas-gutierrez-b3b25114b/)
