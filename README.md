# Sistema Programable de Control de Riego
Sistema de control de riego programable mediante centralita electrónica controlada por una placa de desarrollo NodeMCU.

El esquema general de bloques del Sistema se muestra a continuación

![SCR](/diagrama-control-riego.svg)

## Centralita Electrónica de Riego (CER)
Será la encargada del control electrónico de las válvulas de riego, permitiendo en encendido y apagado de las mismas.

## Servicio Web de Control de Riego (SWCR)
El Servicio se encontrará alojado en un Servidor Web con acceso a una base de datos. Dicho servicio será configurable y permitirá la comunicación con el usuario y con la Centralita Electrónica de Riego.

## Cómunicación CER - SWCR
En una primera versión, la comunicación se llevará a cabo mediante peticiones HTTP desde el CER por sondeo a intervalos regulares.

### Mensajes CER - SWCR
<table>
<thead>
  <tr>
    <th>Mensajes CER (mediante POST a "update.php" </th>
    <th>Respuesta del SWCR</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>getZoneStatus</td>
    <td>zones:n&lt;sub&gt;1&lt;/sub&gt;n&lt;sub&gt;2&lt;/sub&gt; ... <br>Donde n&lt;sub&gt;1&lt;/sub&gt;n&lt;sub&gt;2&lt;/sub&gt;, tomarán el valor: 1 para encendido, 0 para apagado <br>Ej: zones:10</td>
  </tr>
  <tr>
    <td>setZoneStatus=12<br>Donde 12 toman el valor:<br>1 para encendido<br>0 para apagado</td>
    <td>OK</td>
  </tr>
  <tr>
    <td>setStatus=estado<br>Donde estado toma el valor:<br>inicio<br>parada<br>error</td>
    <td>OK</td>
  </tr>
</tbody>
</table>

## Interfaz de usuario SWCR
Se empleará una interfal basada en Bootstrap. En la parte superior debe aparecer el logo y nombre: "Sistema de Control de Riego"
En la primera versión no se incluirá sistema de identificación de usuario.

## Sistemas de menú del SWCR
![SCR](/diagrama-menus.svg)

## Inicio (index.php)
Mostrará el acceso a las diferentes opciones mediante menús/botones. Se mostrará en la parte superio la fecha y hora actuales.

## Configuración (config.php)
Mostrará las opciones de configuración. La información se almacenará en la BBDD del SWCR
- *numZones*: Número de zonas. En la versión inicial se contemplan 2 zonas
- *zoneName[]*: Nombre de cada zona. Configurable por el usuario.

## Test (test.php)
Permite el apagado y encenddo de las válvulas de riego. La interfaz mostrará un botón por casa válvula (zona)

## Programa (programa.php)
Permite especificar la hora de encendido y apagado por zonas. La interfaz permitirá seleccionar una zona (1,2) y un programa de cada zona (1-4). Se podrá introducir la hora de encendidio y apagado diario.

#BBDD
Utilizaremos MySQL como sistema gestor de base de datos. La estructura se muestra a continuación





