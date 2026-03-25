# XPath AEE - RA6 - CE e) y i). Auditoría de Infraestructura Cloud

##  ¿Cuántas líneas de código habéis ahorrado al usar grupos?
Al utilizar `<xs:group>` para el bloque de hardware y `<xs:attributeGroup>` para los atributos del servidor, hemos logrado aislar toda la lógica compleja fuera de la definición del elemento principal.

Si miramos específicamente dentro del `complexType` de `<servidor>`, **hemos ahorrado más de 60 líneas de código anidado**. Antes, la definición del servidor era enorme y difícil de leer porque arrastraba todo el árbol del hardware. Ahora, la llamada al hardware ocupa tan solo **3 líneas** (`<xs:group ref="ComponentesHardware" />`), y los atributos **1 sola línea** (`<xs:attributeGroup ref="AtributosServidor" />`). Aunque las líneas se han movido a la raíz del XSD, el modelo de datos principal es infinitamente más limpio y fácil de mantener.

## b. ¿Qué error os da VS Code si intentáis poner dos servidores con el mismo ID?
Al intentar duplicar un atributo `@id` (por ejemplo, poniendo `id="srv-web-01"` en dos servidores distintos), la validación XML en VS Code lanza un error de restricción de identidad (Identity Constraint) disparado por la regla `<xs:unique name="UnicoID">`. 

El error exacto que arroja el validador (como el de Red Hat) es:
`cvc-identity-constraint.4.1: Duplicate unique value [srv-web-01] declared for identity constraint "UnicoID" of element "catalogo_cloud".`

Esto garantiza a nivel de esquema que no haya colisiones de identificadores en toda la infraestructura de TechNova Cloud.
