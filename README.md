# Examen Parcial de Desarrollo Web - Nova Servicios

**Estudiante:** Fernando Castillo Vargas
**Código:** 2017518488

## 1. Planificación (Brief)

Nova Servicios necesita un portal web responsive para consultar servicios y simular solicitudes de soporte TI. El sistema debe ser accesible, adaptarse a webs móviles y de escritorio, y contar con un modelo conceptual para el tracking de tickets.

## 2. Historias de Usuario (Prioridad MoSCoW)

1. **[Obligatorio]** Como usuario, quiero ver un catálogo de servicios para saber qué tipo de soporte puedo pedir. _(Criterio: 4 tarjetas visibles en pantalla)._
2. **[Obliatorio]** Como usuario, quiero un formulario validado para simular mi solicitud de soporte. _(Criterio: Validaciones nativas y botón desactivado/activado)._
3. **[Obligatorio]** Como usuario, quiero ver el estado de los tickets de ejemplo. _(Criterio: Tabla estática con 4 estados visible y responsive)._
4. **[Deseable]** Como usuario, quiero leer preguntas frecuentes para resolver dudas rápidas. _(Criterio: Uso de detalles/summary para FAQ)._
5. **[Deseable]** Como usuario con discapacidad visual, quiero que el sitio sea navegable por teclado. _(Criterio: Foco visible en todos los elementos interactivos)._

## 3. Wireframe (Baja fidelidad)

[Encabezado y Menú de navegación]
[Hero / Presentación Principal]
[Catálogo de Servicios (Grid)]
[Sección de FAQ]
[Tabla de Estados]
[Formulario de Solicitud de Soporte]
[Pie de página y Contacto]

## 4. Reglas de Negocio del Modelo de Datos

- Un Usuario y un Servicio pueden tener múltiples Solicitudes (1:N).
- Cada cambio de estado en una Solicitud genera un registro en "Actualización" (1:N).
- Toda acción crítica (ej. cambiar prioridad) genera un registro en "Auditoría" ligado al usuario que hizo el cambio (1:N), guardando el valor anterior y nuevo.

## 5. Análisis del caso práctico (13)

**Solicitudes duplicadas (1001 y 1005)**:
Para determinar si son duplicadas, se debe comparar los campos comunes de un ticket: _id_usuario_, _id_servicio_, _tipo_incidencia_ y la **cercamía en tiempo** de _fecha_creacion_ en la tabla **Solicitud**. Si la descripción detalla el mismo problema, conservaría la solicitud más antigua (1001) para respetar el orden de cola o la que tenga la descripción más detallada, y cambiaría el estado de la otra a "Cerrado/Cancelado" agregando una nota de "Duplicado". Se entiende que esta actividad es totalmente manual y dependiente de un procedimiento de tratatmiento de solicitudes duplicadas.

**Cambio no autorizado en la prioridad (Solicitud 1002)**:
Para investigar, relacionaría el evento de la tabla Auditoría (donde _entidad_afectada_ = 'Solicitud' y _entidad_id_ = 1002) cruzando el _id_usuario_ = 9 con la tabla Usuario. Verificaría si el rol de ese usuario es "técnico". Dado que la tabla de Auditoría guarda el valor_anterior (Media) y valor_nuevo (Alta), podemos reconocer el historial del ticket y escalar el incidente internamente si el usuario 9 no tenía los permisos para la acción **CAMBIO_PRIORIDAD**.
