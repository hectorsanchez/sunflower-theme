# Columna Location para Administración de Usuarios en Discourse

## Descripción

Este tema personalizado agrega una columna "Location" a la vista de administración de usuarios en Discourse, permitiendo a los administradores ver la ubicación de los usuarios directamente en la lista de usuarios.

## Características

- ✅ Agrega una columna "Location" a todas las vistas de administración de usuarios (Active, New, Staff, Suspended, Silenced, Staged)
- ✅ Obtiene automáticamente la ubicación de los usuarios desde la API de Discourse
- ✅ Busca la ubicación en múltiples campos: user_fields, location estándar, y bio
- ✅ Sistema de cache para mejorar el rendimiento
- ✅ Estilos personalizados que coinciden con el tema Sunflower
- ✅ Funciona con la navegación SPA de Discourse
- ✅ Responsive y accesible

## Instalación

### 1. Actualizar el tema en Discourse

1. Ve a **Admin > Customize > Themes** en tu instalación de Discourse
2. Encuentra el tema "Sunflower" y haz clic en "Edit"
3. En la sección "Common", busca el archivo `common/header.html`
4. Copia y pega el contenido del archivo `common/header.html` de este repositorio
5. Guarda los cambios

### 2. Verificar la instalación

1. Ve a **Admin > Users > Active** (o cualquier otra vista de usuarios)
2. Deberías ver la nueva columna "Location" en la tabla
3. La columna se llenará automáticamente con la ubicación de cada usuario

## Cómo funciona

### Obtención de datos de ubicación

El script busca la ubicación del usuario en el siguiente orden:

1. **Campos personalizados (user_fields)**: Busca en los primeros 20 campos personalizados por palabras clave como "location", "ubicación", "city", "country"
2. **Campo location estándar**: Utiliza el campo `location` nativo de Discourse
3. **Campo bio**: Busca en la biografía del usuario por patrones como "Location: [ciudad]"

### Cache y rendimiento

- Las ubicaciones se almacenan en cache para evitar llamadas repetidas a la API
- El cache persiste durante la sesión del navegador
- Se evitan reintentos fallidos para usuarios sin ubicación

### Estilos visuales

La columna utiliza los colores del tema Sunflower:
- **Encabezado**: Fondo amarillo (#f4d35e) con texto marrón oscuro
- **Celdas**: Fondo crema claro (#faf0ca) con bordes suaves
- **Hover**: Efectos de escala y cambio de color
- **Ubicaciones válidas**: Texto en marrón más oscuro (#8A4A19)

## Personalización

### Cambiar colores

Puedes modificar los colores editando las variables CSS en el archivo `common/header.html`:

```css
.location-column-header {
  background-color: #tu-color !important;
  color: #tu-texto !important;
}
```

### Cambiar posición de la columna

Para cambiar la posición de la columna, modifica esta línea en el script:

```javascript
// Insertar después de la columna "Last Posted" o antes de la última columna
const lastPostedHeader = thead.querySelector('th:last-child');
if (lastPostedHeader) {
  thead.insertBefore(locationHeader, lastPostedHeader);
} else {
  thead.appendChild(locationHeader);
}
```

### Agregar más campos de búsqueda

Para buscar en campos adicionales, modifica la función `getUserLocation`:

```javascript
// Agregar más campos personalizados
if (userData.user.custom_field_name) {
  location = userData.user.custom_field_name;
}
```

## Compatibilidad

- **Discourse**: Versión 3.5.0.beta8 o superior
- **Navegadores**: Chrome, Firefox, Safari, Edge (versiones modernas)
- **Temas**: Compatible con cualquier tema de Discourse
- **Plugins**: No interfiere con otros plugins

## Solución de problemas

### La columna no aparece

1. Verifica que el archivo `common/header.html` esté guardado correctamente
2. Limpia la caché del navegador
3. Verifica que estés en una página de administración de usuarios
4. Revisa la consola del navegador para errores JavaScript

### Las ubicaciones no se cargan

1. Verifica que los usuarios tengan información de ubicación en sus perfiles
2. Revisa la consola del navegador para errores de API
3. Verifica que la API de Discourse esté funcionando correctamente

### Problemas de estilo

1. Verifica que el tema Sunflower esté activo
2. Los estilos se aplican con `!important` para evitar conflictos
3. Puedes sobrescribir estilos en tu CSS personalizado

## Desarrollo

### Estructura del código

- **Función principal**: `addLocationColumn()` - Agrega la columna a la tabla
- **API**: `getUserLocation()` - Obtiene la ubicación desde la API de Discourse
- **Cache**: `userLocationCache` - Almacena ubicaciones para mejorar rendimiento
- **Eventos**: Maneja navegación SPA y cambios de pestañas

### Agregar funcionalidades

Para agregar más funcionalidades:

1. **Filtrado**: Agregar filtros por ubicación
2. **Ordenamiento**: Permitir ordenar por ubicación
3. **Exportación**: Incluir ubicación en exportaciones CSV
4. **Búsqueda**: Buscar usuarios por ubicación

## Licencia

Este código está bajo la misma licencia MIT que el tema Sunflower original.

## Soporte

Para soporte técnico o preguntas:
1. Revisa la documentación de Discourse
2. Consulta los foros de la comunidad de Discourse
3. Abre un issue en este repositorio

## Changelog

### v1.0.0
- Implementación inicial de la columna Location
- Soporte para múltiples fuentes de datos de ubicación
- Sistema de cache para mejorar rendimiento
- Estilos personalizados del tema Sunflower
- Compatibilidad con navegación SPA de Discourse
