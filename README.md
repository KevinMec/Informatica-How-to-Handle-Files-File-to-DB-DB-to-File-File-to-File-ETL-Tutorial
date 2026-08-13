🚀 Proyecto ETL: Procesamiento y Transformación de Archivos Planos con Informatica PowerCenter



📝 Descripción del Proyecto
Este proyecto demuestra la implementación de un flujo de trabajo ETL (Extract, Transform, Load) integral utilizando Informatica PowerCenter. El objetivo principal fue diseñar, configurar y automatizar la integración de datos entre diferentes sistemas de almacenamiento, manejando conversiones complejas entre archivos planos (Flat Files) y bases de datos relacionales [00:52].

El desarrollo abarca tres escenarios de negocio reales, aplicando transformaciones de limpieza y filtrado de datos para garantizar la integridad de la información en los sistemas de destino.

🛠️ Tecnologías y Herramientas Utilizadas
ETL Tool: Informatica PowerCenter (Source Analyzer, Target Designer, Mapping Designer, Workflow Manager & Monitor)

Bases de Datos: Relacionales (Oracle / SQL)

Tipos de Origen/Destino: Archivos Planos (CSV, DAT, TXT) delimitados por coma, pipe (|), tabuladores y tilde (~).

Transformaciones Aplicadas: Filter Transformation.

⚙️ Arquitectura y Escenarios de Integración (Paso a Paso)
Escenario 1: Ingesta de Archivo Plano a Base de Datos Relacional (File to DB)
Se implementó un pipeline para leer datos estructurados desde un archivo separado por comas (CSV) y cargarlos en una tabla de base de datos relacional.

Configuración del Origen: Se importó el archivo fuente employees_src_files.csv hacia el Source Analyzer [13:28]. Se ajustaron los metadatos y se optimizó la precisión de los tipos de datos (por ejemplo, extendiendo variables String a 255 caracteres y Numbers a 20) para evitar problemas de truncamiento durante la carga de strings y espacios nulos [15:39].

Generación Dinámica del Destino: En lugar de crear la tabla manualmente en el motor de base de datos, se utilizó el Target Designer para generar y ejecutar la sentencia SQL CREATE TABLE directamente desde la herramienta hacia el esquema destino [20:04].

Mapeo y Ejecución: Se desarrolló el Mapping vinculando el File Reader con el Relational Writer y se ejecutó la sesión en el Workflow Manager, logrando la inserción exitosa del lote de registros en la base de datos [28:05].

Escenario 2: Extracción de Base de Datos a Archivo Plano (DB to File)
Se diseñó un flujo inverso para consultar una tabla transaccional y generar un reporte en formato de archivo de texto con un delimitador personalizado.

Definición de Origen y Destino: Se extrajo la metadata de la tabla products desde la base de datos como fuente [30:08]. Posteriormente, se diseñó un Target tipo Flat File especificando el carácter Pipe (|) como delimitador [32:26].

Lógica de Transformación: Se integró un Filter Transformation para aislar un subconjunto de datos crítico. Utilizando la sintaxis nativa de la herramienta, se aplicó la condición IN(Product_ID, 50, 150, 200, 28) para filtrar y dar paso únicamente a los productos requeridos [35:16].

Generación de Archivo: Se configuraron las propiedades de la sesión para incluir los nombres de las columnas como encabezados (Headers) en el archivo de salida (products.out). Tras ejecutar el workflow, el motor generó automáticamente el archivo físico en el directorio del servidor /TgtFiles con los registros exactos [45:42].

Escenario 3: Procesamiento y Transformación de Archivo a Archivo (File to File)
Implementación de un proceso de transformación puramente basado en archivos, consumiendo un archivo de texto original y exportando a un formato estructurado con nueva delimitación.

Configuración de Origen: Importación del archivo fuente insurance.dat, validando el reconocimiento correcto del delimitador original (espacio/tabulación) [47:42].

Configuración de Destino: Creación de un target dinámico configurado para delimitar los campos de salida mediante el carácter tilde (~) [50:43].

Filtrado Avanzado: Se aplicó un Filter Transformation con una condición compuesta rigurosa para depurar registros: Location = 'hyderabad' AND Employee_ID > 50 [52:56].

Carga Exitosa: El flujo se ejecutó leyendo la totalidad del archivo y aplicando las reglas de negocio en memoria, escribiendo exitosamente el subconjunto de registros depurados en el archivo y directorio de salida final [57:03].

📈 Impacto y Resultados del Proyecto
Automatización DDL ETL: Se eliminó la necesidad de rutinas de creación de tablas manuales (DDL), integrando la ejecución SQL directamente en el flujo del proceso de mapeo.

Flexibilidad de Formatos: Se demostró un alto nivel de dominio en la configuración de componentes File Readers y File Writers, manejando múltiples codificaciones y delimitadores complejos (comas, pipes, tabulaciones y tildes).

Calidad y Lógica de Datos: La implementación de transformaciones de filtrado condicional aseguró que solo la información relevante, estructurada y validada llegara a las capas analíticas y archivos de salida.

Nota: Este repositorio incluye una descripción de los mappings, configuración de los flujos de trabajo (Workflows) y los metadatos exportados como evidencia técnica de las integraciones desarrolladas.
