# Inventario de activos

**NOVA, A.C.**

## Cómo se leen las columnas

**Propiedad dominante:** C confidencialidad · I integridad · D disponibilidad · A autenticidad ·
NR no repudio.
**Plano:** dónde vive para efectos de este proyecto.

## Los activos

| ID | Activo | Categoría | Qué pasa si falla o se pierde | Propiedad | Criticidad | Plano |
|---|---|---|---|---|---|---|
| A-01 | Calificaciones, asistencias y reportes de conducta en la plataforma de control escolar | Información | No se pueden generar las boletas. Se pierde todo lo que pasó desde el último respaldo bimestral | **D** | Alta | Solo documentado |
| A-02 | Expedientes de los alumnos: contacto, salud y quién puede recoger a cada menor | Información | Si alguien cambia quién puede recoger a un niño, o una alergia o un medicamento, el colegio actúa sobre un dato falso sin darse cuenta | **I** | Alta | Representado |
| A-03 | Reportes psicopedagógicos de unos treinta alumnos | Información | Si se filtran, el daño lo sufre el niño, y lo puede seguir afectando después de salir de NOVA | **C** | Alta | Representado |
| A-04 | Fotografías escolares de los últimos seis ciclos, incluidas las de egresados | Información | Si se filtran, quedan expuestas fotos de menores con su grupo. No se respaldan nunca | **C** | Media | Representado |
| A-05 | Grabaciones de las ocho cámaras | Información | Muestran a los niños en pasillos y patio. La pantalla está encendida todo el día en el escritorio de la subdirectora | **C** | Baja | Solo documentado |
| A-06 | Servidor de control escolar, Windows Server 2016 | Equipo físico | Se detiene la plataforma de calificaciones y boletas. No recibe actualizaciones desde 2022 | **D** | Alta | Solo documentado |
| A-07 | Servidor de archivos, Ubuntu Server 20.04 | Equipo físico | Sin él no hay expedientes, fotos ni reportes psicopedagógicos, y no existe copia de nada de eso. Nunca se ha actualizado | **D** | Alta | Solo documentado |
| A-08 | Laptop que comparten las dos psicopedagogas | Equipo físico | Si se pierde o se la llevan, salen con ella las evaluaciones en las que estén trabajando | **C** | Media | Solo documentado |
| A-09 | Seis computadoras del aula de cómputo, Windows 10 | Equipo físico | Las usan los alumnos sin control. Son la entrada más probable de un programa malicioso | **D** | Baja | Solo documentado |
| A-10 | La cuenta compartida del asistente pedagógico | Cuenta | La usan quince personas. Si alguien hace mal uso, no hay forma de saber quién fue | **A** | Media | Solo documentado |
| A-11 | El acceso remoto permanente del proveedor de la plataforma | Cuenta | Es una puerta abierta al servidor de control escolar todo el tiempo, sin que el colegio sepa cuándo se usa | **A** | Media | Solo documentado |
| A-12 | El asistente pedagógico de inteligencia artificial | Servicio de tercero | Recibe calificaciones, notas y reportes psicopedagógicos. Plan de consumidor, sin acuerdo de tratamiento de datos | **C** | Media | Solo documentado |
| A-13 | Proveedor de la plataforma de control escolar | Servicio de tercero | Sin su soporte la plataforma no se arregla. El colegio no puede configurarla | **D** | Media | Solo documentado |
| A-14 | Empresa de fotografía escolar | Servicio de tercero | Recibe cada año la lista completa de alumnos con nombre y grupo. No hay contrato firmado | **C** | Media | Solo documentado |
| A-15 | Aseguradora del seguro escolar | Servicio de tercero | Recibe por correo una hoja de cálculo con nombre, edad y padecimientos de los alumnos | **C** | Media | Solo documentado |
| A-16 | Plataforma de videollamadas, versión gratuita | Servicio de tercero | Ahí se hacen las sesiones de seguimiento psicopedagógico, con la cuenta personal de cada quien | **C** | Media | Solo documentado |
| A-17 | Grupos de WhatsApp de cada salón | Servicio de tercero | Circulan fotos de los niños y comentarios de desempeño en celulares personales. Nadie saca a quien deja el colegio | **C** | Media | Solo documentado |
| A-18 | Google Workspace de dirección y administración | Servicio de tercero | Sin correo, la dirección y la administración no se comunican con familias, aseguradora ni proveedores | **D** | Media | Solo documentado |
| A-19 | Nómina y documentos de contratación del personal | Información | Datos de las 28 personas que trabajan en el colegio | **C** | Baja | Solo documentado |
| A-20 | El maestro de cómputo | Persona | Es el único que administra los dos servidores, en sus horas libres. Si falta, nadie sabe cómo funcionan | **D** | Alta | Solo documentado |

## Notas del inventario

**A-02 es el que más cuesta ver.** Lo obvio sería poner confidencialidad, porque son datos de salud de
menores. Pero lo que más duele no es que alguien los vea: es que alguien los **cambie sin que se note**.
Si se modifica quién puede recoger a un niño, el colegio se lo entrega a quien no debe. Si se borra una
alergia o se cambia un medicamento, el colegio se lo administra mal en horario escolar. Por eso domina
**integridad**. De ahí se sigue que el control que importa no es esconder el expediente, sino saber quién
lo cambió y poder compararlo contra una copia buena, y hoy no existe ninguna copia.

**A-03 sí es confidencialidad, y está aquí a propósito.** Los reportes psicopedagógicos son de niños que
no pueden decidir qué se hace con su información. Hoy están en una carpeta a la que también entran las
catorce maestras titulares, y desde hace unos meses se suben al asistente de A-12.

**A-10 es autenticidad, no confidencialidad.** Lo que se pierde con una cuenta compartida no es el secreto
ni el servicio, es poder saber quién subió cada documento y quién copió y pegó cada comentario de boleta.

**A-12 a A-18 son de terceros y aun así van en el inventario.** NOVA no los controla, pero depende de
ellos, y varios reciben datos de los alumnos. Que no sean del colegio no los saca del alcance: los mueve a
"solo documentado".

**Lo que no se pudo inventariar.** NOVA no tiene inventario de equipos y nadie sabe cuántos hay. Quedaron
fuera las tabletas del programa que terminó, que están en una caja y nadie sabe si prenden, y los catorce
celulares personales de las maestras, que no son del colegio pero llevan los grupos de A-17. Los activos
de arriba salieron de la ficha de la organización, no de una lista del colegio. **Es probable que falte
algo, y eso ya es un hallazgo.**
