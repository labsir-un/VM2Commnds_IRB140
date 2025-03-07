# Implementación de un Entorno de Robótica Colaborativa con Detección de Fatiga Basada en Visión Artificial

## Descripción General

El avance de la **robótica colaborativa** ha permitido una interacción más segura y eficiente entre humanos y robots en entornos industriales. Sin embargo, la seguridad del operario sigue siendo un desafío crítico, ya que factores como la **fatiga** pueden afectar su capacidad de respuesta, aumentar la probabilidad de errores y comprometer la seguridad del sistema en general. 

Este proyecto propone un sistema basado en **visión artificial** que monitorea el estado de fatiga de un operario y actúa en tiempo real para detener la operación de un **robot ABB IRB 140** en caso de riesgo. Para lograrlo, se implementó una solución de detección de fatiga utilizando una **cámara Intel RealSense D435**, **redes neuronales para el análisis de gesticulaciones faciales**, y un **PLC Allen Bradley Logix 5000** que interrumpe el funcionamiento del robot en caso de detectar niveles de fatiga críticos. Además, el sistema emplea una **arquitectura de ticket de comunicaciones**, asegurando un flujo de datos robusto y confiable entre los distintos componentes.

## Objetivos del Proyecto

- Desarrollar un sistema de detección de fatiga basado en visión artificial que permita monitorear en tiempo real el estado de alerta del operario, utilizando análisis de gesticulaciones faciales como un indicador del nivel de fatiga.

- Integrar un mecanismo de control proactivo que interrumpa automáticamente la operación del robot ABB IRB 140 al detectar signos de fatiga excesiva, garantizando así la seguridad del operario y reduciendo la probabilidad de accidentes en entornos de robótica colaborativa.

- Comparar la comunicación entre los módulos del sistema mediante la implementación de diferentes arquitectura de comunicaciones, asegurando un flujo de información eficiente entre la visión artificial y el controlador IRC5 del robot.

- Diseñar una solución escalable y adaptable a diferentes entornos industriales, considerando la posibilidad de futuras mejoras como la integración de sensores fisiológicos complementarios (ritmo cardíaco, temperatura corporal) y la optimización de los algoritmos de detección para condiciones de iluminación variables.

## ⚙ Metodología y Arquitectura del Sistema  

El sistema de detección de fatiga está estructurado en varias etapas clave:  

### Captura y Procesamiento de Imágenes  
Se utiliza una **cámara Intel RealSense D435** para capturar imágenes en tiempo real del operario.  
Se aplican **algoritmos de visión artificial** para identificar signos de fatiga, considerando:  
   - Apertura ocular  
   - Frecuencia de parpadeo  
   - Expresiones faciales  

La información visual es procesada mediante un **modelo de redes neuronales preentrenadas** capaz de **clasificar el nivel de fatiga**.  

[![Ver Video](https://img.youtube.com/vi/Hj6JkPNJw48/0.jpg)](https://www.youtube.com/watch?v=Hj6JkPNJw48)



