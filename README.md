# coipo_control-casino — Maqueta del control de ingreso al Casino Institucional

Maqueta de validación del sistema de control de ingreso al Casino Institucional de CONAF
para el Servicio de Bienestar, elaborada por la Unidad de Información y Análisis (UIA).
Iniciativa CON005.

**Ver la maqueta:** https://alvarozvjac.github.io/coipo_control-casino/

> Demostración no operacional. Personas, RUT, grados, valores y registros son ficticios. Lo que se haga en la maqueta no se guarda: al recargar la página vuelve al
> estado inicial.

## Cómo probarla

En el encabezado, el recuadro **«Maqueta · probar como»** cambia entre los cuatro perfiles.

| Perfil | Qué se puede probar |
|---|---|
| Terminal casino | Equipo instalado en el casino: terminal (RUT digitado, emisión del ticket) y propuesta de ticket |
| Funcionario | «Mi casino»: menú de la semana, selección del menú mensual (normal, hipocalórico o vegano), avisos de los días que no almorzará, almuerzos con invitados y reporte CSV |
| Jefe Casino | Estadísticas, detalle de ingresos, planificación de raciones, menú semanal, emisión de reportes, cierres del casino, personas habilitadas (grado y tramo) y configuración |
| Jefa de Bienestar | Estadísticas agregadas, emisión de reportes y cierres del casino |

**Terminal del casino:** la persona digita su RUT en un teclado numérico USB y presiona
Enter; la tecla `*` equivale a la K. La pantalla y el ticket muestran su nombre completo,
para que el personal del casino verifique la identidad. El **simulador del teclado
numérico**, al costado, digita el RUT de cada persona de prueba; también se puede usar el
teclado del computador. Las tres primeras personas (Carolina, Jorge y Daniela) muestran la
emisión completa del ticket; Daniela tiene hoy 2 almuerzos a su nombre. Otros casos: almuerzo
ya registrado, aviso de ausencia para hoy (Ignacio: igual puede almorzar; el aviso se anula solo y el
ingreso queda marcado «Asistió pese a aviso» en el detalle), habilitación suspendida, RUT que no está en la nómina y RUT mal digitado. La
hora está fijada en 13:05 y se cambia en Configuración. La validación con RUT y PIN queda
para una versión futura.

**Ticket:** sigla CONAF, fecha y lugar; cantidad de almuerzos y menú; nombre completo en mayúsculas, hora e ID único (año y correlativo anual, por ejemplo 2026-004812). El ID se registra en el detalle de ingresos del Jefe Casino, en «Mi casino» del funcionario y en el detalle por ticket del reporte mensual; el detalle de ingresos permite buscar por ID.

**Mi casino (funcionario):** en este orden, el menú de la semana publicado por el Jefe Casino
(entrada, plato normal, hipocalórico y vegano, y postre); «Selecciona tu menú mensual» (normal,
hipocalórico o vegano, hasta el día 25 del mes anterior); «Avisa los días que no almorzarás»
(un día o un rango, hasta las 23:59 del día anterior); «Almuerzo con invitados», con el monto
que se descontará; y el reporte del mes en CSV para Excel (ID de ticket, fecha, hora, almuerzos,
menú y monto). El aviso de ausencia sirve para planificar las raciones y no bloquea: si la
persona cambia de planes y digita su RUT, almuerza igual y su aviso se anula solo. Solo se
descuentan los almuerzos consumidos. Los almuerzos con
invitados se descuentan al funcionario según su tramo.

**Planificación (Jefe Casino):** próximos 10 días hábiles con habilitados, ausencias
avisadas, menú normal, hipocalórico y vegano, almuerzos de invitados, raciones planificadas y
consumo habitual como referencia.

**Menú del mes:** el funcionario elige el menú de cada mes hasta el día 25 del mes anterior;
«Mi casino» muestra el mes actual, el siguiente y, si este ya cerró, el próximo que se puede
elegir, y aclara que sin elección el menú es Normal. Para casos justificados (ingreso nuevo,
indicación médica) el Jefe Casino registra un **cambio de menú por excepción** en Personas
habilitadas, para el mes actual o el siguiente, con motivo y registro de quién y cuándo.

**Menú semanal (Jefe Casino):** cada lunes publica la minuta de la semana (entrada, plato
normal, hipocalórico y vegano, y postre), que reemplaza el envío de la
minuta por correo electrónico. Los cambios quedan como borrador hasta publicarlos. La maqueta
usa como ejemplo las minutas reales de octubre de 2026, ajustadas a la semana actual y las dos
anteriores.

**Reportes:** la pantalla muestra el descuento por planilla del mes. El botón «Emisión reporte
mensual» despliega tres reportes que se descargan en CSV para Excel: 1) reporte descuento
mensual (por trabajador y detalle por ticket), 2) reporte consumo por unidad y 3) reporte
anual por mes.

**Valor del almuerzo:** se define por tramo según el grado (tramo 1: grados 3 a 11;
tramo 2: 12 a 14; tramo 3: 15 a 21). Las calidades jurídicas son Dotación, Plazo fijo y Honorarios; solo Dotación tiene grado, y
quienes no lo tienen (plazo fijo y honorarios) reciben el tramo que asigna el Jefe Casino. Los valores son de ejemplo.

**Cierres del casino:** al registrar o anular un cierre (clima, mantención, catástrofe,
corte de suministro u otro), el otro perfil recibe una alerta. Durante un cierre vigente
la terminal no emite tickets. Al abrir como Jefe Casino aparece una alerta de ejemplo
enviada por la Jefa de Bienestar.

**Reiniciar datos de prueba**, en el pie de página, vuelve todo al estado inicial.

## Contenido del repositorio

- `index.html`: la maqueta completa en un solo archivo (código, estilos e imágenes
  incluidos), sin dependencias externas.

Documentos de referencia: solicitud del Servicio de Bienestar (13-08-2026) y propuesta
comercial «Control de Comedor» de GeoVictoria (agosto 2026). Por acuerdo de la reunión UIA
del 22-10-2026, la solución identifica a las personas por su RUT digitado en un teclado
numérico, sin datos biométricos, licencia ni arriendo; la validación con RUT y PIN queda
para una versión futura.
