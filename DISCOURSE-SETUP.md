# Configuración de Discourse para la Columna Location

## Configuración de Campos Personalizados de Usuario

Para que la columna Location funcione de manera óptima, es recomendable configurar campos personalizados en Discourse que permitan a los usuarios especificar su ubicación.

### 1. Habilitar Campos Personalizados de Usuario

1. Ve a **Admin > Customize > User Fields**
2. Haz clic en **"New User Field"**
3. Configura el primer campo de ubicación:

```
Field Name: Location
Field Type: Text
Required: No (recomendado)
Show on Profile: Yes
Show on User Card: Yes
Searchable: Yes
```

4. Configura un segundo campo para país/región:

```
Field Name: Country/Region
Field Type: Text
Required: No
Show on Profile: Yes
Show on User Card: Yes
Searchable: Yes
```

### 2. Configuración de Perfiles de Usuario

#### Opción A: Usar el campo Location estándar

1. Ve a **Admin > Customize > User Fields**
2. Busca la sección "User Profile Fields"
3. Habilita el campo "Location" si no está habilitado
4. Configura las opciones de visualización

#### Opción B: Campos personalizados específicos

Crea campos más específicos para diferentes tipos de ubicación:

```
Field 1: City
Field 2: State/Province  
Field 3: Country
Field 4: Time Zone
```

### 3. Configuración de Grupos y Permisos

Para que los usuarios puedan editar su ubicación:

1. Ve a **Admin > Groups**
2. Selecciona el grupo "trust_level_1" o crea un grupo personalizado
3. En **"Group Management"** > **"User Fields"**
4. Marca los campos de ubicación como editables por el grupo

### 4. Configuración de Búsqueda

Para mejorar la búsqueda por ubicación:

1. Ve a **Admin > Customize > User Fields**
2. Marca los campos de ubicación como "Searchable"
3. Esto permitirá buscar usuarios por ubicación en la búsqueda global

## Configuración del Tema

### 1. Verificar que el tema esté activo

1. Ve a **Admin > Customize > Themes**
2. Asegúrate de que el tema "Sunflower" esté marcado como activo
3. Si no está activo, haz clic en "Activate"

### 2. Verificar el archivo header.html

1. En el tema Sunflower, haz clic en "Edit"
2. Ve a la sección "Common"
3. Verifica que el archivo `common/header.html` contenga el código de la columna Location
4. Si no está, copia y pega el contenido del archivo correspondiente

### 3. Configuración de colores personalizados

Si quieres cambiar los colores de la columna Location:

1. Edita el archivo `common/header.html`
2. Busca la sección de estilos CSS
3. Modifica los valores de color según tus preferencias

## Configuración de la API

### 1. Verificar permisos de API

La columna Location hace llamadas a la API de Discourse. Verifica que:

1. Los usuarios administradores tengan acceso a la API
2. No haya restricciones de CORS que bloqueen las llamadas
3. La API esté funcionando correctamente

### 2. Configuración de rate limiting

Si tienes muchos usuarios, considera ajustar el rate limiting:

1. Ve a **Admin > Settings > API**
2. Ajusta los límites de rate limiting según tus necesidades
3. La columna Location hace una llamada por usuario, así que considera esto

## Configuración de Caché

### 1. Caché del navegador

La columna Location utiliza caché del navegador para mejorar el rendimiento:

- Las ubicaciones se almacenan en memoria durante la sesión
- Se evitan llamadas repetidas a la API
- El caché se limpia automáticamente al cerrar el navegador

### 2. Caché del servidor

Si quieres implementar caché del servidor:

1. Considera usar Redis o Memcached
2. Implementa un endpoint de API personalizado para ubicaciones
3. Agrega headers de caché apropiados

## Configuración de Privacidad

### 1. Permisos de visualización

Considera quién puede ver la ubicación de los usuarios:

1. **Solo administradores**: La columna solo aparece en la vista de administración
2. **Usuarios autenticados**: Permite que todos los usuarios vean ubicaciones
3. **Grupos específicos**: Restringe la visualización a ciertos grupos

### 2. Configuración de campos privados

Si quieres que algunos campos de ubicación sean privados:

1. En la configuración del campo personalizado
2. Marca "Show on Profile" como "No"
3. Solo los administradores podrán ver estos campos

## Configuración de Rendimiento

### 1. Lazy loading

La columna Location implementa lazy loading:

- Las ubicaciones se cargan solo cuando son visibles
- Se evita cargar datos innecesarios
- Mejora el rendimiento en listas largas

### 2. Paginación

Para listas muy largas de usuarios:

1. Considera implementar paginación en la columna Location
2. Carga solo las ubicaciones de la página actual
3. Implementa un botón "Cargar más" si es necesario

## Configuración de Monitoreo

### 1. Logs de errores

Monitorea los errores de la columna Location:

1. Revisa la consola del navegador para errores JavaScript
2. Verifica los logs del servidor para errores de API
3. Implementa logging personalizado si es necesario

### 2. Métricas de rendimiento

Considera monitorear:

- Tiempo de carga de la columna
- Número de llamadas a la API
- Tasa de éxito de las llamadas
- Uso de caché

## Configuración de Backup

### 1. Backup del código personalizado

Guarda una copia de seguridad del código:

1. Copia el contenido del archivo `common/header.html`
2. Guárdalo en un archivo separado
3. Documenta cualquier personalización que hayas hecho

### 2. Backup de la configuración

Documenta la configuración de Discourse:

1. Campos personalizados creados
2. Configuración de grupos y permisos
3. Configuración del tema
4. Cualquier otra personalización relevante

## Solución de Problemas Comunes

### 1. La columna no aparece

**Síntomas**: No se ve la columna Location en la administración de usuarios

**Soluciones**:
- Verifica que el archivo `common/header.html` esté guardado
- Limpia la caché del navegador
- Verifica que estés en una página de administración de usuarios
- Revisa la consola del navegador para errores

### 2. Las ubicaciones no se cargan

**Síntomas**: La columna aparece pero muestra "N/A" para todos los usuarios

**Soluciones**:
- Verifica que los usuarios tengan información de ubicación
- Revisa la consola del navegador para errores de API
- Verifica que la API de Discourse esté funcionando
- Comprueba los permisos de API

### 3. Problemas de estilo

**Síntomas**: La columna aparece pero no se ve bien

**Soluciones**:
- Verifica que el tema Sunflower esté activo
- Los estilos usan `!important` para evitar conflictos
- Puedes sobrescribir estilos en CSS personalizado
- Verifica que no haya conflictos con otros temas o plugins

### 4. Problemas de rendimiento

**Síntomas**: La página se vuelve lenta o no responde

**Soluciones**:
- Verifica el número de usuarios en la lista
- Considera implementar paginación
- Monitorea el uso de memoria del navegador
- Verifica que no haya llamadas infinitas a la API

## Recursos Adicionales

### 1. Documentación de Discourse

- [User Fields](https://docs.discourse.org/t/creating-custom-user-fields/12345)
- [Theme Development](https://docs.discourse.org/t/theme-development/12345)
- [API Documentation](https://docs.discourse.org/t/api-documentation/12345)

### 2. Comunidad

- [Meta Discourse](https://meta.discourse.org/)
- [Foros de soporte](https://meta.discourse.org/c/support)
- [Desarrollo de temas](https://meta.discourse.org/c/theme)

### 3. Herramientas de desarrollo

- [Discourse Theme CLI](https://github.com/discourse/discourse_theme)
- [Discourse Plugin CLI](https://github.com/discourse/discourse_plugin)
- [Discourse Docker](https://github.com/discourse/discourse_docker)
