# Data Model: Control de ingreso al Casino Institucional (maqueta HTML)

**Fecha**: 2026-11-06 | **Spec**: [spec.md](./spec.md)

La maqueta guarda todo en memoria (variables JavaScript de `index.html`) y lo reconstruye con
`seedAll()` al cargar o al usar «Reiniciar datos de prueba». Solo el perfil activo persiste en el
navegador (`localStorage` `casino.perfil`). Los nombres entre paréntesis son las variables actuales.

Leyenda: **[existe]** ya está en la maqueta · **[nuevo]** o **[cambia]** según este plan.

## Persona habilitada (`P`) [cambia]

| Campo | Tipo | Regla |
|---|---|---|
| key | RUT sin puntos ni guion, con DV | Único; DV válido (FR-001) |
| nombre | texto | Nombre completo |
| unidad | texto de `UNI` | — |
| dependencia **[nuevo]** | «Oficina Central» o «Región Metropolitana» | FR-028; mismos niveles y valores |
| calidad | Dotación, Plazo fijo, Honorarios | — |
| nivel | 1, 2, 3 o sin nivel | Desde carga mensual; nunca el sueldo (FR-025) |
| pago | «Planilla» o «Efectivo mensual» | Efectivo mensual fuera del descuento (FR-010, FR-029) |
| hab | sí/no | Suspendida no emite ticket (FR-004) |
| menú por mes | Normal, Hipocalórico, Vegano | Plazo día 25; sin elección = Normal (FR-016) |

## Cuenta de usuario [nuevo] (FR-031)

| Campo | Tipo | Regla |
|---|---|---|
| usuario | texto único | Para Funcionario, asociada a un RUT de `P` |
| perfil | funcionario, casino, bienestar | Una cuenta = un perfil |
| rut | RUT o vacío | Obligatorio si perfil = funcionario |
| estado | activa, bloqueada, clave temporal | Bloqueada no inicia sesión |
| clave | ficticia, solo maqueta | Nunca se muestra en listas ni se exporta |

Transiciones: creada → activa; activa ⇄ bloqueada; activa/bloqueada → clave temporal (al
restablecer) → activa (al iniciar sesión y cambiarla).

## Registro de cuentas [nuevo]

fecha, hora, autor (Jefe Casino), cuenta, acción (crear, bloquear, desbloquear, restablecer).
Solo se agrega; no se edita ni borra. Lectura: Jefa de Bienestar (FR-031).

## Ticket / ingreso (`R`) [cambia]

| Campo | Regla |
|---|---|
| id | `AAAA-NNNNNN`, correlativo anual (FR-005) |
| key, fecha, hora | Un ticket válido por persona y día (FR-003) |
| almuerzos | titular + invitados |
| menú, valor | Valor del nivel al emitir; no cambia después (FR-024) |
| origen | Terminal, **Terminal sin conexión [nuevo]**, Manual, Contingencia |
| estado | Válido o Anulado (solo del día, con motivo) (FR-013) |
| conAviso | «Asistió pese a aviso» (FR-018) |
| duplicado **[nuevo]** | marca calculada al sincronizar: misma persona y día con más de un válido |

## Estado de conexión de la terminal [nuevo] (FR-033)

| Campo | Regla |
|---|---|
| sinConexion | interruptor de Configuración (solo maqueta) |
| nominaCopia | copia de `P` y de los cierres al iniciar el corte; la terminal valida contra ella |
| pendientes | tickets emitidos durante el corte, por sincronizar |

Transiciones: conectada → sin conexión (se toma la copia) → sincronizando → conectada (tickets
integrados; duplicados marcados para el Jefe Casino).

## Venta en efectivo / visita institucional [existe]

Folio `EF-AAAA-NNNN` para ventas; marca de visita; vale extra por almuerzo (FR-011).

## Rendición mensual a Finanzas [nuevo] (FR-030)

| Campo | Regla |
|---|---|
| mes | AAAA-MM |
| totalCalculado | ventas en efectivo + cobros mensuales en efectivo del mes |
| fecha | fecha de rendición |
| montoRendido | entero en pesos |
| observación | texto |
| autor | Jefe Casino |

Si `montoRendido ≠ totalCalculado`, se muestra la diferencia como advertencia.

## Otras entidades [existen]

Nivel y valor (`cfg`, vigencias), carga mensual de niveles (`NIVCARGA`), aviso de ausencia e
invitación, minuta semanal (`MINUTAS`, borrador/publicado), cierre del casino (`CIERRES`, con alerta
al otro perfil), configuración del servicio (`cfg`).
