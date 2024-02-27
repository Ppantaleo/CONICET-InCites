## CONICET InCites 2019 - 2023

### Tabla 1. Documentos publicados por año - CONICET - 2019/2023

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