## CONICET InCites 2019 - 2023

### Tabla 1. Documentos publicados por año - CONICET - 2019/2023

La Tabla 1 muestra la cantidad de Documentos publicados por CONICET durante el periodo 2019 - 2023. Se aplica el siguiente código sobre el dataser WOS_documents.csv y los datos son coincidentes con los mostrados en HTML dentro de la web de InCites. También, se evidencia un valor de NA con 10 cantidades asignadas. 

```r
# Cargar las librerías necesarias
library(dplyr)
library(readr)

# Leer el archivo CSV
datos <- read_csv("C:/path/.../WOS_documents.csv")

# Agrupar los datos por el campo 'Publication Date' y contar las publicaciones por año
publicaciones_por_año <- datos %>%
  group_by(`Publication Date`) %>%
  summarise(Cantidad_de_Publicaciones = n())

# Ver el resultado
print(publicaciones_por_año)

```

![Tabla completa 1](/images/Tabla_completa_1.jpg)

### Tabla 2. % de documentos citados por año - CONICET - 2019/2023

```r
# Cargar las librerías necesarias
library(dplyr)
library(readr)

# Leer el archivo CSV
datos <- read_csv("C:/path/.../WOS_documents.csv")

# Agregar una nueva columna que indica si el documento ha sido citado al menos una vez
datos <- datos %>%
  mutate(Citado = ifelse(`Times Cited` > 0, 1, 0))

# Agrupar los datos por 'Publication Date' y calcular el porcentaje de documentos citados por año
porcentaje_citados_por_año <- datos %>%
  group_by(`Publication Date`) %>%
  summarise(Porcentaje_Citados = mean(Citado, na.rm = TRUE) * 100)

# Imprimir el resultado
print(porcentaje_citados_por_año)

```
![Tabla completa 2](/images/Tabla_completa_2.jpg)

### Impacto. Número y % de publicaciones en primer cuartil del Journal Citation Rank (JCR) (Q1)

```r
# Cargar las librerías necesarias
library(dplyr)
library(readr)

# Leer el archivo CSV
datos <- read_csv("C:/path/.../WOS_Publication_Sources.csv")

# Asegurarse de que 'Web of Science Documents' es un número
datos$`Web of Science Documents` <- as.numeric(datos$`Web of Science Documents`)

# Filtrar publicaciones en el primer cuartil (Q1)
publicaciones_Q1 <- datos %>%
  filter(`JCI Quartile` == "Q1")

# Calcular el número total de publicaciones en Q1 sumando 'Web of Science Documents', ignorando NA
numero_total_documentos_Q1 <- sum(publicaciones_Q1$`Web of Science Documents`, na.rm = TRUE)

# Calcular el número total de documentos en toda la base de datos, ignorando NA
numero_total_documentos <- sum(datos$`Web of Science Documents`, na.rm = TRUE)

# Calcular el porcentaje de documentos en Q1 respecto al total de documentos
porcentaje_documentos_Q1 <- (numero_total_documentos_Q1 / numero_total_documentos) * 100

# Crear una tabla resumen
tabla_resumen <- data.frame(
  "Número Total de Documentos en Q1" = numero_total_documentos_Q1,
  "Porcentaje de Documentos en Q1" = round(porcentaje_documentos_Q1, 2)
)

# Imprimir la tabla resumen
print(tabla_resumen)

```
