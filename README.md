**INFORME EVALUACIÓN N° 1**

Sistema de Gestión Almacén Lukas

_Análisis, Levantamiento de Requisitos y Planificación_

**Asignatura:** Sistemas de Información

**Profesor:** Jorge Esteban Cornejo Elgueta

**Equipo de Desarrollo:**

_Cristian Salazar_

_Lukas Caballero_

_Felipe Oria_

_Benjamín Acuña_

_Simón Aros_

**Cliente / Empresa:** Almacén Lukas — Sr. Claudio Caballero

**Fecha de Entrega:** Abril 2026

# Índice de Contenidos

1\. Introducción .............................................................................................................

2\. Objetivo .............................................................................................................

2.1 Objetivos específicos .............................................................................................................

3\. Descripción general de la empresa ................................................................................................

4\. Descripción general del problema .............................................................................................

4.1 diagrama BPMN ...........................................................................

5\. Requisitos del Sistema ...................................................................................................

5.1 Requisitos Funcionales ...............................................................................................

5.2 Requisitos No Funcionales ............................................................................................

6\. Análisis ................................................................................

7\. Conclusiones .............................................................................................................

8\. Referencias ..............................................................................................................

# 1\. Introducción

El presente informe tiene como propósito documentar las fases iniciales del desarrollo de un sistema de gestión para el Almacén Lukas, negocio de comercio minorista ubicado en la comuna de Lo Prado, Santiago de Chile.

El proceso de desarrollo sigue los lineamientos del Ciclo de Vida de Desarrollo de Software (CVDS) y aplica los principios de la Ingeniería de Requisitos tal como los define Sommerville (2011), quien sostiene que los requisitos son la base sobre la cual se construye todo sistema de software exitoso. En ese sentido, el análisis de requisitos no es un proceso aislado, sino un esfuerzo continuo de comprensión, validación y negociación con los stakeholders del sistema.

El equipo de desarrollo llevó a cabo un proceso de elicitación de requisitos mediante entrevistas estructuradas con el Sr. Claudio Caballero, propietario del Almacén Lukas, con el objetivo de comprender en profundidad la problemática operativa del negocio, sus procesos actuales y las expectativas sobre la solución tecnológica a implementar.

El informe se organiza en las siguientes secciones: descripción del problema (situaciones AS-IS y TO-BE), levantamiento y clasificación de requisitos, y finalmente el análisis técnico-económico de las herramientas seleccionadas para el desarrollo.

# 2\. Objetivo

El objetivo de este proyecto es desarrollar e implementar un sistema informático de gestión de morosos para el almacén Lukas en un plazo de un semestre académico, con el fin de reducir el tiempo dedicado al registro y cobro de los pedidos fiados en al menos un 80%.

# 2.1. Objetivos específicos

- Identificar los procesos actuales de gestión de crédito y los puntos críticos de pérdida de información mediante entrevistas de licitación con el cliente.

- ​Modelar el flujo de procesos utilizando la notación BPMN para estandarizar el registro y cobro de deudas.

- Estructurar una matriz de requisitos funcionales y no funcionales que garantice la seguridad, portabilidad y usabilidad del sistema en dispositivos móviles.

- ​Desarrollar el sistema de gestión utilizando el stack tecnológico propuesto integrando los módulos de clientes, créditos y pagos.

- Validar el funcionamiento del sistema y la precisión de los datos mediante pruebas de usuario y capacitación _in situ_ al propietario del almacén.

# 3\. Descripción general de la empresa

El Almacén Lukas es un negocio familiar de comercio minorista fundado en el año 2015, ubicado en calle Chicago 121, Lo Prado, Región Metropolitana. Su propietario, el Sr. Claudio Caballero, comercializa abarrotes y productos de limpieza para el hogar, atendiendo principalmente a la comunidad vecinal del sector.

## 4 descripción general del problema

Entre los servicios que el almacén ofrece destaca el crédito vecinal, modalidad de venta fiada a clientes de confianza que constituye un diferenciador clave frente a minimarkets y otros establecimientos competidores de la zona. Sin embargo, este servicio opera de manera completamente manual, el propietario los mantiene anotados en una agenda y hay veces en las que ocupa la memoria lo que genera una serie de problemas críticos para la gestión del negocio.

El registro de todas las deudas del crédito vecinal se realiza mediante hojas de notas y apuntes personales del propietario. No existe ningún sistema digital de gestión de clientes ni de deudas.

La siguiente tabla sintetiza los problemas identificados durante el proceso de levantamiento de información con el cliente:

| **#** | **Problema identificado** | **Impacto en el negocio** |
| --- | --- | --- |
| 1   | **Desorganización en el registro de deudas** | El propietario no sabe con exactitud quién debe ni cuánto debe en un momento dado, lo que provoca pérdidas económicas por deudas olvidadas. |
| --- | --- | --- |
| 2   | **Pérdida de información de clientes** | Las hojas de notas físicas se deterioran, extravían o dañan con facilidad, causando pérdida irreversible de registros de crédito. |
| --- | --- | --- |
| 3   | **Proceso manual y lento de cobro mensual** | Al cierre de cada mes, el propietario invierte varias horas revisando apuntes para identificar morosos, tiempo que podría dedicar a la operación del negocio. |
| --- | --- | --- |
| 4   | **Sin visibilidad del estado de cuenta por cliente** | Imposibilidad de conocer rápidamente el saldo total adeudado por un cliente específico sin revisar múltiples registros. |
| --- | --- | --- |

El flujo actual del proceso de crédito vecinal puede describirse de la siguiente manera: cuando un cliente solicita productos a crédito, el propietario anota manualmente en una libreta o hoja suelta el nombre del cliente, los productos entregados y el monto adeudado. No existe un proceso estandarizado de registro. Al cierre de cada mes, el propietario debe revisar manualmente todos estos apuntes para identificar a los clientes con deuda pendiente y contactarlos directamente por WhatsApp para realizar el cobro.

El propio cliente describió esta situación con las siguientes palabras durante la entrevista: "Al llegar fin de mes, se debe revisar entre todas las hojas de notas y apuntes y encontrar a los clientes que no han pagado para ir a cobrar directo por WhatsApp". Este proceso manual consume un tiempo considerable que podría destinarse a la operación directa del negocio.

## 4.1 diagrama BPMN

Utilizando lo anteriormente descrito y habiéndonos basado en la problemática presentada, podemos representar el flujo de procesos de las siguiente forma:

# 5\. Requisitos del Sistema

De acuerdo con Sommerville (2011), un requisito es una condición o capacidad que debe cumplir un sistema para satisfacer una necesidad del usuario o del negocio. Los requisitos se clasifican en funcionales, que describen qué debe hacer el sistema, y no funcionales, que establecen restricciones sobre cómo debe operar.

Los requisitos presentados a continuación fueron obtenidos mediante el proceso de elicitación de requisitos llevado a cabo en reuniones con el cliente. Estos fueron ordenados según prioridad de desarrollo, desde las funcionalidades esenciales hasta las características de calidad del sistema. El listado completo con criterios de aceptación detallados se encuentra en el documento Listado de Requisitos Iniciales (formato Excel) entregado junto a este informe.

## 5.1 Requisitos Funcionales

Los requisitos funcionales describen las funciones específicas que el sistema debe ser capaz de ejecutar. Se presentan ordenados según la secuencia lógica de implementación:

| **R.N°** | **Nombre** | **Tipo** | **Actor** | **Descripción** | **Estado** |
| --- | --- | --- | --- | --- | --- |
| R.1 | **Registrar Cliente** | Funcional | Propietario | El sistema permite registrar clientes con nombre, RUT, teléfono y dirección. | Aprobado |
| --- | --- | --- | --- | --- | --- |
| R.2 | **Gestionar Crédito Vecinal** | Funcional | Propietario | Registro de ventas a crédito con monto, productos y fecha; actualización automática del saldo. | Aprobado |
| --- | --- | --- | --- | --- | --- |
| R.3 | **Registrar Pago de Deuda** | Funcional | Propietario | Permite ingresar abonos parciales o totales, actualizando el saldo y el historial. | Aprobado |
| --- | --- | --- | --- | --- | --- |
| R.4 | **Listar Clientes Morosos** | Funcional | Propietario | Genera listado actualizado de clientes con deuda mayor a $0, con saldo y último pago. | Aprobado |
| --- | --- | --- | --- | --- | --- |

Los requisitos funcionales se han ordenado priorizando aquellos que constituyen el núcleo del sistema: la gestión de clientes (R.1) es prerrequisito de la gestión de crédito (R.2), la que a su vez habilita el registro de pagos (R.3). A partir de estos tres módulos base se construyen las funcionalidades de consulta y comunicación (R.4 y R.5).

## 5.2 Requisitos No Funcionales

Los requisitos no funcionales establecen las restricciones y atributos de calidad que debe cumplir el sistema. Siguiendo la clasificación de Sommerville (2011), se identificaron requisitos en las categorías de seguridad, rendimiento, usabilidad, confiabilidad y portabilidad:

| **RFN.N°** | **Nombre** | **Categoría** | **Descripción** |
| --- | --- | --- | --- |
| RNF.1 | **Autenticación** | Seguridad | Acceso mediante usuario/contraseña; contraseña encriptada; bloqueo tras 3 intentos fallidos. |
| --- | --- | --- | --- |
| RNF.2 | **Tiempo de respuesta** | Rendimiento | Consultas < 2 s; carga inicial < 5 s; listado de morosos < 3 s. |
| --- | --- | --- | --- |
| RNF.3 | **Interfaz responsiva (móvil)** | Usabilidad | Sistema operable desde smartphone; navegación táctil funcional. |
| --- | --- | --- | --- |
| RNf.4 | **Respaldo de datos** | Confiabilidad | Exportación manual de respaldo (CSV/JSON) con fecha y hora visible. |
| --- | --- | --- | --- |
| RNF.5 | **Portabilidad** | Portabilidad | Sistema accesible desde navegador web estándar sin instalación de software adicional. |
| --- | --- | --- | --- |

## 6\. Análisis

Siguiendo los principios del análisis estructurado, el estudio del Sistema de Gestión Almacén Lukas se divide en la comprensión de su esencia lógica y su posterior adaptación a las restricciones tecnológicas del entorno.

**6.1 El Modelo Esencial**

El objetivo de esta fase es capturar las políticas de negocio ignorando las limitaciones tecnológicas actuales. Para el Almacén Lukas, la esencia del sistema radica en la necesidad de gestionar el crédito vecinal de manera precisa. El sistema debe eliminar por completo la dependencia de la memoria del propietario y de los registros físicos en agendas. Su comportamiento requerido es registrar la deuda en el instante en que el cliente solicita productos a crédito y mantener un cálculo exacto del saldo adeudado para evitar pérdidas económicas por desorganización.

**6.2 Herramientas de Modelado**

El análisis del sistema se fundamenta en los instrumentos de levantamiento y modelado desarrollados durante las entrevistas, los cuales permiten estructurar la solución tecnológica en torno a las necesidades operativas reales del almacén.

Análisis del Flujo de Procesos (BPMN): El diagrama BPMN evidencia que el modelo operativo actual ("AS-IS") es lineal y altamente dependiente de la intervención manual del propietario. El flujo crítico de la problemática se concentra en la etapa de "Cierre de mes", donde la bifurcación lógica (¿Cliente con deudas pendientes?) obliga a una revisión física de múltiples libretas. Esta revisión es el principal cuello de botella que impide la escalabilidad del servicio de crédito vecinal. El diagrama también establece la frontera del sistema: la etapa de "Cobro" (contactar por WhatsApp) es una acción externa que el propietario mantendrá, por lo que el sistema no necesita automatizar la mensajería, sino proveer la información exacta para ejecutarla.

**Trazabilidad entre Problemas y Requisitos Funcionales:**

A partir de la tabla de problemas identificados, la arquitectura de requisitos funcionales se diseñó como una respuesta directa para mitigar los impactos negativos en el negocio:

La pérdida de información de clientes y la desorganización en el registro (Problemas 1 y 2) se resuelven mediante la implementación de los módulos R.1 (Registrar Cliente) y R.2 (Gestionar Crédito Vecinal), los cuales centralizan los datos y reemplazan la dependencia de los registros físicos.

El proceso manual y lento de cobro y la falta de visibilidad del estado de cuenta (Problemas 3 y 4) son abordados directamente por los requisitos R.3 (Registrar Pago de Deuda) y R.4 (Listar Clientes Morosos), los cuales calculan los saldos en tiempo real y eliminan las horas invertidas en la revisión manual a fin de mes.

**Restricciones de Calidad según el Contexto de Uso:**

Las tablas de requisitos no funcionales reflejan las condiciones del entorno del minimarket. Dado que el punto de venta es dinámico, el sistema exige una Interfaz responsiva móvil (RNF.3) para ser operado desde un smartphone, junto con un Tiempo de respuesta rápido (RNF.2) (consultas menores a 2 segundos) para no entorpecer la atención presencial de otros clientes en el local. Además, para proteger la integridad de los datos frente a las antiguas pérdidas de libretas, se establecen medidas de Autenticación (RNF.1) y Respaldo de datos (RNF.4).

**6.3 El Modelo de Implantación del Usuario**

Una vez definida la lógica, el modelo esencial se adapta para incorporar la realidad física y tecnológica del minimarket:

Frontera de Automatización: El sistema se encargará del registro, cálculo y generación de listados (reduciendo el tiempo de revisión manual), pero la acción de contactar al cliente para el cobro vía WhatsApp quedará fuera de la automatización, manteniéndose como una labor manual del propietario.

Restricciones de la Tecnología Real: El sistema físico se implementará bajo estrictos atributos de calidad. Debe poseer una interfaz responsiva con navegación táctil, ya que el propietario interactuará con el sistema operándolo desde un smartphone.

Seguridad y Mantenibilidad: Para mitigar la vulnerabilidad de las libretas de papel frente a extravíos o daños, la implantación requiere autenticación mediante usuario y contraseña, además de una función que permita exportar manualmente los datos en formatos estándar para asegurar la confiabilidad de la información. Todo esto se ejecutará en un navegador estandarizado para garantizar la portabilidad sin instalaciones adicionales.

## 7\. Conclusiones

El presente informe documenta la fase de análisis y levantamiento de requisitos del Sistema de Gestión Almacén Lukas, primera etapa formal del ciclo de vida de desarrollo del software. A través del proceso de elicitación de requisitos, el equipo pudo identificar con claridad el problema central del negocio: la gestión manual del crédito vecinal mediante hojas de notas, que genera desorganización, pérdida de información y una inversión desproporcionada de tiempo en el proceso de cobro mensual.

Se levantaron 9 requisitos (4 funcionales y 5 no funcionales) que cubren de manera integral las necesidades expresadas por el cliente. Estos requisitos fueron ordenados según su prioridad de desarrollo, estableciendo como núcleo del sistema los módulos de gestión de clientes, crédito vecinal y pagos, sobre los cuales se construyen las funcionalidades de consulta y comunicación.

El análisis de sistemas realizado permitió traducir la problemática del registro manual en una arquitectura lógica eficiente, asegurando que cada requisito funcional mitigue un punto crítico identificado en el flujo BPMN. Este proceso garantiza que la solución propuesta no solo sea viable técnicamente, sino que responda con precisión a la necesidad de optimizar los tiempos de cobro y asegurar la integridad de la información del negocio.

En síntesis, el proyecto cuenta con una base sólida de análisis para avanzar hacia las fases de diseño de interfaces, desarrollo e integración que se documentarán en las evaluaciones subsiguientes del semestre.

# 8\. Referencias

Las siguientes referencias han sido utilizadas para fundamentar el marco teórico y metodológico del presente informe, siguiendo las normas de citación APA (7ª edición).

Sommerville, I. (2011). _Ingeniería del software_ (9.ª ed.). Pearson Educación.

Pressman, R. S. (2010). _Ingeniería del software: Un enfoque práctico_ (7.ª ed.). McGraw-Hill.

Brooks, F. P. (1987). No silver bullet: Essence and accidents of software engineering. _IEEE Computer, 20_(4), 10–19. https://doi.org/10.1109/MC.1987.1663532

IEEE/ANSI 830-1998. (1998). _IEEE Recommended Practice for Software Requirements Specifications_. Institute of Electrical and Electronics Engineers.

Caballero, C. (2026, abril). _\[Entrevistas de levantamiento de requisitos\]_. Almacén Lukas, Lo Prado, Santiago.

_Documento elaborado con fines académicos — Asignatura: Sistemas de Información — Abril 2026_