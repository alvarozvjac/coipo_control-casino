# coipo_control-casino — Maqueta del control de ingreso al Casino Institucional

Maqueta de validación del sistema de control de ingreso al Casino Institucional de CONAF
para el Servicio de Bienestar, elaborada por la Unidad de Información y Análisis (UIA).
Iniciativa CON005.

**Ver la maqueta:** https://alvarozvjac.github.io/coipo_control-casino/

> Demostración no operacional. Personas, RUT, niveles y registros son ficticios; los valores del almuerzo por nivel y el vale extra son los informados por Bienestar (marzo 2026). Lo que se haga en la maqueta no se guarda: al recargar la página vuelve al
> estado inicial.

## Cómo probarla

En el encabezado, el recuadro **«Maqueta · probar como»** cambia entre los cuatro perfiles.

| Perfil | Qué se puede probar |
|---|---|
| Terminal casino | Equipo instalado en el casino: terminal (RUT digitado, emisión del ticket) y propuesta de ticket |
| Funcionario | «Mi casino»: menú de la semana, selección del menú mensual (normal, hipocalórico o vegano), avisos de los días que no almorzará, almuerzos con invitados y reporte CSV |
| Jefe Casino | Menú semanal, planificación de raciones, reportes, comensales (personas habilitadas e ingresos en una sola vista), configuración, cierres del casino e información (estadísticas) |
| Jefa de Bienestar | Información (estadísticas agregadas), emisión de reportes y cierres del casino |

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

**Ticket:** sigla CONAF, fecha y lugar; cantidad de almuerzos y menú; nombre completo en mayúsculas, hora e ID único (año y correlativo anual, por ejemplo 2026-004812). El ID se registra en «Comensales» del Jefe Casino, en «Mi casino» del funcionario y en el detalle por ticket del reporte mensual; «Comensales» permite buscar por ID y abre a la persona.

**Mi casino (funcionario):** en este orden, el menú de la semana publicado por el Jefe Casino
(entrada, plato normal, hipocalórico y vegano, y postre); «Selecciona tu menú mensual», una
tabla compacta con una lista desplegable por mes (normal, hipocalórico o vegano) que se guarda al
elegir, hasta el día 25 del mes anterior; el mes vencido aparece «Cerrado»; «Avisa los días que no almorzarás»
(un día o un rango, hasta las 23:59 del día anterior); «Almuerzo con invitados», con el monto
que se descontará; y el reporte del mes en CSV para Excel (ID de ticket, fecha, hora, almuerzos,
menú y monto). El aviso de ausencia sirve para planificar las raciones y no bloquea: si la
persona cambia de planes y digita su RUT, almuerza igual y su aviso se anula solo. Solo se
descuentan los almuerzos consumidos. Los almuerzos con
invitados se descuentan al funcionario con un vale extra por invitado.

**Manual de usuario (todos los perfiles):** pestaña con introducción, diagrama de flujo del proceso
(por perfil y etapa), la sección del perfil activo, reglas y valores, y contingencia y preguntas
frecuentes. La casilla «Ver el manual completo» muestra las secciones de los cuatro perfiles.

**Información (Jefe Casino y Jefa de Bienestar):** selector Día, Semana, Mes o Año (calendario),
con flechas para recorrer períodos y botón «Período actual»; se abre en el último período
completo para no mostrar cifras de un período recién iniciado. Muestra: 1) las unidades de CONAF
que más usan el casino (10 primeras, con cantidad y %, y el resto agrupado); 2) los almuerzos
registrados, con comparación con el período anterior, promedio por día, personas distintas,
invitados, externos y visitas, y un gráfico del período; 3) las 3 franjas de 15 minutos más
concurridas, con su cantidad, porcentaje y promedio por día, y el gráfico de todas las franjas.

**Comensales (Jefe Casino):** une las antiguas pestañas «Detalle de ingresos» y «Personas
habilitadas». Debajo, la lista de comensales con su barra de período y filtros: una fila por persona con nivel, forma de pago, almuerzos y último ingreso del
período (hoy, semana, mes o fechas), búsqueda por nombre, RUT, unidad o ID de ticket, y filtros
(con o sin almuerzos, anulados, registro manual, sin nivel, efectivo mensual, suspendidas). Al
abrir una persona se ven sus tickets (reimprimir y anular los del día) y se cambian su nivel,
forma de pago y habilitación. Arriba, tres tarjetas de selección: «Registrar» (ingreso manual, venta en efectivo, visita
institucional, planilla de contingencia), «Personas» (agregar, carga masiva, cambio de menú por
excepción) y «Reportes» en CSV (ingresos del período, nómina de habilitados, ficha por persona,
externos y visitas). Al pie, los externos y visitas del período.

**Planificación (Jefe Casino):** próximos 10 días hábiles con habilitados, ausencias
avisadas, menú normal, hipocalórico y vegano, almuerzos de invitados, raciones planificadas y
consumo habitual como referencia.

**Menú del mes:** el funcionario elige el menú de cada mes hasta el día 25 del mes anterior;
«Mi casino» muestra el mes actual, el siguiente y, si este ya cerró, el próximo que se puede
elegir, y aclara que sin elección el menú es Normal. Para casos justificados (ingreso nuevo,
indicación médica) el Jefe Casino registra un **cambio de menú por excepción** en Personas
habilitadas, para el mes actual o el siguiente, con motivo y registro de quién y cuándo.

**Propuestas a las preguntas del Jefe Casino (02-11-2026), rotuladas en la maqueta:**
- *Venta en efectivo* (externos o acompañantes) y *visita institucional* con cargo a la
  Dirección Ejecutiva, desde «Registrar» en Comensales: ticket con su marca, sin descuento por planilla.
  En la venta en efectivo el sistema asigna un folio correlativo anual (`EF-AAAA-NNNN`), que se
  imprime en el ticket como comprobante de pago y aparece en el reporte de caja.
  Se cobran con el vale extra ($6.000).
- *Forma de pago* por persona en Comensales (Planilla o Efectivo mensual), para
  personal en convenio como FAO; queda fuera del descuento y tiene su propio reporte.
- *Planilla de contingencia*: si el sistema completo no está disponible, se descarga una
  planilla en blanco y luego se carga al sistema.
- Reportes nuevos: cobro mensual en efectivo, caja de ventas en efectivo y visitas
  institucionales.

**Menú semanal (Jefe Casino):** cada lunes publica la minuta de la semana (entrada, plato
normal, hipocalórico y vegano, y postre), que reemplaza el envío de la
minuta por correo electrónico. Los cambios quedan como borrador hasta publicarlos. La maqueta
usa como ejemplo las minutas reales de octubre de 2026, ajustadas a la semana actual y las dos
anteriores.

**Reportes:** la pantalla muestra el resumen del descuento por planilla del mes, una revisión antes de emitir (mes en curso, personas sin nivel, niveles del mes cargados, anulados y registros manuales) y el desglose por nivel; el detalle por trabajador y por ticket va en el CSV. El botón «Emisión reporte
mensual» despliega tres reportes que se descargan en CSV para Excel: 1) reporte descuento
mensual (por trabajador y detalle por ticket), 2) reporte consumo por unidad y 3) reporte
anual por mes.

**Valor del almuerzo:** se define por nivel según el sueldo imponible del trabajador (Casino
Oficina Central, valores de marzo 2026): nivel 1, imponible hasta $1.200.000, $2.880; nivel 2,
de $1.200.001 a $2.050.000, $3.380; nivel 3, desde $2.050.001, $3.980. El vale extra ($6.000) se
cobra por cada invitado del funcionario, por cada venta en efectivo a externos y por cada
almuerzo de visita institucional. Remuneraciones informa cada mes el nivel de cada trabajador y
el Jefe Casino lo carga en Configuración («Actualización mensual de niveles», filas RUT;nivel);
el sistema guarda solo el nivel, no el sueldo. Reportes advierte si faltan los niveles del mes.
Las calidades jurídicas son Dotación, Plazo fijo y Honorarios.

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
