# Quickstart: validación de la maqueta

**Requisitos**: navegador moderno (Chrome, Edge o Firefox). Sin servidor ni instalación.

**Abrir**: `index.html` directamente desde el disco, o la versión publicada
https://alvarozvjac.github.io/coipo_control-casino/. Antes de cada recorrido: «Reiniciar datos de
prueba» (pie de página). Abrir la consola del navegador: no debe haber errores en ningún paso.

Detalle de datos y pantallas: [data-model.md](./data-model.md),
[contracts/ui-perfiles.md](./contracts/ui-perfiles.md), [contracts/archivos.md](./contracts/archivos.md).

## Regresión (funcionalidad existente)

| # | Pasos | Resultado esperado |
|---|---|---|
| 1 | Terminal: digitar el RUT de Carolina, Jorge y Daniela | Ticket emitido; Daniela con 2 almuerzos |
| 2 | Terminal: repetir el RUT de Carolina | «Almuerzo ya registrado» con la hora |
| 3 | Terminal: Ignacio (aviso de ausencia) | Ticket emitido; en Comensales, «Asistió pese a aviso» |
| 4 | Terminal: suspendida, RUT fuera de nómina, RUT mal digitado | No emite; motivo y acción sugerida |
| 5 | Jefe Casino → Reportes → Emisión reporte mensual | 3 CSV que abren en Excel sin caracteres extraños |
| 6 | Mi casino: elegir menú, avisar ausencia, descargar CSV | Cada acción reflejada; CSV con 8 columnas |

## Validación de los cambios del plan

| # | Pasos | Resultado esperado | Req. |
|---|---|---|---|
| 7 | «Probar como» → Funcionario | Pantalla de inicio de sesión con usuario y clave de prueba; al ingresar, «Mi casino» | FR-031 |
| 8 | Jefe Casino → Comensales → Personas → Cuentas: bloquear la cuenta del funcionario de prueba; intentar iniciar sesión | No permite ingresar: «Cuenta bloqueada» | FR-031 |
| 9 | Jefe Casino: restablecer la clave; Jefa de Bienestar → Reportes → Registro de cuentas | Aparecen bloqueo y restablecimiento con autor, fecha y hora; no se ve ninguna clave | FR-031 |
| 10 | Configuración → activar «Simular corte de conexión»; Terminal: RUT de Jorge | Aviso «Sin conexión»; ticket «Registrado sin conexión» | FR-033 |
| 11 | Durante el corte: suspender a una persona en Comensales y digitar su RUT en la terminal | La terminal aún emite (usa la nómina copiada) | FR-033 |
| 12 | Durante el corte: ingreso manual de Jorge; luego desactivar el corte y «Sincronizar» | Comensales → «Duplicados por resolver» muestra a Jorge con 2 tickets; anular uno con motivo lo resuelve | FR-033 |
| 13 | Comensales: filtrar Dependencia = Región Metropolitana | Lista personas de RM con los mismos niveles y valores | FR-028 |
| 14 | Persona FAO (Efectivo mensual): emitir ticket y revisar reportes | No aparece en el descuento por planilla; en cobro mensual en efectivo con el valor de su nivel | FR-029 |
| 15 | Reportes → caja: registrar rendición con un monto distinto al total | Advertencia con la diferencia; la rendición queda registrada | FR-030 |
| 16 | Manual → Reglas y Pendientes | Lista real de datos registrados, conservación sin plazo; pendientes solo visitas y contingencia | FR-027, FR-032 |
| 17 | Información → Día | 3 franjas de 15 minutos más concurridas visibles | SC-009 |
