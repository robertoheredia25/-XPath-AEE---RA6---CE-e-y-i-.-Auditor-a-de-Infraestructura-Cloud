# XPath AEE - RA6 - CE e) y i). Auditoría de Infraestructura Cloud

##  ¿Cuántas líneas de código habéis ahorrado al usar grupos?

Al utilizar `<xs:group>` para el bloque de hardware y `<xs:attributeGroup>` para los atributos del servidor, hemos logrado aislar toda la lógica compleja fuera de la definición del elemento principal.

Si miramos específicamente dentro del `complexType` de `<servidor>`, **hemos ahorrado más de 60 líneas de código anidado**. Antes, la definición del servidor era enorme y difícil de leer porque arrastraba todo el árbol del hardware. Ahora, la llamada al hardware ocupa tan solo **3 líneas** (`<xs:group ref="ComponentesHardware" />`), y los atributos **1 sola línea** (`<xs:attributeGroup ref="el atributo" />`). Aunque las líneas se han movido a la raíz del XSD, el modelo de datos principal es infinitamente más limpio y fácil de mantener.

Gracias a esta creacios de grupos y atributos hemos ahorrado unas 30 lineas ya que le codigo original tenia 222 lineas y este gracias a la creacion de los grupos y los atributos de grupos estamos en torno a unas 192

## ¿Qué error os da VS Code si intentáis poner dos servidores con el mismo ID?

Al intentar duplicar un atributo `@id` (por ejemplo, poniendo `id="srv-web-01"` en dos servidores distintos), la validación XML en VS Code lanza un error de restricción de identidad (Identity Constraint) disparado por la regla `<xs:unique name="UnicoID">`. 

El error que nos da es:
`cvc-identity-constraint.4.1: Duplicate unique value [srv-web-01] declared for identity constraint "UnicoID" of element "catalogo_cloud".`
