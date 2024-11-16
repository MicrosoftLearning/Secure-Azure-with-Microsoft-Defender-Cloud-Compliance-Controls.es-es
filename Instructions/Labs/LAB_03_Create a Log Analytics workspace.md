---
lab:
  title: "Ejercicio\_03: Creación de un área de trabajo de Log Analytics"
  module: Module 04 - Create a Log Analytics workspace
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tienes acceso administrativo. 


Al recopilar registros y datos, la información se almacena en un área de trabajo. Un área de trabajo tiene un identificador de área de trabajo y un identificador de recurso únicos. El nombre del área de trabajo debe ser único para un grupo de recursos determinado. Después de crear un área de trabajo, configura los orígenes de datos y las soluciones para almacenar sus datos allí. 

---

## Tarea de aptitudes

- Crear un área de trabajo de Log Analytics.
- Asociación del área de trabajo a un grupo de recursos existente.
- Especificación de una región específica para la implementación del área de trabajo.

## Instrucciones del ejercicio 

### Utiliza el menú Áreas de trabajo de Log Analytics para crear un área de trabajo.

1. Inicia una sesión en el explorador e inicia sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. En el cuadro de búsqueda de la parte superior del portal, escribe **áreas de trabajo de Log Analytics.** Selecciona **Áreas de trabajo de Log Analytics** en los resultados de la búsqueda.

3. En la página **Áreas de trabajo de Log Analytics**, selecciona **+ Crear.**

4. En la página **Aspectos básicos** de **Crear área de trabajo de Log Analytics,** introduce o selecciona esta información:
   
   |Configuración|Valor|
   |---|---|
   |**Detalles del proyecto**|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Escribe **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre|Escribe **azwrkspc1a.**|
   |Región|Seleccione **Este de EE. UU**.|

5. Selecciona la pestaña **Revisar + crear** de la parte inferior de la página.
  
6. Selecciona **Crear.**

> **Resultados:** has creado un área de trabajo de Log Analytics, para recopilar datos de recursos de Azure.
