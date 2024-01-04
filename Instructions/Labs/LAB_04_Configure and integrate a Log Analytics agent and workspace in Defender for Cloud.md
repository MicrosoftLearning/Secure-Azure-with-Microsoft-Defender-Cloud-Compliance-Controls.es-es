---
lab:
  title: "Ejercicio 04: Recopilación de datos de las cargas de trabajo con el agente de Log\_Analytics"
  module: Module 04 - Configure and integrate a Log Analytics agent and workspace in Defender for Cloud
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tiene acceso administrativo. 


Defender for Cloud recopila datos de las máquinas virtuales de Azure, los conjuntos de escalado de máquinas virtuales, los contenedores de IaaS y máquinas que no son de Azure (incluidas las del entorno local) para supervisar las amenazas y vulnerabilidades de seguridad. Algunos planes de Defender requieren componentes de supervisión para recopilar datos de las cargas de trabajo. Si el agente de Log Analytics está activado, Defender for Cloud lo implementará en todas las VM de Azure compatibles y en las nuevas que se hayan creado. 

---

## Tareas de aptitudes

- Usa los valores predeterminados del agente de Log Analytics para tu tipo de agente.

- Seleccione su área de trabajo.
  
- Define el nivel de datos de eventos de seguridad que se almacenarán en el nivel del área de trabajo.

## Instrucciones del ejercicio 

### Configuración de la integración con el agente de Log Analytics.

>**Nota**: Cuando el agente de Log Analytics está activado, Defender for Cloud implementa el agente en todas las máquinas virtuales de Azure compatibles y en las nuevas que se hayan creado. 

1. Inicie una sesión en el explorador e inicie sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. En el menú de Defender for Cloud, abra **Parámetros del entorno**.

4. Seleccione su suscripción.

5. En la columna Cobertura de configuración y supervisión de los planes de Defender, selecciona **Configuración y supervisión.**

7. En la fila de Log Analytics, en la columna Configuración, haz clic en **Editar configuración.**

8. En la plantilla de configuración de aprovisionamiento automático, completa las siguientes acciones:

   - En Selección de área de trabajo, haz clic en **Área de trabajo personalizada.**

   - Haz clic en el **menú desplegable** y **selecciona** el área de trabajo que has creado previamente.

   - En **Almacenamiento de eventos de seguridad**, haz clic en el **menú desplegable** y selecciona **Todos los eventos.**

   - Haz clic en **Aplicar** en la parte inferior de la plantilla de aprovisionamiento automático.
   
![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/c1c812e7-b5ca-4caa-b8e6-34a6e4b325fd)




> **Resultados**: has configurado el agente y el área de trabajo de Log Analytics en Microsoft Defender for Cloud.
