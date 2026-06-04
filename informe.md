# INFORME EVALUACIÓN N°2
## Sistema de Gestión Almacén Lukas
### Propuesta de Solución, Factibilidad, Diseño y Prototipo

**Asignatura:** Sistemas de Información  
**Profesor:** Jorge Esteban Cornejo Elgueta  
**Equipo:** Cristian Salazar, Lukas Caballero, Felipe Oria, Benjamín Acuña, Simón Aros  
**Cliente:** Almacén Lukas — Sr. Claudio Caballero  
**Fecha:** Junio 2026

---

## Índice de Contenidos

1. Introducción
2. Historias de Usuario
3. Propuesta de Solución
   3.1 Descripción General
   3.2 Procesos del Sistema
      - Proceso AS-IS (Estado Actual)
      - Proceso TO-BE (Estado Propuesto con el Sistema)
   3.3 Funcionalidades Principales
   3.4 Aspectos Técnicos
4. Estudios de Factibilidad
   4.1 Factibilidad Económica
   4.2 Factibilidad Legal
   4.4 Factibilidad Operacional
5. Análisis Costo / Beneficio
   5.1 Costos del Proyecto
   5.2 Beneficios Estimados
   5.3 Proyección de Retorno de Inversión (ROI)
6. Diagrama de Jerarquía Modular
7. Diagramas de Casos de Uso
8. Diagramas de Clases
   - Diccionario
9. Prototipo
   9.1 Pantallas del prototipo
10. Conclusiones
11. Referencias

---

## 1. Introducción

El presente documento constituye la segunda entrega formal del proyecto de desarrollo del Sistema de Gestión Almacén Lukas, correspondiente a la asignatura de Sistemas de Información. Sobre la base del trabajo realizado en la Evaluación N°1, que abarcó el levantamiento y análisis de requisitos, la descripción del problema y la modelación, este informe avanza hacia las etapas de diseño, planificación y validación de la solución.

Como se documentó en la entrega anterior, el Almacén Lukas, pequeño comercio minorista ubicado en la comuna de Lo Prado, Santiago, enfrenta una problemática operativa crítica: la gestión del crédito vecinal —servicio de venta fiada a clientes de confianza— se realiza de forma completamente manual mediante libretas físicas y anotaciones en papel. Esta situación provoca desorganización en el registro de deudas, pérdida de información, y un proceso de cobro mensual lento e ineficiente que el propietario, Sr. Claudio Caballero, debe ejecutar manualmente cada fin de mes.

Este informe se estructura en torno a los siguientes ejes: la propuesta de solución tecnológica, que define el sistema a construir en términos de procesos, funcionalidades y aspectos técnicos; el estudio de factibilidad en sus dimensiones técnica, económica, legal y operacional; el análisis costo-beneficio con proyección del retorno de inversión; el diagrama de jerarquía modular que organiza los módulos del sistema; las historias de usuario y los diagramas UML (a insertar posteriormente por el equipo); y finalmente el prototipo de interfaz del sistema, acompañado de las conclusiones del informe.

El desarrollo del sistema sigue los lineamientos del Ciclo de Vida de Desarrollo de Software (CVDS), integrando los principios de Sommerville (2011) y Pressman (2010) para garantizar que la solución propuesta sea técnicamente sólida, económicamente viable y operacionalmente adoptable por el cliente. El equipo de desarrollo ha mantenido comunicación continua con el Sr. Claudio Caballero para validar los avances y asegurar la alineación entre las necesidades del negocio y las decisiones de diseño.

---

## 2. Historias de Usuario

Las Historias de Usuario (User Stories) son descripciones breves y centradas en el usuario que capturan las funcionalidades requeridas del sistema desde la perspectiva del actor que las utiliza. Siguiendo la metodología ágil, cada historia se expresa bajo la sintaxis estándar: "Yo como [rol], necesito [funcionalidad], para [beneficio]", acompañada de sus criterios de aceptación que definen las condiciones de cumplimiento.

Las historias de usuario se derivan directamente de los requisitos funcionales (R.1 a R.4) levantados en la Evaluación N°1 y se organizan a partir de una historia épica (UH0) que encapsula la necesidad global del negocio.

### UH1: Registrar Cliente — Correspondiente a R.1

| | |
|---|---|
| **Yo como** | Propietario |
| **Necesito** | Registrar a los clientes en el sistema indicando su nombre, RUT, teléfono y dirección |
| **Para** | Mantener la información organizada y evitar la pérdida de datos que ocurría al usar hojas de notas físicas |
| **Criterio de aceptación** | El sistema debe permitir realizar todas las funcionalidades CRUD (Crear, Leer, Actualizar y Eliminar) sobre el registro de cada cliente. |

### UH2: Gestionar Crédito Vecinal — Correspondiente a R.2

| | |
|---|---|
| **Yo como** | Propietario |
| **Necesito** | Registrar las ventas a crédito guardando el monto, los productos entregados y la fecha |
| **Para** | Eliminar la dependencia de la memoria y asegurar que todas las deudas queden correctamente anotadas en el momento de la solicitud |
| **Criterio de aceptación** | El sistema debe realizar la actualización automática del saldo del cliente de forma inmediata tras registrar el nuevo crédito. |

### UH3: Registrar Pago de Deuda — Correspondiente a R.3

| | |
|---|---|
| **Yo como** | Propietario |
| **Necesito** | Ingresar los abonos parciales o totales que realizan los clientes |
| **Para** | Descontar los pagos de la deuda total y mantener el estado de cuenta siempre al día |
| **Criterio de aceptación** | Al ingresar el pago, el sistema debe actualizar el saldo de la deuda y mantener el registro en el historial del cliente. |

### UH4: Listar Clientes Morosos — Correspondiente a R.4

| | |
|---|---|
| **Yo como** | Propietario |
| **Necesito** | Generar un listado actualizado de los clientes que tengan una deuda mayor a $0, incluyendo su saldo y la fecha de su último pago |
| **Para** | Identificar rápidamente a quién debo contactar a fin de mes para realizar el cobro, sin tener que revisar libretas manualmente |
| **Criterio de aceptación** | El sistema debe generar este listado con un tiempo de respuesta lo suficientemente bajo para no entorpecer la atención en el local. |

---

## 3. Propuesta de Solución

A partir de los problemas identificados y los requisitos levantados en la primera etapa del proyecto, el equipo de desarrollo propone la construcción e implementación de un sistema informático de escritorio para la gestión del crédito vecinal del Almacén Lukas. La propuesta responde de manera directa a las cuatro problemáticas críticas documentadas: desorganización en el registro de deudas, pérdida de información de clientes, proceso manual y lento de cobro mensual, y falta de visibilidad del estado de cuenta por parte del propietario.

### 3.1 Descripción General

La solución consiste en el desarrollo de una aplicación de escritorio (desktop) instalable directamente en el computador principal del almacén, que permita al propietario gestionar de forma centralizada y digital todos los aspectos del crédito vecinal. La aplicación operará de manera completamente offline (On-Premise), sin dependencia de conexión a internet, lo que garantiza disponibilidad permanente y control total de la información sensible del negocio.

El sistema recibirá el nombre de "SGC-Lukas" (Sistema de Gestión de Crédito), y constituirá el reemplazo completo del sistema manual actual basado en libretas y anotaciones. La aplicación integrará los módulos de gestión de clientes, registro de ventas a crédito, control de pagos, generación de reportes y seguridad de acceso, todos interconectados sobre una base de datos local.

### 3.2 Procesos del Sistema

El rediseño del proceso de crédito vecinal transita desde el modelo AS-IS (estado actual) hacia el modelo TO-BE (estado propuesto) de la siguiente manera:

#### Proceso AS-IS (Estado Actual)

El proceso actual es completamente manual y altamente dependiente de la intervención del propietario en cada etapa. Cuando un cliente solicita productos a crédito, el Sr. Caballero anota en una libreta o hoja suelta el nombre, los productos entregados y el monto. No existe estandarización del registro. Al cierre de cada mes, el propietario revisa manualmente todos los apuntes acumulados para identificar deudas pendientes y contacta a cada cliente directamente por WhatsApp para realizar el cobro. Este proceso consume entre 4 y 8 horas mensuales y está sujeto a errores, olvidos y pérdida de información.

#### Proceso TO-BE (Estado Propuesto con el Sistema)

Con la implementación del SGC-Lukas, el flujo del proceso se transforma radicalmente:

1. **Registro del cliente:** Al incorporar un nuevo cliente al sistema de crédito, el propietario registra sus datos básicos (nombre, RUT, teléfono, dirección) en la aplicación en menos de 60 segundos.
2. **Registro de venta a crédito:** Cuando un cliente solicita productos fiados, el propietario ingresa la transacción en la aplicación indicando el monto y la descripción. El sistema actualiza automáticamente el saldo adeudado del cliente.
3. **Registro de pago o abono:** Cuando un cliente realiza un pago total o parcial, el propietario lo registra en la aplicación, actualizando el saldo en tiempo real e historial de pagos.
4. **Consulta de estado de cuenta:** En cualquier momento, el propietario puede consultar el saldo de un cliente específico con un solo clic, eliminando la búsqueda manual en libretas.
5. **Generación del listado de morosos:** Al cierre de mes, el sistema genera automáticamente un listado actualizado de todos los clientes con deuda pendiente, incluyendo saldo total y fecha del último pago. El propietario solo debe revisar este listado para proceder a los cobros vía WhatsApp.

### 3.3 Funcionalidades Principales

Las funcionalidades del sistema se organizan en cuatro módulos principales, alineados con los requisitos funcionales aprobados en la Evaluación N°1:

| Módulo | Funcionalidad | Descripción |
|--------|---------------|-------------|
| Módulo Clientes | Registrar Cliente (R.1) | Alta, modificación, consulta y baja de clientes con datos completos (nombre, RUT, teléfono, dirección). |
| Módulo Crédito | Gestionar Crédito Vecinal (R.2) | Registro de ventas a crédito con monto, descripción, fecha y actualización automática del saldo acumulado. |
| Módulo Pagos | Registrar Pago de Deuda (R.3) | Ingreso de abonos parciales o totales, con actualización del saldo y generación automática de historial de pagos. |
| Módulo Reportes | Listar Clientes Morosos (R.4) | Generación del listado actualizado de clientes con deuda mayor a $0, incluyendo saldo total y fecha del último pago. |

### 3.4 Aspectos Técnicos

La solución técnica ha sido diseñada considerando las restricciones del entorno del cliente (computador de escritorio, operación offline, bajo presupuesto) y las competencias del equipo de desarrollo. El stack tecnológico seleccionado es el siguiente:

| Componente | Tecnología | Justificación |
|------------|------------|---------------|
| Lenguaje de programación | Python 3.12 | Lenguaje de alta productividad, open source, con amplia comunidad y soporte. Dominio del equipo. |
| Interfaz gráfica (GUI) | CustomTkinter / Tkinter | Framework de interfaz de escritorio nativo para Python. No requiere instalación de dependencias externas adicionales. |
| Base de datos | SQLite 3 | Motor de base de datos local embebido en Python. No requiere servidor ni configuración de red. Ideal para aplicaciones de escritorio monousuario. |
| ORM / Acceso a datos | sqlite3 (stdlib) | Módulo nativo de Python para interacción con SQLite. Sin dependencias externas. |
| Empaquetado | PyInstaller | Genera un ejecutable (.exe) independiente para Windows, sin necesidad de que el cliente tenga Python instalado. |
| Control de versiones | Git / GitHub | Versionado del código fuente y colaboración del equipo de desarrollo. |
| Sistema operativo target | Windows 10/11 | Sistema operativo del equipo del cliente. Compatibilidad confirmada con Python y CustomTkinter. |

La arquitectura de la aplicación sigue el patrón MVC (Modelo-Vista-Controlador), separando la lógica de negocio (modelos de datos), la interfaz gráfica (vistas) y la lógica de control (controladores). Esto facilita el mantenimiento, las pruebas y la incorporación de nuevas funcionalidades en versiones futuras del sistema.

La base de datos SQLite se almacenará en el directorio de la aplicación, en un archivo `.db` protegido. Se implementará una función de exportación manual a formato CSV para que el propietario pueda realizar respaldos periódicos en una memoria USB u otro dispositivo externo, cumpliendo con el requisito no funcional RNF.2.

---

## 4. Estudios de Factibilidad

El estudio de factibilidad tiene como propósito evaluar si el proyecto es viable desde distintas perspectivas antes de comprometer recursos en su desarrollo. De acuerdo con Pressman (2010), un estudio de factibilidad completo debe contemplar al menos las dimensiones técnica, económica, legal y operacional.

### 4.1 Factibilidad Económica

La factibilidad económica determina si el cliente cuenta con los recursos financieros disponibles y si los beneficios obtenidos justifican la inversión realizada.

En términos de costos directos de software y herramientas, los costos son nulos (todas las tecnologías son open source). El costo real del proyecto se expresa en horas de trabajo del equipo de desarrollo, valoradas a la tarifa de mercado de un desarrollador junior en Chile.

#### Estimación de costos de desarrollo

| Ítem | Horas estimadas | Tarifa (CLP/hr) | Costo estimado (CLP) |
|------|-----------------|-----------------|----------------------|
| Análisis y diseño del sistema | 30 hrs | $6.000 | $180.000 |
| Desarrollo del módulo Clientes | 20 hrs | $6.000 | $120.000 |
| Desarrollo del módulo Crédito y Pagos | 30 hrs | $6.000 | $180.000 |
| Desarrollo del módulo Reportes | 15 hrs | $6.000 | $90.000 |
| Desarrollo del módulo Seguridad (auth) | 10 hrs | $6.000 | $60.000 |
| Diseño de interfaz gráfica (GUI) | 20 hrs | $6.000 | $120.000 |
| Pruebas, corrección de errores y QA | 20 hrs | $6.000 | $120.000 |
| Documentación y entrega | 15 hrs | $6.000 | $90.000 |
| Licencias de software | — | — | $0 (open source) |
| Hardware adicional | — | — | $0 (equipo existente) |
| **TOTAL ESTIMADO** | **160 hrs** | — | **$960.000** |

### 4.2 Factibilidad Legal

La factibilidad legal evalúa si el proyecto está sujeto a restricciones normativas que puedan impedir o condicionar el proyecto.

#### Protección de datos personales

El sistema almacenará datos personales de los clientes del almacén (nombre, RUT, teléfono, dirección), lo cual está regulado en Chile por la Ley N°19.628 sobre Protección de la Vida Privada y por las modificaciones introducidas mediante la Ley N°21.719 (2024) que moderniza la legislación de protección de datos personales en el país. Para dar cumplimiento a esta normativa, el sistema contempla las siguientes medidas:

- Almacenamiento de datos en base de datos local (no en la nube), minimizando la exposición a terceros.
- Acceso restringido mediante autenticación con usuario y contraseña.
- Los datos serán utilizados exclusivamente para la gestión interna del crédito vecinal del almacén, con consentimiento implícito en la relación comercial preexistente entre el propietario y sus clientes.
- No se compartirá información personal con terceros ni se realizará tratamiento de datos con fines distintos a la gestión del crédito vecinal.

#### Licencias de software

Todas las tecnologías utilizadas en el desarrollo del sistema (Python, SQLite, CustomTkinter, PyInstaller, Git) poseen licencias de código abierto (PSF License, dominio público, MIT License, GPL) que permiten su uso, modificación y distribución sin restricciones para proyectos de naturaleza académica y comercial de pequeña escala. No existe ningún conflicto legal en el uso de estas herramientas para el proyecto propuesto.

#### Regulaciones comerciales

El Almacén Lukas opera como negocio de comercio minorista bajo la normativa del SII (Servicio de Impuestos Internos) chileno. El sistema propuesto es una herramienta de gestión interna y no sustituye ni reemplaza los instrumentos tributarios legalmente exigidos (boletas, facturas). No existe ninguna regulación comercial o tributaria que prohíba ni restrinja el uso de un sistema de gestión de crédito interno para negocios de esta naturaleza.

### 4.4 Factibilidad Operacional

La factibilidad operacional evalúa si el sistema, una vez desarrollado, será efectivamente utilizado y aceptado por los usuarios finales en el entorno real de trabajo.

#### Perfil del usuario final

El usuario principal del sistema es el Sr. Claudio Caballero, propietario del Almacén Lukas, adulto de mediana edad con experiencia básica-intermedia en el uso de computadores (navegación web, manejo de WhatsApp, uso de teclado y mouse). El propietario ha manifestado disposición y motivación para adoptar una solución digital que reemplace el proceso manual actual, tal como lo expresó durante las entrevistas de levantamiento de requisitos.

#### Facilidad de uso

El diseño de la interfaz del sistema prioriza la simplicidad y eficiencia operativa por sobre la complejidad funcional. Cada tarea principal (registrar crédito, registrar pago, consultar estado de cuenta, generar listado de morosos) se puede ejecutar en no más de 3 pasos desde la pantalla principal. El sistema dispone de mensajes de confirmación y alerta claros para guiar al usuario en caso de error de ingreso.

#### Capacitación requerida

Se estima que el propietario requerirá una sesión de capacitación de 1 a 2 horas para dominar las funciones principales del sistema. El equipo de desarrollo entregará un manual de usuario impreso y en formato PDF, con instrucciones ilustradas para cada módulo. El sistema está diseñado para ser operado de manera autónoma sin necesidad de soporte técnico externo en el uso diario.

#### Impacto en la operación del negocio

La implementación del sistema no interrumpirá la operación diaria del almacén. La transición desde el sistema manual al digital puede realizarse de forma gradual: el propietario puede comenzar registrando solo los nuevos clientes y créditos en la aplicación mientras mantiene temporalmente el registro paralelo en libreta. A medida que gana confianza en el sistema, el registro manual puede abandonarse progresivamente.

---

## 5. Análisis Costo / Beneficio

El análisis costo-beneficio tiene como objetivo determinar si los beneficios esperados del sistema justifican económicamente la inversión requerida para su desarrollo e implementación. Siguiendo la metodología de Pressman (2010), se identifican y cuantifican los costos del proyecto, se estiman los beneficios tangibles e intangibles, y se proyecta el retorno de la inversión (ROI) a un horizonte de 3 años.

### 5.1 Costos del Proyecto

#### Costos de desarrollo (únicos)

El costo base de desarrollo es de $960.000, correspondiente a 160 horas de trabajo del equipo valoradas a CLP $6.000/hora (tarifa de mercado de desarrollador junior en Chile). A este costo se agrega una estimación de imprevistos del 10%, resultando en:

| Concepto | Monto (CLP) |
|----------|-------------|
| Costo de desarrollo (160 hrs) | $960.000 |
| Imprevistos (10%) | $96.000 |
| Licencias de software | $0 |
| **TOTAL COSTO DE DESARROLLO** | **$1.056.000** |

### 5.2 Beneficios Estimados

#### Beneficio 1: Ahorro de tiempo en gestión mensual de cobranzas

Actualmente, el propietario dedica entre 4 y 8 horas mensuales a revisar libretas para identificar clientes morosos y preparar los cobros de fin de mes. Con el sistema, este proceso se reduce a menos de 30 minutos (consulta del listado de morosos y exportación de datos). Estimando un ahorro mínimo de 6 horas mensuales, y valorando el tiempo del propietario a un costo de oportunidad de CLP $3.500/hora (equivalente a la remuneración promedio por hora de un trabajador de comercio minorista en Chile según datos del INE 2025):

- Ahorro anual por tiempo de gestión: **$252.000 CLP**

#### Beneficio 2: Reducción de pérdidas por créditos no cobrados

La desorganización del sistema manual genera periódicamente deudas olvidadas o registradas incorrectamente. Durante la entrevista de levantamiento de requisitos, el propietario reconoció pérdidas mensuales estimadas en el rango de CLP $15.000 a $40.000 por deudas no recuperadas a causa de la desorganización. Tomando el valor conservador mínimo:

- Recuperación adicional mensual estimada: $15.000 CLP
- Beneficio anual por reducción de pérdidas: **$180.000 CLP**

#### Beneficio 3: Reducción de costos en materiales físicos

El almacén utiliza actualmente libretas, hojas sueltas y materiales de escritura para el registro de créditos, con un costo estimado de CLP $2.500 mensuales.

- Ahorro anual en materiales: **$30.000 CLP**

#### Beneficio 4: Beneficios intangibles

Adicionalmente, se identifican beneficios intangibles de alto valor para el negocio:

- Mayor confianza y satisfacción de los clientes al contar con información precisa de su saldo.
- Imagen de mayor profesionalismo y modernización del negocio.
- Reducción del estrés operativo del propietario y mejora en la calidad de vida laboral.
- Base de datos de clientes que permite identificar patrones de comportamiento de compra.

#### Resumen de beneficios cuantificables anuales

| Fuente de beneficio | Monto anual (CLP) |
|---------------------|------------------|
| Ahorro de tiempo en gestión (6 hrs/mes) | $252.000 |
| Reducción de créditos no cobrados | $180.000 |
| Ahorro en materiales físicos | $30.000 |
| **TOTAL BENEFICIO ANUAL CUANTIFICABLE** | **$462.000** |

### 5.3 Proyección de Retorno de Inversión (ROI)

La proyección del ROI se calcula sobre un horizonte de 3 años, considerando la inversión inicial de desarrollo (CLP $1.056.000), los costos operacionales anuales (CLP $48.000) y los beneficios cuantificables anuales (CLP $462.000).

| Período | Beneficios acumulados | Costos acumulados | ROI (%) |
|---------|----------------------|-------------------|---------|
| Año 0 (desarrollo) | $0 | $1.056.000 | -100% |
| Año 1 | $462.000 | $1.104.000 | -60,8% |
| Año 2 | $924.000 | $1.152.000 | -21,6% |
| Año 3 | $1.386.000 | $1.200.000 | +17,6% |

**Fórmula:**

```
ROI = (Beneficios Acumulados − Costos Acumulados) / Inversión Inicial × 100
```

El análisis indica que el sistema alcanza el punto de equilibrio (break-even) aproximadamente a los 2 años y 4 meses desde su implementación. A partir del año 3, el sistema genera un retorno positivo de CLP $186.000, lo que equivale a un ROI del +17,6% sobre la inversión total. Este horizonte de recuperación es consistente con el tamaño y la naturaleza del negocio.

Es importante destacar que los beneficios intangibles (mejora de imagen, reducción del estrés, fidelización de clientes) no han sido incluidos en el cálculo cuantitativo, por lo que el ROI real podría ser significativamente mayor. Adicionalmente, si el propietario decide ampliar el uso del sistema (registro de inventario, facturación simple), los beneficios se incrementarían sin un costo proporcional de desarrollo.

**Conclusión del análisis costo-beneficio:** El proyecto es económicamente justificable. Con una inversión equivalente de CLP $1.056.000 y un retorno positivo a partir del tercer año, el sistema representa una inversión rentable para el Almacén Lukas, con beneficios cuantificables desde el primer mes de operación.

---

## 6. Diagrama de Jerarquía Modular

El Diagrama de Jerarquía Modular (también denominado Diagrama de Estructura Modular o "Structure Chart") representa la descomposición funcional del sistema en módulos y submódulos, organizados según relaciones de jerarquía y dependencia. Este diagrama permite visualizar la arquitectura general del SGC-Lukas y la forma en que cada componente contribuye al cumplimiento de los requisitos del sistema.

El sistema se descompone en 5 módulos principales, cada uno con sus submódulos correspondientes:

> **Diagrama:** SGC-Lukas — Sistema de Gestión de Crédito Vecinal
> 
> 1. **Seguridad**
>    - 1.1 Login
>    - 1.2 Gestión sesión
>    - 1.3 Cambio contraseña
> 2. **Clientes**
>    - 2.1 Registrar cliente
>    - 2.2 Buscar/consultar cliente
>    - 2.3 Editar cliente
>    - 2.4 Eliminar cliente
> 3. **Crédito**
>    - 3.1 Registrar venta fiada
>    - 3.2 Actualizar saldo
>    - 3.3 Historial de crédito
> 4. **Pagos**
>    - 4.1 Registrar pago
>    - 4.2 Abono parcial
>    - 4.3 Historial de pagos
> 5. **Reportes**
>    - 5.1 Listado morosos
>    - 5.2 Estado de cuenta
>    - 5.3 Exportar CSV

El módulo de **Seguridad (1)** es transversal al sistema: toda operación requiere que el usuario haya iniciado sesión correctamente. Cumple con el requisito no funcional RNF.1.

El módulo de **Clientes (2)** implementa el requisito funcional R.1 y es prerrequisito para los módulos de Crédito y Pagos.

El módulo de **Crédito (3)** implementa R.2, registrando cada venta fiada y actualizando el saldo del cliente en la base de datos.

El módulo de **Pagos (4)** implementa R.3, permitiendo el registro de abonos y el seguimiento del historial de pagos por cliente.

Finalmente, el módulo de **Reportes (5)** implementa R.4 y permite al propietario obtener en segundos la información necesaria para gestionar el proceso de cobro mensual.

---

## 7. Diagramas de Casos de Uso

> **Diagrama de Casos de Uso:** Sistema de Gestión Almacén Lukas
> 
> **Actor:** Propietario
> 
> **Casos de uso principales:**
> - Registrar Cliente (CRUD)
> - Gestionar Crédito Vecinal
> - Registrar Pago de Deuda
> - Listar Clientes Morosos (Si requiere cobrar)
> - Exportar Respaldo de Datos
> 
> **Relaciones `<<include>>`:**
> - Registrar Cliente incluye: Validar RUT, Crear Perfil, Actualizar Datos, Autenticar Acceso (Login)
> - Gestionar Crédito Vecinal incluye: Autenticar Acceso (Login), Registrar Detalle Venta, Calcular Nuevo Saldo
> - Exportar Respaldo de Datos deriva en: Seleccionar Formato (CSV/JSON), Generar Archivo

El diseño se centra en un único actor que administra de forma centralizada la operación, dando cumplimiento a las historias de usuario definidas.

**Actor (Propietario):** Representa al usuario que interactúa directamente con el sistema para gestionar las operaciones diarias del negocio.

**Casos de Uso Principales y Relaciones:**

- **Registrar Cliente (CRUD):** Permite la gestión integral de los datos de los usuarios. Este caso de uso integra (`<<include>>`) procesos obligatorios para su funcionamiento: Validar RUT, Crear Perfil, Actualizar Datos y la necesidad de Autenticar Acceso (Login) para garantizar la seguridad.
- **Gestionar Crédito Vecinal:** Representa la acción de registrar ventas fiadas. Depende de inclusiones (`<<include>>`) fundamentales como Autenticar Acceso (Login), Registrar Detalle Venta y Calcular Nuevo Saldo, automatizando así el cálculo de la deuda.
- **Registrar Pago de Deuda:** Acción directa que permite ingresar los abonos realizados por los clientes para descontarlos de su saldo pendiente.
- **Listar Clientes Morosos:** Interacción de consulta que filtra a los clientes con deuda pendiente para gestionar su cobranza.
- **Exportar Respaldo de Datos:** Flujo orientado a la seguridad de la información, el cual deriva en las acciones de Seleccionar Formato (CSV/JSON) y finalmente Generar Archivo.

---

## 8. Diagramas de Clases

El diagrama de clases define el modelo de datos estático y las relaciones entre los componentes de la lógica de negocio del sistema propuesto. Se identifican cinco clases fundamentales que dan soporte a la arquitectura descrita:

> **Diagrama de Clases:**
> 
> - **SistemaGestor:** Actúa como controlador de los procesos generales. Contiene las operaciones `listarClientesMorosos()` y `exportarRespaldoDatos()`. Mantiene una relación donde **Administra** (1 a *) múltiples instancias de la clase Cliente y, a su vez, es validado (**Validated by**) por la clase Propietario.
> - **Propietario:** Clase encargada de la autenticación y seguridad del sistema. Protege la integridad del acceso mediante los atributos privados `usuario` (String) y `contrasenaEncriptada` (String), y expone el método público `autenticarAcceso()`.
> - **Cliente:** Entidad central del sistema que agrupa la información requerida por el negocio. Sus atributos privados son `nombre`, `rut`, `telefono`, `direccion` (tipo String) y `saldoDeuda` (tipo Float). Provee los métodos base para su gestión: `crear()`, `leer()`, `actualizar()` y `eliminar()`. Posee dependencias directas con el crédito y los pagos.
> - **CreditoVecinal:** Clase transaccional vinculada a Cliente mediante una relación donde el cliente **Posee** de 1 a * créditos. Almacena el detalle de la venta mediante los atributos `fecha` (Date), `descripcionProductos` (String) y `monto` (Float). Sus métodos operativos son `registrarCredito()` y `actualizarSaldoAutomatico()`.
> - **Pago:** Clase transaccional vinculada a Cliente mediante una relación donde el cliente **Realiza** de 1 a * pagos. Registra los abonos con los atributos `fecha` (Date) y `montoAbono` (Float). Se gestiona a través de los métodos `ingresarAbono()` y `actualizarHistorial()`.

### Diccionario

#### 1. Clase: SistemaGestor

Actúa como el controlador principal de los procesos generales del sistema, orquestando las acciones de alto nivel.

- **Atributos:** (No posee atributos definidos en el modelo actual).
- **Métodos:**
  - `+listarClientesMorosos()`: Filtra y retorna la lista de clientes que mantienen un saldo deudor.
  - `+exportarRespaldoDatos()`: Genera y exporta un archivo con el respaldo de la información del sistema.
- **Relaciones:**
  - **Administra (1 a *):** Múltiples instancias de la clase Cliente (Relación de composición).
  - **Validated by:** Depende de la clase Propietario para la validación de acceso.

#### 2. Clase: Propietario

Es la clase encargada de gestionar la autenticación, protegiendo la integridad y el acceso al sistema.

- **Atributos:**
  - `-usuario` (String): Identificador de acceso del propietario (Privado).
  - `-contrasenaEncriptada` (String): Contraseña de acceso sometida a encriptación (Privado).
- **Métodos:**
  - `+autenticarAcceso()`: Verifica las credenciales ingresadas contra las almacenadas en el sistema.
- **Relaciones:**
  - Valida el acceso a la clase SistemaGestor.

#### 3. Clase: Cliente

Entidad central del sistema que agrupa la información requerida por el negocio.

- **Atributos:**
  - `-nombre` (String): Nombre completo del cliente (Privado).
  - `-rut` (String): Rol Único Tributario o identificador del cliente (Privado).
  - `-telefono` (String): Número de contacto del cliente (Privado).
  - `-direccion` (String): Dirección de residencia del cliente (Privado).
  - `-saldoDeuda` (Float): Monto total que el cliente adeuda al negocio (Privado).
- **Métodos:**
  - `+crear()`: Crea un nuevo registro de cliente.
  - `+leer()`: Consulta los datos de un cliente existente.
  - `+actualizar()`: Modifica la información del cliente.
  - `+eliminar()`: Da de baja un registro de cliente.
- **Relaciones:**
  - **Posee (1 a *):** Múltiples instancias de la clase CreditoVecinal (Relación de composición).
  - **Realiza (1 a *):** Múltiples instancias de la clase Pago (Relación de composición).

#### 4. Clase: CreditoVecinal

Clase transaccional que registra las ventas fiadas realizadas a los clientes.

- **Atributos:**
  - `-fecha` (Date): Fecha en que se realiza la venta a crédito (Privado).
  - `-descripcionProductos` (String): Detalle de los artículos adquiridos (Privado).
  - `-monto` (Float): Valor monetario de la venta fiada (Privado).
- **Métodos:**
  - `+registrarCredito()`: Registra la nueva venta a crédito en el sistema.
  - `+actualizarSaldoAutomatico()`: Suma el monto del nuevo crédito al saldo de la deuda del cliente.
- **Relaciones:**
  - Pertenece a un Cliente.

#### 5. Clase: Pago

Clase transaccional que gestiona los abonos realizados por los clientes para disminuir su deuda.

- **Atributos:**
  - `-fecha` (Date): Fecha en la que el cliente realiza el abono (Privado).
  - `-montoAbono` (Float): Cantidad de dinero entregada como pago (Privado).
- **Métodos:**
  - `+ingresarAbono()`: Registra el pago en el sistema.
  - `+actualizarHistorial()`: Resta el monto abonado del saldo deudor del cliente y deja un registro del movimiento.
- **Relaciones:**
  - Es realizado por un Cliente.

---

## 9. Prototipo

El prototipo del SGC-Lukas ha sido desarrollado con el objetivo de validar el diseño de la interfaz gráfica y el flujo de navegación del sistema antes de proceder a la codificación final. El prototipo fue construido respetando los requisitos funcionales (R.1 a R.4) y no funcionales levantados en la Evaluación N°1, con especial atención a los atributos de usabilidad (RNF.3) y eficiencia.

La interfaz ha sido diseñada bajo los siguientes principios:

- **Simplicidad:** pantalla principal con acceso directo a las 4 funciones más frecuentes (registrar crédito, registrar pago, buscar cliente, listar morosos).
- **Eficiencia:** cada operación se completa en 3 pasos o menos, minimizando el tiempo de registro en el mostrador del almacén.
- **Claridad visual:** uso de colores semafóricos para el estado de deuda de los clientes (verde: sin deuda, amarillo: deuda reciente, rojo: deuda vencida).
- **Compatibilidad:** interfaz optimizada para pantalla de escritorio (1366×768 o superior), operable con teclado y mouse.

### 9.1 Pantallas del prototipo

#### Pantalla 1 — Inicio de sesión

La pantalla de login solicita usuario y contraseña. Tras 3 intentos fallidos, el acceso queda bloqueado temporalmente (RNF.1). La pantalla muestra el nombre del sistema y el logotipo del almacén.

> **Mockup:** Pantalla de inicio de sesión con campos de Usuario y Contraseña, botón "INGRESAR", aviso de bloqueo tras 3 intentos fallidos, y enlace "¿Olvidaste tu contraseña?".

#### Pantalla 2 — Menú principal / Dashboard

Pantalla de bienvenida que muestra el número total de clientes activos, la deuda total pendiente del mes, y accesos rápidos a cada módulo del sistema (Clientes, Créditos, Pagos, Reportes).

> **Mockup:** Dashboard con tarjetas de resumen (Clientes Activos: 145, Deuda Total del Mes: $1.450.000 CLP) y 4 botones de acceso rápido a los módulos principales.

#### Pantalla 3 — Módulo Clientes

Listado completo de clientes con opciones de búsqueda, crear, editar y ver el estado de cuenta de cada cliente con un solo clic. Incluye indicador visual del saldo (colores semafóricos).

> **Mockup:** Tabla de clientes con columnas Nombre, RUT, Saldo Actual (con colores: rojo para deuda, verde para $0, amarillo para deuda moderada) y botones de acción Editar / Estado Cuenta. Barra de búsqueda y botón "Crear Cliente".

#### Pantalla 4 — Registro de crédito y pago

Formulario unificado para registrar créditos o pagos. Selecciona el cliente desde un campo autocompletado, ingresa el monto y descripción del crédito. Confirma la operación y muestra el nuevo saldo. La misma pantalla, con variante de formulario, permite registrar abonos o pagos totales.

> **Mockup:** Formulario con pestañas "NUEVO CRÉDITO (VENTA FIADA)" y "NUEVO ABONO O PAGO". Campos: Cliente (autocompletado), Monto del Crédito (CLP), Descripción. Previsualización de saldo actual vs. nuevo saldo proyectado. Botón "CONFIRMAR CRÉDITO".

#### Pantalla 5 — Listado de morosos

Reporte generado automáticamente con todos los clientes que tienen saldo mayor a $0, ordenados por monto de deuda (descendente). Incluye nombre, teléfono, deuda total y fecha del último pago. Permite exportar el listado a CSV con un clic.

> **Mockup:** Tabla de clientes morosos con columnas de datos de contacto y deuda. Botón "EXPORTAR A CSV". Indicador de total de clientes y cantidad de morosos.

---

## 10. Conclusiones

El presente informe documenta la etapa de diseño, planificación y prototipado del Sistema de Gestión Almacén Lukas (SGC-Lukas), dando continuidad al trabajo de análisis y levantamiento de requisitos documentado en la Evaluación N°1.

Desde la perspectiva del equipo de desarrollo, los principales resultados y aprendizajes de esta etapa son los siguientes:

En primer lugar, se logró traducir los requisitos funcionales y no funcionales levantados en la primera entrega en una arquitectura de sistema concreta y coherente. La elección del stack tecnológico (Python + CustomTkinter + SQLite) responde de manera directa a las restricciones del entorno del cliente —sistema offline, computador de escritorio Windows, presupuesto nulo para licencias— y a las competencias técnicas del equipo, lo que minimiza los riesgos de implementación. El patrón MVC adoptado garantiza un código mantenible y extensible para versiones futuras.

En segundo lugar, el estudio de factibilidad confirmó la viabilidad del proyecto en todas sus dimensiones: técnicamente, el equipo cuenta con las herramientas y competencias necesarias; económicamente, la solución no requiere inversión en software ni hardware adicional; legalmente, el sistema cumple con las disposiciones de la Ley N°19.628 y su modificación (Ley N°21.719) sobre protección de datos personales; y operacionalmente, el usuario final tiene el perfil y la motivación para adoptar el sistema con una curva de aprendizaje mínima.

En tercer lugar, el análisis costo-beneficio demostró que, con una inversión inicial de desarrollo equivalente a CLP $1.056.000, los beneficios cuantificables anuales ascienden a CLP $462.000, permitiendo recuperar la inversión en aproximadamente 2 años y 4 meses. Este análisis refuerza la justificación técnico-económica del sistema y evidencia que la solución no solo es viable, sino rentable a mediano plazo para el Almacén Lukas.

En cuarto lugar, el diagrama de jerarquía modular y los diagramas UML (casos de uso y clases) estructuraron la arquitectura funcional del sistema, identificando las dependencias entre módulos y definiendo las responsabilidades de cada clase. Este modelo servirá como guía directa para la distribución de tareas de desarrollo en las etapas subsiguientes del proyecto.

Finalmente, el prototipo de interfaz desarrollado permitió al equipo validar el diseño de la experiencia de usuario antes de comprometer horas de codificación. Las pantallas diseñadas priorizan la eficiencia operativa en el contexto del mesón de atención del almacén, donde el propietario debe interactuar con el sistema mientras atiende clientes. Los mockups fueron revisados con el Sr. Caballero, quien expresó conformidad con el diseño propuesto.

En síntesis, el equipo de desarrollo concluye que el proyecto SGC-Lukas avanza sobre una base sólida y bien fundamentada, con una propuesta técnicamente robusta, económicamente justificada y operacionalmente viable. Los pasos siguientes contemplan el desarrollo incremental de los módulos definidos, con entregas parciales para validación continua con el cliente, culminando en la implementación final y capacitación del Sr. Caballero en el uso del sistema.

---

## 11. Referencias

Las siguientes referencias sustentan el marco teórico, metodológico y normativo del presente informe, siguiendo las normas de citación APA (7ª edición):

- Sommerville, I. (2011). *Ingeniería del software* (9.ª ed.). Pearson.
- Pressman, R. S. (2010). *Ingeniería del software: Un enfoque práctico* (7.ª ed.). McGraw-Hill.
- Brooks, F. P. (1987). No silver bullet: Essence and accidents of software engineering. *IEEE Computer, 20*(4).
- IEEE/ANSI 830-1998. (1998). *IEEE Recommended Practice for Software Requirements Specifications*. Institute of Electrical and Electronics Engineers.
- Ley N°19.628. (1999, agosto 28). Sobre protección de la vida privada. *Diario Oficial de la República de Chile*.
- Ley N°21.719. (2024). Modifica la Ley N°19.628, sobre protección de la vida privada, en materia de datos personales. *Diario Oficial de la República de Chile*.
- Instituto Nacional de Estadísticas (INE). (2025). *Encuesta Suplementaria de Ingresos*. Gobierno de Chile.
- Caballero, C. (2026, abril). [Entrevistas de levantamiento de requisitos]. Almacén Lukas, Lo Prado, Chile.

---

*Sistemas de Información — 2026*
