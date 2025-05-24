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

Una vez instalado el programa y configurado correctamente el entorno de trabajo, se estará listo para iniciar con el proceso de programación y ensamblaje de componentes dentro del entorno virtual proporcionado por Quanser.

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

![image](https://github.com/user-attachments/assets/f2e3931e-8672-407b-8a9a-9f942b058e28)
*Imagen 5. Modeloaje de Plantas disponibles*

Una vez dentro del entorno principal de Quanser Interactive Labs, se debe hacer clic sobre la planta "Qube 2 – DC Motor". Esta opción abre una nueva ventana emergente donde se visualiza un entorno simulado que representa el sistema de servomotor.

Este entorno incluye:

* Vista en 3D del sistema Qube 2, permitiendo observar la rotación del motor y su comportamiento dinámico.

* Controles de simulación, tales como iniciar, pausar y reiniciar el experimento.

* Sensores virtuales que permiten visualizar y medir la posición angular, velocidad y señales de control.

* Interfaz para conectar con MATLAB/Simulink, lo cual permite ejecutar algoritmos de control desarrollados por el usuario en tiempo real.

![image](https://github.com/user-attachments/assets/ee9b7202-9200-4838-86d2-8c27fcae51db)

*Imagen  6. Diseño virtual de planta*

## 4. Concepto Transmisión Polea-Correa

El sistema de transmisión por polea y correa es un mecanismo ampliamente utilizado para transferir movimiento y potencia entre dos ejes separados. Este tipo de transmisión se basa en el uso de una correa flexible que conecta dos poleas: una motriz (coneUna vez ejecutado este comando, se abrirá una ventana emergente donde se podrá seleccionar una de las tres plantas disponibles para comenzar a trabajar.ctada al motor) y otra conducida (conectada a la carga). Al girar la polea motriz, la correa transmite ese movimiento a la polea conducida, permitiendo modificar la velocidad y el torque de salida según el diámetro de las poleas involucradas.

Entre sus ventajas destacan la simplicidad mecánica, el bajo costo, el funcionamiento silencioso y la capacidad de absorber vibraciones. Además, permite transmisiones a distancia y cierta flexibilidad en la alineación de los ejes. Sin embargo, también presenta desventajas como el posible deslizamiento de la correa, la necesidad de mantenimiento periódico (ajuste de tensión y reemplazo de la correa) y una eficiencia menor comparada con sistemas más rígidos como engranajes.

**Puntos claves:**

* *Relación de transmisión:* Se determina por el cociente entre los diámetros de las poleas. Esto permite adaptar la velocidad y el torque entre el motor y la carga.

* *Tensión adecuada:* Es fundamental mantener la correa con la tensión correcta para evitar deslizamientos y asegurar una transmisión eficiente y duradera.

### 4.1. Relación de Transmisión

La relación de transmisión en un sistema de polea-correa indica cómo se modifica la velocidad de rotación entre la polea motriz (la que transmite el movimiento) y la polea conducida (la que recibe el movimiento). Esta relación depende directamente del tamaño de las poleas, y se calcula como:

Relación de transmisión (i) = $$\frac {Diámetro de la polea conducida}{Diámetro de la polea motriz}$$

Este valor también puede expresarse usando las velocidades de rotación:

$$i: \frac{Velocidad de la polea motriz}{Velocidad de la polea conducida}$$

### 4.2. Inercia Reflejada

En un sistema de polea-correa, la inercia reflejada se refiere a cómo la inercia de la carga (conectada a la polea conducida) se “ve” desde el motor (polea motriz), tomando en cuenta la relación de transmisión. Este concepto es clave en el diseño de sistemas de control de movimiento, ya que afecta directamente la respuesta dinámica del motor.

La inercia reflejada $J_{ref}$ al eje del motor se obtiene mediante la siguiente fórmula:

$$J_{ref}: \frac{J_{carga}}{i^{2}}$$

Donde:
* $J_{carga}$ es la inercia real de la carga.
* 𝑖
i es la relación de transmisión (diámetro polea conducida / diámetro polea motriz).

### 4.3. Torque de Carga

El torque de carga en un sistema de transmisión por polea-correa es el torque que debe entregar el motor para mover la carga conectada a la polea conducida. Este torque depende de la relación de transmisión, el tipo de carga y la eficiencia del sistema.

**Relación entre torque del motor y torque de la carga:**

$$T{motor}: \frac{T_{carga}}{i*n}$$

Donde:

* $T{motor}$ es el torque que debe generar el motor
* $T_{carga}$ es el torque requerido por la carga
* $i$ es la relación de transmisión (diámetro polea conducida / diámetro polea motriz)
* $n$ es la eficiencia del sistema (entre 0 y 1)

## 5. Ejercicios

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
