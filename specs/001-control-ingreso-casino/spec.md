# Feature Specification: Control de ingreso al Casino Institucional

**Feature Branch**: `speckit`

**Created**: 2026-11-06

**Status**: Draft

**Input**: User description: "revisa https://alvarozvjac.github.io/coipo_control-casino/" — especificación
elaborada a partir de la maqueta publicada (iniciativa CON005, 48 commits al 06-11-2026), su README y
su Manual de usuario.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Ingreso al casino con RUT y emisión del ticket (Priority: P1)

Un funcionario habilitado llega al casino en el horario del servicio, digita su RUT en el teclado
numérico de la terminal y presiona Enter. La terminal valida el RUT, muestra su nombre completo para
que el personal verifique la identidad y emite un ticket con la sigla CONAF, fecha, lugar, cantidad
de almuerzos, menú, nombre en mayúsculas, hora e ID único.

**Why this priority**: es el núcleo del servicio; sin el registro del ingreso no existe base para el
descuento por planilla ni para los reportes.

**Independent Test**: con solo la nómina de habilitados y la terminal, digitar el RUT de una persona
de prueba y verificar que se emite el ticket correcto y que queda registrado.

**Acceptance Scenarios**:

1. **Given** una persona habilitada sin ticket hoy y dentro del horario, **When** digita su RUT
   válido y presiona Enter, **Then** se emite un ticket con ID `AAAA-NNNNNN` correlativo anual y el
   ingreso queda registrado con su nivel y el valor vigente.
2. **Given** una persona que ya tiene ticket hoy, **When** vuelve a digitar su RUT, **Then** la
   terminal informa «almuerzo ya registrado», indica la hora del ticket anterior y no emite otro.
3. **Given** una persona con invitados registrados para hoy, **When** digita su RUT, **Then** un solo
   ticket muestra la cantidad total de almuerzos a su nombre.
4. **Given** una persona que avisó que no almorzaría hoy, **When** digita su RUT, **Then** recibe su
   ticket, el aviso se anula y el ingreso queda marcado «Asistió pese a aviso».
5. **Given** un RUT con dígito verificador inválido, un RUT que no está en la nómina, una persona
   suspendida, una hora fuera del horario o un cierre vigente, **When** se digita el RUT, **Then** la
   terminal no emite ticket y muestra el motivo y la acción sugerida.
6. **Given** el teclado numérico, **When** el RUT termina en K, **Then** la tecla `*` se acepta como K.

---

### User Story 2 - Descuento mensual por planilla y reportes a Remuneraciones (Priority: P1)

El Jefe Casino o la Jefa de Bienestar revisa el resumen del mes (personas, almuerzos y monto por
nivel), atiende las advertencias de la revisión previa y emite el reporte de descuento mensual por
trabajador y por ticket para Remuneraciones, además del consumo por unidad y el reporte anual.

**Why this priority**: es el resultado administrativo que justifica el sistema y reemplaza el
control manual.

**Independent Test**: con ingresos registrados de un mes, emitir el reporte de descuento y comprobar
que el monto de cada trabajador coincide con sus almuerzos consumidos por el valor de su nivel más
los vales extra.

**Acceptance Scenarios**:

1. **Given** un mes con ingresos, **When** se abre Reportes, **Then** se muestra el desglose por nivel
   (valor, personas, almuerzos y monto) y la revisión previa: mes en curso, personas sin nivel,
   niveles del mes cargados, tickets anulados y registros manuales.
2. **Given** personas sin nivel en el mes, **When** se intenta emitir, **Then** el sistema advierte
   que esos almuerzos no tienen valor hasta cargar o corregir el nivel.
3. **Given** el mes revisado, **When** se emite el «Reporte descuento mensual», **Then** se descarga
   un archivo que abre en Excel con el detalle por trabajador y por ticket, excluidos los tickets
   anulados y las personas con forma de pago Efectivo mensual.
4. **Given** un funcionario nivel 3 con un invitado, **When** se calcula su descuento de ese día,
   **Then** el monto es $3.980 + $6.000 = $9.980.

---

### User Story 3 - Gestión de comensales por el Jefe Casino (Priority: P2)

El Jefe Casino administra en una sola vista a las personas habilitadas y sus ingresos: busca por
nombre, RUT, unidad o ID de ticket, filtra por período y condición, abre a una persona para ver sus
tickets, reimprime o anula los del día con motivo y cambia su nivel, forma de pago o habilitación.
Desde «Registrar» ingresa almuerzos manuales, ventas en efectivo, visitas institucionales y la
planilla de contingencia; desde «Personas» agrega personas, hace cargas masivas y registra cambios
de menú por excepción.

**Why this priority**: permite corregir errores y operar ante fallas, condición para que el
descuento sea confiable.

**Independent Test**: anular un ticket del día con motivo y verificar que no aparece en el
descuento y que queda registrado quién y cuándo lo anuló.

**Acceptance Scenarios**:

1. **Given** un ticket emitido hoy, **When** el Jefe Casino lo anula indicando motivo, **Then** el
   ticket queda «Anulado», no se descuenta y se registra quién, cuándo y por qué.
2. **Given** un ticket de un día anterior, **When** se intenta anular, **Then** el sistema no lo
   permite.
3. **Given** una falla de la terminal, **When** el Jefe Casino registra un ingreso manual con RUT y
   motivo, **Then** el ingreso queda marcado «Registro manual».
4. **Given** una venta en efectivo a un externo, **When** se registra, **Then** se emite un ticket con
   folio `EF-AAAA-NNNN` y cobro del vale extra, sin descuento por planilla, que aparece en el
   reporte de caja.
5. **Given** una planilla de contingencia con filas RUT;hora de un día, **When** se carga, **Then**
   se registran los ingresos válidos y se informa por fila cada RUT inválido, fuera de nómina, con
   hora inválida o con ticket ya existente ese día.

---

### User Story 4 - «Mi casino»: menú, ausencias, invitados y reporte personal (Priority: P2)

El funcionario consulta el menú de la semana publicado; elige su menú mensual (Normal, Hipocalórico
o Vegano) hasta el día 25 del mes anterior; avisa los días que no almorzará (un día o un rango) e
inscribe almuerzos con invitados hasta las 23:59 del día anterior, viendo el monto que se le
descontará; y descarga el reporte de sus almuerzos del mes.

**Why this priority**: entrega información para planificar raciones y transparencia al funcionario
sobre lo que se le descuenta.

**Independent Test**: elegir un menú para el mes siguiente, avisar una ausencia y descargar el
reporte personal, verificando cada resultado.

**Acceptance Scenarios**:

1. **Given** una fecha anterior o igual al día 25, **When** el funcionario elige el menú del mes
   siguiente, **Then** la elección queda guardada; **Given** un mes cuyo plazo venció, **Then** ese mes
   aparece «Cerrado».
2. **Given** que no eligió menú, **When** llega el mes, **Then** su menú es Normal.
3. **Given** un aviso de ausencia, **When** la persona digita su RUT ese día, **Then** almuerza igual y
   el aviso se anula (no bloquea).
4. **Given** un mes con almuerzos, **When** descarga su reporte, **Then** obtiene ID de ticket, fecha,
   hora, almuerzos, menú y monto de cada día.

---

### User Story 5 - Menú semanal y planificación de raciones (Priority: P3)

Cada lunes el Jefe Casino publica la minuta de la semana (entrada, plato normal, hipocalórico y
vegano, y postre); los cambios quedan como borrador hasta publicarlos. Revisa la planificación de
los próximos 10 días hábiles: habilitados, ausencias avisadas, menús elegidos, invitados, raciones
planificadas y consumo habitual de referencia.

**Why this priority**: reemplaza el envío de la minuta por correo y reduce la sobreproducción, pero
el servicio puede operar sin ello.

**Independent Test**: publicar una minuta y verificar que aparece en «Mi casino»; comprobar que una
ausencia avisada reduce las raciones planificadas de ese día.

**Acceptance Scenarios**:

1. **Given** una minuta en borrador, **When** el Jefe Casino la publica, **Then** los funcionarios la
   ven en «Mi casino».
2. **Given** ausencias e invitados registrados, **When** se abre Planificación, **Then** las raciones
   de cada día y menú reflejan habilitados − ausencias + invitados.

---

### User Story 6 - Cierres del casino y alertas (Priority: P3)

El Jefe Casino o la Jefa de Bienestar registra o anula un cierre del casino (clima, mantención,
catástrofe, corte de suministro u otro) con fecha, horario y detalle; el otro perfil recibe una
alerta y la terminal deja de emitir tickets durante el cierre vigente.

**Why this priority**: evento poco frecuente, pero sin control genera tickets en días sin servicio.

**Independent Test**: registrar un cierre para hoy y verificar que la terminal muestra «Casino
cerrado» y que el otro perfil recibe la alerta.

**Acceptance Scenarios**:

1. **Given** un cierre vigente, **When** alguien digita su RUT, **Then** la terminal muestra «Casino
   cerrado» y no emite ticket; los almuerzos ya registrados no se anulan.
2. **Given** un cierre registrado por la Jefa de Bienestar, **When** el Jefe Casino entra al
   sistema, **Then** ve la alerta.

---

### User Story 7 - Información estadística del uso del casino (Priority: P3)

El Jefe Casino y la Jefa de Bienestar eligen Día, Semana, Mes o Año y recorren períodos. Ven las 10
unidades que más usan el casino, los almuerzos registrados frente al período anterior, promedio por
día, personas distintas, invitados, externos y visitas, y las 3 franjas de 15 minutos más
concurridas. La vista abre en el último período completo.

**Why this priority**: apoya decisiones de gestión, sin afectar la operación diaria.

**Independent Test**: seleccionar un mes con datos y comprobar que los totales coinciden con los
ingresos registrados de ese mes.

**Acceptance Scenarios**:

1. **Given** datos del mes anterior, **When** se abre Información, **Then** muestra ese mes (último
   completo) y no el mes recién iniciado.
2. **Given** la Jefa de Bienestar, **When** consulta Información, **Then** ve solo cifras agregadas,
   sin detalle por trabajador.

---

### User Story 8 - Configuración del servicio y actualización mensual de niveles (Priority: P2)

El Jefe Casino configura el horario, la ubicación, los plazos, los valores por nivel y el vale
extra, y carga cada mes el archivo de Remuneraciones con filas RUT;nivel.

**Why this priority**: sin niveles del mes el descuento no puede calcularse.

**Independent Test**: cargar un archivo RUT;nivel y comprobar que las personas «Sin nivel» quedan con
nivel y que Reportes deja de advertirlo.

**Acceptance Scenarios**:

1. **Given** un cambio de valor del almuerzo, **When** se guarda, **Then** rige para los almuerzos
   registrados desde ese momento y los anteriores conservan su valor.
2. **Given** el archivo de niveles del mes, **When** se carga, **Then** se guarda solo el nivel (1, 2
   o 3), nunca el sueldo imponible, y se informan las filas con error.

### Edge Cases

- RUT terminado en K digitado con `*`; RUT con o sin puntos y guion.
- Persona habilitada sin nivel asignado: puede almorzar, pero su almuerzo no tiene valor hasta
  cargar su nivel.
- Cambio de nivel o de valor a mitad de mes: cada ticket conserva el valor con que se emitió.
- Ausencia avisada y luego ingreso: no bloquea; el aviso se anula y se marca el ingreso.
- Elección de menú o aviso fuera de plazo: no se acepta; el cambio de menú por excepción lo registra
  el Jefe Casino con motivo, para el mes actual o el siguiente.
- Correlativo anual: el ID de ticket y el folio de efectivo reinician en 1 cada año sin repetirse.
- Cierre registrado mientras hay personas en fila: la terminal deja de emitir desde ese momento.
- Planilla de contingencia con filas duplicadas o de personas con ticket ese día: se rechazan por
  fila.
- Funcionario que ve en su reporte un almuerzo que no tomó: debe avisar al Jefe Casino antes del
  cierre del mes.

## Requirements *(mandatory)*

### Functional Requirements

**Terminal e identificación**

- **FR-001**: El sistema MUST identificar a la persona solo por su RUT digitado, validando el dígito
  verificador; MUST NOT usar datos biométricos.
- **FR-002**: El sistema MUST mostrar el nombre completo de la persona antes de emitir el ticket.
- **FR-003**: El sistema MUST emitir como máximo un ticket por persona y día; los almuerzos de sus
  invitados MUST ir en ese mismo ticket.
- **FR-004**: El sistema MUST rechazar la emisión, indicando motivo y acción sugerida, ante RUT
  inválido, RUT fuera de nómina, habilitación suspendida, hora fuera del horario o cierre vigente.
- **FR-005**: Cada ticket MUST tener un ID único con año y correlativo anual, y MUST contener sigla
  CONAF, fecha, lugar, cantidad de almuerzos, menú, nombre completo en mayúsculas, hora e ID.

**Cobro y reportes**

- **FR-006**: El valor del almuerzo MUST determinarse por el nivel vigente de la persona al momento
  del ticket (valores de marzo 2026: nivel 1 $2.880; nivel 2 $3.380; nivel 3 $3.980) y el vale extra
  ($6.000) MUST cobrarse por cada invitado, venta en efectivo o almuerzo de visita institucional.
- **FR-007**: Solo los almuerzos consumidos y no anulados MUST generar cobro.
- **FR-008**: El sistema MUST emitir el reporte de descuento mensual (por trabajador y por ticket),
  el consumo por unidad y el reporte anual por mes, en archivos que se abran en Excel.
- **FR-009**: El sistema MUST mostrar una revisión previa a la emisión del reporte mensual (mes en
  curso, personas sin nivel, niveles del mes cargados, anulados, registros manuales).
- **FR-010**: Las personas con forma de pago «Efectivo mensual» MUST quedar fuera del descuento por
  planilla y tener su propio reporte de cobro.
- **FR-011**: Las ventas en efectivo MUST tener un folio correlativo anual `EF-AAAA-NNNN`, impreso
  en el ticket y en un reporte de caja; las visitas institucionales MUST tener su propio reporte.

**Gestión de comensales**

- **FR-012**: El Jefe Casino MUST poder buscar y filtrar comensales por período, nombre, RUT, unidad
  o ID de ticket, y por condición (con o sin almuerzos, anulados, registro manual, sin nivel,
  efectivo mensual, suspendidas).
- **FR-013**: El Jefe Casino MUST poder reimprimir y anular, con motivo, solo tickets del día.
- **FR-014**: El Jefe Casino MUST poder registrar ingresos manuales con RUT y motivo, cargar la
  planilla de contingencia (RUT;hora) con validación por fila, y agregar o cargar masivamente
  personas.
- **FR-015**: El Jefe Casino MUST poder cambiar nivel, forma de pago, habilitación y menú por
  excepción de una persona; cada cambio MUST registrar quién, cuándo y motivo.

**Funcionario**

- **FR-016**: El funcionario MUST poder elegir su menú mensual hasta el día configurado del mes
  anterior (por defecto el 25); sin elección, el menú MUST ser Normal.
- **FR-017**: El funcionario MUST poder avisar ausencias (día o rango) e inscribir invitados hasta
  las 23:59 del día anterior, viendo el monto que se le descontará.
- **FR-018**: Un aviso de ausencia MUST NOT impedir el ingreso; al ingresar, el aviso MUST anularse y
  el ingreso marcarse «Asistió pese a aviso».
- **FR-019**: El funcionario MUST poder descargar el reporte de sus almuerzos del mes.

**Menú, planificación, cierres e información**

- **FR-020**: El Jefe Casino MUST poder editar en borrador y publicar la minuta semanal.
- **FR-021**: El sistema MUST mostrar la planificación de raciones de los próximos 10 días hábiles
  por tipo de menú.
- **FR-022**: El Jefe Casino y la Jefa de Bienestar MUST poder registrar y anular cierres con motivo;
  el otro perfil MUST recibir una alerta, y la terminal MUST dejar de emitir durante el cierre.
- **FR-023**: El sistema MUST mostrar estadísticas por Día, Semana, Mes y Año, abriendo en el último
  período completo; la Jefa de Bienestar MUST ver solo cifras agregadas.

**Configuración y datos**

- **FR-024**: Horario, ubicación, plazos, valores por nivel y vale extra MUST ser configurables; un
  cambio de valor MUST regir desde ese momento sin alterar tickets ya emitidos.
- **FR-025**: El sistema MUST cargar mensualmente el nivel de cada trabajador desde un archivo
  RUT;nivel y MUST NOT guardar sueldos.
- **FR-026**: Cada perfil MUST acceder solo a sus funciones: Terminal casino (terminal y propuesta de
  ticket), Funcionario (Mi casino), Jefe Casino (menú, planificación, reportes, comensales,
  configuración, cierres, información) y Jefa de Bienestar (información, reportes, cierres).
- **FR-027**: Todos los perfiles MUST tener acceso a un Manual de usuario con el flujo del proceso,
  reglas, contingencia y preguntas frecuentes.

**Definiciones pendientes con impacto en alcance y cobro**

- **FR-028**: Los usuarios de la Región Metropolitana fuera de Oficina Central MUST tener la condición
  [NEEDS CLARIFICATION: ¿pueden usar el casino de Oficina Central, con qué valores y bajo qué
  habilitación? Pendiente de Bienestar].
- **FR-029**: El personal en convenio (FAO) con forma de pago Efectivo mensual MUST pagar
  [NEEDS CLARIFICATION: ¿qué valor por almuerzo se le cobra: el de algún nivel, el vale extra u otro?
  Pendiente de Bienestar].
- **FR-030**: El efectivo de ventas y cobros mensuales MUST custodiarse y rendirse según
  [NEEDS CLARIFICATION: ¿quién custodia el efectivo, con qué periodicidad se rinde y ante quién?
  Pendiente de Bienestar y Finanzas].

### Key Entities *(include if feature involves data)*

- **Persona habilitada**: RUT, nombre completo, unidad, calidad jurídica (Dotación, Plazo fijo,
  Honorarios), nivel vigente, forma de pago (Planilla o Efectivo mensual), estado de habilitación.
- **Nivel y valor**: nivel 1–3 con rango de sueldo imponible referencial, valor del almuerzo y fecha
  de vigencia; vale extra con su fecha de vigencia.
- **Carga mensual de niveles**: mes, RUT y nivel informados por Remuneraciones.
- **Ticket (ingreso)**: ID anual, persona, fecha, hora, almuerzos (titular + invitados), menú, valor
  aplicado, origen (terminal, manual, contingencia), estado (válido o anulado) con motivo, marca de
  asistencia pese a aviso.
- **Venta en efectivo / visita institucional**: folio EF o marca de visita, cantidad, vale extra,
  responsable del registro.
- **Elección de menú mensual**: persona, mes, tipo de menú; cambio por excepción con motivo, autor y
  fecha.
- **Aviso de ausencia** e **invitación**: persona, fecha o rango, cantidad de invitados, estado.
- **Minuta semanal**: semana, por día entrada, plato normal, hipocalórico, vegano y postre; estado
  borrador o publicado.
- **Cierre del casino**: fecha, horario, motivo, detalle, autor, estado; alerta al otro perfil.
- **Configuración del servicio**: servicio, ubicación, horario, plazos.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Una persona habilitada obtiene su ticket en menos de 10 segundos desde que empieza a
  digitar su RUT.
- **SC-002**: El 100 % de los montos del reporte de descuento mensual coincide con un recálculo
  manual (almuerzos consumidos no anulados × valor del nivel al emitir + vales extra).
- **SC-003**: Ningún ticket duplicado por persona y día en un mes de operación.
- **SC-004**: El Jefe Casino emite los tres reportes mensuales en menos de 5 minutos después de
  revisar las advertencias.
- **SC-005**: El 100 % de las anulaciones, registros manuales, cambios de nivel, forma de pago,
  menú por excepción y cierres tiene autor, fecha y motivo.
- **SC-006**: La diferencia entre raciones planificadas y almuerzos registrados baja frente al
  consumo habitual de referencia en los tres primeros meses de uso.
- **SC-007**: El sistema no almacena sueldos imponibles ni datos biométricos (verificable revisando
  los datos y exportaciones).
- **SC-008**: El 90 % de los funcionarios completa la elección de menú o un aviso de ausencia en el
  primer intento, sin ayuda.

## Assumptions

- La especificación describe la solución tal como la valida la maqueta; la maqueta usa datos
  ficticios y no guarda nada al recargar (constitución, principio I).
- Valores de almuerzo y vale extra: Casino Oficina Central, informados por Bienestar (marzo 2026).
- Plazo del menú mensual (día 25) es un valor de ejemplo que define Bienestar y es configurable.
- Horario de referencia: 12:30 a 15:00.
- Remuneraciones entrega cada mes un archivo RUT;nivel antes de emitir el reporte de descuento.
- La terminal es un equipo del casino con teclado numérico USB e impresora de tickets.
- La validación con RUT y PIN, la integración automática con el sistema de remuneraciones y la
  biometría quedan fuera de alcance (versión futura o descartadas).
- Dependencias abiertas, sin bloquear la spec: autorización y presupuesto de visitas institucionales
  (Dirección Ejecutiva y Finanzas) y lugar y plazo de la planilla de contingencia (Informática).
- Fuentes: solicitud del Servicio de Bienestar (13-08-2026), preguntas del Jefe Casino (02-11-2026),
  acuerdo UIA (22-10-2026); la propuesta «Control de Comedor» de GeoVictoria fue evaluada y
  descartada.
