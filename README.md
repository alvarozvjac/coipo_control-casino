# coipo_control-casino — Maqueta del control de ingreso al Casino Institucional

Maqueta de validación del sistema de control de ingreso al Casino Institucional de CONAF
para el Servicio de Bienestar, elaborada por la Unidad de Información y Análisis (UIA).
Iniciativa CON005.

**Ver la maqueta:** https://alvarozvjac.github.io/coipo_control-casino/

> Demostración no operacional. Personas, RUT, grados, valores, huellas y registros son
> ficticios. Lo que se haga en la maqueta no se guarda: al recargar la página vuelve al
> estado inicial.

## Cómo probarla

En el encabezado, el recuadro **«Maqueta · probar como»** cambia entre los dos perfiles.

| Perfil | Qué se puede probar |
|---|---|
| Jefe Casino | Terminal del casino (huella o RUT + PIN, emisión del ticket), propuesta de ticket, estadísticas, detalle de ingresos, emisión del reporte mensual de descuento, cierres del casino, personas habilitadas (grado y tramo), enrolamiento de huellas y configuración |
| Jefa de Bienestar | Estadísticas agregadas, emisión de reportes, cierres del casino y propuesta de ticket |

**Terminal del casino:** el **simulador del lector**, al costado, reemplaza al lector de
huella. «Poner dedo» simula que la persona apoya su dedo; «RUT + PIN» carga su RUT en la
vía alternativa (el PIN se muestra solo en la maqueta). Las tres primeras personas
(Carolina, Jorge y Daniela) muestran la emisión completa del ticket. Otros casos de la
lista: almuerzo ya registrado, PIN bloqueado, habilitación suspendida, huella no
reconocida y dedo mal apoyado. La hora está fijada en 13:05 y se cambia en Configuración.

**Valor del almuerzo:** se define por tramo según el grado (tramo 1: grados 3 a 11;
tramo 2: 12 a 14; tramo 3: 15 a 21). Quienes no tienen grado (honorarios, Código del
Trabajo) reciben el tramo que asigna el Jefe Casino. Los valores son de ejemplo.

**Cierres del casino:** al registrar o anular un cierre (clima, mantención, catástrofe,
corte de suministro u otro), el otro perfil recibe una alerta. Durante un cierre vigente
la terminal no emite tickets. Al abrir como Jefe Casino aparece una alerta de ejemplo
enviada por la Jefa de Bienestar.

**Reiniciar datos de prueba**, en el pie de página, vuelve todo al estado inicial.

## Contenido del repositorio

- `index.html`: la maqueta completa en un solo archivo (código, estilos e imágenes
  incluidos), sin dependencias externas.

Documentos de referencia: solicitud del Servicio de Bienestar (13-08-2026) y propuesta
comercial «Control de Comedor» de GeoVictoria (agosto 2026). La solución UIA mantiene la
identificación por huella con un lector propio, sin licencia ni arriendo, y RUT + PIN
como vía alternativa para quien no consienta el uso de su huella (Ley N° 21.719).
