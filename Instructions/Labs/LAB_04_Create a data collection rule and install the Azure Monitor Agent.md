---
lab:
  title: 'Ejercicio 4: Instalación del agente de Azure Monitor y creación de una regla de recopilación de datos'
  module: Module 05 - Collect guest operating system monitoring data from Azure and hybrid virtual machines using Azure Monitor Agent
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tienes acceso administrativo. 


Las reglas de recopilación de datos (DCR) especifican los datos que se van a recopilar, mientras que el agente de Azure Monitor aplica estas reglas para recopilar registros y métricas de máquinas virtuales en Azure, otras nubes o entornos locales. Juntos, permiten una supervisión coherente y centralizada en distintos entornos.

---

## Tareas de aptitudes

- Creación de una regla de recopilación de datos.

- Selección de recursos de destino para la recopilación de datos.

- Instala un agente de Azure Monitor.
  
- Configuración de orígenes y destinos de los datos.

- Selección de los tipos de origen de datos y los datos que se van a recopilar.

- Elección de un destino de entrega de datos.

## Instrucciones del ejercicio 

### Instala el agente de Azure Monitor y crea y define una regla de recopilación de datos.

>**Nota**: crea la regla de recopilación de datos en la misma región que el área de trabajo de Log Analytics o el área de trabajo de Azure Monitor. Puedes asociarla a máquinas o contenedores de cualquier suscripción o grupo de recursos del inquilino. El agente de Azure Monitor se instalará automáticamente en los recursos virtuales de Azure.

1. Inicia una sesión en el explorador e inicia sesión en el [menú de Azure Portal.](https://portal.azure.com/)
  
3. En el cuadro de búsqueda de la parte superior del portal, escribe las **reglas de recopilación de datos.** Selecciona **Reglas de recopilación de datos** en los resultados de la búsqueda.
  
4. En la página **Reglas de recopilación de datos**, selecciona **+ Crear.**
  
    ![image](https://github.com/user-attachments/assets/a472bc6f-fa96-4615-a67c-c99e8b9ce7a4)

5. En la página **Aspectos básicos** del **panel Crear regla de recopilación de datos**, especifica la siguiente configuración (deja lo demás con los valores predeterminados):

    |Configuración|Valor|
    |---|---|
    |**Detalles de la regla**|
    |Nombre de regla|**dcr-1**|
    |Suscripción|Selecciona tu suscripción.|
    |Grupo de recursos|**az-rg-1**|
    |Región|**Este de EE. UU.**|
    |Tipo de plataforma|**Windows**|
    |Punto de conexión de recopilación de datos|Deja la configuración predeterminada en Ninguno|

   ![image](https://github.com/user-attachments/assets/6c63c48f-f7a9-4fb2-8fc0-e22084cd5013)

6. Haz clic en el botón situado en la parte inferior de la página **Aspectos básicos** con la etiqueta **Siguiente: Recursos > continuar.**
   
7. En la página **Recursos**, selecciona **+ Agregar recursos.**

   ![image](https://github.com/user-attachments/assets/7e45996b-478b-4be4-9df3-df6127da6cb4)

8. En la plantilla **Seleccionar un ámbito**, activa la casilla **Suscripción** en la selección **Ámbito.**

   ![image](https://github.com/user-attachments/assets/0d228e47-039e-4418-ae66-025957e368bc)

9. En la parte inferior de la plantilla **Seleccionar un ámbito**, haz clic en **Aplicar.**
  
10. En la parte inferior de la página **Recursos**, selecciona **Siguiente: Recopilar y entregar >.**

    ![image](https://github.com/user-attachments/assets/95556211-654f-4810-98a0-5cd8fac13bff)  

11. En la **página Recopilar y entregar**, haz clic en **+ Agregar origen de datos.**

    ![image](https://github.com/user-attachments/assets/8274b0c1-8617-4889-9aef-78e050f2bd00)

12. En la plantilla **Agregar origen de datos**, en **Tipo de origen de datos**, selecciona la siguiente configuración:
    
    |Configuración|Valor|
    |---|---|
    |**Agregar origen de datos**|
    |Selecciona el tipo de origen de datos y los datos que se recopilarán para los recursos.|
    |Tipo de origen de datos*|**Registros de eventos de Windows**|
    |Elige Aspectos básicos para habilitar la recopilación de registros de eventos.|
    |Configura los niveles y registros de eventos que se van a recopilar:|
    |Aplicación|**Crítico**, **Error**, **Advertencia**|
    |Seguridad|**Auditoría correcta**, **Error de auditoría**|
    |Sistema|**Crítico**, **Error**, **Advertencia**|

    ![image](https://github.com/user-attachments/assets/33039994-0613-40f4-9c55-03f795b38b9b)

13. En la parte inferior de la plantilla **Agregar origen de datos**, selecciona **Siguiente: Destino >.**

14. En la plantilla **Agregar origen de datos**, en la pestaña **Destino**, selecciona la siguiente configuración.
    
    |Configuración|Valor|
    |---|---|
    |**Agregar origen de datos**|
    |Destino|**+ Incorporación del destino**|
    |Tipo de destino|**Registros de Azure Monitor**|
    |Suscripción|Selecciona tu suscripción.|
    |Detalles del destino|**azwrkspc1a (az-rg-1**)|

     ![image](https://github.com/user-attachments/assets/dc2d2906-4a57-4df9-a33c-fd6ae34a8457)

15. En la parte inferior de la plantilla **Agregar origen de datos**, selecciona **Agregar origen de datos.**

16. En la parte inferior de la página **Recopilar y entregar**, selecciona **Revisar + crear.**

    ![image](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

17. En la parte inferior de la página **Revisar + crear**, selecciona **Crear.**

    ![image](https://github.com/user-attachments/assets/b532f92e-af10-4b4d-bb52-10d15ad38d4a)

> **Resultados**: has instalado el agente de Azure Monitor y creado una regla de recopilación de datos.
