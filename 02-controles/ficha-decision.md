# Ficha de decisión

Organización: NOVA, A.C.

## El objetivo de negocio

NOVA quiere abrir un portal en internet para que los papás puedan entrar y ver las calificaciones y
las boletas de sus hijos sin tener que ir al colegio a pedirlas. Este portal se conectaría a la
plataforma de control escolar que ya tiene el colegio, la que corre en el servidor con Windows Server
2016.

Este es un cambio de negocio, no de seguridad: el colegio lo quiere para dejar de imprimir boletas y
para que los papás dejen de llamar a la administración cada vez que necesitan una calificación.

## Pregunta 1. Qué tipo de prueba elegiría

Elegiría una prueba de penetración.

El portal va a quedar expuesto en internet y va a dar acceso a datos de alumnos que son menores de
edad, incluidas calificaciones y reportes de conducta. Antes de dejar que cualquier papá entre desde
su casa, necesito saber si alguien de fuera podría realmente entrar al sistema y hasta dónde llegaría,
no solo si hay fallas conocidas en la lista que arroja un escaneo.

## Pregunta 2. Por qué descarté los otros dos tipos

Escaneo de vulnerabilidades. Lo descarté como prueba principal porque un escaneo solo dice que hay una
puerta sin llave, no dice si esa puerta lleva a algún lado. Con un servidor tan viejo como el de
control escolar, un escaneo iba a sacar cientos de hallazgos y no me iba a decir si alguien puede de
verdad entrar y leer los datos de un alumno.

Auditoría. La descarté porque una auditoría revisa que el colegio cumpla con lo que dijo que hace, no
si el sistema resiste un ataque real. NOVA además casi no tiene políticas escritas, así que una
auditoría en este momento me diría poco. Se puede pasar una auditoría impecable y de todos modos caer
en el primer intento de entrar de verdad.

## Pregunta 3. A quién le pediría la autorización

Se la pediría a la directora, porque es quien responde legalmente por el colegio y por los datos de
los alumnos. El maestro de cómputo administra el servidor, pero no tiene la facultad para autorizar
una prueba sobre datos de menores de edad.

Como la plataforma de control escolar es de un proveedor externo que tiene acceso remoto permanente al
servidor, también habría que avisarle a él antes de probar, porque el sistema y el servidor están bajo
su soporte.

El documento de autorización tendría que decir:

Qué sistemas se van a probar, con sus direcciones. En este caso el servidor de control escolar y el
portal nuevo, no el servidor de archivos que guarda las fotos y los reportes psicopedagógicos, porque
ese servidor no forma parte de este objetivo de negocio.

Cuándo empieza y cuándo termina la prueba, con fecha y hora de inicio y fin.

Hasta dónde se puede llegar. Aquí hay que decidir si se pueden usar datos reales de alumnos o solo una
copia de prueba, porque el sistema maneja datos de salud y datos de menores de edad.

A quién avisar si se encuentra algo grave y en cuánto tiempo.

Quién firma. En este caso la directora, junto con el visto bueno del proveedor, porque el servidor no
es del colegio para tocarlo sin avisarle a quien lo administra.
