# Comandos y detecciones

Práctica de shell, veinticuatro ejercicios. Ambiente montado en ~/practica siguiendo el bloque de
configuración del ejercicio.

## Tabla de comandos

| comando | para qué sirve | ejemplo que corrí |
|---|---|---|
| wc -l | contar líneas | wc -l < registros/auth.log |
| grep -c | contar cuántas líneas contienen un texto | grep -c "Failed password" registros/auth.log |
| grep -oE | sacar solo la parte del texto que hace match con un patrón, por ejemplo una IP | grep -oE "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" registros/auth.log |
| sort y uniq -c | ordenar los valores y después contar cuántas veces se repite cada uno | grep "Failed password" registros/auth.log \| grep -oE "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" \| sort \| uniq -c \| sort -rn |
| cut | sacar una columna de un archivo separado por comas | cut -d, -f3 documentos/empleados.csv \| sort -u |
| find | buscar archivos por nombre en todo un árbol de carpetas | find . -name "*.log" \| wc -l |
| file | ver de qué tipo es un archivo de verdad, sin fiarse de la extensión | file documentos/reporte.txt |
| sha256sum | calcular el hash de un archivo, para poder demostrar después que nadie lo modificó | grep "45.83.12.7" registros/auth.log > evidencia-45.83.12.7.log && sha256sum evidencia-45.83.12.7.log |

## Las cuatro preguntas

1. Por qué el acceso de ana no es sospechoso y el de bruno sí, si los dos dicen Accepted

Ana entró con llave pública, desde una IP interna de la red, 192.168.10.20, y esa IP nunca antes había
fallado ningún intento. Bruno entró con contraseña, y desde la misma IP que estuvo probando
contraseñas contra el usuario admin sesenta veces antes, 45.83.12.7. Que las dos líneas digan Accepted
solo dice que el inicio de sesión funcionó, no dice si la conexión es confiable. Lo que cambia todo es
de dónde viene la conexión y cómo se autenticó.

2. La política dice bloqueo tras 5 intentos, hubo 60. Qué significa eso sobre esa política

Significa que la política está escrita pero no está aplicada en ningún lado. Nadie configuró el
servidor para bloquear después de 5 intentos fallidos, porque si eso estuviera activo, la IP
45.83.12.7 no hubiera podido probar sesenta veces seguidas. Una política que nadie implementó no
protege a nadie, solo deja constancia de que sabían qué hacer y no lo hicieron.

3. Qué habrías necesitado tener puesto para enterarte esa misma mañana y no tres semanas después

Habría necesitado una alerta que avisara cuando la misma IP falla muchas veces seguidas contra el mismo
servicio, y otra alerta cuando alguien usa sudo para leer un archivo como /etc/shadow. Sin algo que lea
el log en el momento y avise, esto solo se descubre revisando el archivo después, cuando ya pasó.

4. Por qué le saqué hash al archivo de evidencia. Qué pasaría si no lo hubiera hecho y alguien edita el log mañana

Le saqué hash porque eso permite demostrar después que el archivo que guardé es exactamente el mismo
que se generó ese día, sin que nadie le haya cambiado una sola línea. Si no lo hubiera hecho y alguien
edita el log mañana, ya no tendría forma de probar que la evidencia no fue modificada, y eso le quita
valor si algún día se necesita mostrar qué pasó.

## Resumen con mis propias palabras

En la práctica de shell aprendí que con pocos comandos se puede leer un registro y encontrar lo que pasó: contar intentos fallidos, sacar las IP que más se repiten y separar un acceso normal de uno sospechoso. Que dos líneas digan Accepted no significa lo mismo; lo que importa es desde dónde entró cada quien y cómo se autenticó.

También vi que una política escrita no protege si nadie la configura, y que sacar el hash de la evidencia sirve para demostrar después que nadie la cambió. Para NOVA esto importa porque hoy no tiene ningún registro que alguien revise, así que un ataque así se descubriría semanas después o nunca.

### Dudas que me quedaron

- No sé cómo se pondría en NOVA una alerta como la que propuse en la pregunta 3, si el colegio no tiene a nadie que revise los registros.
