# Implementación de un Entorno de Robótica Colaborativa con Detección de Fatiga Basada en Visión Artificial

## Descripción General

El avance de la **robótica colaborativa** ha permitido una interacción más segura y eficiente entre humanos y robots en entornos industriales. Sin embargo, la seguridad del operario sigue siendo un desafío crítico, ya que factores como la **fatiga** pueden afectar su capacidad de respuesta, aumentar la probabilidad de errores y comprometer la seguridad del sistema en general. 

Este proyecto propone un sistema basado en **visión artificial** que monitorea el estado de fatiga de un operario y actúa en tiempo real para detener la operación de un **robot ABB IRB 140** en caso de riesgo. Para lograrlo, se implementó una solución de detección de fatiga utilizando una **cámara Intel RealSense D435**, **redes neuronales para el análisis de gesticulaciones faciales**, y un **PLC Allen Bradley Logix 5000** que interrumpe el funcionamiento del robot en caso de detectar niveles de fatiga críticos. Además, el sistema emplea una **arquitectura de ticket de comunicaciones**, asegurando un flujo de datos robusto y confiable entre los distintos componentes.

## Objetivos del Proyecto

- Diseñar e implementar un sistema de **detección de fatiga basado en visión artificial**.  
- Integrar una solución de **control reactivo** que garantice la seguridad del operario mediante la interrupción automática del robot en caso de fatiga.  
- Validar la **precisión y tiempo de respuesta** del sistema en un entorno controlado.  
- Desarrollar una **arquitectura de ticket de comunicaciones**
