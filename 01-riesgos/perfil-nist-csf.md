# Perfil NIST CSF 2.0

**NOVA, A.C.**

Para cada activo crítico o riesgo Alto se buscó en `frameworks/CSF-2.0-vigente.csv` la **subcategoría** que
describe el resultado que hace falta. La subcategoría dice *qué tiene que estar logrado*; el control es
*cómo se logra*.

| Activo | Función | Categoría | Subcategoría | Qué resultado exige |
|---|---|---|---|---|
| A-03 reportes psicopedagógicos (R-01) | PROTECT | PR.AA | **PR.AA-05** | Que los permisos de acceso estén definidos, se revisen y sigan el principio de mínimo privilegio |
| A-10 cuenta compartida del asistente (R-05) | PROTECT | PR.AA | **PR.AA-01** | Que las identidades y credenciales de los usuarios autorizados estén gestionadas |
| A-12 asistente pedagógico (R-02) | GOVERN | GV.SC | **GV.SC-05** | Que los requisitos de seguridad se establezcan en los contratos y acuerdos con proveedores |
| A-02 expedientes (R-03) | PROTECT | PR.DS | **PR.DS-11** | Que los respaldos se creen, se protejan, se mantengan y se prueben |
| A-06 servidor de control escolar (R-04) | PROTECT | PR.PS | **PR.PS-02** | Que el software se mantenga, se reemplace o se retire de acuerdo con el riesgo |
| A-06 servidor de control escolar (R-04) | IDENTIFY | ID.RA | **ID.RA-08** | Que existan procesos para recibir, analizar y responder a los avisos de vulnerabilidades |
| A-11 acceso remoto del proveedor (R-08) | DETECT | DE.CM | **DE.CM-06** | Que se monitoree la actividad de los proveedores externos para encontrar eventos adversos |
| A-09 aula de cómputo (R-03) | DETECT | DE.CM | **DE.CM-09** | Que el hardware, el software y sus datos se monitoreen para encontrar eventos adversos |
| Todo el colegio | GOVERN | GV.RR | **GV.RR-02** | Que estén establecidos y comunicados los roles y responsabilidades de ciberseguridad |
| Todo el colegio | IDENTIFY | ID.AM | **ID.AM-01** | Que se mantenga un inventario del hardware |

## Lo que salió al llenar esta tabla

**RESPOND y RECOVER quedaron vacías, y fue decisión.** NOVA no tiene de qué agarrarse para responder ni
para recuperarse: no hay nadie responsable de la seguridad, y los expedientes, las fotografías y los
reportes psicopedagógicos nunca se respaldan. Escribir un resultado de recuperación sobre respaldos que no
existen no tendría sentido. Primero tiene que estar logrado PR.DS-11, que haya respaldos, y GV.RR-02, que
alguien responda. Hoy, el día de un incidente, NOVA no podría restaurar nada de lo que hay en el servidor de
archivos.

**Cuatro de los diez renglones caen en GOVERN e IDENTIFY**, y casi todos tienen que ver con terceros o con
que nadie está a cargo. El asistente, la plataforma y el acceso remoto dependen de proveedores con los que
no hay acuerdos por escrito. Eso no se arregla comprando algo.

> Los diez identificadores están verificados contra `frameworks/CSF-2.0-vigente.csv`, que solo trae las
> subcategorías vigentes. No se usó ningún identificador retirado de la versión 1.1, como PR.AC.

## Resumen con mis propias palabras

El perfil me ayudó a entender la diferencia entre lo que tiene que estar logrado y cómo se logra. La subcategoría dice el resultado, por ejemplo que los respaldos existan y se prueben, y el control es la forma de llegar ahí, como un disco que se conecta cada semana. Si escribo un control en lugar del resultado, el renglón está mal.

Al llenarlo vi que en NOVA casi todo depende de que alguien se haga responsable y de los acuerdos con proveedores, y eso no se arregla comprando una herramienta. RESPOND y RECOVER quedaron vacías porque el colegio no tiene con qué responder ni con qué recuperarse si pasa algo.

### Dudas que me quedaron

- No sé si está bien dejar dos funciones completamente vacías, o si convenía poner un renglón en RECOVER aunque hoy no haya respaldos.
