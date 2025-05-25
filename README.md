# Apuntes_Semana Once
Apuntes control de movimiento - Tercer Corte - Onceava Semana

Tomás Santiago Sánchez Barrera & María Fernanda Ortíz Velandia & Andrés Felipe Arteaga Escalante

# Guía para uso de gemelos digitales de Quanser

**Introducción al trabajo de Quanser**

Las plantas Quanser son plataformas físicas diseñadas para la enseñanza y la investigación en el campo de la ingeniería de control, mecatrónica, automatización y robótica. Desarrolladas por la empresa canadiense Quanser, estas plantas permiten a estudiantes e investigadores experimentar de forma práctica con sistemas dinámicos reales, implementando y validando algoritmos de control en tiempo real.

Estas plantas están diseñadas para integrarse fácilmente con herramientas como MATLAB/Simulink y el entorno QUARC, lo cual permite una rápida conexión entre la teoría matemática y la aplicación práctica. Gracias a esta compatibilidad, es posible diseñar, simular y probar controladores de manera eficiente, utilizando modelos precisos y sensores de alta resolución.

Entre las plantas más utilizadas se encuentran el péndulo invertido, el ball and beam, los helicópteros de 2 y 3 grados de libertad, sistemas de levitación magnética, y la Qube-Servo 2, entre muchas otras. Cada una de estas plantas representa un desafío particular en términos de modelado y control, lo que las convierte en herramientas ideales para la formación en control clásico, control moderno, robusto, adaptativo y no lineal.

El uso de plantas Quanser permite no solo la comprensión profunda de los conceptos de control, sino también el desarrollo de habilidades prácticas esenciales en ingeniería, como el diseño de sistemas en tiempo real, el análisis de señales, la identificación de parámetros y la validación experimental.

En este informe se presenta un estudio sobre una de estas plantas, detallando su comportamiento dinámico, el diseño del modelo matemático correspondiente, la implementación del controlador y la evaluación de su desempeño bajo condiciones reales de operación.


## 1. Funcionamiento Motor Qube-Servo 2

El Qube-Servo 2 es una plataforma didáctica desarrollada por Quanser que permite la implementación y análisis de sistemas de control en tiempo real. Este dispositivo compacto integra un servomotor de precisión y sensores de alta resolución, y está diseñado para facilitar la experimentación con una amplia variedad de algoritmos de control, tanto clásicos como modernos.

Entre las aplicaciones más comunes del Qube-Servo 2 se encuentran el control de velocidad, el seguimiento de posición, y, especialmente, el estudio del péndulo invertido rotacional, un sistema altamente no lineal e inestable que ha sido durante décadas un caso de estudio fundamental en el área de control automático. Gracias a su arquitectura modular y su compatibilidad con entornos como MATLAB/Simulink y QUARC, el Qube-Servo 2 brinda una experiencia práctica que complementa la teoría de control con experimentación física de alta fidelidad.

Esta planta es ampliamente utilizada en cursos de ingeniería de control, mecatrónica y robótica, debido a su versatilidad, facilidad de uso y capacidad para demostrar conceptos clave como la realimentación, la linealización, el control PID, el control óptimo (LQR), y el control adaptativo, entre otros.

En este informe se presenta el análisis, diseño e implementación de distintos controladores aplicados al Qube-Servo 2, con el objetivo de comprender su dinámica, mejorar su rendimiento y validar los modelos teóricos mediante pruebas experimentales.

## 2. Descarga conexión Planta Quanser

Para el desarrollo del trabajo y el diseño del modelo de la planta, se utiliza una herramienta digital conocida como gemelo digital, la cual permite simular el comportamiento de la planta seleccionada de manera virtual. Esta simulación facilita la comprensión de la dinámica del sistema y permite implementar y probar algoritmos de control antes de aplicarlos en la planta física.

Para acceder a esta herramienta y comenzar a trabajar con el sistema, es necesario seguir los siguientes pasos:

* Registrarse en el portal oficial de Quanser a través del siguiente enlace: https://portal.quanser.com/Accounts/Login?returnUrl=/, utilizando su correo institucional.

![image](https://github.com/user-attachments/assets/7c05bc20-ff1d-4b9f-b47a-a8497eacbca8)

*Imagen 1. Ingreso de datos Quanser Web*

Una vez se haya ingresado al portal de Quanser, el sistema solicitará algunos datos personales para la creación del perfil de usuario. Este paso es necesario para poder descargar el software requerido para el uso y desarrollo de proyectos con las plantas virtuales.

Después de completar el registro y descargar el archivo correspondiente desde el sitio web de Quanser, se debe acceder al entorno de MATLAB, donde se llevará a cabo el siguiente procedimiento:

* Desde MATLAB, se debe buscar, descargar e instalar el complemento llamado Quanser Interactive Labs for MATLAB, el cual permite la integración del entorno de simulación con las herramientas de Quanser, incluyendo los gemelos digitales.

![image](https://github.com/user-attachments/assets/ad78c73a-767f-4812-84ef-93bf952304df)

*Imagen 2. Instalación Quanser con Matlab*

En este laboratorio se desarrollará un modelo básico en Simulink utilizando bloques del entorno QUARC, con el objetivo de controlar un motor de corriente continua (DC) y medir el ángulo de rotación correspondiente. Esta práctica permitirá familiarizarse con la interfaz de programación en tiempo real y establecer la comunicación entre el modelo digital y la planta simulada mediante el uso de sensores y actuadores virtuales.

![Imagen de WhatsApp 2025-05-18 a las 22 07 42_1a259855](https://github.com/user-attachments/assets/7e4d87b2-a5d2-4710-ab38-ac2baa72e96c)

*Imagen 3. Montaje Planta Quanzer dentro de entorno Simulink*

## 3. Inicio de Aplicación

Una vez instalado el programa y configurado correctamente el entorno de trabajo, estará listo para iniciar con el proceso de programación y ensamblaje de componentes dentro del entorno virtual proporcionado por Quanser.

Para comenzar con el desarrollo del proyecto, se deben seguir los siguientes pasos desde la ventana de comandos de MATLAB:

* Escribir QLabs.setup y presionar Enter para configurar el entorno de Quanser Interactive Labs.

* A continuación, digitar QLabs.launch y presionar Enter para iniciar la interfaz gráfica del laboratorio virtual.

Una vez ejecutado este comando, se abrirá una ventana emergente donde se podrá seleccionar una de las tres plantas disponibles para comenzar a trabajar.

![image](https://github.com/user-attachments/assets/c96b09b5-e503-4935-bf95-4118626a30ea)

*Imagen 4. Plantas disponibles Quanser*

Dentro de la ventana emergente que se abre tras ejecutar el comando QLabs.launch, se pueden observar tres opciones de plantas virtuales disponibles para simular. Cada una representa un sistema dinámico diferente que permite desarrollar experimentos de control y modelado en entornos de ingeniería realistas. Estas plantas son:

### 3.1. Qube 2 – DC Motor
Esta planta representa un sistema de servomotor DC, ideal para realizar experimentos que cubren los fundamentos del diseño de sistemas de control clásicos. Es útil para implementar algoritmos de control de posición y velocidad, así como para estudiar la respuesta dinámica del sistema. Suele incluir ejercicios como control proporcional-integral-derivativo (PID), identificación de sistemas, y análisis de estabilidad.

### 3.2. Aero
La planta Aero simula un sistema aeroespacial, compuesto por hélices que representan grados de libertad en actitud (pitch y yaw). Es un sistema no lineal dinámicamente acoplado, lo que lo hace ideal para experimentos avanzados de control en tiempo real. Este módulo es ampliamente utilizado para aprender a estabilizar sistemas complejos, como los utilizados en drones o vehículos aéreos no tripulados.

### 3.3. Ball and Beam
Esta planta representa el clásico experimento de control de una bola sobre una viga, donde el objetivo es mantener la bola equilibrada en una posición deseada a lo largo del haz. Este sistema es altamente inestable y requiere el uso de sensores de posición y estrategias avanzadas de control como el control en lazo cerrado, observadores de estado o controladores robustos. Es ampliamente utilizado para enseñar conceptos de retroalimentación, control óptimo y dinámica avanzada.

Una vez dentro del entorno principal de Quanser Interactive Labs, se debe hacer clic sobre la planta "Qube 2 – DC Motor". Esta opción abre una nueva ventana emergente donde se visualiza un entorno simulado que representa el sistema de servomotor.

Este entorno incluye:

* Vista en 3D del sistema Qube 2, permitiendo observar la rotación del motor y su comportamiento dinámico.

* Controles de simulación, tales como iniciar, pausar y reiniciar el experimento.

* Sensores virtuales que permiten visualizar y medir la posición angular, velocidad y señales de control.

* Interfaz para conectar con MATLAB/Simulink, lo cual permite ejecutar algoritmos de control desarrollados por el usuario en tiempo real.

![image](https://github.com/user-attachments/assets/ee9b7202-9200-4838-86d2-8c27fcae51db)

*Imagen  6. Diseño virtual de planta*

## 4. Modelo mediante Bloques Planta Quanser

Para iniciar el proceso de diseño de plantas y controladores en el entorno Simulink, es necesario conectar el bloque del Qube 2 – DC Motor dentro de un nuevo modelo. Este procedimiento permite que MATLAB/Simulink se comunique con la planta virtual y se puedan enviar señales de control y recibir datos en tiempo real.

Pasos a seguir:

**1. Abrir Simulink:**

* En la ventana de MATLAB, escribe simulink y presiona Enter para abrir el entorno de modelado.

**2. Crear un nuevo modelo:**

* Haz clic en "Blank Model" (modelo en blanco) para iniciar un nuevo proyecto.

**3. Insertar bloques de QUARC:**

* Abre la biblioteca de bloques y busca QUARC Targets. Aquí encontrarás los bloques necesarios para interactuar con la planta.

* Dentro de esa biblioteca, ubica el bloque "Qube-Servo 2 - DC Motor" (puede variar ligeramente dependiendo de la versión del software).

![Imagen de WhatsApp 2025-05-20 a las 20 42 29_02d9e5d6](https://github.com/user-attachments/assets/98e66953-2d5c-4799-b0c2-09e0a66b3cd7)

*Imagen 7. Bloque del motor*

Una vez insertado el bloque del motor en el modelo de Simulink, es necesario configurar sus parámetros para asegurar una correcta comunicación con la planta. Esta configuración varía dependiendo de si se trabaja con gemelos digitales (planta virtual) o con el motor físico.

**1. Acceder a la configuración del bloque:**

* Haz doble clic sobre el bloque del motor para abrir su ventana de propiedades.

**2. Asignar un nombre al dispositivo:**

* En el campo correspondiente al nombre del hardware, asigna el nombre HL_1. Este identificador será usado en el resto del modelo para hacer referencia al motor.

**3. Tipo de dispositivo:***

Dependiendo del entorno que se utilice, se selecciona el tipo de dispositivo:

Para gemelos digitales:

* Tipo de dispositivo: qube_servo2_usb

* Identificador de dispositivo: 0@tcpip://localhost:18920

Para motor físico:

* Tipo de dispositivo: qube_servo3_usb

* Identificador de dispositivo: 0

Esto indica al sistema si debe comunicarse con el entorno virtual (simulación) o con el hardware real, respectivamente.

![Imagen de WhatsApp 2025-05-20 a las 20 42 42_e7e2581f](https://github.com/user-attachments/assets/243a0314-4b15-48b5-aa30-0c7f3e595344)

*Imagen 8. Configuración del motor*

En el modelo de Simulink, los bloques que se muestran permiten establecer la comunicación directa con el motor Qube, ya sea para enviar señales de control o para leer variables físicas medidas por los sensores. El bloque HIL Write Analog se utiliza para enviar una señal analógica al motor. En este caso, se está enviando una señal constante de 2.5 voltios al canal 0, lo cual genera una acción de control sobre el motor, como el movimiento o la generación de torque, dependiendo de la configuración. Por otro lado, el bloque HIL Read Timebase se encarga de leer datos en tiempo real provenientes de los sensores del motor. Se utilizan distintos canales: el canal a0 corresponde al sensor de corriente, que permite medir el consumo del motor; el canal e0 corresponde al sensor de posición, es decir, los encoders que indican la posición angular del motor; y el canal 014000 permite leer la velocidad angular del motor. Estos bloques son fundamentales para diseñar un sistema de control en lazo cerrado, ya que permiten actuar sobre el sistema y al mismo tiempo medir su respuesta para aplicar las estrategias de control correspondientes.

![Imagen de WhatsApp 2025-05-20 a las 20 49 40_8994fbc0](https://github.com/user-attachments/assets/463a3882-bc16-4628-afec-1ce63d9ee4a2)

*Imagen 9. Información del motor*

Para el bloque HIL Write Analog, es importante asegurarse de que el nombre de la tarjeta coincida con el nombre asignado al motor en la configuración inicial, en este caso HIL-1. Además, es fundamental verificar que la casilla “Active during normal simulation” esté activada. Esta opción permite que el bloque funcione correctamente durante la simulación normal, asegurando que la señal analógica se envíe al motor durante la ejecución del modelo. Con esta configuración, el sistema estará listo para enviar comandos de control analógicos al motor a través del canal especificado, en este caso, el canal 0.

![Imagen de WhatsApp 2025-05-20 a las 20 50 23_44b88c98](https://github.com/user-attachments/assets/d6ef654b-dd6b-4239-a8fa-84eaa01b88fa)

*Imagen 10. Configuración bloque HIL Write Analog*

Para el bloque HIL Read Timebase, lo primero que debemos hacer es asegurarnos de que el nombre de la tarjeta coincida con el del motor, en este caso HIL-1, y que la opción “Active during normal simulation” esté activada para garantizar el correcto funcionamiento durante la simulación. Además, es necesario habilitar las salidas de lectura que correspondan a los sensores utilizados. En este ejemplo, como se requiere la lectura de posición, velocidad y corriente, se configuran los siguientes campos:

* Analog channels: para la lectura de la corriente, se utiliza el canal 0.

* Encoder channels: para la lectura de la posición, se activa el canal [0].

* Other channels: para la lectura de la velocidad, se especifica el canal [14000].

De esta forma, el bloque queda configurado para recibir las señales de los sensores conectados a la tarjeta de hardware, lo que permite monitorear en tiempo real el comportamiento del motor durante la simulación.

![Imagen de WhatsApp 2025-05-20 a las 20 52 23_9778c15e](https://github.com/user-attachments/assets/863556b9-0bc1-4535-a917-212c838726b2)

*Imagen 11. Configuración Bloque HIL Read *

El bloque HIL Read Timebase permite leer datos de entrada desde los canales de una tarjeta Hardware-in-the-Loop (HIL), funcionando además como base de tiempo para el modelo. Para su correcta configuración, es importante seguir los siguientes pasos:

**Nombre de la tarjeta (Board name):**
Asegúrate de que el nombre de la tarjeta coincida con el del resto del sistema. En este caso, debe ser HIL-1.

**Activación en simulación normal:**
Verifica que la opción “Active during normal simulation” esté marcada. Esto permite que el bloque funcione correctamente durante la simulación en tiempo real.

**Canales de lectura necesarios:**
Debemos activar los canales de entrada correspondientes a los sensores requeridos en la simulación. En este caso, se desea obtener datos de:

* Corriente del motor:
Habilitar el canal analógico donde se encuentra conectado el sensor. Haz clic en el campo Analog channels, busca "Motor Current Sensor [A]" en la lista y agrégalo utilizando el botón “>>” si aún no está agregado.

* Posición del motor:
Para esto, se utiliza un codificador. Agrega el canal correspondiente en el campo Encoder channels. En este ejemplo, se ha seleccionado el canal [0].

* Velocidad del motor:
Se debe ingresar el canal correspondiente en el campo Other channels. Por ejemplo, el canal [140000].

![Imagen de WhatsApp 2025-05-20 a las 20 55 47_68a4681e](https://github.com/user-attachments/assets/b42a35e1-bd53-4885-a659-3cd597119dfa)

*Imagen 12. Creación Analog Channels*

Al hacer clic en el campo Encoder channels, se desplegará una lista con los codificadores disponibles que tiene el motor. Generalmente se mostrarán ambos encoders disponibles.

Para este caso específico, solo es necesario utilizar un encoder, ya que las pruebas que se realizarán con el motor no requieren detección de cambio de giro ni la lectura de ambos encoders.

Selecciona el encoder deseado en la lista y haz clic en el botón “>>” para agregarlo, en caso de que no esté ya incluido en el campo de canales.

![Imagen de WhatsApp 2025-05-20 a las 20 57 38_0f1eb66d](https://github.com/user-attachments/assets/bebbbb70-a780-4d07-a0af-c74d6a053323)

*Imagen 13. Datos del motor mediante el encoder*

Al hacer clic en el campo Other channels, se desplegará una lista con diferentes señales adicionales disponibles. En este caso, seleccionamos la opción Tachometer, que en el motor Quanser es el sensor encargado de proporcionar la velocidad de rotación del motor.

Si la opción Tachometer no está aún agregada, selecciónala en la lista y haz clic en el botón “>>” para incluirla en los canales activos.

*Imagen 14. Activación de Canales*

## 5. Configuración dek Modelo

### Una carga tiene una inercia de 0.05 kg·m² y se conecta a un motor a través de una relación de transmisión de 4:1.
* Calcula la inercia reflejada al motor.

$$J_{r}=\frac{J_{L}}{N^{2}}$$

$J_{r}=\frac{0.05}{4^{2}}$

$J_{r}=\frac{0.05}{16}$

$J_{r}=0.003125 Kg*m^{2}$

* Si el torque requerido por la carga es de 2 Nm, ¿cuánto torque reflejado sentirá el motor?

$$T_{r}= \frac{T_{L}}{N}$$

$T_{r}=\frac{2}{4}$

$T_{r}=0.5 Nm$


### Un motor eléctrico proporciona un torque constante de 3 Nm a una velocidad de 1500 rpm.

* Calcular la potencia mecánica entregada por el motor en watts.

$$P=T*\omega$$

$T=3 Nm$

$\omega = 2\pi * \frac{rpm}{60}$

$\omega=2\pi* \frac{1500}{60}$

$\omega=2\pi * 25$

$\omega = 157.08 rad/s$

$P=3*157,08$

$P=471,24 W$

### Un sistema de transmisión tiene una eficiencia del 85%. Si el motor entrega una potencia de 500 W:

*  Calcular la potencia útil disponible en la carga.

$$P_{util}=\eta*P_{entrada}$$

$P_{util}=0.85*500$

$P_{util}= 425 W$

## 6. Conclusiones

* El diseño correcto de sistemas de transmisión mecánica (engranajes, correas, cadenas) es esencial para garantizar eficiencia, precisión, seguridad y durabilidad en sistemas automatizados y mecatrónicos.
* Una correcta elección del motor y su relación con la transmisión y la carga permite alcanzar un funcionamiento óptimo. Esto requiere asegurar el torque necesario, una relación de inercia adecuada y el cumplimiento de criterios como el costo, precisión y tiempos de ciclo.
* La inercia y el torque reflejados al eje del motor deben calcularse para anticipar el esfuerzo que el motor debe realizar. Esto es vital para evitar sobrecargas, mejorar el rendimiento dinámico y permitir un control más preciso.
* La relación entre engranajes afecta directamente la velocidad y el torque transmitido. Además, mantener alta eficiencia en el sistema minimiza pérdidas energéticas, mejora la vida útil del equipo y reduce el consumo energético.
* La relación define el equilibrio entre la inercia de la carga y la del motor. Mantenerla en rangos adecuados asegura un control estable y eficiente. Una mala relación puede llevar a inestabilidad, sobreesfuerzo del motor o pérdida de precisión.

## 7. Referencias

* Mecatrónica Integrada (2023). Motores eléctricos: Torque, potencia y eficiencia. Universidad Cooperativa de Colombia – Facultad de Ingeniería Mecatrónica. Material de estudio.

* González, J. (2019). Principios de máquinas eléctricas y transformadores. McGraw-Hill.

* Universidad Nacional de Colombia (2022). Laboratorio de máquinas eléctricas: prácticas con motores de inducción y corriente continua. Facultad de Ingeniería Eléctrica.

* Universidad Cooperativa de Colombia – Facultad de Ingeniería Mecatrónica. (2023). Motores eléctricos: Torque, potencia y eficiencia. Material de estudio interno.
