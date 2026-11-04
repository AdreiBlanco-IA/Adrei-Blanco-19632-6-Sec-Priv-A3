# Bitácora de uso de inteligencia artificial

NOVA, A.C.

Este registro es obligatorio. No es para vigilar, es para poder explicar mi propio proceso, y para
que si algo sale mal sepa de dónde salió.

## Cómo se llena

Un renglón por cada vez que usé IA para algo que terminó en un entregable. Si la usé solo para
entender algo y no lo entregué, no lo anoto.

| Fecha | Qué herramienta | Para qué la usé | Qué me dio | Qué hice con eso |
|---|---|---|---|---|
| 23 sep | Asistente de la materia | Entender el documento de operaciones maliciosas y pruebas de seguridad, para saber qué pedía cada entregable | Un resumen de los cuatro tipos de prueba y las tres distinciones entre ellas | Lo usé para decidir qué tipo de prueba le convenía a NOVA, pero escribí la justificación con la información real del colegio, no con el resumen |
| 23 sep | Asistente de la materia | Redactar la ficha de decisión sobre NOVA | Un borrador con un objetivo de negocio, el tipo de prueba elegido y quién debía autorizarla | El primer borrador inventó un objetivo que no estaba en ningún documento, un portal para que los papás vieran calificaciones. Lo rechacé y pedí que usara solo lo que sí dice el documento de NOVA, que es el asistente pedagógico de inteligencia artificial que ya está contratado |
| 23 sep | Asistente de la materia | Resolver y documentar los veinticuatro ejercicios de la práctica de shell | Los comandos y las respuestas de las cuatro preguntas de la investigación | Antes de dejar cualquier respuesta, se corrió cada comando en la terminal para comprobar que el resultado fuera real y no inventado |
| 23 sep | Asistente de la materia | Escribir la carta de organización de NOVA | Un borrador basado en el documento de la organización que ya tenía | Lo comparé línea por línea contra el documento original, para que no agregara nada que no estuviera ahí |
| 8 oct | Asistente de IA | Tareas de redacción e interpretación del análisis de malware de la sesión 16 | — | — |
| 3 nov | Claude (Claude Code con acceso a Chrome) | Redactar el inventario de activos, a partir de la ficha de NOVA y del ejemplo de Taller Reforma | La tabla de veinte activos con sus siete columnas, la nota de ponderación de A-02 y la nota de lo que no se pudo inventariar | Lo escribió y lo subió a 00-organizacion/activos.md a petición mía. Pendiente: revisarlo renglón por renglón contra la ficha y anotar aquí qué cambié o rechacé |
| 3 nov | Claude (Claude Code con acceso a Chrome) | Redactar el registro de riesgos, sobre el inventario, el análisis de malware y el caso php2shell | Nueve riesgos con P, I, tratamiento y residual, los dos riesgos aceptados y tres recomendaciones del caso php2shell | Lo escribió y lo subió a 01-riesgos/registro-riesgos.md a petición mía. No incluye la verificación de la línea de tiempo contra fuentes primarias. Pendiente: revisar las calificaciones de P e I y anotar aquí qué cambié o rechacé |
| 3 nov | Claude (Claude Code con acceso a Chrome) | Redactar el perfil NIST CSF 2.0 | Diez renglones con identificadores revisados contra frameworks/CSF-2.0-vigente.csv y la nota de que RESPOND y RECOVER quedaron vacías | Lo escribió y lo subió a 01-riesgos/perfil-nist-csf.md a petición mía. Pendiente: comprobar cada identificador en el Excel y anotar aquí qué cambié o rechacé |
| 3 nov | Claude (Claude Code con acceso a Chrome) | Completar la sección de lo que no detecta mi regla de Wazuh | Cinco límites de la regla y cómo cambiarla para detectar el comportamiento | Lo agregó a 04-detecciones/regla-wazuh.md a petición mía. La salida del logtest y mi resumen no los tocó: los tengo que poner yo |

## Lo que aprendí de usarla

Sirve para no quedarme en blanco y para no perder tiempo armando la estructura de cada documento.

Inventa con seguridad. En la ficha de decisión propuso un objetivo de negocio que sonaba real pero no
estaba en ningún documento que le di. Sonaba igual de convencido que cuando sí tenía la información
correcta.

No sabe nada de mi organización si no se lo doy. Todo lo que aparece sobre NOVA en estos documentos
viene del documento de la organización que ya existía, no de algo que la IA se haya inventado.

Lo que sí tengo que hacer es poder explicar por qué cada decisión es la que tomé, no la IA, porque
eso es lo que se revisa en la defensa, no el documento.

Declarar el uso de IA no baja la calificación. No declararlo sí.
