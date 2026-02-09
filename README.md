Data Cleaning Documentation – Manager Survey

Este repositorio documenta el proceso de limpieza, estandarización y modelado de la base de datos Ask A Manager Salary Survey 2021, con el objetivo de obtener un conjunto de datos consistente y listo para análisis.

1. Variables en la base de datos original

En esta sección se describen las variables tal como aparecen en la base original.
Los nombres se mantienen en inglés para facilitar la trazabilidad con el dataset fuente, mientras que las descripciones están en español.

Variable original	Tipo	Descripción
Timestamp	Fecha / datetime	Fecha y hora en la que el encuestado diligenció el formulario.
How old are you?	Texto	Edad reportada por la persona encuestada.
What industry do you work in?	Texto	Industria o sector económico en el que trabaja la persona.
Job title	Texto	Cargo o título del puesto de trabajo actual.
If your job title needs additional context, please clarify here:	Texto	Información adicional o aclaración sobre el cargo cuando el título no es suficiente.
What is your annual salary? (...)	Numérico (entero)	Salario anual bruto reportado, en la moneda indicada posteriormente.
How much additional monetary compensation do you get, if any (...)	Numérico (decimal)	Compensaciones adicionales como bonos u horas extra en un año promedio.
Please indicate the currency	Texto	Moneda en la que se reportan salario y compensaciones.
If "Other," please indicate the currency here:	Texto	Detalle de la moneda cuando no se encuentra en las opciones estándar.
If your income needs additional context, please provide it here:	Texto	Comentarios adicionales sobre el ingreso reportado.
What country do you work in?	Texto	País en el que trabaja la persona.
If you're in the U.S., what state do you work in?	Texto	Estado dentro de EE. UU. donde trabaja la persona, si aplica.
What city do you work in?	Texto	Ciudad en la que trabaja la persona.
How many years of professional work experience do you have overall?	Texto	Años totales de experiencia laboral profesional.
How many years of professional work experience do you have in your field?	Texto	Años de experiencia profesional en su campo.
What is your highest level of education completed?	Texto	Nivel educativo más alto alcanzado.
What is your gender?	Texto	Género con el que se identifica la persona.
What is your race? (Choose all that apply.)	Texto	Raza o etnia reportada; puede contener múltiples valores.

2. Variables luego del data cleaning

Luego del proceso de limpieza y modelado, se decidió mantener los nombres de las variables en inglés por consistencia técnica. Las nuevas variables permiten análisis comparables y estandarizados.

Variable modelada	Tipo	Descripción
timestamp	Fecha / datetime	Fecha y hora de registro de la encuesta, sin modificaciones.
age	Texto	Edad reportada; se mantiene como texto por la heterogeneidad de formatos.
industry	Texto	Industria luego de limpieza básica de texto.
job_title	Texto	Cargo o título del puesto estandarizado.
job_title_context	Texto	Información adicional sobre el cargo.
annual_salary	Numérica	Salario anual bruto en la moneda indicada en currency.
bonus_compensation	Numérica	Compensaciones adicionales anuales.
currency	Texto	Moneda del salario y compensaciones.
income_context	Texto	Comentarios adicionales sobre el ingreso.
country	Texto	País reportado originalmente, sin estandarizar.
state	Texto	Estado o división administrativa (cuando aplica).
city	Texto	Ciudad reportada originalmente.
years_experience_total	Texto	Años totales de experiencia profesional.
years_experience_field	Texto	Años de experiencia en el campo laboral.
education_level	Texto	Nivel educativo más alto alcanzado.
gender	Texto	Género reportado por la persona.
race	Texto	Raza o etnia reportada.
country_standardized	Texto	País estandarizado (por ejemplo, variantes de USA → United States).
city_clean	Texto	Ciudad limpiada eliminando valores inválidos y caracteres especiales.
salario_anual_cop	Numérica	Salario anual convertido a Pesos Colombianos (COP).
compensaciones_cop	Numérica	Compensaciones convertidas a Pesos Colombianos (COP).
total_compensacion_cop	Numérica	Suma del salario anual y compensaciones en COP.

3. Paso a paso para actualizar los datos y aplicar el modelado

Este procedimiento permite que cualquier persona pueda replicar el proceso de limpieza y modelado.
Para esta implementación se utilizó Python y la librería Pandas, aunque el proceso puede adaptarse a Excel, Power Query, SQL u otras herramientas.

1. Descargar el archivo

Descargar la base Ask A Manager Salary Survey 2021 desde AskAManager.org:
https://docs.google.com/spreadsheets/d/1IPS5dBSGtwYVbjsfbaMCYIWnOuRmJcbequohNxCyGVw

2. Cargar los datos

Importar el archivo en la herramienta seleccionada para la limpieza de datos.

3. Renombrar columnas

Aplicar un diccionario de renombramiento para simplificar y estandarizar los nombres de las variables.

4. Limpieza de variables de texto

Limpiar las columnas de país y ciudad eliminando:

Espacios extra

Caracteres especiales

Emojis

Respuestas no geográficas

Estandarizar países usando reglas predefinidas (ejemplo: todas las variantes de USA → United States).

5. Filtrar el archivo

Mantener únicamente los registros que:

Tengan salarios reportados en USD

Correspondan al país United States

6. Conversión de variables monetarias

Definir la tasa de cambio USD → COP correspondiente al día del ejercicio.

Convertir salario anual y compensaciones a Pesos Colombianos.

7. Creación de variables derivadas

Crear:

salario_anual_cop

compensaciones_cop

Crear total_compensacion_cop como la suma de ambas.

8. Validaciones finales

Revisar valores nulos.

Verificar rangos de salarios.

Confirmar coherencia en las conversiones monetarias.

9. Guardar la base modelada

Exportar el dataset final en formato .xlsx para análisis o visualización.

10. Subir los archivos al repositorio de GitHub

Verificar que el repositorio local esté conectado al repositorio remoto:
https://github.com/lucasduenas/viz_storytelling

Agregar los archivos actualizados:

git add .


Realizar un commit descriptivo:

git commit -m "Actualización de datos y data cleaning"


Subir los cambios:

git push



