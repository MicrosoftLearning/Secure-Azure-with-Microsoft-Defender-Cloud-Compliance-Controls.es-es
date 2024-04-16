---
lab:
  title: 'Ejercicio 03a: Habilitación de Defender for Cloud en una suscripción de Azure'
  module: Module 03 - Set up Microsoft Defender for Cloud
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tiene acceso administrativo. 


El objetivo principal de este ejercicio es proporcionar experiencia práctica en la configuración y habilitación de Microsoft Defender for Cloud dentro de una suscripción de Azure. Esto te permitirá supervisar y proteger tus recursos en la nube frente a amenazas de seguridad. 

---

## Tareas de aptitudes

- Actualización de la suscripción de Microsoft Defender for Cloud.
  
- Implementación de Microsoft Monitoring Agent en las máquinas necesarias para una cobertura completa.

## Instrucciones del ejercicio

### Actualización de Microsoft Defender for Cloud

1. Inicia sesión en el [menú de Azure Portal.](https://portal.azure.com/)

2. En Azure Portal, en el cuadro de texto Buscar recursos, servicios y documentos de la parte superior de la página, escriba Microsoft Defender for Cloud y presione la tecla Entrar.

3. En la **hoja Introducción** de **Microsoft Defender for Cloud**, ve a la pestaña **Actualización**. Desplázate hacia abajo hasta que esté visible la sección **Selección de las suscripciones y las áreas de trabajo que se protegerán con características de seguridad mejoradas**.

4. Activa el plan Microsoft Defender seleccionando tu **Suscripción** y el **área de trabajo de Log Analytics** que has creado en el módulo 02.

5. Haz clic en el botón azul grande **Actualizar** situado en la parte inferior de la página.
   
    ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/256bd584-b04f-4d5b-81a7-c83dd1af3b4f)
   
6. En la hoja **Introducción** de **Microsoft Defender for Cloud**, ve a la pestaña **Instalar agentes**, y desplázate hacia abajo.

    ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/8120ec8f-23dc-4636-bc45-b415c7894b8c)

7. Activación de la casilla asociada a la suscripción en la que se instalarán los agentes y haz clic en **Instalar agentes.**

### Acciones alternativas para la actualización de tu suscripción de Microsoft Defender for Cloud.

1. Vaya a **Microsoft Defender for Cloud** y, en el panel de navegación izquierdo de la sección Administración, haga clic en **Configuración del entorno**.
   
2. En la hoja **Microsoft Defender for Cloud, configuración del entorno**, haz clic en **Expandir todo,** desplázate hacia abajo hasta que aparezca tu suscripción y haz clic en la suscripción pertinente.

3. En la hoja **Configuración, planes de Defender**, selecciona **Habilitar todos los planes** y haz clic en **Guardar.**

   ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/4b684851-98ae-4720-a3e3-afa99aab8c43)




   

   
> **Resultados**: has actualizado y habilitado Defender for Cloud en tu suscripción de Azure.
