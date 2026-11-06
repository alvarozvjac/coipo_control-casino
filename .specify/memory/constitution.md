<!--
Sync Impact Report
- Version change: (plantilla sin completar) → 1.0.0
- Principios definidos: I. Maqueta de validación no operacional; II. Archivo único autocontenido;
  III. Protección de datos personales y minimización; IV. Reglas de negocio trazables a su fuente;
  V. Perfiles con funciones separadas y registro de acciones; VI. Lenguaje institucional y
  estándar de interfaz UIA
- Secciones agregadas: Restricciones de la solución; Flujo de trabajo y control de calidad; Governance
- Secciones eliminadas: ninguna
- Plantillas dependientes: plan-template.md, spec-template.md y tasks-template.md leen esta
  constitución en tiempo de ejecución; no requieren cambios
- TODO diferidos: ninguno
-->

# Control de Casino Institucional (CON005) Constitution

## Core Principles

### I. Maqueta de validación no operacional

La solución en este repositorio es una maqueta para validar funcionalidades con el Servicio de
Bienestar, el Jefe Casino y la UIA; no es un sistema en producción.

- Toda persona, RUT, nivel y registro MUST ser ficticio. Solo los valores del almuerzo por nivel y
  el vale extra MAY ser reales, con su fuente y fecha indicadas.
- La interfaz MUST mostrar en forma visible que es una «maqueta no operacional».
- Los datos de prueba MUST volver a su estado inicial al recargar la página o al usar «Reiniciar
  datos de prueba». Solo MAY persistirse en el navegador la preferencia de perfil activo.
- Cada propuesta que todavía no está acordada con la contraparte MUST quedar rotulada como
  propuesta en la propia maqueta.

Razón: la maqueta se presenta y circula entre unidades; debe ser imposible confundirla con un
sistema que descuenta remuneraciones reales.

### II. Archivo único autocontenido

- La maqueta completa MUST residir en `index.html` (código, estilos e imágenes incluidos).
- No MUST haber dependencias externas en tiempo de ejecución (CDN, fuentes remotas, APIs).
- MUST funcionar abierta desde GitHub Pages y desde el disco local, sin servidor ni compilación.

Razón: se publica en GitHub Pages, se comparte como archivo y se entrega a la fábrica COIPO como
insumo; cualquier dependencia de red rompe la demostración en redes institucionales.

### III. Protección de datos personales y minimización (Ley N° 21.719)

- La identificación de personas MUST hacerse por RUT digitado en teclado numérico. Están
  prohibidos los datos biométricos.
- El sistema MUST guardar solo el nivel de valor del almuerzo de cada persona, nunca el sueldo
  imponible ni otros datos de remuneraciones.
- Cada dato personal nuevo que se proponga MUST justificar su finalidad en la spec (qué proceso
  lo necesita y quién lo ve).
- Los reportes y exportaciones MUST limitarse a los datos que necesita su destinatario.

Razón: acuerdo de la reunión UIA del 22-10-2026 y línea de Gobernanza de Datos de la UIA frente a
la Ley N° 21.719.

### IV. Reglas de negocio trazables a su fuente

- Cada regla de negocio (valores por nivel, vale extra, plazos de elección de menú y de aviso de
  ausencia, formas de pago, calidades jurídicas) MUST tener una fuente identificada: solicitud de
  Bienestar, información de Remuneraciones, preguntas del Jefe Casino o acuerdo UIA, con fecha.
- Los valores monetarios y plazos MUST ser parámetros configurables, no constantes dispersas.
- Un cambio de regla MUST actualizar a la vez la maqueta, el Manual de usuario y el README.

Razón: los descuentos por planilla afectan remuneraciones; toda cifra debe poder explicarse ante
Bienestar, Remuneraciones o una auditoría.

### V. Perfiles con funciones separadas y registro de acciones

- Los perfiles vigentes son Terminal casino, Funcionario, Jefe Casino y Jefa de Bienestar. Cada
  perfil MUST ver y modificar solo lo que su función requiere.
- Toda acción que altere un cobro o una habilitación (ingreso manual, anulación de ticket, cambio
  de nivel, forma de pago, menú por excepción, cierre del casino) MUST registrar quién, cuándo y
  el motivo.
- Los tickets MUST tener un ID único con año y correlativo anual; las ventas en efectivo, un folio
  propio `EF-AAAA-NNNN`.
- Solo los almuerzos efectivamente consumidos MAY generar descuento.

Razón: separación de funciones y trazabilidad del descuento por planilla y de la caja.

### VI. Lenguaje institucional y estándar de interfaz UIA

- Todos los textos MUST estar en español formal del sector público chileno, con formatos
  chilenos (RUT con dígito verificador, $ con punto de miles, fechas DD-MM-AAAA).
- La interfaz MUST seguir el estándar de interfaz de las maquetas UIA (coipo_master_produccion,
  `ESTANDAR_UI.md`).
- Las exportaciones MUST ser CSV que se abran correctamente en Excel en configuración regional
  chilena.
- La terminal MUST ser utilizable solo con teclado numérico (la tecla `*` equivale a la K).

Razón: los usuarios son funcionarios de CONAF y personal del casino, no especialistas.

## Restricciones de la solución

- Tecnología de la maqueta: HTML, CSS y JavaScript sin frameworks ni proceso de compilación.
- Publicación: GitHub Pages (`.nojekyll`) desde la rama principal.
- Fuera de alcance de esta versión: validación con RUT y PIN, integración real con el sistema de
  remuneraciones, impresoras de tickets reales y biometría. Se registran como versión futura.
- Referencias: solicitud del Servicio de Bienestar (13-08-2026), propuesta comercial «Control de
  Comedor» de GeoVictoria (agosto 2026) como alternativa evaluada y descartada, acuerdo UIA del
  22-10-2026.

## Flujo de trabajo y control de calidad

- Cada funcionalidad nueva o cambio relevante MUST pasar por `/speckit-specify` antes de
  modificar `index.html`, y la spec MUST indicar qué perfiles afecta.
- Antes de publicar en la rama principal MUST verificarse: los cuatro perfiles cargan sin errores
  de consola, el flujo de terminal con las personas de prueba, la descarga de cada CSV y que el
  Manual de usuario refleja el cambio.
- La maqueta se entrega a la fábrica COIPO con sus insumos (00-PROBLEMA, 01-SOLUCION) y la spec
  vigente.

## Governance

Esta constitución prevalece sobre otras prácticas del repositorio. Las enmiendas MUST quedar en un
commit propio con la versión nueva y el motivo. Versionado semántico: MAJOR al eliminar o
redefinir un principio; MINOR al agregar un principio o sección; PATCH en aclaraciones de
redacción. Cada spec, plan y PR MUST verificar el cumplimiento de estos principios; cualquier
excepción MUST justificarse por escrito en el plan.

**Version**: 1.0.0 | **Ratified**: 2026-11-06 | **Last Amended**: 2026-11-06
