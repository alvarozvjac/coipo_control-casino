# Contrato: pantallas por perfil

Pestañas visibles por perfil (`PERF` en `index.html`). Los cambios de este plan van en negrita.

| Perfil | Inicio de sesión | Pestañas |
|---|---|---|
| Terminal casino | No (identificación solo por RUT) | Terminal, Propuesta de ticket, Manual |
| Funcionario | **Usuario y clave (simulado)** | Mi casino, Manual |
| Jefe Casino | **Usuario y clave (simulado)** | Menú semanal, Planificación, Reportes, Comensales, Configuración, Cierres, Información, Manual |
| Jefa de Bienestar | **Usuario y clave (simulado)** | Información, Reportes, Cierres, Manual |

## Elementos nuevos o modificados

| Ubicación | Perfil | Elemento | Requisito |
|---|---|---|---|
| Al cambiar de perfil | Funcionario, Jefe Casino, Jefa de Bienestar | **Pantalla de inicio de sesión** con datos de prueba precargados y rótulo de maqueta; «Cerrar sesión» en el encabezado | FR-031 |
| Comensales → Personas | Jefe Casino | **Tarjeta «Cuentas de usuario»**: crear, bloquear/desbloquear, restablecer clave | FR-031 |
| Reportes | Jefa de Bienestar | **Registro de cuentas de usuario** (solo lectura, CSV) | FR-031 |
| Configuración | Jefe Casino | **Interruptor «Simular corte de conexión (solo maqueta)»** y botón «Sincronizar» | FR-033 |
| Terminal | Terminal casino | **Aviso «Sin conexión»**; ticket con marca «Registrado sin conexión» | FR-033 |
| Comensales | Jefe Casino | **Filtro «Duplicados por resolver»** y columna/filtro **«Dependencia»** | FR-033, FR-028 |
| Reportes → caja en efectivo | Jefe Casino | **Sección «Rendición a Finanzas»** con advertencia de diferencia | FR-030 |
| Manual de usuario | Todos | **Reglas actualizadas**: datos registrados, conservación, RM, FAO, efectivo, sin conexión, cuentas; pendientes reducidos a visitas y contingencia | FR-027 a FR-033 |

Mensajes de la terminal sin cambio de texto: RUT inválido, fuera de nómina, suspendida, fuera de
horario, casino cerrado, almuerzo ya registrado (FR-004).
