# coipo_control-casino — Maqueta del control de ingreso al Casino Institucional

Maqueta de validación del sistema de control de ingreso al Casino Institucional de CONAF
para el Servicio de Bienestar, elaborada por la Unidad de Información y Análisis (UIA).
Iniciativa CON005.

**Ver la maqueta:** https://alvarozvjac.github.io/coipo_control-casino/

> Demostración no operacional. Personas, RUT, niveles y registros son ficticios; los valores del almuerzo por nivel y el vale extra son los informados por Bienestar (marzo 2026). Lo que se haga en la maqueta no se guarda: al recargar la página vuelve al
> estado inicial.

**Vista celular:** en computador, el botón «Vista celular» de la cabecera muestra la maqueta dentro de un marco de teléfono de 390 × 844 px, para presentarla sin abrir las herramientas del navegador. Se cierra con «Cerrar» o Esc. En un teléfono real el botón no aparece.

## Modelo de cobro (definido por el Jefe Casino, 17-11-2026)

- **Suscripción mensual (personas inscritas):** el descuento de cada mes se envía a
  Remuneraciones entre el 5° y el 8° día hábil. Cobra todos los días hábiles del mes al valor
  del nivel de la persona; al mes siguiente se rebajan las ausencias avisadas a tiempo, los
  días con licencia médica (informe mensual de licencias, aunque no se hayan avisado) y los
  cierres del casino. Sin aviso a tiempo, el día se cobra. Si la persona avisó y llega igual,
  el aviso se anula y el día se cobra.
- **Mes vencido (directora, fiscal y gerentes):** solo los almuerzos consumidos el mes
  anterior, al valor de su nivel.
- **No inscritos** de Oficina Central y Región Metropolitana: la terminal los reconoce y cada
  almuerzo se cobra con el vale extra ($6.000), descontado el mes siguiente o pagado en caja.
  El Jefe Casino indica, ticket por ticket en Comensales, si el vale se pagó en caja (efectivo o
  transferencia); si no lo marca, se descuenta.
  Se anotan el lunes, al publicarse la minuta semanal, para que el casino planifique.
- **Contrato en trámite:** la persona elige pagar cada almuerzo en caja o acumularlo; al
  marcar el contrato como vigente, lo acumulado se descuenta el mes siguiente junto con la
  primera suscripción.
- **Visitas de la Dirección Ejecutiva:** se pagan con «Cargo CONAF».
- **Despacho a la Dirección Ejecutiva:** el Jefe Casino registra solo la cantidad de
  almuerzos despachados; se cobran con «Cargo CONAF» al valor del vale extra.
- **Venta en caja:** efectivo o transferencia a la cuenta del casino (con N° de operación);
  el folio digital `EF-AAAA-NNNN` reemplaza el talonario de papel. El **depósito del efectivo**
  en la cuenta del casino (fecha, monto y N° de comprobante) se registra en Comensales →
  Registrar, que muestra el efectivo aún sin depositar y avisa al superar $100.000; reemplaza
  la planilla Excel.

Quedan como **opciones configurables** en Configuración → «Reglas de cobro», hasta que
Bienestar las confirme: el plazo del aviso de ausencia (24 horas antes del inicio del
almuerzo, por defecto, o hasta las 23:59 del día anterior), cómo se anotan los eventuales
(solo el lunes hasta una hora límite, o hasta el día anterior), si un eventual sin anotarse
puede almorzar y cómo paga el vale extra un no inscrito.

## Cómo probarla

**Página de inicio e ingreso.** La maqueta abre en una página de inicio que explica quién usa
el sistema y cómo se ingresa. El botón **«Ingresar con mi cuenta CONAF»** lleva a una
**simulación del IAM** (`iam.conaf.cl`), el inicio de sesión único que ya usan en producción
otros sistemas de la UIA: misma tarjeta, campos Usuario y Contraseña y mensaje «Usuario o
contraseña incorrectos». Es solo una simulación: no se conecta al IAM, no envía datos a ningún
lugar y únicamente acepta las cuentas ficticias de prueba (no escriba su contraseña real):

| Perfil | Usuario (RUT ficticio) | Contraseña de prueba |
|---|---|---|
| Funcionario inscrito (Valentina Araya Cortés) | 18.345.210-K | `Almuerzo.2026` |
| Funcionario no inscrito (Tomás Henríquez Vidal) | 17.345.118-0 | `Eventual.2026` |
| Jefe Casino (Rodrigo Salinas Vera) | 13.456.789-9 | `Casino.2026` |
| Jefa de Bienestar (María Fernanda Ortiz Lagos) | 12.987.654-9 | `Bienestar.2026` |

El panel «Cuentas de prueba» de la misma pantalla las completa con un clic. El perfil queda
según la cuenta con que se ingresa, y «Cerrar sesión» vuelve a la página de inicio.

**El terminal del casino no tiene inicio de sesión:** es el equipo instalado en el casino y se
abre en su propia dirección, `…/coipo_control-casino/#terminal` (también desde el enlace
«Equipo del casino: abrir el terminal» de la página de inicio).

| Perfil | Qué se puede probar |
|---|---|
| Terminal casino | Equipo instalado en el casino: terminal (RUT digitado, emisión del ticket) y propuesta de ticket |
| Funcionario | «Mi casino»: su descuento del mes, menú de la semana, selección del menú mensual (normal, hipocalórico o vegano), avisos de los días que no almorzará con su motivo, almuerzos con invitados y reporte CSV. Si no está inscrito: «Anotarme para almorzar un día» |
| Jefe Casino | Menú semanal, planificación de raciones, reportes, comensales (personas habilitadas e ingresos en una sola vista), configuración, cierres del casino e información (estadísticas) |
| Jefa de Bienestar | Información (estadísticas agregadas), emisión de reportes y cierres del casino |

**Terminal del casino:** la persona digita su RUT en un teclado numérico USB y presiona
Enter; la tecla `*` equivale a la K. La pantalla y el ticket muestran su nombre completo,
para que el personal del casino verifique la identidad. El **simulador del teclado
numérico**, al costado, digita el RUT de cada persona de prueba; también se puede usar el
teclado del computador. Las tres primeras personas (Carolina, Jorge y Daniela) muestran la
emisión completa del ticket; Daniela tiene hoy 2 almuerzos a su nombre. Otros casos: almuerzo
ya registrado, aviso de ausencia para hoy (Ignacio: igual puede almorzar; el aviso se anula solo y el
ingreso queda marcado «Asistió pese a aviso» en el detalle), habilitación suspendida, persona no inscrita anotada para hoy (Paula) o sin anotarse (Tomás), contrato en trámite que paga en caja (Matías), RUT que no está en la nómina y RUT mal digitado. La
hora está fijada en 13:05 y se cambia en Configuración. La validación con RUT y PIN queda
para una versión futura.

**Ticket:** sigla CONAF, fecha y lugar; cantidad de almuerzos y menú; nombre completo en mayúsculas, hora e ID único (año y correlativo anual, por ejemplo 2026-004812). El ID se registra en «Comensales» del Jefe Casino, en «Mi casino» del funcionario y en el detalle por ticket del reporte mensual; «Comensales» permite buscar por ID y abre a la persona.

**Mi casino (funcionario):** bajo el nombre, el descuento del mes (días hábiles menos las rebajas del mes anterior, por el valor del nivel). En este orden, el menú de la semana publicado por el Jefe Casino
(entrada, plato normal, hipocalórico y vegano, y postre); «Selecciona tu menú mensual», una
tabla compacta con una lista desplegable por mes (normal, hipocalórico o vegano) que se guarda al
elegir, hasta el día 25 del mes anterior; el mes vencido aparece «Cerrado»; «Avisa los días que no almorzarás»
(un día o un rango, con su motivo, dentro del plazo de «Reglas de cobro»); «Almuerzo con invitados», con el monto
que se descontará; y el reporte del mes en CSV para Excel (ID de ticket, fecha, hora, almuerzos,
menú y monto). El aviso a tiempo se rebaja del descuento del mes siguiente y no bloquea: si la
persona cambia de planes y digita su RUT, almuerza igual, su aviso se anula y ese día se cobra.
Los almuerzos con invitados se descuentan al funcionario con un vale extra por invitado. Una
persona no inscrita ve, en lugar del menú mensual y los avisos, la tabla «Anotarme para almorzar
un día» con el plato de cada día de la minuta publicada.

**Manual de usuario (PDF):** botón «Manual de usuario (PDF)» en la cabecera, visible en todos los
perfiles. Descarga un único PDF (20 páginas, A4) con introducción, ingreso al sistema, diagrama de flujo del proceso,
los cuatro perfiles con sus funcionalidades y capturas, reglas y valores, y contingencia y
preguntas frecuentes. El PDF va incluido dentro de `index.html`, por lo que funciona sin conexión.

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
(con o sin almuerzos, anulados, registro manual, sin nivel, efectivo mensual, mes vencido, no
inscritos, contrato en trámite, suspendidas). Al abrir una persona se ven sus tickets (reimprimir
y anular los del día) y se cambian su nivel, forma de pago, modalidad de cobro, situación del
contrato y habilitación. Arriba, tres tarjetas de selección: «Registrar» (ingreso manual, venta en caja, visita
con Cargo CONAF, despacho a la Dirección Ejecutiva, depósito del efectivo, planilla de contingencia), «Personas» (agregar, carga masiva, cambio de menú por
excepción) y «Reportes» en CSV (ingresos del período, nómina de habilitados, ficha por persona,
externos y visitas). Al pie, los externos y visitas del período.

**Planificación (Jefe Casino):** próximos 10 días hábiles con inscritos, ausencias
avisadas, menú normal, hipocalórico y vegano, invitados y comensales eventuales anotados,
raciones planificadas y consumo habitual como referencia.

**Menú del mes:** el funcionario elige el menú de cada mes hasta el día 25 del mes anterior;
«Mi casino» muestra el mes actual, el siguiente y, si este ya cerró, el próximo que se puede
elegir, y aclara que sin elección el menú es Normal. Para casos justificados (ingreso nuevo,
indicación médica) el Jefe Casino registra un **cambio de menú por excepción** en Personas
habilitadas, para el mes actual o el siguiente, con motivo y registro de quién y cuándo.

**Propuestas a las preguntas del Jefe Casino (02-11-2026), rotuladas en la maqueta:**
- *Venta en caja* (externos o acompañantes; efectivo o transferencia con N° de operación) y
  *visita con Cargo CONAF*, desde «Registrar» en Comensales: ticket con su marca, sin descuento por planilla.
  En la venta en caja el sistema asigna un folio correlativo anual (`EF-AAAA-NNNN`), que se
  imprime en el ticket como comprobante de pago y aparece en el reporte de caja.
  Se cobran con el vale extra ($6.000).
- *Forma de pago* por persona en Comensales (Planilla o Efectivo mensual), para
  personal en convenio como FAO; queda fuera del descuento y tiene su propio reporte.
- *Planilla de contingencia*: si el sistema completo no está disponible, se descarga una
  planilla en blanco y luego se carga al sistema.
- Reportes nuevos: cobro mensual en efectivo, caja (ventas en efectivo y transferencias,
  vales de no inscritos pagados en caja y depósitos del mes) y Cargo CONAF (visitas y
  despachos a la Dirección Ejecutiva).

**Menú semanal (Jefe Casino):** cada lunes publica la minuta de la semana (entrada, plato
normal, hipocalórico y vegano, y postre), que reemplaza el envío de la
minuta por correo electrónico. Los cambios quedan como borrador hasta publicarlos. La maqueta
usa como ejemplo las minutas reales de octubre de 2026, ajustadas a la semana actual y las dos
anteriores.

**Reportes:** se abre en el mes en curso y muestra el descuento que se envía a Remuneraciones: días hábiles del mes, trabajadores por modalidad, rebajas del mes anterior (avisos, licencias y cierres) y total. La revisión antes de emitir indica el plazo de envío (5° a 8° día hábil), personas sin nivel, informe de licencias, avisos fuera de plazo, mes vencido, no inscritos, contratos en trámite, anulados y registros manuales; el desglose por nivel incluye una fila de no inscritos. El detalle por trabajador va en el CSV. El botón «Emisión reporte
mensual» despliega tres reportes que se descargan en CSV para Excel: 1) reporte descuento
mensual (por trabajador y detalle por ticket), 2) reporte consumo por unidad y 3) reporte
anual por mes (con el monto descontado en cada mes).

**Valor del almuerzo:** se define por nivel según el sueldo imponible del trabajador (Casino
Oficina Central, valores de marzo 2026): nivel 1, imponible hasta $1.200.000, $2.880; nivel 2,
de $1.200.001 a $2.050.000, $3.380; nivel 3, desde $2.050.001, $3.980. El vale extra ($6.000) se
cobra por cada invitado del funcionario, por cada venta en efectivo a externos y por cada
almuerzo de visita, y por cada almuerzo de una persona no inscrita. Un cambio en la tabla de
tramos rige desde el mes siguiente. Remuneraciones envía cada mes el **RUT y el sueldo
imponible** de Oficina Central y la Región Metropolitana, y el Jefe Casino lo carga en
Configuración («Actualización mensual de niveles»: archivo CSV o columnas pegadas desde Excel,
contenido oculto). El sistema calcula el nivel con la tabla del mes, muestra una vista previa
(cambios de nivel, filas rechazadas y personas de la nómina que no vienen en el archivo, para
revisar bajas) y descarta los sueldos sin mostrarlos ni guardarlos. La lectura directa de
.xlsx queda para cuando se conozca el formato del archivo. Reportes advierte si faltan los
niveles del mes. El **informe mensual de licencias médicas** se carga en Configuración con
RUT y fechas, sin diagnóstico.
Las calidades jurídicas son Dotación, Plazo fijo y Honorarios.

**Cierres del casino:** al registrar o anular un cierre (clima, mantención, catástrofe,
corte de suministro u otro), el otro perfil recibe una alerta. Durante un cierre vigente
la terminal no emite tickets. Al abrir como Jefe Casino aparece una alerta de ejemplo
enviada por la Jefa de Bienestar.

**Reiniciar datos de prueba**, en el pie de página, vuelve todo al estado inicial.

## Estándar visual de la flota COIPO

La maqueta se revisó contra `identidad/ESTANDAR_UI.md` de `coipo_master_produccion`: banner
institucional con el título en su zona y versión corta bajo 560 px (§8.2), alto mínimo 68 px,
verde institucional #064928, foco visible con contraste 3:1, chips y textos con contraste
4,5:1, movimiento reducido (`prefers-reduced-motion`), áreas táctiles de 44 px, puntos de
quiebre estándar (559,98 / 767,98 / 899,98 px) y reflujo sin desplazamiento horizontal a
320 px. Pendiente: tema oscuro (UI-3).

## Contenido del repositorio

- `index.html`: la maqueta completa en un solo archivo (código, estilos e imágenes
  incluidos), sin dependencias externas.

Documentos de referencia: solicitud del Servicio de Bienestar (13-08-2026) y propuesta
comercial «Control de Comedor» de GeoVictoria (agosto 2026). Por acuerdo de la reunión UIA
del 22-10-2026, la solución identifica a las personas por su RUT digitado en un teclado
numérico, sin datos biométricos, licencia ni arriendo; la validación con RUT y PIN queda
para una versión futura.
