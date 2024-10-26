---
lab:
  title: 'Ejercicio 07: Conexión a un servidor de Azure SQL mediante un punto de conexión privado de Azure con Azure Portal'
  module: Module 08 - Connect to an Azure SQL server using an Azure Private Endpoint using the Azure portal
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tiene acceso administrativo. 


Un punto de conexión privado de Azure es el bloque de creación fundamental para Private Link en Azure. Permite que los recursos de Azure, como las máquinas virtuales (VM), se comuniquen de manera privada y segura con los recursos de Private Link, como el servidor de Azure SQL.

---

## Tareas de aptitudes

- Crear una red virtual y un host bastión.
  
- Cree una máquina virtual.
  
- Crear un servidor SQL de Azure y un punto de conexión privado.
  
- Probar la conectividad con el punto de conexión privado del servidor SQL.

## Instrucciones del ejercicio 

### Creación de un grupo de recursos y una red virtual.

>**Nota**: El host bastión se utilizará para conectarse de forma segura a la máquina virtual a fin de probar el punto de conexión privado. 

1. Inicie una sesión en el explorador e inicie sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. En el cuadro de búsqueda de la parte superior del portal, escribe **Redes virtuales.** En los resultados de la búsqueda, seleccione **Redes virtuales**.

3. En la página **Redes virtuales**, seleccione **+ Crear**.

4. En la pestaña **Aspectos básicos** de **Crear red virtual**, escriba o seleccione esta información:
   
   |Configuración|Value|
   |---|---|
   |**Detalles del proyecto**|
   |Subscription|Selecciona tu suscripción.|
   |Resource group|Selecciona **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre de la red virtual|Escribe **vnet-2.**|
   |Region|Seleccione **(EE. UU.) Este de EE. UU.** .|  
    
5. Seleccione **Siguiente** para ir a la pestaña **Seguridad**.
  
6. Seleccione **Habilitar Azure Bastion** en la sección Azure Bastion de la pestaña Seguridad.

   >**Nota**: Azure Bastion es un servicio de pago que proporciona conectividad RDP y SSH segura a las máquinas virtuales a través de TLS. Cuando se conecta a través de Azure Bastion, las máquinas virtuales no necesitan una dirección IP pública. 

7. Escribe o selecciona la siguiente información en el campo **Azure Bastion**:

   |Configuración|Value|
   |---|---|
   |**Detalles del proyecto**|
   |Host de Azure Bastion |Escribe **az-bastionhost-1a.**|
   |Nombre de la dirección IP pública de Azure Bastion|Seleccione **Crear una dirección IP pública**|
   |Incorporación de una dirección IP pública|Seleccione **Aceptar**|

9. Seleccione **Siguiente** para continuar a la pestaña **Direcciones IP**.

10. En el cuadro **espacio de direcciones IPv4** configurado existente debajo de la columna **Subredes**, haz clic en la entrada **predeterminada**.

11. En la plantilla **Editar subred**, escriba o seleccione la siguiente información:

    |Configuración|Value|
    |---|---|
    |**Detalles del proyecto**|
    |Propósito de subred|Deja la configuración predeterminada en Predeterminada.|
    |Nombre|**subnet-2**|
    |Intervalo de direcciones IPv4|Deja la configuración predeterminada en 10.0.0.0/16.|
    |Dirección inicial|Deja la configuración predeterminada en /24 (256 direcciones).|

13. En la parte inferior de la página **Editar subred**, selecciona **Guardar.**

14. En la parte inferior de la página **Direcciones IP**, selecciona **Revisar + crear.**

    >**Nota**: La implementación de Bastion puede tardar hasta 15 minutos en completar la creación de instancias.

15. En la parte inferior de la página **Revisar + crear**, selecciona **Crear.**
 
### Cree una máquina virtual.

>**Nota**: En esta tarea, crearás una máquina virtual que se usará para probar el punto de conexión privado.

1. En el portal, busque y seleccione **Máquinas virtuales**.

2. En **Máquinas virtuales**, seleccione **+ Crear** y, después, **Máquina virtual de Azure**.

3. En Crear una máquina virtual, escribe o selecciona esta información en la página **Aspectos básicos**:

   |Configuración|Value|
   |---|---|
   |**Detalles del proyecto**|
   |Suscripción|Seleccione su suscripción.|
   |Resource group|Selecciona **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre de la máquina virtual|Escribe **vm-3.**|
   |Region|Seleccione **(EE. UU.) Este de EE. UU.** .|
   |Opciones de disponibilidad|En el menú desplegable Zona de disponibilidad, seleccione **No se necesita redundancia de la infraestructura**.|
   |Tipo de seguridad|En el menú desplegable Tipo de seguridad, seleccione **Estándar**.|
   |Imagen|Seleccione **Windows Server 2022 Datacenter - x64 Gen2**.|
   |Arquitectura VM|Seleccione **x64**.|
   |Ejecución de Azure Spot con descuento|Deja la configuración predeterminada en desactivada.|
   |Size|Deja la configuración predeterminada en Standard_D2s_v3-2 VCPU, 8 GiB de memoria.|
   |**Cuenta de administrador**|
   |Nombre de usuario|Escribe **Tenantadmin2.**|
   |Contraseña|Introduce **Superuser#170.**|
   |Confirmar contraseña|Vuelve a introducir **Superuser#170.**|
   |**Reglas de puerto de entrada**|
   |Selección de puertos de entrada|Seleccione **Ninguno**.|

5. Seleccione **Siguiente: Discos** y, luego, **Siguiente: Redes**.
  
6. En la página **Redes**, escribe o selecciona esta información:

   |Configuración|Valor|
   |---|---|
   |**Interfaz de red**|
   |Virtual network|Seleccione **vnet-2**.|
   |Subnet|Selecciona **subnet-2 (10.0.0.0/24).**|
   |Dirección IP pública|Seleccione **Ninguno**.|
   |Grupo de seguridad de red de NIC|Seleccione **Básica**.|
   |Puertos de entrada públicos|Seleccione **Ninguno**.|
   |Selección de puertos de entrada|Deja la configuración predeterminada vacía.|
   |Eliminar NIC al eliminar la VM|Deja activada la configuración predeterminada en Habilitar redes aceleradas.|
   |Equilibrio de carga|Deja la configuración predeterminada en Ninguno.|
  
6. Seleccione **Revisar + crear**.

7. Revise la configuración y, a continuación, seleccione **Crear**.

### Creación de un servidor SQL de Azure y un punto de conexión privado

>**Nota**: En esta tarea, crearás un SQL Server en Azure.

1. En el cuadro de búsqueda de la parte superior del portal, escribe **SQL Database.** Seleccione **Bases de datos SQL** en los resultados de la búsqueda.

2. En la página **Bases de datos SQL**, selecciona **+Crear.**
   
3. En la pestaña **Básico** de **Crear base de datos SQL**, escriba o seleccione esta información:

   |Configuración|Value|
   |---|---|
   |**Detalles del proyecto**|
   |Subscription|Selecciona tu suscripción.|
   |Resource group|Selecciona **az-rg-1.**|
   |**Detalles de la base de datos**|
   |Nombre de la base de datos|Escribe **az-sql-db1a.**|
   |Nombre del servidor|Escribe **az-sql-svr1a.** Si el nombre ya existe, cree uno único.|
   |Location|Seleccione **(EE. UU.) Este de EE. UU.** .|
   |**Autenticación**|
   |Método de autenticación|Seleccione **Uso de la autenticación de SQL**.|
   |Inicio de sesión del administrador del servidor|Escribe **Tenantadmin2.**|
   |Contraseña|Introduce **Superuser#170.**|
   |Confirmación de la contraseña|Introduce **Superuser#170.**|

4. Seleccione **Aceptar**.
   
   |Configuración|Value|
   |---|---|
   |**Detalles de la base de datos**|
   |¿Quiere usar un grupo elástico de SQL?|Deja la configuración predeterminada en No.|
   |Entorno de la carga de trabajo|Deja la configuración predeterminada en Desarrollo.|
   |Proceso y almacenamiento|Deja la configuración predeterminada en Uso general: sin servidor.|
   |**Redundancia del almacenamiento de copia de seguridad**|
   |Redundancia del almacenamiento de copia de seguridad|Seleccione **Almacenamiento de copias de seguridad con redundancia local**.|
   
5. Seleccione la pestaña **Redes** o el botón **Siguiente: Redes**.

6. En la pestaña **Redes**, escriba o seleccione esta información:

   |Configuración|Valor|
   |---|---|
   |**Conectividad de red**|
   |Método de conectividad|Seleccione **Punto de conexión privado**.|
   |Directiva de conexión|Deja la configuración predeterminada en Predeterminado: usa la directiva Redirigir para todas las conexiones de cliente que se originan dentro de Azure (excepto las conexiones de punto de conexión privado) y Proxy para todas las conexiones de cliente que se originan fuera de Azure.|
   |Conexiones de cifrado|Deja la configuración predeterminada en TLS.12|

7. Seleccione **+ Agregar punto de conexión privado** en **Puntos de conexión privados**.

8. En **Crear un punto de conexión privado**, escriba o seleccione esta información:

   |Configuración|Valor|
   |---|---|
   |Suscripción|Selecciona tu suscripción.|
   |Resource group|Selecciona **az-rg-1.**|
   |Location|Seleccione **Este de EE. UU**.|
   |Nombre|Escribe **az-pe-1a.**|
   |Recurso secundario de destino|Deja la configuración predeterminada en SqlServer.|
   |**Redes**|
   |Virtual network|Seleccione **vnet-2**.|
   |Subnet|Selecciona **subnet-2.**|
   |**Integración de DNS privado**|
   |Integración con una zona DNS privada|Deja la configuración predeterminada en Sí.|
   |Zona DNS privada|Deja la configuración predeterminada (nuevo) privatelink.database.windows.net.|

9. Seleccione **Aceptar**.

10. Seleccione **Revisar + crear**.

11. Seleccione **Crear**.

### Deshabilitación del acceso público al servidor lógico de Azure SQL

>**Nota**: Para este escenario, supongamos que quieres deshabilitar todo el acceso público a Azure SQL Server y permitir solo las conexiones desde tu red virtual. La configuración **Acceso público** puede tener como valor predeterminado **Deshabilitar.**

1. En el cuadro de búsqueda de Azure Portal, escribe **az-sql-svr1a** o el nombre del servidor que especificaste en los pasos anteriores.

2. Selecciona **Redes** en la sección **Seguridad** de **az-sql-svr1a.** En la página **Redes**, seleccione la pestaña **Acceso público** y, luego, seleccione **Deshabilitar** para **Acceso a una red pública**.

   ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/44ff5c24-70cf-49ed-b2ab-5e210c478b3a)

3. Seleccione **Guardar**.

### Prueba de la conectividad con el punto de conexión privado

>**Nota**: En esta tarea, utilizarás la máquina virtual que has creado en los pasos anteriores para conectarte a SQL Server con el punto de conexión privado.

1. En el panel de navegación de la izquierda, seleccione **Grupos de recursos**.

2. Selecciona **az-rg-1.**

3. Selecciona **vm-3.**

4. En la página de información general de **vm-3**, selecciona Conectar, y luego, **Bastion.**

5. Introduce el nombre de usuario **Tenantadmin2** y la contraseña **Superuser#170** que has introducido durante la creación de la máquina virtual.

   **Importante:** Ve a la configuración de Edge/elementos emergentes y redirige/y cambia el conmutador Bloqueado a **desactivado,** antes de seleccionar Conectar.

7. Seleccione el botón **Conectar**.
  
8. Abra Windows PowerShell en el servidor después de conectarse.

9. Introduce `nslookup sqlserver-name.database.windows.net.` Sustituir **sqlserver-name** por el nombre de SQL Server que has creado en los pasos anteriores. Recibirá un mensaje similar al que se muestra a continuación:

   ````  
   Server:  UnKnown
   Address:  168.63.129.16
   
   Non-authoritative answer:
   Name:    az-sql-svr1a.privatelink.database.windows.net
   Address:  10.1.0.5
   Aliases:  az-sql-svr1a.database.windows.net
   ````
    
>**Nota**: se devuelve una dirección IP privada de 10.1.0.5 para el nombre de SQL Server. Esta dirección se encuentra en la subred **az-sql-svr1a** de la red virtual **vnet-2** que has creado anteriormente.

9. Instala [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) en **vm-3.**
 
10. Abra **SQL Server Management Studio**.

11. En **Conectar con el servidor**, escriba o seleccione esta información:

    |Configuración|Value|
    |---|---|
    |Tipo de servidor|Seleccione **Motor de base de datos**.|
    |Nombre de servidor|Escribe **az-sql-svr1a.database.windows.net.**|
    |Autenticación|Seleccione **Autenticación de SQL Server**.|
    |Nombre de usuario|Escribe **Tenantadmin2**.|
    |Contraseña|Introduce **Superuser#170**.|
    |Recordar contraseña|Seleccione **Sí**.|
    |Seguridad de la conectividad|
    |Cifrado|Deja el valor predeterminado en Obligatorio.|
   
13. Seleccione **Conectar**.

14. Examine las bases de datos en el menú izquierdo.

15. Cierra la conexión de escritorio remoto a vm-3.
  
> **Resultados**: te has conectado a un Azure SQL Server con un punto de conexión privado de Azure con Azure Portal.
