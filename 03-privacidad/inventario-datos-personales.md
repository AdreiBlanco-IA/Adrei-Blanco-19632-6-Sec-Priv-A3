# Inventario de datos personales

**NOVA, A.C.**

Práctica: `laboratorio/practica-datos-personales.md`. Recorrí mi `00-organizacion/activos.md`
activo por activo y me pregunté si ahí hay información de alguna persona identificable. Los CWE
de la penúltima columna son los que trabajé en `04-detecciones/cve-cwe.md`.

Dejé fuera a `A-20`, el maestro de cómputo, porque es una persona y no guarda datos. Sus propios
datos están en la nómina (`A-19`). Junté `A-06` con `A-01` y `A-07` con `A-02`, `A-03` y `A-04`:
el servidor es el activo y lo que importa es lo que tiene dentro.

## La tabla

| Activo | Qué datos contiene | ¿Sensibles? | De quién son | Dónde viven | Cuánto tiempo se conservan | Qué CWE podría exponer estos datos | Si se expusiera, ¿habría que informar a los titulares? |
|---|---|---|---|---|---|---|---|
| `A-01` en `A-06` · Plataforma de control escolar | Calificaciones, asistencias, reportes de conducta, y los datos de los 240 alumnos y de sus tutores | No *(ver nota sobre conducta)* | De los 240 alumnos, **todos menores de edad**, y de sus tutores | En el servidor Windows Server 2016 del rincón de la dirección. Una copia cada bimestre en un disco externo, **no sé dónde se guarda ese disco**. El proveedor (`A-13`) entra cuando quiere por su acceso remoto (`A-11`). Las listas de calificaciones también se suben al asistente de IA (`A-12`) | **No se sabe.** La ficha no dice si se borran los alumnos que egresan | `CWE-416`: el servidor no se actualiza desde 2022 y un fallo de memoria en Windows daría control del equipo completo, como en `CVE-2024-38063` | **Sí.** Son datos de menores y de sus familias, y una calificación o un reporte de conducta alterados afectan al niño |
| `A-02` en `A-07` · Expedientes de los alumnos | Datos de contacto, alergias, padecimientos, medicamentos que se dan en horario escolar, y quién puede recoger a cada menor | **Sí**, los de salud | De los alumnos, de sus tutores, y **de las personas autorizadas para recoger al niño**, que no son ni alumnos ni tutores | En el servidor Ubuntu Server 20.04 de la dirección, **sin ningún respaldo**. Los padecimientos además salen cada año por correo a la aseguradora (`A-15`) | **No se sabe** | `CWE-22`: si algún servicio de ese servidor arma rutas con lo que pide el usuario, se podría salir de la carpeta y sacar los expedientes | **Sí.** Son datos de salud de menores, y saber quién puede recoger a un niño pone en riesgo su seguridad física |
| `A-03` en `A-07` · Reportes psicopedagógicos | Evaluaciones, diagnósticos y reportes de seguimiento | **Sí**, son de salud | De unos treinta alumnos, menores de edad. Es probable que también hablen de sus familias *(ver nota)* | En el servidor Ubuntu, en una carpeta a la que **también entran las catorce maestras titulares**, sin respaldo. En la laptop que comparten las psicopedagogas (`A-08`). Desde hace unos meses, **subidos al asistente de IA** (`A-12`) | **No se sabe.** Nadie ha dicho cuándo se borran | `CWE-22`, por la misma carpeta del servidor de archivos | **Sí.** Es el caso más claro: un diagnóstico de un niño puede seguirlo afectando cuando ya salió del colegio |
| `A-04` en `A-07` · Fotografías escolares | Fotos individuales y de grupo de los últimos seis ciclos | No *(ver nota)* | De los alumnos actuales, **de los egresados**, que ya no tienen relación con el colegio, y de los compañeros que salen en las fotos de grupo | En el servidor Ubuntu, sin respaldo. Antes de 2020 estaban en la computadora de la directora: **no sé si ahí se borraron** | **Seis ciclos, y nadie borra las de los egresados** | `CWE-22`, por el mismo servidor | **Sí.** Son fotos de menores que se pueden identificar por su grupo |
| `A-05` · Grabaciones de las cámaras | Video de pasillos y patio | No *(ver nota)* | De los alumnos, del personal, y de cualquier persona que entre al colegio: padres, proveedores, visitas | En la grabadora de la dirección. La pantalla está encendida todo el día en el escritorio de la subdirectora, a la vista de quien pase | Treinta días, en ciclo | **No lo sé.** La ficha no dice qué sistema tiene la grabadora ni si está en la red | **No**, en general: es imagen de lugares comunes que se borra a los treinta días. Cambiaría si una grabación mostrara algo de un niño en particular |
| `A-08` · Laptop de las psicopedagogas | Las evaluaciones y reportes que estén trabajando | **Sí**, de salud | De los alumnos que atienden | En la laptop. **No sé si se quedan ahí copias** después de pasarlas al servidor | **No se sabe** | `CWE-416`: un fallo de memoria del sistema operativo de la laptop. La ficha no dice qué sistema tiene | **Sí**, por la misma razón que `A-03` |
| `A-09` · Computadoras del aula de cómputo | **No se sabe.** Las usan los alumnos sin control: pueden tener trabajos, sesiones abiertas o cuentas guardadas | No se sabe | De los alumnos | En las seis computadoras con Windows 10 | **No se sabe** | `CWE-416`, en Windows 10 | **No se puede decir** sin saber qué tienen dentro |
| `A-10` y `A-12` · Asistente pedagógico de IA y su cuenta compartida | Calificaciones, notas sueltas de las maestras, comentarios de boleta, reportes de conducta, y **reportes psicopedagógicos** | **Sí** | De los alumnos | En los servidores del proveedor del asistente, en un **plan de consumidor sin acuerdo de tratamiento de datos**. Quince personas entran con la misma cuenta, así que no se sabe quién subió qué | **No se sabe.** Los términos dicen que el proveedor puede usar el contenido para mejorar sus servicios | `CWE-917`: un servicio que recibe texto y lo interpreta puede hacer con él algo que nadie pidió. Pero aquí el problema principal no es técnico: los datos ya salieron del colegio por contrato | **Sí.** Hay datos de salud de menores en manos de un tercero que puede usarlos para sus propios fines |
| `A-14` · Empresa de fotografía escolar | Lista completa de alumnos con nombre y grupo, y las fotos que toma | No | De los alumnos | En el portal propio de la empresa, donde los padres compran las fotos. Se acordó de palabra hace ocho años, **sin contrato** | **No se sabe.** No hay contrato que lo diga | `CWE-22`: si el portal arma la ruta de cada foto con lo que pide el usuario, alguien podría ver las fotos de otros grupos | **Sí.** Nombre, grupo y foto juntos identifican a un menor |
| `A-15` · Aseguradora del seguro escolar | Nombre, edad y **padecimientos declarados** de los alumnos | **Sí**, de salud | De los alumnos | En una hoja de cálculo que se manda **por correo** una vez al año. Vive en el correo del colegio (`A-18`), en el de la aseguradora, y en quien la haya descargado | **No se sabe**, ni del lado del colegio ni de la aseguradora | `CWE-125`: un fallo como Heartbleed en el servicio de correo dejaría leer lo que pasa por él. Pero el problema principal es que la hoja viaja suelta | **Sí.** Son datos de salud de menores |
| `A-16` · Plataforma de videollamadas gratuita | Lo que se dice en las juntas con padres y en las **sesiones de seguimiento psicopedagógico** | **Sí**, en las sesiones psicopedagógicas | De los alumnos, de sus tutores, y del personal que participa | En la plataforma, con la **cuenta personal** de cada quien. No sé si se graban las sesiones | **No se sabe** | No lo puedo conectar a un CWE concreto: no sé qué plataforma es | **Sí**, si se expusiera una sesión psicopedagógica |
| `A-17` · Grupos de WhatsApp de cada salón | Avisos, tareas, fotos de los niños en actividades, a veces comentarios sobre el desempeño de un alumno, y los teléfonos de quienes están en el grupo | No *(ver nota)* | De los alumnos, de los tutores que están en el grupo, y de las maestras | En los **celulares personales** de las catorce maestras y de cada familia. **Las maestras que se van siguen en los grupos** | **Indefinido.** Nadie borra los grupos ni saca a nadie | No es un fallo técnico del colegio: los datos ya están en celulares que nadie administra | **Sí**, si se exponen comentarios sobre el desempeño de un niño identificable |
| `A-18` · Google Workspace de dirección y administración | Correos con las familias, con la aseguradora y con los proveedores, incluida la hoja de padecimientos | **Sí**, por la hoja de la aseguradora | De los alumnos, de los tutores, y de los contactos de los proveedores | En las cuentas de Google de la dirección y la administración. Las maestras no están aquí: usan su Gmail personal | **No se sabe** | `CWE-125`, como en `A-15`, en lo que pasa por el correo | **Sí** |
| `A-19` · Nómina y documentos de contratación | Nómina, CURP y documentos de contratación | No *(ver nota)* | De las 28 personas que trabajan en el colegio | **No se sabe.** La ficha no dice en qué equipo están | **No se sabe** | No lo puedo conectar sin saber dónde están | **Sí.** Con CURP y nómina se puede afectar el patrimonio de una persona |

## Quién puede consentir y quién no

**Los 240 alumnos son menores de edad y no pueden consentir por sí mismos.** Lo hacen sus tutores.
Pero en la tabla hay titulares que **no dieron sus datos y nadie les pidió permiso**:

- **Las personas autorizadas para recoger a un niño** (`A-02`). Sus datos los dio el tutor, no
  ellas.
- **Los egresados** (`A-04`). Sus fotos siguen guardadas. Algunos ya serán mayores de edad, y el
  consentimiento lo dio su tutor cuando eran niños, para una finalidad que ya terminó.
- **Los compañeros que salen en las fotos de grupo** y en las fotos de actividades de WhatsApp
  (`A-04`, `A-17`).
- **Cualquier persona que entra al colegio** y queda en las cámaras (`A-05`).

Igual que en el ejemplo del año pasado, la mayoría de esos datos no son de los «clientes» del
colegio, que serían los tutores que pagan. Son de niños y de otras personas que nunca supieron que
sus datos pasaban por ahí.

## Notas sobre los sensibles dudosos

- **Reportes de conducta (`A-01`).** Los marqué como no sensibles, pero tengo la duda. Un reporte
  de conducta puede decir algo sobre la salud o la situación familiar de un niño. Si lo dice, ese
  reporte en particular sí sería sensible.
- **Situación familiar.** La ficha de NOVA dice que los datos de los tutores incluyen la
  «situación familiar». No sé qué incluye: si habla de un divorcio o de quién tiene la custodia,
  podría dar origen a discriminación.
- **Fotografías (`A-04`, `A-17`) y cámaras (`A-05`).** La definición incluye los datos
  biométricos. Una foto no es biométrica por sí sola, así que las marqué como no sensibles. No sé
  si la empresa de fotografía o la grabadora hacen algo más con las caras.
- **Reportes psicopedagógicos (`A-03`).** Los marqué como sensibles porque son de salud. La duda es
  sobre las familias: si un reporte habla de la familia del niño, también son datos de la familia,
  y no lo puedo saber sin abrirlos.
- **Nómina (`A-19`).** La marqué como no sensible. Si los documentos de contratación incluyen un
  examen médico, esa parte sí sería sensible. La ficha no lo dice.

## Lo que no pude establecer

1. **Cuánto tiempo se conserva casi todo.** Solo sé dos plazos: las cámaras, treinta días, y las
   fotografías, seis ciclos. Del resto no hay plazo, y lo que no se sabe que se debe borrar no se
   borra nunca. Tampoco sé cuánto tiempo guardan los datos el asistente de IA, la empresa de
   fotografía ni la aseguradora.
2. **Si hay copias fuera de los servidores.** No sé si la laptop de las psicopedagogas guarda
   copias de los reportes, si siguen fotos en la computadora de la directora, dónde está el disco
   externo de los respaldos, ni qué se mandan las maestras por su Gmail personal.
3. **Qué hace el asistente de IA con los reportes psicopedagógicos.** Los términos dicen que puede
   usar el contenido para mejorar sus servicios y nadie los ha leído. No sé si eso lo hace
   encargado de NOVA o si usa los datos para sus propios fines.

## Resumen personal

Entendí que no es lo mismo preguntar qué le pasa al colegio que preguntar a quién le pasa. En el
inventario de activos pensé en NOVA. Aquí tuve que pensar en los niños, y casi todos los datos son
de menores que no pueden decidir nada sobre ellos.

Lo que más me costó fue la columna de «de quién son». Al principio puse alumnos y tutores en todo,
pero al revisar con calma aparecieron personas que no esperaba: las que pueden recoger a un niño,
los egresados que siguen en las fotos, los compañeros de las fotos de grupo y cualquiera que pase
frente a una cámara. Ninguno de ellos dio su permiso.

También vi que lo que obliga a avisar no es qué tan grave es el fallo técnico, sino de quién son los
datos. Un fallo en el servidor de archivos importa mucho más por los reportes psicopedagógicos
que por el servidor. Para NOVA esto significa que lo primero es saber cuánto tiempo guarda cada
cosa y dónde hay copias, porque hoy casi todo dice «no se sabe».
