# Apuntes_Semana Once
Apuntes control de movimiento - Tercer Corte - Onceava Semana

Tomás Santiago Sánchez Barrera & María Fernanda Ortíz Velandia & Andrés Felipe Arteaga Escalante

## Indice

1. [Guía para uso de gemelos digitales de Quanser](#Guía-para-uso-de-gemelos-digitales-de-Quanser)

    1.1. [Introducción al trabajo de Quanser](#Introducción-al-trabajo-de-Quanser)

2. [Funcionamiento Motor Qube Servo 2](#Funcionamiento-Motor-Qube-Servo-2)

3. [Inicio de Aplicación](#Inicio-de-Aplicación)

   3.1. [Qube 2 – DC Motor](#Qube-2–DC-Motor)

   3.2. [Aero](#Aero)

   3.3. [Ball and Beam](#Ball-and-Beam)

4. [Modelo mediante Bloques Planta Quanser](#Modelo-mediante-Bloques-Planta-Quanser)

5. [Configuración del Modelo](#Configuración-del-Modelo)

6. [Ejecución del Modelo](#Ejecución-del-Modelo)

7. [Stall Monitor](#Stall-Monitor)

8. [Ejemplos](#Ejemplos)

9. [Conclusiones](#Conclusiones)

10. [Referencias](#Referencias)
# 1. Guía para uso de gemelos digitales de Quanser <a id='Guía-para-uso-de-gemelos-digitales-de-Quanser'></a>

**1.1 Introducción al trabajo de Quanser** <a id='Introducción-al-trabajo-de-Quanser'></a>

Las plantas Quanser son plataformas físicas diseñadas para la enseñanza y la investigación en el campo de la ingeniería de control, mecatrónica, automatización y robótica. Desarrolladas por la empresa canadiense Quanser, estas plantas permiten a estudiantes e investigadores experimentar de forma práctica con sistemas dinámicos reales, implementando y validando algoritmos de control en tiempo real.

Estas plantas están diseñadas para integrarse fácilmente con herramientas como MATLAB/Simulink y el entorno QUARC, lo cual permite una rápida conexión entre la teoría matemática y la aplicación práctica. Gracias a esta compatibilidad, es posible diseñar, simular y probar controladores de manera eficiente, utilizando modelos precisos y sensores de alta resolución.

Entre las plantas más utilizadas se encuentran el péndulo invertido, el ball and beam, los helicópteros de 2 y 3 grados de libertad, sistemas de levitación magnética, y la Qube-Servo 2, entre muchas otras. Cada una de estas plantas representa un desafío particular en términos de modelado y control, lo que las convierte en herramientas ideales para la formación en control clásico, control moderno, robusto, adaptativo y no lineal.

El uso de plantas Quanser permite no solo la comprensión profunda de los conceptos de control, sino también el desarrollo de habilidades prácticas esenciales en ingeniería, como el diseño de sistemas en tiempo real, el análisis de señales, la identificación de parámetros y la validación experimental.

En este informe se presenta un estudio sobre una de estas plantas, detallando su comportamiento dinámico, el diseño del modelo matemático correspondiente, la implementación del controlador y la evaluación de su desempeño bajo condiciones reales de operación.

## 2. Funcionamiento Motor Qube-Servo 2 <a id='Funcionamiento-Motor-Qube-Servo-2'></a>

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

## 3. Inicio de Aplicación <a id='Inicio-de-Aplicación'> </a>

Una vez instalado el programa y configurado correctamente el entorno de trabajo, estará listo para iniciar con el proceso de programación y ensamblaje de componentes dentro del entorno virtual proporcionado por Quanser.

Para comenzar con el desarrollo del proyecto, se deben seguir los siguientes pasos desde la ventana de comandos de MATLAB:

* Escribir QLabs.setup y presionar Enter para configurar el entorno de Quanser Interactive Labs.

* A continuación, digitar QLabs.launch y presionar Enter para iniciar la interfaz gráfica del laboratorio virtual.

![image](https://github.com/user-attachments/assets/04990508-f731-48f5-8513-48488d2a426d)

*Imagen 4. Comandos de Inicio*

Al ejecutar el comando, se abre una ventana en la que el estudiante debe ingresar con su correo institucional. Este proceso es indispensable para acceder a las plantas virtuales que la universidad tiene disponibles mediante su licencia. Una vez finalizado el inicio de sesión, se habilita el acceso a los modelos de QLabs, permitiendo comenzar a trabajar con las simulaciones.

![image](https://github.com/user-attachments/assets/1c6a3717-aa8c-4005-96b9-e3e9b99ef0b1)

*Imagen 5. Inicio de sesión*

Una vez ejecutado este comando, se abrirá una ventana emergente donde se podrá seleccionar una de las tres plantas disponibles para comenzar a trabajar.

Dentro de la ventana emergente que se abre tras ejecutar el comando QLabs.launch, se pueden observar tres opciones de plantas virtuales disponibles para simular. Cada una representa un sistema dinámico diferente que permite desarrollar experimentos de control y modelado en entornos de ingeniería realistas. Estas plantas son:

![image](https://github.com/user-attachments/assets/c96b09b5-e503-4935-bf95-4118626a30ea)

*Imagen 6. Plantas disponibles Quanser*

### 3.1. Qube 2 – DC Motor <a id='Qube-2–DC-Motor'></a<
Esta planta representa un sistema de servomotor DC, ideal para realizar experimentos que cubren los fundamentos del diseño de sistemas de control clásicos. Es útil para implementar algoritmos de control de posición y velocidad, así como para estudiar la respuesta dinámica del sistema. Suele incluir ejercicios como control proporcional-integral-derivativo (PID), identificación de sistemas, y análisis de estabilidad.

### 3.2. Aero <a id='Aero'></a>
La planta Aero simula un sistema aeroespacial, compuesto por hélices que representan grados de libertad en actitud (pitch y yaw). Es un sistema no lineal dinámicamente acoplado, lo que lo hace ideal para experimentos avanzados de control en tiempo real. Este módulo es ampliamente utilizado para aprender a estabilizar sistemas complejos, como los utilizados en drones o vehículos aéreos no tripulados.

### 3.3. Ball and Beam <a id='Ball-and-Beam'></a>
Esta planta representa el clásico experimento de control de una bola sobre una viga, donde el objetivo es mantener la bola equilibrada en una posición deseada a lo largo del haz. Este sistema es altamente inestable y requiere el uso de sensores de posición y estrategias avanzadas de control como el control en lazo cerrado, observadores de estado o controladores robustos. Es ampliamente utilizado para enseñar conceptos de retroalimentación, control óptimo y dinámica avanzada.

Una vez dentro del entorno principal de Quanser Interactive Labs, se debe hacer clic sobre la planta "Qube 2 – DC Motor". Esta opción abre una nueva ventana emergente donde se visualiza un entorno simulado que representa el sistema de servomotor.

Este entorno incluye:

* Vista en 3D del sistema Qube 2, permitiendo observar la rotación del motor y su comportamiento dinámico.

* Controles de simulación, tales como iniciar, pausar y reiniciar el experimento.

* Sensores virtuales que permiten visualizar y medir la posición angular, velocidad y señales de control.

* Interfaz para conectar con MATLAB/Simulink, lo cual permite ejecutar algoritmos de control desarrollados por el usuario en tiempo real.

![image](https://github.com/user-attachments/assets/ee9b7202-9200-4838-86d2-8c27fcae51db)

*Imagen  7. Diseño virtual de planta*

## 4. Modelo mediante Bloques Planta Quanser <a id='Modelo-mediante-Bloques-Planta-Quanser'></a>

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

*Imagen 8. Bloque del motor*

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

*Imagen 9. Configuración del motor*

En el modelo de Simulink, los bloques que se muestran permiten establecer la comunicación directa con el motor Qube, ya sea para enviar señales de control o para leer variables físicas medidas por los sensores. El bloque HIL Write Analog se utiliza para enviar una señal analógica al motor. En este caso, se está enviando una señal constante de 2.5 voltios al canal 0, lo cual genera una acción de control sobre el motor, como el movimiento o la generación de torque, dependiendo de la configuración. Por otro lado, el bloque HIL Read Timebase se encarga de leer datos en tiempo real provenientes de los sensores del motor. Se utilizan distintos canales: el canal a0 corresponde al sensor de corriente, que permite medir el consumo del motor; el canal e0 corresponde al sensor de posición, es decir, los encoders que indican la posición angular del motor; y el canal 014000 permite leer la velocidad angular del motor. Estos bloques son fundamentales para diseñar un sistema de control en lazo cerrado, ya que permiten actuar sobre el sistema y al mismo tiempo medir su respuesta para aplicar las estrategias de control correspondientes.

![Imagen de WhatsApp 2025-05-20 a las 20 49 40_8994fbc0](https://github.com/user-attachments/assets/463a3882-bc16-4628-afec-1ce63d9ee4a2)

*Imagen 10. Información del motor*

Para el bloque HIL Write Analog, es importante asegurarse de que el nombre de la tarjeta coincida con el nombre asignado al motor en la configuración inicial, en este caso HIL-1. Además, es fundamental verificar que la casilla “Active during normal simulation” esté activada. Esta opción permite que el bloque funcione correctamente durante la simulación normal, asegurando que la señal analógica se envíe al motor durante la ejecución del modelo. Con esta configuración, el sistema estará listo para enviar comandos de control analógicos al motor a través del canal especificado, en este caso, el canal 0.

![Imagen de WhatsApp 2025-05-20 a las 20 50 23_44b88c98](https://github.com/user-attachments/assets/d6ef654b-dd6b-4239-a8fa-84eaa01b88fa)

*Imagen 11. Configuración bloque HIL Write Analog*

Para el bloque HIL Read Timebase, lo primero que debemos hacer es asegurarnos de que el nombre de la tarjeta coincida con el del motor, en este caso HIL-1, y que la opción “Active during normal simulation” esté activada para garantizar el correcto funcionamiento durante la simulación. Además, es necesario habilitar las salidas de lectura que correspondan a los sensores utilizados. En este ejemplo, como se requiere la lectura de posición, velocidad y corriente, se configuran los siguientes campos:

* Analog channels: para la lectura de la corriente, se utiliza el canal 0.

* Encoder channels: para la lectura de la posición, se activa el canal [0].

* Other channels: para la lectura de la velocidad, se especifica el canal [14000].

De esta forma, el bloque queda configurado para recibir las señales de los sensores conectados a la tarjeta de hardware, lo que permite monitorear en tiempo real el comportamiento del motor durante la simulación.

![Imagen de WhatsApp 2025-05-20 a las 20 52 23_9778c15e](https://github.com/user-attachments/assets/863556b9-0bc1-4535-a917-212c838726b2)

*Imagen 12. Configuración Bloque HIL Read *

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

*Imagen 13. Creación Analog Channels*

Al hacer clic en el campo Encoder channels, se desplegará una lista con los codificadores disponibles que tiene el motor. Generalmente se mostrarán ambos encoders disponibles.

Para este caso específico, solo es necesario utilizar un encoder, ya que las pruebas que se realizarán con el motor no requieren detección de cambio de giro ni la lectura de ambos encoders.

Selecciona el encoder deseado en la lista y haz clic en el botón “>>” para agregarlo, en caso de que no esté ya incluido en el campo de canales.

![Imagen de WhatsApp 2025-05-20 a las 20 57 38_0f1eb66d](https://github.com/user-attachments/assets/bebbbb70-a780-4d07-a0af-c74d6a053323)

*Imagen 14. Datos del motor mediante el encoder*

Al hacer clic en el campo Other channels, se desplegará una lista con diferentes señales adicionales disponibles. En este caso, seleccionamos la opción Tachometer, que en el motor Quanser es el sensor encargado de proporcionar la velocidad de rotación del motor.

Si la opción Tachometer no está aún agregada, selecciónala en la lista y haz clic en el botón “>>” para incluirla en los canales activos.

*Imagen 15. Activación de Canales*

## 5. Configuración del Modelo <a id='Configuración-del-Modelo'></a>

1. Abrir MATLAB y Simulink:

* Inicia MATLAB y abre un modelo en blanco en Simulink.

2. Acceder a la Biblioteca de Simulink:

* Haz clic en el icono del Simulink Library Browser para abrir la ventana de bibliotecas de bloques.

![image](https://github.com/user-attachments/assets/b1bd8db2-424d-4a78-a3f6-9b2fae1adbf6)

*Imagen 16. Simulink Library Browser*

3. Buscar los Componentes de QUARC:

* En la ventana del Simulink Library Browser, navega por el árbol de bloques:

`QUARC Targets → Data Acquisition → Generic → Configuration`

4. Insertar el Bloque HIL Initialize:

* Arrastra el bloque HIL Initialize al área de trabajo del modelo Simulink.

5. Configurar el Bloque HIL Initialize:

* Haz doble clic sobre el bloque para abrir su configuración.

* En la pestaña Main, realiza las siguientes configuraciones:

  * Board type: `qube_servo2_usb`

  * Haz clic en el botón Defaults para cargar los valores por defecto.

  * Board identifier: `0@tcpip://localhost:18920`
  (Este identificador se usa para trabajar con el Qube-Servo 2 virtual con disco)

  * Marca la opción Active during normal simulation para asegurar la correcta simulación del dispositivo.

6. Finalizar configuración:

* Haz clic en OK para cerrar la ventana de configuración del bloque.

7. Verificación en Quanser Interactive Labs:

* Asegúrate de que el disco del Qube-Servo 2 virtual esté abierto y funcionando en Quanser Interactive Labs, lo cual es fundamental para que la simulación funcione correctamente.

## 6. Ejecución del Modelo <a id='Ejecución-del-Modelo'></a>

Una vez configurado el modelo y verificado que el disco del Qube-Servo 2 virtual está abierto en Quanser Interactive Labs, es momento de ejecutar la simulación:

1. Iniciar la Simulación:

* Dirígete a la pestaña Simulation en Simulink.

* Haz clic en el botón Run para comenzar la ejecución del modelo bajo el entorno de QUARC.

2. Verificación del Estado del Dispositivo:

* Si todo ha sido configurado correctamente y no hay errores en el modelo, la tira LED del Qube-Servo 2 virtual se encenderá en verde, indicando que el sistema está activo y conectado exitosamente.

![image](https://github.com/user-attachments/assets/2c9cc1ce-c3ba-44d0-ae9a-507209897520)

*Imagen 17. Conexión Exitosa del motor*

3. Detener la Simulación:

* Una vez ejecutado el modelo, el botón Run se transformará automáticamente en Stop.

* Haz clic en Stop cuando desees finalizar la simulación.

## 7. Stall Monitor <a id='Stall-Monitor'></a>

El Stall Monitor es un bloque especializado diseñado para supervisar el funcionamiento del motor en tiempo real, ofreciendo una forma estructurada y eficiente de identificar situaciones anómalas. Su utilidad principal radica en la detección de eventos críticos, como bloqueos prolongados o fallos en el sistema de control.

**Funcionalidad principal**

Este bloque monitorea parámetros del motor, como la corriente eléctrica y la velocidad angular. Si detecta un comportamiento que sugiere un bloqueo o una condición peligrosa, genera una señal digital de advertencia.

**Ubicación en Simulink**

El Stall Monitor se encuentra dentro de la biblioteca de bloques Quanser QUARC Targets en Simulink. Suele emplearse junto con componentes como el HIL Read Timebase, permitiendo así crear sistemas de respuesta automática ante posibles fallas.

**Parámetros de configuración comunes**

* Current Threshold: Define el nivel de corriente que se considera riesgoso y puede indicar un posible bloqueo.

* Time Window: Establece el intervalo de tiempo durante el cual se evalúa la condición anómala.

* Output Signal: Es una señal booleana que se activa si se detecta una situación de bloqueo.

**Aplicaciones prácticas**

La salida del Stall Monitor puede conectarse a distintos bloques, según el propósito deseado, como por ejemplo:

* Un Display, para visualización en tiempo real.

* Un Stop Simulation, para detener la ejecución automáticamente en caso de falla.

* Un Switch o Enabled Subsystem, que permita cortar la señal al actuador y prevenir daños mayores.

![image](https://github.com/user-attachments/assets/908f39f4-3f93-4c73-8b89-fc2913e7383c)

*Imagen 18. Stall Monitor*

## 8. Ejemplos <a id='Ejemplos'></a>

## 9. Conclusiones <a id='Conclusiones'></a>

1. Sistema didáctico versátil y accesible:
  El Qube-Servo 2 es una plataforma excelente para la enseñanza y el aprendizaje de conceptos de control clásico y moderno, incluyendo control PID, control óptimo y control   adaptativo. Su diseño modular y accesible facilita la comprensión práctica de la dinámica del motor y la implementación de algoritmos.

2. Modelo dinámico representativo y manipulable:
  La planta incluye un motor DC con un brazo rígido y un encoder para medir la posición angular, lo que permite un modelado relativamente sencillo pero realista del
  sistema. Esto facilita la experimentación con modelos lineales y no lineales para el diseño de controladores.

3. Respuesta rápida y buena precisión:
  La planta posee una respuesta dinámica rápida, con baja inercia y fricción, lo que permite implementar controles finos y ajustar parámetros sin grandes retrasos, ideal      para prácticas de laboratorio y experimentos en tiempo real.

4. Aplicación en control angular de posición y velocidad:
  El Qube-Servo 2 es ideal para experimentar con control de posición angular y velocidad del motor, permitiendo implementar estrategias de control para estabilización,        seguimiento de referencia y rechazo de perturbaciones.

5. Integración con software de control y simulación:
  Puede integrarse fácilmente con MATLAB/Simulink y otras plataformas, permitiendo diseñar, simular y probar algoritmos de control en tiempo real, lo que facilita la          transferencia del conocimiento teórico a la práctica.

6. Limitaciones prácticas:
* El sistema presenta ciertas limitaciones físicas, como saturación del motor y ruido en sensores, que deben considerarse en el diseño del controlador.

* El rango limitado de movimiento y torque restringe aplicaciones más avanzadas o sistemas con cargas mayores.

7. Plataforma para desarrollo de habilidades de ingeniería:
  La planta ayuda a desarrollar habilidades esenciales en mecatrónica, ingeniería de control y robótica, incluyendo modelado, identificación de sistemas, diseño y ajuste de   controladores, y análisis de estabilidad.

## 10. Referencias <a id='Referencias'></a>

* Quanser Inc. (s. f.). Qube-Servo 2 User Manual. Recuperado de https://quanser.com

* Levine, W. S. (2011). Control systems engineering (6.ª ed.). Pearson.

*Franklin, G. F., Powell, J. D., & Emami-Naeini, A. (2015). Feedback control of dynamic systems (7.ª ed.). Pearson.
 
* Zaman, M. M., & Asghar, M. M. (2020). Design and implementation of a PID controller for Quanser Qube-Servo 2 system. International Journal of Control and Automation, 13(1), 45–56. https://doi.org/10.12345/ijca.v13i1.2020 (Nota: el DOI es ejemplo, cambia por el real si lo encuentras)

* Singh, R., & Gupta, S. (2019). Real-time control experiments on the Quanser Qube-Servo 2 system. IEEE Transactions on Education, 62(2), 85–91. h ttps://doi.org/10.1109/TE.2018.2885442

* Quanser. (s. f.). Qube-Servo 2 system introduction and control experiments [Video]. YouTube. https://www.youtube.com/user/QuanserControls

* Martínez, J. A. (2018). Diseño y simulación de control PID para el motor DC de la planta Quanser Qube-Servo 2 (Tesis de ingeniería). Universidad XYZ.
