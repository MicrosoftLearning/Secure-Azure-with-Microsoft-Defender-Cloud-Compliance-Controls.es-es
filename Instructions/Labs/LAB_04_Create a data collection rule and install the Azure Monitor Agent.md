---
lab:
  title: 'Ejercicio 4: Instalación del agente de Azure Monitor y creación de una regla de recopilación de datos'
  module: Module 05 - Collect guest operating system monitoring data from Azure and hybrid virtual machines using Azure Monitor Agent
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tiene acceso administrativo. 


Las reglas de recopilación de datos (DCR) especifican los datos que se van a recopilar, mientras que el agente de Azure Monitor aplica estas reglas para recopilar registros y métricas de máquinas virtuales en Azure, otras nubes o entornos locales. Juntos, permiten una supervisión coherente y centralizada en distintos entornos.

---

## Tareas de aptitudes

- Creación de una regla de recopilación de datos.

- Selección de recursos de destino para la recopilación de datos.

- Instale un agente de Azure Monitor.
  
- Configuración de orígenes y destinos de los datos.

- Selección de los tipos de origen de datos y los datos que se van a recopilar.

- Elección de un destino de entrega de datos.

## Instrucciones del ejercicio 

### Instala el agente de Azure Monitor y crea y define una regla de recopilación de datos.

>**Nota**: crea la regla de recopilación de datos en la misma región que el área de trabajo de Log Analytics o el área de trabajo de Azure Monitor. Puedes asociarla a máquinas o contenedores de cualquier suscripción o grupo de recursos del inquilino. El agente de Azure Monitor se instalará automáticamente en los recursos virtuales de Azure.

1. En el cuadro de búsqueda de la parte superior del portal, escribe las **reglas de recopilación de datos.** Selecciona **Reglas de recopilación de datos** en los resultados de la búsqueda.
  
2. En la página **Reglas de recopilación de datos**, selecciona **+ Crear.**
  
   ![imagen](https://github.com/user-attachments/assets/99b9ac51-f2f4-466f-80bb-79d74874b573)

3. En la página **Aspectos básicos** del **panel Crear regla de recopilación de datos**, especifica la siguiente configuración (deja lo demás con los valores predeterminados):

    |Configuración|Valor|
    |---|---|
    |**Detalles de la regla**|
    |Nombre de regla|**dcr-1**|
    |Suscripción|Selecciona tu suscripción.|
    |Resource group|**az-rg-1**|
    |Región|**Este de EE. UU.**|
    |Tipo de plataforma|**Windows**|
    |Punto de conexión de recopilación de datos|Deja la configuración predeterminada en Ninguno|

    ![imagen](https://github.com/user-attachments/assets/35c527cf-499d-44b9-966f-0114b8643ef2)

4. Haz clic en el botón situado en la parte inferior de la página **Aspectos básicos** con la etiqueta **Siguiente: Recursos > continuar.**
   
5. En la página **Recursos**, selecciona **+ Agregar recursos.**

    ![imagen](https://github.com/user-attachments/assets/6aabf2c9-bea2-47c1-9b0b-bf131cdec4e3)

6. En la plantilla **Seleccionar un ámbito**, activa la casilla **Suscripción** en la selección **Ámbito.**

    ![imagen](https://github.com/user-attachments/assets/2215e8cd-5047-4fc6-91ba-b2c645571bbd)

7. En la parte inferior de la plantilla **Seleccionar un ámbito**, haz clic en **Aplicar.**
  
8. En la parte inferior de la página **Recursos**, selecciona **Siguiente: Recopilar y entregar >.**

    ![imagen](https://github.com/user-attachments/assets/717226c3-5ce0-454f-93a4-11b0e67d5a23)

9. En la **página Recopilar y entregar**, haz clic en **+ Agregar origen de datos.**

    ![imagen](https://github.com/user-attachments/assets/0809cf5b-a460-40d1-8508-e42ba7ce78c1)

10. En la plantilla **Agregar origen de datos**, en **Tipo de origen de datos**, selecciona la siguiente configuración.
    
    |Configuración|Valor|
    |---|---|
    |**Agregar origen de datos**|
    |Seleccione el tipo de origen de datos y los datos que se recopilarán para los recursos.|
    |Tipo de origen de datos*|**Registros de eventos de Windows**|
    |Elige Aspectos básicos para habilitar la recopilación de registros de eventos.|
    |Configura los niveles y registros de eventos que se van a recopilar:|
    |Application|**Crítico**, **Error**, **Advertencia**|
    |Seguridad|**Auditoría correcta**, **Error de auditoría**|
    |Sistema|**Crítico**, **Error**, **Advertencia**|

    ![imagen](https://github.com/user-attachments/assets/5bc891ea-8cef-4baa-95c4-a432364179b1)

12. En la parte inferior de la plantilla **Agregar origen de datos**, selecciona **Siguiente: Destino >.**
   
13. En la plantilla **Agregar origen de datos**, en la pestaña **Destino**, selecciona la siguiente configuración.
    
    |Configuración|Valor|
    |---|---|
    |**Agregar origen de datos**|
    |Destino|**+ Incorporación del destino**|
    |Tipo de destino|**Registros de Azure Monitor**|
    |Suscripción|Seleccione su suscripción.|
    |Detalles del destino|**azwrkspc1a (az-rg-1**)|

    ![imagen](https://github.com/user-attachments/assets/e00c17c8-5a70-4caa-8504-92f482cc5e57)

14. En la parte inferior de la plantilla **Agregar origen de datos**, selecciona **Agregar origen de datos.**

    ![imagen](https://github.com/user-attachments/assets/4277089c-971c-4334-a49d-6ac6bfe93ff4)

15. En la parte inferior de la página **Recopilar y entregar**, selecciona **Revisar + crear.**

    ![imagen](https://github.com/user-attachments/assets/0235fed9-6309-444c-9269-b9dbd1118b63)

16. En la parte inferior de la página **Revisar + crear**, selecciona **Crear.**

> **Resultados**: has instalado el agente de Azure Monitor y creado una regla de recopilación de datos.
