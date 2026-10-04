# Gestión de Eventos en Tkinter (Semana 16)

## Objetivo del Proyecto

Avanzar con la base desarrollada en la Semana 15 manteniendo su estructura general: sistema de inicio de sesión, arquitectura multicapa, almacenamiento local en JSON, operaciones CRUD de productos, registro de ventas, menú de navegación e identidad visual.

La sección **Usuarios** se reestructura para ilustrar el ciclo completo de un evento: la interacción de la persona en pantalla, la captura con `bind()`, el procesamiento en el callback (`event`), la lógica en la capa de servicios, la actualización en el archivo JSON y el reflejo inmediato en la interfaz gráfica.

## Relación con la Semana 15

Se conserva la línea gráfica, la barra inferior de estado y la barra lateral de opciones. Mientras que el módulo de **Ventas** sigue utilizando el enfoque tradicional mediante `command=`, la sección **Usuarios** sirve como el caso práctico principal para el manejo de eventos mediante controladores.

## Características de la Semana 16

La administración de usuarios incluye las siguientes opciones:

- Registro e ingreso de nuevos usuarios.
- Búsqueda y consulta de la lista general.
- Selección gráfica desde una tabla `ttk.Treeview`.
- Carga automática del registro seleccionado hacia los campos del formulario.
- Modificación de datos existentes.
- Eliminación con diálogo de confirmación.
- Restablecimiento o limpieza de los campos del formulario.
- Asignación y manejo de roles (`Administrador`, `Empleado`, `Cliente`).

*Nota:* Los nuevos registros creados desde la pantalla de gestión se limitan a los roles de `Empleado` o `Cliente`, preservando intacta la cuenta de `Administrador` del sistema.

### Esquema del flujo:

```text
Acción en la interfaz -> Evento -> bind() -> Callback(event) -> Servicio -> Archivo JSON -> Interfaz
```

## Control de Eventos Utilizados

Acciones por botones estándar (`command=`):
- Registrar
- Actualizar
- Eliminar
- Limpiar

Acciones vinculadas con `bind()`:
- `<<TreeviewSelect>>`: Carga los datos de la fila seleccionada dentro del formulario.
- `<Return>`: Permite guardar el usuario presionando la tecla Enter.
- `<Escape>`: Cancela la selección y vacía los campos de texto.
- `<<ComboboxSelected>>`: Monitorea los cambios de selección en la lista desplegable (`ttk.Combobox`).

### Flujo de datos del Treeview:

```text
Tabla Treeview -> Obtención de ID -> buscar_usuario_por_identificador() -> Instancia Usuario -> Carga en Formulario
```
## Estructura del proyecto

```text
biblioteca_app/
├── assets/
│   ├── icons/
│   └── logo/
│       ├── logo.png
│       └── icono.png
├── datos/
│   ├── libros.json
│   ├── usuarios.json
│   └── ventas.json
├── modelos/
│   ├── usuario.py
│   ├── libro.py
│   └── venta.py
├── servicios/
│   ├── archivo_servicio.py
│   └── biblioteca_servicio.py
├── ui/
│   ├── login_view.py
│   └── main_view.py
└── main.py
```
## Persistencia de Datos

El sistema almacena la información de usuarios, productos y ventas en archivos JSON que se leen durante la inicialización del programa:

```text
restaurante_app/datos/usuarios.json
restaurante_app/datos/productos.json
restaurante_app/datos/ventas.json
```

Ante cualquier operación de inserción, edición o borrado de datos, el servicio actualiza la estructura en memoria y sobreescribe el archivo `usuarios.json`.

## Gestión de Accesos

La vista principal `MainView` gestiona el acceso mediante las propiedades del objeto `usuario_actual`:

- `Administrador`: Acceso total, incluyendo el módulo de `Usuarios`.
- `Empleado` y `Cliente`: Menú restringido sin acceso visible a la gestión de usuarios.

## Instrucciones de Ejecución

Ejecutar el intérprete global de Python:

```powershell
python main.py
```

## Credenciales de Acceso para Pruebas

- **Administrador:**  
  Usuario: `admin`  
  Contraseña: `1234`

- **Empleado:**  
  Usuario: `juan`  
  Contraseña: `abcd`

- **Cliente:**  
  Usuario: `ruth`  
  Contraseña: `cliente123`
