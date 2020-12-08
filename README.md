# BE - NT1 - Grupo 5
 - Felizzola, Andrea Soledad	felizzolandre@gmail.com
 - Garcia, Cesar Oscar	cesar.osc.garcia@gmail.com
 - Garzon, Bruno	bruno.garzon95@gmail.com
 - Bogado, Mateo Tomas	bgdtomas21@gmail.com

# Sistema ERP básico 📖
## Objetivos 📋
Desarrollar un sistema de ERP Básico para una empresa Pyme, que permita la administración y uso de recursos en ella. 
De cara a los empleados de RRHH: Empleados, Posiciones, Gerencias, Centros de Costo, etc. 
Utilizar Visual Studio 2019 preferentemente y crear una aplicación utilizando ASP.NET MVC Core versión 3.1.

<hr />

## Enunciado 📢
La idea principal de este trabajo práctico, es que Uds. se comporten como un equipo de desarrollo. Este documento, les acerca, un equivalente al resultado de una primera entrevista entre el cliente y alguien del equipo, el cual relevó e identificó la información aquí contenida. A partir de este momento, deberán comprender lo que se está requiriendo y construir dicha aplicación,

Deben recopilar todas las dudas que tengan y evacuarlas con su nexo (el docente) de cara al cliente. De esta manera, él nos ayudará a conseguir la información ya un poco más procesada. Es importante destacar, que este proceso, no debe esperar a ser en clase; es importante, que junten algunas consultas, sea de índole funcional o técnicas, en lugar de enviar cada consulta de forma independiente.

### Consultas

Las consultas que sean realizadas por correo a mailto:federico.marchese@ort.edu.ar deben seguir el siguiente formato:

Subject: [NT1-<CURSO LETRA>-GRP-<GRUPO NUMERO>] <Proyecto XXX> | Informativo o Consulta

Body:

1.`<xxxxxxxx>`

2.`<xxxxxxxx>`

### Ejemplo
Subject: [NT1-A-GRP-5] Agenda de Turnos | Consulta

Body:

1.La relación del paciente con Turno es 1:1 o 1:N?

2.Está bien que encaremos la validación del turno activo, con una propiedad booleana en el Turno?

<hr />

## Proceso de ejecución en alto nivel ☑️
 - Crear un nuevo proyecto en [visual studio](https://visualstudio.microsoft.com/en/vs/).
 - Adicionar todos los modelos dentro de la carpeta Models cada uno en un archivo separado.
 - Especificar todas las restricciones y validaciones solicitadas a cada una de las entidades. [DataAnnotations](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations?view=netcore-3.1).
 - Crear las relaciones entre las entidades
 - Crear una carpeta Data que dentro tendrá al menos la clase que representará el contexto de la base de datos DbContext. 
 - Crear el DbContext utilizando base de datos en memoria (con fines de testing inicial). [DbContext](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext?view=efcore-3.1), [Database In-Memory](https://docs.microsoft.com/en-us/ef/core/providers/in-memory/?tabs=vs).
 - Agregar los DbSet para cada una de las entidades en el DbContext.
 - Crear el Scaffolding para permitir los CRUD de las entidades al menos solicitadas en el enunciado.
 - Aplicar las adecuaciones y validaciones necesarias en los controladores.  
 - Realizar un sistema de login con al menos los roles equivalentes a <Usuario Cliente> y <Usuario Administrador> (o con permisos elevados).
 - Si el proyecto lo requiere, generar el proceso de registración. 
 - Un administrador podrá realizar todas tareas que impliquen interacción del lado del negocio (ABM "Alta-Baja-Modificación" de las entidades del sistema y configuraciones en caso de ser necesarias).
 - El <Usuario Cliente> sólo podrá tomar acción en el sistema, en base al rol que tiene.
 - Realizar todos los ajustes necesarios en los modelos y/o funcionalidades.
 - Realizar los ajustes requeridos del lado de los permisos.
 - Todo lo referido a la presentación de la aplicaión (cuestiones visuales).
 - Para la visualización se recomienda utilizar [Bootstrap](https://getbootstrap.com/), pero se puede utilizar cualquier herramienta que el grupo considere.

<hr />

## Entidades 📄
- Usuario
- Empleado
- Telefono
- TipoTelefono
- Foto
- Posición
- Gerencia
- CentroDeCosto
- Gastos
- Empresa

`Importante: Todas las entidades deben tener su identificador único Id`

**`
Las propiedades descriptas a continuación, son las mínimas que deben tener las entidades. Ustedes pueden agregar las que consideren necesarias. De la misma manera, ustedes deben definir los tipos de datos asociados a cada una de ellas, como así también las restricciones que apliquen en cada caso.
`**

**Usuario**
```
- Nombre
- Email
- FechaAlta
- Password
```

**Empleado**
```
- Nombre
- Apellido
- DNI
- Telefonos
- Direccion
- FechaAlta
- Email 
- ObraSocial
- Legajo
- EmpleadoActivo
- Posicion
- Foto
```
**Telefono**
```
- Numero
- TipoTelefono
```

**TipoTelefono**
```
- Nombre
```

**Imagen**
```
- Nombre
- Path (url)
```

**Posicion**
```
- Nombre
- Descipcion
- Sueldo
- Empleado
- Responsable(Jefe)
- Gerencia
```

**Gerencia**
```
- Nombre
- EsGerenciaGeneral
- Direccion(Gerencia)
- Responsable(Posicion)
- Posiciones
- Gerencias
- Empresa
```

**CentroDeCosto**
```
- Nombre
- MontoMaximo
- Gastos
```

**Gasto**
```
- Descipcion
- CentroDeCosto
- Empleado
- Monto
- Fecha
```

**Empresa**
```
- Nombre
- Rubro
- Logo
- Direccion
- TelefonoContacto
- EmailContacto
```

**NOTA:** aquí un link para refrescar el uso de los [Data annotations](https://www.c-sharpcorner.com/UploadFile/af66b7/data-annotations-for-mvc/).

<hr />

## Caracteristicas y Funcionalidades ⌨️
`Todas las entidades deben tener implementado su correspondiente ABM, a menos que sea implícito el no tener que soportar alguna de estas acciones.`

`IMPORTANTE: Solo empleados de RRHH pueden realizar modificaciones en la nómina de Empleados, Pero todos pueden ver información general de la Empresa.`

**Usuario**
- Los Empleados no pueden auto registrarse.

**Empleado**
- Los empleados deben ser agregados por otro Empleado.
	- Al momento del alta del empleado se le definirá un username y password.
    - También se le asignará a estas cuentas el rol de empleado y adicionalmente el de RRHH si corresponde.
- Puede navegar el organigrama. 
- Puede actualizar datos de contacto, como el teléfonos, dirección, etc., pero no puede modificar su DNI, Nombre, Apellido, etc.
- Pueden Imputar gastos a su Centro de Costo.
- Cada empleado puede listar sus gastos en orden descendiente por fecha.

**Organigrama**
- La visualización del organigrama siempre estará disponible para cualquier Empleado de la compañía. 
- Se parte por la Gerencia General (solo puede existir una) y se visualiza el Responsable de la misma.
- Al hacer click en ella se visualizará el siguiente nivel de jerárquico con cada una de las gerencias que la componga y sus correspondientes responsables.
    - En el caso de ser una Gerencia que no tiene subGerencias, mostrar todos los empleados que la componen (Solo Apellido y Nombre), en formado de lista ascendente por Apellido y Nombre.
    - Se podrá hacer click en cada empleado, para visualizar una tarjeta de contacto.
    - La tarjeta de contacto tendrá: Apellido, Nombre, Nombre de la posición, Teléfonos e Email.
    Importante: Solo se visualizarán empleados que estén activos en la nómina. 

**Empleado de RRHH**
- Un empleado de RRHH puede crear, modificar todos los datos de los Empresa, de otros empleados, Gerencias, Posiciones, etc., tiene control total de la información contenida en el sistema.
    - No puede eliminar Empleados pero si puede deshabilitarlos para indicar que no son empleados actuales de nómina.
- El Empleado de RRHH puede listar todos los empleado y por cada uno ver en sus detalles, como así también, realizar modificaciones en los mismos. 
- Puede ver un listado de empleados, con sueldo ordenado decrecientemente por el concepto y luego creciente por Apellido y Nombre. 
    - Se debe incluir Sueldo, Apellido, Nombre y Nombre de la posición.
- No puede modificar ni eliminar un Gasto de otro Empleado.
- Puede listar todos los gastos de todos los empleados en forma decreciente por fecha y ordenados de manera creciente por Apellido y Nombre. Se debe incluir la información de a qué gerencia pertenece.
- Listar los montos totales de gastos por cada gerencia, independientemente de si es una Gerencia o SubGerencia.

**Posición**
- La posición es la que dará la relación entre un Empleado y la Gerencia a la cual éste pertenece.
- La posición puede o no tener empleados actualmente ocupándola. Ej. La posición de gerente de IT, puede estar disponible, sin un empleado que la esté ocupando.
- El Responsable de dicha posición es otra posición, no es un empleado. En todo caso, tiene una Posición de la cual depende, y esa otra posición tiene un Empleado o no que está ocupando la posición (ej. una posición puede ser desarrollador y otra posición puede ser líder técnico, siendo el líder técnico la posición que es responsable del desarrollador).
- La posición es la que tiene un sueldo designado, no es el empleado.
- Pertenece a una Gerencia.

**Centro de Costo**
- El centro de Costos puede ser creado y utilizado por cualquier gerencia de cualquier nivel.
- Los empleados solo pueden imputar gastos al centro de costo que tenga la gerencia a la cual pertenecen de forma directa.
- Se pueden imputar gastos al centro de costo dejando registro de cual es el empleado que lo está imputando, siempre y cuando, no supere el monto máximo del Centro de Costos.

**Aplicación General**
- Información institucional, en base a la información de la Empresa, con su respectiva imagen (Logo)
- No existe un limite para las posiciones dependientes. Ejemplo, pueden existir 10 o 1000 posiciones que dependan de una posición gerencial. En otras palabras, un Gerente asignado a una posición de Gerente de IT, puede tener 1, 10 o 1000 posiciones de IT general que dependen de ella. 
- Los accesos a las funcionalidades y/o capacidades, debe estar basada en los roles que tenga cada individuo.
