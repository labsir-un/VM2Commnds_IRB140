# Implementación de un Entorno de Robótica Colaborativa con Detección de Fatiga Basada en Visión Artificial

**Autores:**  
- **Manuel Felipe Carranza Montenegro** *(Estudiante, Ingeniería Mecatrónica)*  
- **Ing. Pedro Fabián Cárdenas Herrera** *(Profesor, Universidad Nacional de Colombia)*  
- **Ing. Ricardo Emiro Ramírez Heredia** *(Profesor, Universidad Nacional de Colombia)*  

**Institución:**  
- **Universidad Nacional de Colombia**  
- **Facultad de Ingeniería**  
- **Ingeniería Mecatrónica**

---

## Descripción General

El avance de la **robótica colaborativa** ha permitido una interacción más segura y eficiente entre humanos y robots en entornos industriales. Sin embargo, la seguridad del operario sigue siendo un desafío crítico, ya que factores como la **fatiga** pueden afectar su capacidad de respuesta, aumentar la probabilidad de errores y comprometer la seguridad del sistema en general. 

Este proyecto propone un sistema basado en **visión artificial** que monitorea el estado de fatiga de un operario y actúa en tiempo real para detener la operación de un **robot ABB IRB 140** en caso de riesgo. Para lograrlo, se implementó una solución de detección de fatiga utilizando una **cámara Intel RealSense D435**, **redes neuronales para el análisis de gesticulaciones faciales**, y un **PLC Allen Bradley Logix 5000** que interrumpe el funcionamiento del robot en caso de detectar niveles de fatiga críticos. Además, el sistema emplea una **arquitectura de ticket de comunicaciones**, asegurando un flujo de datos robusto y confiable entre los distintos componentes.

---

## Objetivos del Proyecto

- Desarrollar un sistema de detección de fatiga basado en visión artificial que permita monitorear en tiempo real el estado de alerta del operario, utilizando análisis de gesticulaciones faciales como un indicador del nivel de fatiga.

- Integrar un mecanismo de control proactivo que interrumpa automáticamente la operación del robot ABB IRB 140 al detectar signos de fatiga excesiva, garantizando así la seguridad del operario y reduciendo la probabilidad de accidentes en entornos de robótica colaborativa.

- Comparar la comunicación entre los módulos del sistema mediante la implementación de diferentes arquitectura de comunicaciones, asegurando un flujo de información eficiente entre la visión artificial y el controlador IRC5 del robot.

- Diseñar una solución escalable y adaptable a diferentes entornos industriales, considerando la posibilidad de futuras mejoras como la integración de sensores fisiológicos complementarios (ritmo cardíaco, temperatura corporal) y la optimización de los algoritmos de detección para condiciones de iluminación variables.

## Metodología y Arquitectura del Sistema  

El sistema de detección de fatiga está estructurado en varias etapas clave:  

### Captura y Procesamiento de Imágenes  
Se utiliza una **cámara Intel RealSense D435** para capturar imágenes en tiempo real del operario.  
Se aplican **algoritmos de visión artificial** para identificar signos de fatiga, considerando:  
   - Apertura ocular  
   - Frecuencia de parpadeo  
   - Expresiones faciales  

La información visual es procesada mediante un **modelo de redes neuronales preentrenadas** capaz de **clasificar el nivel de fatiga**.  

[![Ver Video](https://img.youtube.com/vi/Hj6JkPNJw48/0.jpg)](https://www.youtube.com/watch?v=Hj6JkPNJw48)

---

## Arquitectura de Comunicaciones

El sistema implementa dos arquitecturas de comunicación principales para garantizar una integración fluida entre la visión artificial y el control del robot:

1. Comunicación entre el módulo de visión artificial, el PLC e Ignition.
2. Comunicación entre el módulo de visión artificial y el robot ABB mediante sockets TCP/IP.

### 1. Comunicación entre el Módulo de Visión Artificial, el PLC e Ignition  

Esta arquitectura permite que la información sobre el nivel de fatiga del operario fluya desde el módulo de visión hasta el sistema de control y supervisión industrial.

#### Flujo de Datos:
1. El módulo de visión artificial en Python procesa imágenes en tiempo real y calcula el nivel de fatiga.  
2. Node-RED toma esta información y la convierte en formato JSON.  
3. OPC UA (Open Platform Communications - Unified Architecture) transporta la información desde Node-RED al PLC Allen Bradley Logix 5000.  
4. El PLC analiza los datos y actualiza variables de control para la seguridad del robot.  
5. Ignition recibe estos datos desde OPC UA y los muestra en una interfaz gráfica en tiempo real con registro de eventos y alarmas.  
6. Si el nivel de fatiga es crítico, el PLC genera una señal de parada que se envía al robot.  

#### Tecnologías Usadas:
- Python: Procesamiento de visión artificial.
- Node-RED: Middleware para manejar y distribuir la información.
- OPC UA: Comunicación estándar industrial entre sistemas heterogéneos.
- Ignition SCADA: Monitoreo, registro y supervisión en tiempo real.
- Allen Bradley PLC (Logix 5000): Control de seguridad del robot.

#### Ventajas:
- Comunicación estandarizada y escalable con OPC UA.  
- Integración con sistemas industriales ya existentes.  
- Monitoreo en tiempo real con alertas y reportes históricos.  

### 2. Comunicación entre el PLC y el Robot ABB IRB 140 mediante Sockets TCP/IP  

Esta arquitectura garantiza una respuesta rápida y eficiente del robot a las señales de fatiga enviadas por el PLC.

#### Flujo de Datos: 
1. Se abre una conexión por sockets TCP/IP con el ABB Robot Controller (IRC5).  
2. El módulo de visión artificial envía comandos al ABB Driver en el controlador del robot.  
3. El robot ABB IRB 140 recibe y ejecuta la orden de parada.  
4. Cuando el operario valida su estado, el módulo de visión artificial envía una señal de reactivación al robot, permitiendo que continúe la operación.  

#### Tecnologías Usadas: 
- ABB IRC5 Controller: Controlador del robot ABB IRB 140.  
- Sockets TCP/IP: Comunicación directa y rápida entre PLC y Robot.  

#### Ventajas:
- Baja latencia en la transmisión de datos.  
- Protocolo ligero y eficiente sin necesidad de middleware adicional.  
- Interfaz directa con el controlador IRC5 del robot.  

### Resumen de la Arquitectura de Comunicaciones  

| Componente | Función |
|------------|---------|
| Módulo de visión artificial (Python) | Captura de imágenes y análisis de fatiga. |
| Node-RED | Middleware para convertir y transmitir datos. |
| OPC UA | Estándar de comunicación entre sistemas industriales. |
| PLC Allen Bradley Logix 5000 | Lógica de control de seguridad. |
| Ignition SCADA | Supervisión y monitoreo en tiempo real. |
| Sockets TCP/IP | Comunicación directa entre el PLC y el Robot ABB. |
| ABB IRC5 Controller | Control y ejecución del robot ABB IRB 140. |

Esta arquitectura permite que el sistema funcione en tiempo real, asegurando que cuando se detecta fatiga en el operario, se interrumpa la operación del robot en menos de un segundo, mientras la información se muestra en la interfaz SCADA para monitoreo remoto.

Este sistema optimiza la seguridad en entornos de robótica colaborativa al integrar visión artificial, control industrial y comunicaciones eficientes mediante OPC UA y sockets TCP/IP.

<img width="1426" alt="Screenshot 2025-03-07 at 03 48 14" src="https://github.com/user-attachments/assets/5660121b-d723-438c-bdbd-cfcc94af3031" />

## Resultados del Sistema de Detección de Fatiga  

El sistema fue evaluado en dos entornos:  

1. **Prueba en el entorno real del LabSir**: Se validó la integración del sistema con el robot ABB IRB 140 y el PLC Allen Bradley.  
2. **Simulación en RobotStudio**: Se verificó la respuesta del robot en un entorno virtual antes de la implementación física.  

---

### 1. Resultados en el Laboratorio LabSir  

#### **Precisión en la Detección de Fatiga**  
- La detección de fatiga mediante visión artificial alcanzó una **precisión del 85%** en la clasificación de fatiga.  
- Se observaron mejores resultados en condiciones de **iluminación estable**.  
- En operarios con gafas, la precisión disminuyó debido a reflejos y variaciones en la detección de la apertura ocular.  

#### **Tiempo de Respuesta del Sistema**  
- Desde la detección de fatiga hasta la activación de la **parada de emergencia del robot**, el tiempo de respuesta promedio fue de **menos de 1 segundo**.  
- Se verificó que la comunicación entre el módulo de visión, el PLC y el robot a través de **sockets TCP/IP** permitió una respuesta rápida y eficiente.  

#### **Eficiencia en la Comunicación PLC-Robot**  
- La integración del **PLC Allen Bradley** con el controlador **ABB IRC5** permitió una ejecución confiable de la parada de emergencia.  
- No se detectaron retrasos significativos en la comunicación entre los módulos del sistema.  

#### **Funcionamiento del SCADA en Ignition**  
- Se logró visualizar en tiempo real el estado del operario y el nivel de fatiga en la **interfaz SCADA**.  
- Se generaron alarmas de manera automática cuando se superó el umbral de fatiga, con **registro de eventos y generación de reportes históricos**.  
- Se configuraron alertas por **correo electrónico** utilizando Node-RED para notificar a los supervisores cuando un operario presentaba fatiga elevada.  

#### **Limitaciones Identificadas**  
- Se observaron **errores en la detección de fatiga en operarios con gafas o con expresiones neutras prolongadas**.  
- En ambientes con **cambios bruscos de iluminación**, la precisión disminuyó ligeramente.

[![Ver Video](https://img.youtube.com/vi/P3-w4-xeezI/0.jpg)](https://www.youtube.com/watch?v=P3-w4-xeezI)

[![Ver Video](https://img.youtube.com/vi/51PFAXfUmWM/0.jpg)](https://www.youtube.com/watch?v=51PFAXfUmWM)

### 2. Resultados en la Simulación con RobotStudio  

Antes de implementar el sistema en el entorno real, se realizó una **validación en RobotStudio** para verificar el comportamiento del robot ante distintos niveles de fatiga simulados.  

#### **Validación de la Interrupción Automática**  
- Se comprobó que al superar el umbral de fatiga, el **robot se detiene inmediatamente** en la simulación.  
- La comunicación entre el **PLC virtual y el robot** en RobotStudio funcionó de manera estable.  

#### **Simulación del Flujo de Trabajo**  
- Se implementaron diferentes **escenarios de fatiga** para evaluar la robustez del sistema:  
  - Fatiga baja (**<40%**): El robot continúa operando normalmente.  
  - Fatiga moderada (**40%-60%**): Se genera una alerta en el SCADA.  
  - Fatiga crítica (**>60%**): El robot se detiene automáticamente.  

- Se verificó que la **transición entre estados** se reflejara correctamente en la interfaz SCADA.  

#### **Comparación con la Prueba Real**  
- En términos de detección de fatiga, los resultados de la simulación fueron **coherentes con los datos obtenidos en el LabSir**, lo que confirmó la fiabilidad del sistema.  
- La diferencia principal radicó en que en la simulación, la iluminación y las condiciones del entorno fueron **más controladas**, por lo que la precisión en la detección de fatiga fue ligeramente superior.

[![Ver Video](https://img.youtube.com/vi/92MZYH_ESPY/0.jpg)](https://www.youtube.com/watch?v=92MZYH_ESPY

### Conclusiones de las Pruebas  

1. **El sistema logró detectar la fatiga del operario con alta precisión**, permitiendo la interrupción automática del robot en situaciones de riesgo.  
2. **El tiempo de respuesta del sistema fue menor a 1 segundo**, lo que garantiza una acción inmediata en entornos industriales.  
4. **La simulación en RobotStudio validó el comportamiento esperado del robot**, facilitando la implementación en el entorno real.  
5. **Se identificaron mejoras necesarias**, como optimizar el modelo de detección para operarios con gafas y en condiciones de iluminación variable.  

Este sistema representa un avance significativo en la seguridad en **robótica colaborativa**, integrando visión artificial, control industrial y comunicación eficiente mediante **OPC UA y sockets TCP/IP**.  

---

## Conclusiones  

1. **Integración de visión artificial y robótica colaborativa**  
   - Se logró combinar un sistema de detección de fatiga basado en visión artificial con un robot ABB IRB 140, permitiendo la **identificación automática del nivel de fatiga** del operario y la toma de decisiones en tiempo real.  

2. **Automatización de la seguridad en entornos industriales**  
   - La implementación de un **sistema de parada automática del robot** en respuesta a la fatiga del operario reduce el riesgo de accidentes en entornos de robótica colaborativa.  
   - La arquitectura del sistema permite una **respuesta rápida (<1 segundo)** ante niveles críticos de fatiga.  

3. **Eficiencia en la comunicación y supervisión del sistema**  
   - La combinación de **sockets TCP/IP, OPC UA y SCADA** permitió una comunicación fluida entre los diferentes módulos, asegurando **transmisión en tiempo real sin interrupciones**.  

4. **Validación exitosa en entornos simulados y reales**  
   - La **simulación en RobotStudio** confirmó que la detección de fatiga y la interrupción del robot funcionan de manera estable en condiciones controladas.  
   - En el entorno real del **Laboratorio LabSir**, se validó la efectividad del sistema, con un **85% de precisión en la detección de fatiga**.  

5. **Limitaciones y oportunidades de mejora**  
   - Se detectaron **dificultades en la detección de fatiga en operarios con gafas o expresiones neutras prolongadas**, lo que sugiere la necesidad de optimizar los modelos de visión artificial.  
   - En condiciones de **iluminación variable**, la precisión del sistema disminuye levemente, por lo que se recomienda mejorar la adaptabilidad del modelo a diferentes entornos.  
   - Se propone la incorporación de **sensores adicionales (frecuencia cardíaca, temperatura)** para mejorar la detección de fatiga de manera más robusta.  

6. **Potencial de implementación industrial y escalabilidad**  
   - La arquitectura modular del sistema permite su **adaptación a otros robots industriales y procesos productivos**, facilitando la **escalabilidad en diferentes sectores de manufactura**.  
   - Se plantea la posibilidad de una **interfaz móvil** para la supervisión remota de múltiples operarios en entornos industriales más amplios.  

Este proyecto demuestra la viabilidad de un **sistema de monitoreo de fatiga en robótica colaborativa**, integrando tecnologías de visión artificial, comunicación industrial y automatización para mejorar la seguridad en entornos de trabajo.  




