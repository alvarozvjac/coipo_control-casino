# Contrato: archivos de entrada y salida

Convenciones comunes (principio VI):

- CSV con separador punto y coma (`;`), codificación UTF-8 con BOM para que Excel en configuración
  regional chilena muestre bien tildes y ñ.
- Montos enteros en pesos, sin símbolo ni separador de miles dentro del CSV.
- Fechas `DD-MM-AAAA`; horas `HH:MM`; RUT con guion y dígito verificador.
- Nunca incluir sueldos, claves ni datos biométricos.

## Entradas (se pegan como filas en la maqueta) [existen]

| Archivo | Formato por fila | Validación por fila |
|---|---|---|
| Actualización mensual de niveles | `RUT;nivel` | RUT válido, en nómina, nivel 1–3 |
| Planilla de contingencia | `RUT;hora` (también tabulador) | RUT válido, en nómina, hora `H:MM`/`HH:MM`, sin ticket ese día |
| Carga masiva de personas | según formulario actual | RUT válido y no repetido |

## Salidas [existen]

Reporte descuento mensual (por trabajador y por ticket), consumo por unidad, reporte anual por mes,
cobro mensual en efectivo, caja de ventas en efectivo, visitas institucionales, ingresos del período,
nómina de habilitados, ficha por persona, externos y visitas, reporte personal del funcionario
(`ID ticket;Fecha;Hora;Almuerzos;Menú;Valor de tu almuerzo;Vales extra (invitados);Monto`) y
planilla de contingencia en blanco (`N°;RUT;Nombre completo;Hora;Firma`).

## Salidas [cambian / nuevas]

| Archivo | Columnas | Requisito |
|---|---|---|
| Nómina de habilitados | agrega `Dependencia` | FR-028 |
| Ingresos del período | `Origen` admite `Terminal sin conexión` | FR-033 |
| Caja mensual en efectivo | agrega al pie `Total a rendir;Monto rendido;Fecha de rendición;Diferencia` | FR-030 |
| Registro de cuentas de usuario **[nuevo]** | `Fecha;Hora;Autor;Cuenta;Perfil;Acción` | FR-031 |
