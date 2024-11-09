---
lab:
  title: 'Ejercicio 02: Creación de una infraestructura de red virtual'
  module: Module 03 - Filter network traffic with a network security group using the Azure portal
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) a la que tienes acceso administrativo. 


Puedes usar un grupo de seguridad de red de Azure para filtrar el tráfico de red que entra y sale de los recursos de Azure en una red virtual de Azure. Los grupos de seguridad de red contienen reglas de seguridad que filtran el tráfico de red por dirección IP, puerto y protocolo. Cuando un grupo de seguridad de red está asociado a una subred, se aplican reglas de seguridad a los recursos implementados en esa subred.

## Diagrama de la arquitectura

![imagen](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/1bfec315-129b-48a9-9c35-1f21c837068f)

---

## Tareas de aptitudes

- Creación de un grupo de seguridad de red y de reglas de seguridad.
  
- Creación de grupos de seguridad de aplicaciones.
  
- Creación de una red virtual y asociar un grupo de seguridad de red a una subred.
  
- Implementación de máquinas virtuales y asociar sus interfaces de red a los grupos de seguridad de aplicación.

## Instrucciones del ejercicio 

### Creación de un grupo de recursos y red virtual de Azure.

>**Nota**: la siguiente tarea crea una red virtual con una subred de recurso.

1. Inicia una sesión en el explorador e inicia sesión en el [menú de Azure Portal.](https://portal.azure.com/)             
   
2. En el cuadro de búsqueda de la parte superior del portal, escribe **Redes virtuales.** En los resultados de la búsqueda, selecciona **Redes virtuales**.

3. En la página **Redes virtuales**, selecciona + **Crear**.

4. En la pestaña **Datos básicos** de **Crear una red virtual**, introduce o selecciona la siguiente información:
   
   |Configuración|Valor|
   |---|---|
   |**Detalles del proyecto**|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Escribe **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre de la red virtual|Escriba **vnet-1**.|
   |Region|Selecciona **(EE. UU.) Este de EE. UU.** .|  
    
5. Selecciona **Siguiente** para ir a la pestaña **Seguridad**.
  
6. Selecciona **Siguiente** para continuar a la pestaña **Direcciones IP**.

7. En el cuadro de espacio de direcciones de **Subredes**, selecciona la subred **predeterminada**.

8. En la plantilla **Editar subred**, escribe o selecciona la siguiente información:

   |Configuración|Valor|
   |---|---|
   |**Detalles de subred**|
   |Propósito de subred|Deja la configuración predeterminada en Predeterminada.|
   |Nombre|Escriba **subnet-1**.|
   |Dirección inicial|Deja la configuración predeterminada en 10.0.0.0/16.|
   |Tamaño de la subred|Deja la configuración predeterminada en /24(256 direcciones).

   ![imagen](https://github.com/user-attachments/assets/4c5834f8-459f-4063-bd82-3e65237c6b1d)

10. Selecciona **Guardar**.

11. Selecciona **Revisar y crear** en la parte inferior de la pantalla y, cuando se supere la validación, selecciona **Crear**.

    ![imagen](https://github.com/user-attachments/assets/4fd02061-2349-42c4-8582-c7178f9b7eb6)

### Creación de grupos de seguridad de aplicaciones para poder agrupar servidores con funciones similares, como los servidores web.

Un grupo de seguridad de aplicaciones (ASG) permite agrupar servidores con funciones similares, como servidores web.

1. En el cuadro de búsqueda que aparece en la parte superior del portal, escribe **Grupo de seguridad de aplicaciones**. Selecciona **Grupos de seguridad de aplicaciones** en los resultados de la búsqueda.

2. En la página **Grupo de seguridad de aplicaciones**, selecciona **Crear**.

3. En la pestaña **Aspectos básicos** de **Crear un grupo de seguridad de aplicaciones**, escribe o selecciona la siguiente información:
   
   |Configuración|Valor|
   |---|---|
   |**Detalles del proyecto**|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Selecciona **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre|Escriba **asg-web**.|
   |Region|Seleccione **Este de EE. UU**.|  
    
4. Seleccione **Revisar + crear**.

5. Selecciona **Crear.**

6. Repite los pasos anteriores, pero especifica los valores siguientes:
    
   |Configuración|Valor|
   |---|---|
   |**Detalles del proyecto**|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Selecciona **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre|Escriba **asg-mgmt**.|
   |Region|Seleccione **Este de EE. UU**.|

7. Seleccione **Revisar + crear**.

8. Selecciona **Crear.**

### Creación de un grupo de seguridad de red para proteger el tráfico de red en tu red virtual.

Un grupo de seguridad de red (NSG) protege el tráfico de red de una red virtual.

1. En el cuadro de búsqueda que aparece en la parte superior del portal, escribe **Grupo de seguridad de red**. En los resultados de la búsqueda, selecciona **Grupos de seguridad de red**.

>**Nota**: en los resultados de búsqueda de grupos de seguridad de red, es posible que veas grupos de seguridad de red (clásicos). Selecciona Grupos de seguridad de red.

2. En la página **Grupos de seguridad de red**, selecciona **+ Crear**.

3. En la pestaña **Aspectos básicos** de **Crear grupo de seguridad de red**, escribe o selecciona esta información:
   
   |Configuración|Valor|
   |---|---|
   |**Detalles del proyecto**|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Selecciona **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre|Escriba **nsg-1**.|
   |Region|Seleccione **Este de EE. UU**.|  
    
4. Seleccione **Revisar + crear**.

5. Selecciona **Crear**.

### Asociación del grupo de seguridad de red a la subred

>**Nota**: en esta tarea, asociarás el grupo de seguridad de red con la subred de la red virtual que has creado anteriormente.

1. En el cuadro de búsqueda que aparece en la parte superior del portal, escribe **Grupo de seguridad de red**. En los resultados de la búsqueda, selecciona **Grupos de seguridad de red**.
   
2. Selecciona **nsg-1**.

3. Selecciona **Subredes** en la sección **Configuración** de **nsg-1**.

4. En la página **nsg-1 | Subredes**, selecciona + **Asociar:**

 ![imagen](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/3b2004f6-963f-43df-9d05-3999d2e97d76)

5. En **Asociación de subred**, selecciona **vnet-1 (test-rg)** en **Red virtual**.

6. En **subnet-1**, selecciona **Subred** y, luego, elige **Aceptar**.

### Creación de reglas de seguridad para el grupo de seguridad de red con la subred de la red virtual que has creado anteriormente.

1. Selecciona **Reglas de seguridad de entrada** en la sección **Configuración** de **nsg-1**.
   
2. En la página **nsg-1 | Reglas de seguridad de entrada**, selecciona + **Agregar:**

3. Crea una regla de seguridad que permita a los puertos 80 y 443 para el grupo de seguridad de la aplicación **asg-web**. En la página **Agregar regla de seguridad de entrada**, especifica o selecciona esta información:

   |Configuración|Valor|
   |---|---|
   |Source|Deje el valor predeterminado, **Cualquiera**.|
   |Source port ranges|Deja la configuración predeterminada en los intervalos de puerto.|
   |Destino|Seleccione **Grupo de seguridad de aplicación**.|
   |Grupos de seguridad de aplicaciones de destino|Seleccione **asg-web**.|
   |Service|Deja la configuración predeterminada en Personalizada.|
   |Intervalos de puertos de destino|Escriba **80 443**.|
   |Protocolo|Seleccione **TCP.**|
   |Action|Deja la configuración predeterminada en Permitir.|
   |Priority|Deja la configuración predeterminada en 100.|
   |Nombre|Introduce **allowweball.**|

4. Seleccione **Agregar**.

5. Completa los pasos anteriores con la siguiente información:

   |Configuración|Valor|
   |---|---|
   |Source|Deje el valor predeterminado, **Cualquiera**.|
   |Source port ranges|Deja la configuración predeterminada en los intervalos de puerto.|
   |Destino|Seleccione **Grupo de seguridad de aplicación**.|
   |Grupo de seguridad de aplicación de destino|Seleccione **asg-mgmt**.|
   |Servicio|Seleccione **RDP**.|
   |Intervalos de puertos de destino|Deja la configuración predeterminada en 3389.|
   |Protocolo|Deja la configuración predeterminada en TCP.|
   |Action|Deja la configuración predeterminada en Permitir.|
   |Priority|Deja la configuración predeterminada en 110.|
   |Nombre|Introduce **allowrdpall.**|
   
6. Seleccione **Agregar**.

### Creación de dos máquinas virtuales (VM) en la red virtual que has creado anteriormente.

1. En el portal, busca y selecciona **Máquinas virtuales**.

2. En **Máquinas virtuales**, selecciona **+ Crear** y, después, **Máquina virtual de Azure**.
   
3. En **Crear una máquina virtual**, escribe o selecciona los datos siguientes en la pestaña **Conceptos básicos**:

   |Configuración|Valor|
   |---|---|
   |**Detalles del proyecto**|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Selecciona **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre de la máquina virtual|Escriba **vm-1**.|
   |Region|Selecciona **(EE. UU.) Este de EE. UU.** .|
   |Opciones de disponibilidad|En el menú desplegable Zona de disponibilidad, selecciona **No se necesita redundancia de la infraestructura**.|
   |Tipo de seguridad|En el menú desplegable Tipo de seguridad, selecciona **Estándar**.|
   |Imagen|En el menú desplegable Imagen, selecciona **Windows Server 2022 Datacenter: Azure Edition - x64 Gen2.**|
   |Arquitectura VM|Deja la configuración predeterminada en x64.|
   |Ejecución de Azure Spot con descuento|Deja la configuración predeterminada en desactivada.|
   |Tamaño|Deja la configuración predeterminada en Standard_D2s_v3-2 VCPU, 8 GiB de memoria.|
   |**Cuenta de administrador**|
   |Tipo de autenticación|Seleccione **Contraseña**.|
   |Nombre de usuario|Escribe **Tenantadmin1.**|
   |Contraseña|Introduce **Superuser#150.**|
   |Confirmar contraseña|Vuelve a introducir **Superuser#150.**|
   |**Reglas de puerto de entrada**|
   |Puertos de entrada públicos|Seleccione **Ninguno**.|
 
4. Selecciona **Siguiente: Discos** y, luego, **Siguiente: Redes**.

5. En la pestaña **Redes**, comprueba o escribe la siguiente información:

   |Configuración|Valor|
   |---|---|
   |**Interfaz de red**|
   |Virtual network|Seleccione **vnet-1**.|
   |Subnet|Seleccione **valor predeterminado (10.0.0.0/24)** .|
   |Dirección IP pública|Deja la configuración predeterminada en nueva IP pública.|
   |Grupo de seguridad de red de NIC|Seleccione **Ninguno**.|
   
6. Selecciona la pestaña **Revisar y crear** o el botón **Revisar y crear** en la parte inferior de la página.

7. Selecciona **Crear**. La máquina virtual puede tardar unos minutos en implementarse.
  
   - Creación de la segunda máquina virtual.

   - Repite los pasos anteriores para crear una segunda máquina virtual denominada **vm-2**.

   - Espera a que las máquinas virtuales terminen de implementarse antes de avanzar a la sección siguiente.

### Asociación de las interfaces de red a un grupo de seguridad de aplicaciones

>**Nota**: cuando creaste las máquinas virtuales, Azure creó una interfaz de red para cada una y la asoció a estas. Agrega la interfaz de red de cada máquina virtual a uno de los grupos de seguridad de aplicaciones que creaste anteriormente:

1. En el cuadro de búsqueda que aparece en la parte superior del portal, escribe **Máquina virtual**. En los resultados de la búsqueda, selecciona **Máquinas virtuales**.

2. Selecciona **vm-1**.
 
3. Selecciona **redes** en la sección de **vm-1**.

4. Selecciona **Grupos de seguridad de aplicaciones** en la sección **Redes** de **vm-1. Selecciona **+ Agregar grupos de seguridad de aplicaciones**.

5. En la plantilla **Agregar grupos de seguridad de aplicaciones**, selecciona **asg-mgmt** en la plantilla **Grupos de seguridad de aplicaciones** y, a continuación, haz clic en el botón **Agregar** en la parte inferior de la página de plantilla.

![imagen](https://github.com/MicrosoftLearning/Secure-Azure-with-Microsoft-Defender-Cloud-Compliance-Controls/assets/91347931/dd17aeba-8e16-431b-b921-527367fea484)

6. Repite los pasos anteriores para **vm-2**, seleccionando **asg-web** en la plantilla **Grupos de seguridad de aplicaciones**.

> **Resultados**: has creado una infraestructura de red virtual y filtrado el tráfico de red con un grupo de seguridad de red con Azure Portal.

> **Nota**: no elimines los recursos de este laboratorio, ya que son necesarios para los siguientes ejercicios: Ejercicio 05: Habilitar el acceso Just-In-Time en máquinas virtuales, Ejercicio 06a: Configuración de firewall y redes virtuales de Key Vault.
