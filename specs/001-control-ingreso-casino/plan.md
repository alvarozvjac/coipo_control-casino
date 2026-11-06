# Implementation Plan: Control de ingreso al Casino Institucional (maqueta HTML)

**Branch**: `speckit` | **Date**: 2026-11-06 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/001-control-ingreso-casino/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command; its definition describes the execution workflow.

## Summary

La maqueta publicada ya implementa FR-001 a FR-027. Este plan la lleva al estado de la spec aclarada
el 2026-11-06, dentro del mismo `index.html` y sin servidor:

1. Inicio de sesión simulado con usuario y clave para Funcionario, Jefe Casino y Jefa de Bienestar,
   cuentas administradas por el Jefe Casino y registro de cuentas consultable por Bienestar (FR-031).
2. Simulación de corte de conexión de la terminal con sincronización y resolución de duplicados
   (FR-033).
3. Dependencia Oficina Central / Región Metropolitana por persona (FR-028) y persona de prueba FAO
   con el valor de su nivel (FR-029).
4. Rendición mensual del efectivo a Finanzas en el reporte de caja (FR-030).
5. Manual de usuario y README corregidos: datos realmente registrados, conservación sin plazo
   (FR-032), reglas nuevas y pendientes reducidos.

Enfoque técnico en [research.md](./research.md): reutilizar los patrones existentes (tarjetas de
Comensales, simulaciones «solo maqueta» de Configuración, registro de quién/cuándo/motivo).

## Technical Context

**Language/Version**: HTML5, CSS3 y JavaScript ES2020 sin transpilación

**Primary Dependencies**: ninguna (sin frameworks, CDN ni fuentes remotas)

**Storage**: memoria del navegador, reconstruida con `seedAll()`; `localStorage` solo para el perfil
activo (`casino.perfil`) y, como máximo, la sesión simulada, envuelto en try/catch

**Testing**: recorrido manual guiado por [quickstart.md](./quickstart.md) en Chrome y Edge, con la
consola sin errores; validación de sintaxis del JavaScript extraído (`node --check`)

**Target Platform**: navegadores de escritorio actuales; GitHub Pages y apertura local (`file://`)

**Project Type**: maqueta web de una sola página (single-file SPA)

**Performance Goals**: la terminal responde al Enter sin demora perceptible; las vistas se
re-dibujan en menos de 300 ms con un año de datos de prueba (hasta 200 almuerzos diarios, SC-009)

**Constraints**: un solo archivo autocontenido (≈280 KB hoy; mantener bajo 400 KB); textos en
español formal; nada se guarda al recargar salvo perfil/sesión simulada

**Scale/Scope**: 4 perfiles, 13 vistas actuales; agrega 1 pantalla de inicio de sesión, 3 tarjetas
nuevas (Cuentas, Registro de cuentas, Rendición) y 2 controles de simulación

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principio | Verificación | Antes | Después del diseño |
|---|---|---|---|
| I. Maqueta no operacional | Cuentas y claves ficticias, rotuladas «Maqueta»; corte de conexión rotulado «solo maqueta»; todo vuelve al estado inicial al recargar | ✅ | ✅ |
| II. Archivo único | Todos los cambios dentro de `index.html`; sin dependencias externas | ✅ | ✅ |
| III. Datos personales | No se agregan sueldos ni biometría; la clave nunca se muestra ni exporta; Manual corregido para declarar los datos reales. FR-032 (sin plazo) registrado como riesgo en la spec | ⚠️ justificado | ⚠️ justificado |
| IV. Reglas trazables | Valores y plazos siguen en `cfg`; decisiones del 2026-11-06 citadas en la spec; Manual y README se actualizan junto con la maqueta | ✅ | ✅ |
| V. Perfiles y registro | Cuentas, bloqueos, restablecimientos, rendición y resolución de duplicados registran autor, fecha y motivo; Bienestar ve el registro de cuentas | ✅ | ✅ |
| VI. Lenguaje y estándar UIA | Textos en español formal; CSV `;` con BOM; estilos existentes reutilizados; `ESTANDAR_UI.md` se verifica en revisión del PR | ✅ | ✅ |

**Resultado**: GATE aprobado. La única observación (III, conservación sin plazo) es una decisión del
usuario ya documentada como riesgo de cumplimiento; no se implementa en la maqueta más allá del texto
del Manual. Ver Complexity Tracking.

## Project Structure

### Documentation (this feature)

```text
specs/001-control-ingreso-casino/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md        # Phase 1 output (/speckit-plan command)
├── quickstart.md        # Phase 1 output (/speckit-plan command)
├── contracts/           # Phase 1 output (/speckit-plan command)
│   ├── archivos.md      # CSV de entrada y salida
│   └── ui-perfiles.md   # Pantallas por perfil
├── checklists/
│   └── requirements.md
└── tasks.md             # Phase 2 output (/speckit-tasks command - NOT created by /speckit-plan)
```

### Source Code (repository root)

```text
index.html     # Maqueta completa: <style> + marcado de vistas (section.view) + <script>
               #   Datos de prueba: seedPersonas, seedAll, PERF, USR, cfg
               #   Terminal: checkRut, emit, renderScreen
               #   Comensales: renderCom, comLista, abrirPanel
               #   Reportes: renderRepo, comReporte, descargarCsv/csvTxt
               #   Configuración: renderNiv, renderTramos
               #   Manual: renderManual
README.md      # Guía de prueba de la maqueta (se actualiza con los cambios)
.nojekyll      # Publicación en GitHub Pages
```

**Structure Decision**: se mantiene el archivo único `index.html` (principio II). Las funciones
nuevas se agregan junto a las de su vista: inicio de sesión y cuentas junto a `pintarPerfil`/`USR`,
corte de conexión junto a la hora simulada de Configuración y `checkRut`/`emit`, rendición junto a
`renderRepo`. README se actualiza en el mismo cambio (principio IV).

## Complexity Tracking

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| Principio III: conservación de registros sin plazo (FR-032) | Decisión del usuario del 2026-11-06 | Un plazo fijo fue propuesto y rechazado; queda como riesgo a validar con Gobernanza de Datos y Fiscalía antes de producción, sin efecto en la maqueta |
