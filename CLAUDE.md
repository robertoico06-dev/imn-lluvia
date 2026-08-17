# Tarea diaria: registro de lluvia — estaciones del IMN

## Objetivo
En cada ejecución, visitá las 8 estaciones automáticas del IMN listadas abajo,
extraé el dato de lluvia más reciente de cada una, y agregá una fila por
estación al archivo `registro_lluvia_imn.csv` de esta carpeta.

## Estaciones a consultar
| estacion | ubicacion | url_tabla |
|---|---|---|
| Rebusca | Puerto Viejo, Heredia | https://www.imn.ac.cr/especial/tablas/larebusca.html |
| SanGerardo | La Virgen de Sarapiquí, Heredia | https://www.imn.ac.cr/especial/tablas/sangerardo.html |
| Poas | Volcán Poás, Alajuela | https://www.imn.ac.cr/especial/tablas/vpoas.html |
| Pozoazul | Sarapiquí, Heredia | https://www.imn.ac.cr/especial/tablas/pozoazul.html |
| Tirimbina | La Virgen de Sarapiquí, Heredia | https://www.imn.ac.cr/especial/tablas/tirimbina.html |
| Sarapiqui | Sarapiquí, Heredia | https://www.imn.ac.cr/especial/tablas/pvsarapiqui.html |
| Horquetas | Horquetas de Sarapiquí, Heredia | https://www.imn.ac.cr/especial/tablas/horquetas.html |
| Hidroelectrica | Horquetas de Sarapiquí, Heredia | https://www.imn.ac.cr/especial/tablas/hidroelectrica.html |

Las páginas principales (con el panel/imagen) tienen el mismo nombre de
estación pero como `https://www.imn.ac.cr/especial/estacionNOMBRE.html`.

## Pasos por cada estación
1. Abrí primero la `url_tabla` de la tabla anterior con WebFetch.
2. Tomá la fila más reciente y anotá "Fecha", "Temp" y "Lluvia".
3. Si esa página no trae datos (tabla vacía o solo encabezados), abrí la
   página principal de esa estación, buscá el enlace de texto que apunta a
   `/especial/tablas/...` cerca del final de la página, y repetí el paso 1
   con esa URL completa (puede que ya no coincida con la tabla de arriba si
   el IMN la cambió).
4. Si aun así no conseguís un número de lluvia en texto, dejá "lluvia_mm"
   vacío y explicá en "notas" qué pasó (por ejemplo: "estación sin
   responder" o "tabla sin datos ese momento"). No inventes ni redondees
   valores que no viste con claridad.
5. "Lluvia" es un acumulado diario, así que no debería bajar dentro del mismo
   día. Si ves que sí bajó respecto a una corrida anterior, es señal de que la
   estación tuvo un reinicio o un error de lectura: anotalo en "notas" en vez
   de guardarlo como si fuera el total normal del día.

## Dónde guardar
Archivo: `registro_lluvia_imn.csv` en esta misma carpeta.

- Si no existe, creálo con este encabezado exacto:
  `fecha,hora_captura,estacion,ubicacion,lluvia_mm,temperatura_c,hora_dato_imn,notas`
- Antes de agregar una fila, revisá si ya hay una fila con la misma "fecha" y
  "estacion". Si ya existe, no la dupliques: actualizala solo si el dato
  nuevo es más reciente que el guardado.
- `fecha`: hoy, en formato AAAA-MM-DD, hora de Costa Rica. Confirmala con el
  comando `date`, no la asumas.
- `hora_captura`: hora local (Costa Rica) en que corriste la tarea, HH:MM.
- `hora_dato_imn`: la hora que muestra la tabla del IMN junto al dato (para
  saber qué tan reciente era la lectura en el momento de la captura).

## Al terminar
1. Hacé commit de los cambios en `registro_lluvia_imn.csv` con un mensaje
   descriptivo (por ejemplo: "Registro de lluvia 2026-08-17") y hacé push a
   la rama por defecto del repositorio (`main`).
2. Escribí en la salida un resumen de 3-5 líneas: cuántas estaciones se
   guardaron bien y cuáles tuvieron problemas.

## Reglas
- Una sola solicitud por estación por ejecución; no hace falta reintentar
  ni refrescar varias veces.
- Estos datos son preliminares y sin control de calidad oficial del IMN;
  tratalos como referencia en tiempo real, no como dato validado.
- No modifiques filas de fechas pasadas, salvo para completar un dato que
  había quedado pendiente.
