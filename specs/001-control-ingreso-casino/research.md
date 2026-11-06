# Research: Control de ingreso al Casino Institucional (maqueta HTML)

**Fecha**: 2026-11-06 | **Plan**: [plan.md](./plan.md) | **Spec**: [spec.md](./spec.md)

Alcance: decisiones técnicas para llevar a la maqueta (`index.html`) los requisitos que la spec
agregó o cambió el 2026-11-06 (FR-028 a FR-033, SC-009) y para corregir el Manual de usuario. La
maqueta ya cubre FR-001 a FR-027.

## R1. Inicio de sesión con usuario y clave (FR-031) en una maqueta sin servidor

- **Decision**: pantalla de inicio de sesión **simulada** para los perfiles Funcionario, Jefe Casino
  y Jefa de Bienestar, con cuentas ficticias precargadas y su clave de prueba visible en un rótulo
  «Maqueta: usuario y clave de prueba». El recuadro «Maqueta · probar como» se mantiene y, al cambiar
  de perfil, abre esa pantalla con los datos de prueba ya escritos. La terminal no pide sesión.
- **Rationale**: la constitución (I, II) exige maqueta no operacional y sin servidor; una clave real
  no tendría dónde validarse. Simular el paso permite validar el flujo y la pantalla con Bienestar.
- **Alternatives considered**: (a) validar claves con hash en el navegador: da una falsa sensación de
  seguridad y no aporta a la validación; (b) omitir el inicio de sesión: deja sin validar FR-031.

## R2. Administración de cuentas por el Jefe Casino y registro consultable por Bienestar (FR-031)

- **Decision**: nueva tarjeta «Cuentas de usuario» en Comensales → Personas (Jefe Casino): crear
  cuenta desde una persona habilitada, bloquear/desbloquear y restablecer clave (genera una clave
  temporal ficticia de un solo uso). Cada acción se agrega a un registro con fecha, hora, autor,
  cuenta y acción. La Jefa de Bienestar ve ese registro en solo lectura en una tarjeta de Reportes
  («Registro de cuentas de usuario»), con descarga CSV.
- **Rationale**: reutiliza el patrón de tarjetas de selección ya existente en Comensales y cumple
  el principio V (quién, cuándo, motivo) compensando que el Jefe Casino opere cobro y cuentas.
- **Alternatives considered**: pestaña nueva «Cuentas»: agrega navegación para una función de uso
  esporádico.

## R3. Simulación de corte de conexión de la terminal (FR-033)

- **Decision**: en Configuración, junto a «Hora simulada (solo maqueta)», un interruptor «Simular
  corte de conexión (solo maqueta)». Con el corte activo la terminal muestra el aviso «Sin conexión ·
  los tickets se guardan y se enviarán al reconectar», sigue validando contra la nómina cargada al
  iniciar el corte (copia instantánea) y marca los tickets «Registrado sin conexión». Los cambios de
  habilitación y los cierres registrados durante el corte no se aplican en la terminal hasta
  reconectar. Al desactivarlo, «Sincronizar» integra los tickets y, si una persona quedó con más de un
  ticket válido el mismo día, los lista en Comensales con el filtro «Duplicados por resolver», donde
  el Jefe Casino anula el que sobra con motivo.
- **Rationale**: la maqueta corre en un solo navegador; un interruptor reproduce el caso de forma
  determinista, igual que la hora simulada. El duplicado solo puede ocurrir si la maqueta permite un
  ingreso manual durante el corte; ese es el caso de prueba.
- **Alternatives considered**: usar `navigator.onLine`: la maqueta no tiene servidor, el evento no
  representa el caso real y no es reproducible en una demostración.

## R4. Usuarios de la Región Metropolitana (FR-028)

- **Decision**: agregar a cada persona el campo «Dependencia» (Oficina Central o Región
  Metropolitana – otra dependencia), mostrarlo en Comensales y agregar un filtro. Algunas personas de
  prueba quedan en Región Metropolitana. Los niveles y valores son los mismos; no hay regla de cobro
  distinta.
- **Rationale**: la decisión de Bienestar no cambia el cobro; basta con que el dato sea visible para
  validar la nómina y los reportes por dependencia.
- **Alternatives considered**: deducir la dependencia desde la unidad: las unidades no identifican
  la ubicación física.

## R5. Personal FAO con pago efectivo mensual (FR-029)

- **Decision**: sin cambio de cálculo: la maqueta ya cobra a las personas con forma de pago Efectivo
  mensual el valor de su nivel (`montoR`). Se agrega una persona de prueba FAO con nivel asignado y se
  quita el tema de «Pendientes de definición» del Manual.
- **Rationale**: el comportamiento actual coincide con la decisión.

## R6. Custodia y rendición mensual del efectivo (FR-030)

- **Decision**: en Reportes, el reporte de caja mensual muestra el total a rendir (ventas en efectivo
  + cobros mensuales en efectivo) y una sección «Rendición a Finanzas» donde el Jefe Casino registra
  la fecha de rendición, el monto rendido y una observación; si el monto no coincide con el total, se
  muestra una advertencia. La rendición queda en el registro de acciones.
- **Rationale**: el reporte de caja ya existe; la rendición mensual solo necesita un registro de
  cierre con su diferencia.
- **Alternatives considered**: cierre de caja diario: descartado por la decisión del usuario.

## R7. Conservación sin plazo (FR-032) y texto del Manual sobre datos registrados

- **Decision**: no requiere código. Se corrige el Manual: la frase «Se registran solo RUT, nombre,
  unidad, nivel, fecha y hora» se reemplaza por la lista real de datos (identificación, unidad,
  dependencia, calidad jurídica, nivel, forma de pago, habilitación, menú, avisos, invitados,
  tickets y motivos de acciones), indicando que no se guardan sueldos ni datos biométricos y que los
  registros se conservan sin plazo de eliminación. Se quitan de «Pendientes de definición» los tres
  temas resueltos y se mantienen visitas institucionales y planilla de contingencia.
- **Rationale**: el texto actual contradice el principio III de la constitución y los datos que la
  maqueta realmente usa.

## R8. Estándar de interfaz UIA (principio VI)

- **Decision**: reutilizar los estilos ya presentes en `index.html` (tarjetas, chips, pill, btn,
  colores institucionales) para todos los elementos nuevos. `ESTANDAR_UI.md` de
  coipo_master_produccion no está en este repositorio; se verifica contra él en la revisión del PR.
- **Rationale**: mantiene la coherencia visual sin depender de un repositorio externo durante la
  implementación.

## R9. Volumen y rendimiento (SC-009)

- **Decision**: sin cambios: la maqueta trabaja en memoria con datos de prueba anuales; 200 almuerzos
  diarios están dentro del volumen que ya genera `seedYear`. Se verifica que la terminal responda al
  Enter sin demora perceptible y que Información muestre las franjas de 15 minutos.
- **Rationale**: el rendimiento real de la fila depende de la terminal física, fuera del alcance de
  la maqueta.
