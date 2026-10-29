Prosa Original:


Detección 1, sobre el IoC de sistema, etapa 5 Instalación:
Alerta si el registro de eventos de Windows de cualquier computadora del colegio muestra la creación de una tarea programada llamada Time Trigger Task.
Detección 2, sobre el IoC de red, etapa 6 Comando y control:
Alerta si el registro de DNS o del firewall de la red del colegio muestra una consulta a api.2ip.ua desde una computadora del aula de cómputo o de la administración. Es un servicio legítimo, así que la alerta es para revisar el equipo, no para bloquear a ciegas.
Cuál detectaría más temprano: la detección 1, porque la persistencia es la etapa 5 y la comunicación con internet es la etapa 6. El orden exacto dentro de una variante concreta no lo pude confirmar sin un informe de sandbox.
Una regla por hash vería el archivo desde la etapa 4, pero cada variante nueva de stop trae otro hash, así que no la usé como detección principal.
Qué no se pudo llenar y por qué: las dos reglas necesitan una fuente de registro, y NOVA no tiene ninguna documentada. No hay auditoría de eventos centralizada ni registro de DNS o firewall en la ficha. Las reglas dicen qué habría que activar, y hoy no hay dónde ejecutarlas.




Regla Creada:

 <group name="malware,stop,ransomware,nova">

  <!-- Regla para detectar la creación de la tarea programada de persistencia del ransomware Stop -->

  <rule id="100207" level="12">

    <!-- Si la fuente es Sysmon (ID 4698 en Windows Security / ID 1 en Sysmon para creación de tareas) -->

    <!-- Usamos el ID 4698 del visor de eventos de Windows (Se creó una tarea programada) -->

    <if_sid>60100</if_sid>

    <match>Time Trigger Task</match>

    <description>NOVA [CRÍTICO]: Posible infección de Ransomware STOP (Djvu) - Se ha creado la tarea programada de persistencia: Time Trigger Task.</description>

    <mitre>

      <id>T1053.005</id> <!-- Scheduled Task: Scheduled Task -->

    </mitre>

  </rule>

</group> 

Log con el que se probo:

{"win":{"system":{"providerName":"Microsoft-Windows-Security-Auditing","eventID":"4698","computer":"NOVA-PC-01","systemTime":"2026-10-29T12:00:00.000Z"},"eventData":{"taskName":"\\Time Trigger Task"}},"message":"A scheduled task was created. Task Name: \\Time Trigger Task"}




Resultado del test:


**Messages:
        INFO: (7202): Session initialized with token '7a6cd00f'

**Phase 1: Completed pre-decoding.
        full event: '{"win":{"system":{"providerName":"Microsoft-Windows-Security-Auditing","eventID":"4698","computer":"NOVA-PC-01","systemTime":"2026-10-29T12:00:00.000Z"},"eventData":{"taskName":"\\Time Trigger Task"}},"message":"A scheduled task was created. Task Name: \\Time Trigger Task"}'

**Phase 2: Completed decoding.
        name: 'json'
        message: 'A scheduled task was created. Task Name: \Time Trigger Task'
        win.eventData.taskName: '\Time Trigger Task'
        win.system.computer: 'NOVA-PC-01'
        win.system.eventID: '4698'
        win.system.providerName: 'Microsoft-Windows-Security-Auditing'
        win.system.systemTime: '2026-10-29T12:00:00.000Z'

Respuesta pregunta:

La regla actual es ciega ante otras formas de persistencia o nombres de tareas distintos. Si cambia el dominio, la regla sigue funcionando porque busca el nombre de la tarea y no la red. Para detectar comportamiento, debes cazar la ejecución desde carpetas de usuario en lugar de un nombre fijo.

Resumen con mis propias palabras:
En esta practica comenzamos creando una regla adaptada a mi analisis de malware, de forma que podamos prevenir y detectar ataques de los equiṕos de la organización, en este caso del malware “Stop”, usamos un parametro de level 12 dentro de la regla para indicar que es urgente que alerte cuando detecte un ataque interno de este tipo. Al terminar de crear la regla se creo un Log ficticio controlado que al correr la prueba nos entrego un archivo en formato JSON en el cual podemos ver los detalles del log-in. Esta regla nos ayudara a detectar con este formato los posibles ataques que se generen y a capturar los detalles en este formato. 
