---
lab:
  title: 'Ejercicio 3: Creación de un área de trabajo de Log Analytics para Microsoft Defender for Cloud'
  module: Module 04 - Create a Log Analytics workspace for Microsoft Defender for Cloud
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tiene acceso administrativo. 


Al recopilar registros y datos, la información se almacena en un área de trabajo. Un área de trabajo tiene un identificador de área de trabajo y un identificador de recurso únicos. El nombre del área de trabajo debe ser único para un grupo de recursos determinado. Después de crear un área de trabajo, configure los orígenes de datos y las soluciones para almacenar sus datos allí. 

---

## Tarea de aptitudes

- Crear un área de trabajo de Log Analytics.
- Asociación del área de trabajo a un grupo de recursos existente.
- Especificación de una región específica para la implementación del área de trabajo.

## Instrucciones del ejercicio 

### Utiliza el menú Áreas de trabajo de Log Analytics para crear un área de trabajo.

1. Inicia una sesión en el explorador e inicia sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. En el menú de Azure Portal, introduce las **áreas de trabajo de Log Analytics** en el cuadro de búsqueda. Cuando comiences a escribir, la lista se filtrará en función de la entrada. Selecciona **Áreas de trabajo de Log Analytics**.

4. Selecciona **Crear**.

5. En la pestaña **Básicos** de **Crear área de trabajo de Log Analytics,** introduce o selecciona esta información:
   
   |Configuración|Value|
   |---|---|
   |**Detalles del proyecto**|
   |Subscription|Selecciona tu suscripción.|
   |Grupo de recursos|Escribe **az-rg-1.** Selecciona **Aceptar**.|
   |**Detalles de instancia**|
   |Nombre|Escribe **azwrkspc1a.**|
   |Región|Selecciona **Este de EE. UU**.|

6. Selecciona la **pestaña Revisar y crear** o selecciona el botón azul Revisar y crear situado en la parte inferior de la página.
  
8. Selecciona **Crear**.

> **Resultados:** has creado un área de trabajo de Log Analytics, para recopilar datos de recursos de Azure, y diagnósticos o datos de registro de Azure Storage.
