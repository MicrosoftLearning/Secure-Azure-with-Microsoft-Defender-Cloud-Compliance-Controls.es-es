---
lab:
  title: 'Ejercicio 4: Instalación del agente de Azure Monitor y creación de una regla de recopilación de datos'
  module: Module 05 - Create a data collection rule and install the Azure Monitor Agent
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tiene acceso administrativo. 


Las reglas de recopilación de datos (DCR) especifican los datos que se van a recopilar, mientras que el agente de Azure Monitor aplica estas reglas para recopilar registros y métricas de máquinas virtuales en Azure, otras nubes o entornos locales. Juntos, permiten una supervisión coherente y centralizada en distintos entornos.

---

## Tareas de aptitudes

- Creación de una regla de recopilación de datos.

- Selección de recursos de destino para la recopilación de datos.
  
- Configuración de orígenes y destinos de los datos.

- Selección de los tipos de origen de datos y los datos que se van a recopilar.

- Elección de un destino de entrega de datos.

## Instrucciones del ejercicio 

### Creación de una regla de recopilación de datos.

>**Nota**: crea la regla de recopilación de datos en la misma región que el área de trabajo de Log Analytics de destino o el área de trabajo de Azure Monitor. Puedes asociar la regla de recopilación de datos a máquinas o contenedores de cualquier suscripción o grupo de recursos del inquilino. 
   
1. En el cuadro de búsqueda de la parte superior del portal, escribe las reglas de recopilación de datos. Selecciona Reglas de recopilación de datos en los resultados de la búsqueda.

2. Seleccione **+ Create** (+ Crear).

![Imagen](https://github.com/user-attachments/assets/e428c441-9d8d-4460-acd9-a97e2aa2b5af)

3. En la pestaña **Básicos** del panel **Crear regla de recopilación de datos**, especifica las siguientes opciones de configuración (deja las demás con los valores predeterminados):

    |Configuración|Valor|
    |---|---|
    |**Detalles de la regla**|
    |Nombre de regla|**dcr-1**|
    |Subscription|nombre de la suscripción de Ignite que estás usando en este laboratorio|
    |Resource group|**az-rg-1**|
    |Región|**Este de EE. UU.**|
    |Tipo de plataforma|**Windows**|
    |Punto de conexión de recopilación de datos|*Deja el valor predeterminado de Ninguno*|

![Imagen](https://github.com/user-attachments/assets/eee884f6-b20f-4d51-9310-6e755746ed9a)   

4. Haz clic en el botón denominado **Siguiente: Recursos >** para continuar.

5. En la pestaña Recursos, selecciona **+Agregar recursos**.
  
>**Nota**: el agente de Azure Monitor se instalará automáticamente en las máquinas virtuales (recursos) seleccionadas para recopilar datos.
   
![Imagen](https://github.com/user-attachments/assets/619106b4-7f5e-44dd-98c7-129689ab89c0)

6. En la plantilla Seleccionar un ámbito, activa la casilla **Ignite-subscription** en la selección Ámbito y haz clic en **Aplicar.**

![Imagen](https://github.com/user-attachments/assets/c95b76cd-1515-47a5-b07b-02dcb28c0bf3)


8. Selecciona **Revisar + crear**.








> **Resultados**: has instalado el agente de Azure Monitor y creado una regla de recopilación de datos..
