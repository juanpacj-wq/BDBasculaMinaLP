# DBB-sculaGEC3: Transformación dbt para Airbyte

## Descripción
Este repositorio contiene una transformación dbt para Airbyte que renombra la tabla `v_Facturacion` a `v_facturacion_mlp` durante el proceso de sincronización. Esta transformación es necesaria para evitar conflictos de nombres cuando se sincronizan datos de múltiples fuentes que comparten el mismo nombre de tabla.

## Detalles de la transformación

### Origen
- **Base de datos**: BDBascMina
- **Esquema**: dbo
- **Tabla**: v_Facturacion

### Destino
- **Base de datos**: dl_captura (Datalake corporativo, capa analítica)
- **Esquema**: minalp
- **Tabla original**: _airbyte_raw_v_facturacion
- **Tabla transformada**: v_facturacion_mlp

## Estructura del repositorio
- `dbt_project.yml`: Configuración principal del proyecto dbt
- `models/schema.yml`: Definición de fuentes y modelos
- `models/v_facturacion_gec3.sql`: Transformación SQL que realiza el renombramiento

## Cómo funciona
1. Airbyte sincroniza los datos desde la fuente (BDBascMina.dbo.v_Facturacion)
2. Los datos se cargan inicialmente en dl_captura.minalp._airbyte_raw_v_facturacion
3. La transformación dbt crea una nueva tabla llamada v_facturacion_gec3 con los mismos datos

## Configuración en Airbyte
Para utilizar esta transformación:
1. En la conexión de Airbyte, habilitar "Custom dbt Transformations"
2. Proporcionar la URL de este repositorio
3. Configurar la rama principal (main/master)
4. Guardar y ejecutar la sincronización

## Mantenimiento
Si es necesario modificar la transformación:
1. Actualizar los archivos relevantes en este repositorio
2. Confirmar los cambios
3. La próxima sincronización de Airbyte utilizará automáticamente la versión actualizada