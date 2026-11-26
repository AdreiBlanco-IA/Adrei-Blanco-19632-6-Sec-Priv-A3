# CVSS · NOVA, A.C.

**Práctica de la sesión 27** · `laboratorio/practica-cvss.md`

Vectores tomados de la ficha de cada CVE en el NVD, versión 3.1, el 26 de noviembre de 2026. Las
notas y las pruebas de qué métrica pesa más se hicieron con la calculadora de FIRST v3.1. Los
nombres de cada pareja salen de `laboratorio/glosario-cvss.md`. Los activos `A-XX` son los de mi
`00-organizacion/activos.md`.

---

## 1 · CVE-2021-41773 · Apache HTTP Server

**Producto afectado:** Apache HTTP Server 2.4.49. Un cambio en cómo normaliza las rutas permite
pedir archivos fuera de las carpetas configuradas.

**Vector según el NVD:**

```
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H   →   9.8  CRÍTICA
```

| Pareja | En palabras | Qué quiere decir aquí |
|---|---|---|
| `AV:N` | Vector de ataque: Red | Basta con mandar una petición web al servidor desde Internet. No hay que estar dentro de la organización |
| `AC:L` | Complejidad: Baja | La petición armada funciona cada vez. No depende de ninguna condición especial del servidor |
| `PR:N` | Privilegios: Ninguno | No hace falta cuenta. El servidor web atiende a cualquiera que le pida una página |
| `UI:N` | Interacción: Ninguna | Nadie del lado de la víctima tiene que abrir ni aceptar nada |
| `S:U` | Alcance: Sin cambio | El daño se queda en el servidor donde corre Apache |
| `C:H` | Confidencialidad: Alta | Se pueden leer archivos fuera de la carpeta del sitio, no solo las páginas publicadas |
| `I:H` | Integridad: Alta | La ficha dice que, si además están habilitados los scripts CGI, se puede ejecutar código, y con eso cambiar lo que sea en el servidor |
| `A:H` | Disponibilidad: Alta | Con código ejecutándose en el servidor, se puede apagar el sitio o borrar lo que lo sostiene |

**La que más pesa aquí es `AC:L`, porque el ataque funciona siempre, sin condiciones.** Lo
comprobé en la calculadora cambiando una métrica a la vez: con `AC:H` la nota baja de 9.8 a
**8.1**. Con `AV:A`, `PR:L` o `UI:R` baja a 8.8, y con `C:L`, `I:L` o `A:L` baja a 9.4.

---

## 2 · CVE-2019-0708 · BlueKeep

**Producto afectado:** el servicio de Escritorio Remoto (RDP) de Windows 7, Windows Server 2008 y
Windows Server 2008 R2, según el ejemplo de la materia.

**Vector según el NVD:**

```
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H   →   9.8  CRÍTICA
```

| Pareja | En palabras | Qué quiere decir aquí |
|---|---|---|
| `AV:N` | Vector de ataque: Red | El atacante solo tiene que alcanzar el puerto de Escritorio Remoto. No tiene que estar sentado frente al equipo |
| `AC:L` | Complejidad: Baja | Las peticiones armadas funcionan cada vez que se mandan |
| `PR:N` | Privilegios: Ninguno | La ficha dice que el atacante no está autenticado: el fallo ocurre antes de pedir usuario y contraseña |
| `UI:N` | Interacción: Ninguna | Nadie tiene que dar clic. Basta con que el servicio esté encendido |
| `S:U` | Alcance: Sin cambio | El daño se queda en la máquina atacada |
| `C:H` | Confidencialidad: Alta | Se ejecuta código en el equipo, así que se lee todo lo que tenga guardado |
| `I:H` | Integridad: Alta | Se puede modificar o borrar cualquier archivo de esa máquina |
| `A:H` | Disponibilidad: Alta | Se puede apagar o inutilizar el equipo completo |

**La que más pesa aquí es `AC:L`, porque no hay que esperar ninguna condición para que funcione.**
Es el mismo vector que el de Apache, así que la calculadora da lo mismo: con `AC:H` baja de 9.8 a
**8.1**. Con `PR:L` baja a 8.8, igual que con `AV:A` o `UI:R`. El ejemplo de Taller Reforma dice
que pesa más `PR:N`. En mi prueba, `PR:N` es la segunda, empatada con `AV` y `UI`.

---

## 3 · CVE-2014-0160 · Heartbleed

**Producto afectado:** OpenSSL 1.0.1 antes de la 1.0.1g, en su manejo de TLS y DTLS.

**Vector según el NVD:**

```
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N   →   7.5  ALTA
```

| Pareja | En palabras | Qué quiere decir aquí |
|---|---|---|
| `AV:N` | Vector de ataque: Red | Basta con conectarse al servicio cifrado del servidor desde Internet y mandarle un paquete armado |
| `AC:L` | Complejidad: Baja | El paquete funciona cada vez, y se puede repetir para sacar más memoria |
| `PR:N` | Privilegios: Ninguno | El paquete se manda al iniciar la conexión, antes de cualquier usuario y contraseña |
| `UI:N` | Interacción: Ninguna | Nadie tiene que hacer nada. El servidor responde solo |
| `S:U` | Alcance: Sin cambio | Lo que se lee es la memoria del mismo proceso que tiene el fallo |
| `C:H` | Confidencialidad: Alta | La ficha dice que se puede sacar información de la memoria, incluidas llaves privadas |
| `I:N` | Integridad: Ninguna | El atacante solo lee. No cambia nada en el servidor |
| `A:N` | Disponibilidad: Ninguna | El servicio sigue funcionando. La víctima ni se entera |

**La que más pesa aquí es `C:H`, porque es el único daño que tiene este fallo.** En la
calculadora, con `C:L` la nota baja de 7.5 a **5.3**, y con `C:N` baja a **0**. Con `AC:H` baja
a 5.9 y con `AV:A`, `PR:L` o `UI:R` a 6.5. Sin la fuga de información no queda nada.

---

## 4 · ¿Existe en NOVA?

Escogí **BlueKeep**.

**No lo tengo. Revisé mi inventario y ninguno de mis activos usa esa tecnología.**

Los equipos con Windows que aparecen en `activos.md` son `A-06`, el servidor de control escolar con
**Windows Server 2016**, y `A-09`, las seis computadoras del aula de cómputo con **Windows 10**.
Ninguno es Windows 7, Server 2008 ni Server 2008 R2.

**Lo que no sé, y es parte del hallazgo:** las laptops de la dirección (2019), la laptop de las
psicopedagogas (`A-08`), las tres computadoras de las administrativas y las tabletas de la caja no
tienen versión de sistema en el inventario. NOVA no tiene inventario de equipos. Que yo no
encuentre Windows 7 no garantiza que no haya uno.

---

## 5 · Cómo cambiaría el vector si lo tuviera

Como contesté «no lo tengo», lo imagino en el equipo donde más daño haría: **`A-06`, el servidor
de control escolar**, porque el proveedor de la plataforma tiene acceso remoto permanente a él
(`A-11`).

| Métrica | NVD | NOVA | Por qué |
|---|---|---|---|
| `AV:N` | Red | `AV:N` | No cambia. El proveedor entra de forma remota y permanente, así que el servidor se alcanza desde fuera del colegio. La ficha no dice por dónde entra |
| `AC:L` | Baja | `AC:L` | No cambia |
| `PR:N` | Ninguno | `PR:N` | No cambia. El fallo está antes del inicio de sesión: tener cuenta no protege |
| `UI:N` | Ninguna | `UI:N` | No cambia |
| `S:U` | Sin cambio | `S:U` | No cambia |
| `C:H` | Alta | `C:H` | Ahí están las calificaciones, los reportes de conducta y los datos de los 240 alumnos y sus tutores (`A-01`) |
| `I:H` | Alta | `I:H` | Se podrían cambiar calificaciones y boletas sin que nadie lo note |
| `A:H` | Alta | `A:H` | En mi inventario `A-06` tiene disponibilidad como propiedad dominante y criticidad Alta. Si se cae, no hay boletas, y el respaldo puede tener hasta dos meses |

**Con lo que dice la ficha de NOVA, no cambiaría ninguna métrica.** El vector queda igual:

```
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```

La única métrica que podría cambiar es `AV`, y depende de un dato que NOVA no tiene: **cómo entra
el proveedor**. Si se comprobara que el Escritorio Remoto solo se alcanza desde la red del colegio
y que el proveedor entra por otra vía, quedaría:

```
CVSS:3.1/AV:A/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```

---

## 6 · Los dos números

| | Nota |
|---|---|
| Vector del NVD | **9.8** Crítica |
| Vector de NOVA, con lo que se sabe hoy | **9.8** Crítica |
| Vector de NOVA, si el Escritorio Remoto no saliera a Internet | **8.8** Alta |

**Por qué no cambió:** en NOVA no hay nada que haga el ataque más difícil. El servidor se alcanza
desde fuera por el acceso del proveedor, no pide cuenta antes del fallo y guarda datos de todos
los alumnos. La nota de NOVA es igual a la del NVD porque al colegio le falta todo lo que podría
bajarla.

**Qué separaría los números:** solo `AV`. Pero aun con 8.8, en la misma red están las seis
computadoras del aula de cómputo (`A-09`), que usan los alumnos sin control. Estar en la red
interna no protege mucho.

---

## 7 · La pregunta de criterio

> Tengo dos hallazgos. Uno de **9.8** en un equipo que mi organización **no tiene**. Otro de
> **5.3** en un equipo que sí tengo y que está expuesto a Internet.
>
> ¿Cuál atiendo primero y por qué?

Primero el de **5.3**. El 9.8 describe un fallo en algo que NOVA no tiene: no hay nada que atacar,
así que no es un riesgo para el colegio. El de 5.3 está en un equipo que sí existe y que cualquiera
alcanza desde Internet. En NOVA, además, podría ser el servidor con datos de menores, y una nota
baja en un activo real pesa más que una alta en uno que no está.

---

## 8 · Qué subcategoría del perfil atiende esto

| | Subcategoría | Por qué |
|---|---|---|
| **El caso** (un fallo de Windows sin parchar en `A-06`) | `PR.PS-02` · Que el software se mantenga, se reemplace o se retire de acuerdo con el riesgo | Ya está en mi perfil para `A-06`. Parchar o reemplazar el servidor cierra el fallo concreto |
| **La clase** (servicios de acceso remoto que cualquiera alcanza) | `PR.IR-01` · Que las redes y los entornos estén protegidos contra acceso lógico y uso no autorizado | **No está en mi perfil.** Si solo el proveedor, por una ruta controlada, pudiera llegar al servidor, el siguiente fallo de este tipo no se alcanzaría desde cualquier lado |

---

## Resumen personal

Lo que más me sirvió fue entender que la nota del NVD mide el fallo en abstracto y que el trabajo
de verdad es ver si me toca. BlueKeep no me toca, porque NOVA no tiene Windows 7 ni Server 2008
en el inventario. Aun así no lo puedo asegurar del todo, porque el colegio no sabe qué sistema
tienen varias de sus computadoras.

Me sorprendió que al imaginarlo en el servidor de control escolar la nota no bajara nada. Esperaba
que el ambiente de NOVA la bajara, pero pasó lo contrario: no hay nada que haga más difícil el
ataque. El servidor se alcanza desde fuera por el acceso del proveedor y tiene los datos de todos
los alumnos. La única métrica que podría bajarla depende de saber cómo entra el proveedor, y eso
nadie en el colegio lo sabe.

Lo que me costó fue encontrar la métrica que más pesa. Pensé que iba a ser `PR:N`, como en el
ejemplo, pero en la calculadora la que más movía la nota en Apache y en BlueKeep era `AC:L`. En
Heartbleed fue `C:H`, porque es el único daño que hace.

Para NOVA esto significa que primero hay que saber qué tiene y qué está expuesto, antes de
preocuparse por la nota de cada aviso.
