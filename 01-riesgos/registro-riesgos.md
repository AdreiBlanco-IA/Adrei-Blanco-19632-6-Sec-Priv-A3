# Registro de riesgos

**NOVA, A.C.**

## Cómo se calificó

**Probabilidad** y **Impacto** en escala de 1 a 5. **Riesgo** es el producto. El **riesgo residual** es lo
que queda después del tratamiento aplicado.

| Nivel | Riesgo |
|---|---|
| 1 a 6 | Bajo |
| 8 a 12 | Medio |
| 15 a 25 | Alto |

## Los riesgos

| ID | Activo | Amenaza | Vulnerabilidad | P | I | Riesgo | Tratamiento | Residual |
|---|---|---|---|---|---|---|---|---|
| R-01 | A-03 | Una maestra titular abre y copia el reporte psicopedagógico de un alumno que no es de su grupo | Los reportes están en una carpeta del servidor de archivos a la que entran las catorce maestras titulares, no solo las dos psicopedagogas | 4 | 5 | **20 Alto** | Mitigar: que la carpeta la abran solo las dos psicopedagogas | **5 Bajo** |
| R-02 | A-12 | El proveedor del asistente usa los reportes psicopedagógicos que se le suben para mejorar su servicio, y quedan fuera del control del colegio | Plan de consumidor de 20 dólares al mes, sin acuerdo de tratamiento de datos. Los términos permiten usar el contenido y nadie los ha leído. Desde hace meses se suben los reportes "para que los comentarios salgan más completos" | 4 | 5 | **20 Alto** | Evitar: dejar de subir reportes psicopedagógicos al asistente | **10 Medio** |
| R-03 | A-02 | Una administrativa abre un adjunto con el ransomware stop y se cifran las carpetas del servidor de archivos que ve su computadora | Expedientes, fotografías y reportes psicopedagógicos nunca se respaldan. El servidor de archivos nunca se ha actualizado, y ninguna etapa del ataque deja un registro que alguien revise | 3 | 5 | **15 Alto** | Mitigar: respaldo semanal en un disco que se desconecta después de copiar, y una prueba de restauración cada bimestre | **6 Bajo** |
| R-04 | A-06 | Alguien desde internet ejecuta código en el servidor de control escolar sin necesitar credenciales, como en php2shell | NOVA no sabe si la plataforma usa PHP ni qué versión corre. El servidor no recibe actualizaciones desde 2022 y el proveedor tiene acceso remoto permanente, así que el servidor se alcanza desde fuera | 3 | 5 | **15 Alto** | Transferir: exigir por escrito al proveedor que avise de fallas graves y aplique los parches en un plazo | **10 Medio** |
| R-05 | A-10 | Una maestra que ya dejó el colegio sigue entrando al asistente con la cuenta compartida y consulta calificaciones y notas de los alumnos | Una sola cuenta para la subdirectora y las catorce maestras. El colegio no puede saber quién entró ni quién subió cada documento | 3 | 4 | **12 Medio** | Mitigar: una cuenta por persona y baja el mismo día que alguien sale | **4 Bajo** |
| R-06 | A-17 | Una maestra que dejó el colegio sigue en el grupo de WhatsApp de su salón y ve fotos de los niños y comentarios sobre su desempeño | Los grupos los administra cada maestra desde su celular personal, y cuando una maestra se va nadie la saca | 4 | 3 | **12 Medio** | Mitigar: que la dirección sea administradora de todos los grupos y saque a quien se va el mismo día | **6 Bajo** |
| R-07 | A-01 | Una falla del servidor o una actualización mal aplicada borra las calificaciones del bimestre | El respaldo de la plataforma es solo cada bimestre, a un disco externo. La ficha no dice que alguien haya probado restaurarlo | 3 | 4 | **12 Medio** | Mitigar: respaldo semanal y prueba de restauración | **4 Bajo** |
| R-08 | A-11 | Alguien que obtiene las credenciales del proveedor entra al servidor de control escolar por el acceso remoto | El acceso es permanente "para poder atender rápido", y el colegio no sabe cuándo se usa ni quién lo usa | 2 | 5 | **10 Medio** | **Aceptar.** Ver abajo | **10 Medio** |
| R-09 | A-14 | La empresa de fotografía sufre una filtración en su portal y se publican las fotos de los alumnos con su nombre y grupo | Recibe cada año la lista completa de alumnos. No hay contrato firmado: se acordó de palabra hace ocho años | 2 | 4 | **8 Medio** | **Aceptar.** Ver abajo | **8 Medio** |

## Los dos riesgos que se aceptan, y por qué

**R-08 · El acceso remoto del proveedor.** Quitarlo dejaría al colegio sin soporte rápido de la plataforma,
y el colegio no tiene a nadie que la pueda arreglar por su cuenta. Se **acepta por ahora**, con dos
condiciones que sí se pueden cumplir: que el proveedor avise a la dirección cada vez que entre, y que el
maestro de cómputo anote la fecha y el motivo. Se revisa al terminar el ciclo escolar, o antes si hay un
aviso de una falla grave en la plataforma, como pasó con php2shell.

**R-09 · La empresa de fotografía.** NOVA **no puede tratar este riesgo por sí sola**: depende de que la
empresa acepte firmar un contrato, y cambiar de empresa a mitad del ciclo no es realista. Se acepta, se
documenta, y se le pide por escrito a la empresa que diga qué hace con la lista y con las fotos, para que
exista constancia de que se pidió. Se revisa antes de la próxima sesión de fotos.

**R-02 y R-04 se quedan en Medio aunque se traten.** Lo que ya se subió al asistente no se puede recuperar,
y NOVA no administra el servidor de la plataforma: solo puede exigirle al proveedor.

## Recomendaciones · caso php2shell

| # | Qué | Quién | Cuándo |
|---|---|---|---|
| 1 | Preguntarle por escrito al proveedor si la plataforma usa PHP, qué versión, y si ya aplicó el parche | La directora. NOVA no tiene responsable de seguridad, y ése es el hallazgo | Esta semana |
| 2 | Cuando salga un aviso de una falla grave sin parche, cortar el acceso desde internet al servidor de control escolar, incluido el del proveedor, y reconectarlo solo cuando el proveedor confirme por escrito que aplicó el parche | El maestro de cómputo, con autorización de la directora | El mismo día del aviso |
| 3 | Para la próxima: nombrar a una persona que reciba los avisos de seguridad y pedirle al proveedor, por contrato, que avise al colegio de cualquier falla grave en un plazo de 24 horas | La directora | Antes de renovar la licencia de la plataforma |
