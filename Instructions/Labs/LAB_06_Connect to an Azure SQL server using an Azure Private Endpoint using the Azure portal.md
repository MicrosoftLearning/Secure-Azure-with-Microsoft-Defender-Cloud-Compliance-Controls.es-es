---
lab:
  title: 'Ejercicio 06: Implementar una máquina virtual para probar la conectividad de forma privada y segura a SQL Server mediante el punto de conexión privado'
  module: Module 06 - Connect to an Azure SQL server using an Azure Private Endpoint using the Azure portal
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
   
2. En el menú de Azure Portal, selecciona + **Crear un recurso** > **Redes** > **Red virtual,** o busca Red virtual en el cuadro de búsqueda del portal.

3. Seleccione **Crear**.

4. En la pestaña **Aspectos básicos** de **Crear red virtual**, escriba o seleccione esta información:
   
   |Configuración|Value|
   |---|---|
   |**Detalles del proyecto**|
   |Subscription|Seleccione su suscripción.|
   |Resource group|Seleccione **Crear nuevo**. Escribe **CreateSQLEndpointTutorial.** Seleccione **Aceptar**.|
   |**Detalles de instancia**|
   |Nombre de la red virtual|Escribe **myVNet1a.**|
   |Region|Seleccione **(EE. UU.) Este de EE. UU.** .|  
    
5. Seleccione **Siguiente** para ir a la pestaña **Seguridad**.
  
6. Seleccione **Habilitar Azure Bastion** en la sección Azure Bastion de la pestaña Seguridad.

   >**Nota**: Azure Bastion usa el explorador para conectarse a las máquinas virtuales de la red virtual a través de Secure Shell (SSH) o el protocolo de escritorio remoto (RDP) mediante sus direcciones IP privadas. Las máquinas virtuales no necesitan direcciones IP públicas, software cliente ni configuración especial.

7. Escriba o seleccione la siguiente información en el campo **Nombre de host de Azure Bastion**:

   |Configuración|Valor|
   |---|---|
   |Nombre de host de Azure Bastion|Escriba **mybastionhost**|
   |Nombre de la dirección IP pública de Azure Bastion|Seleccione **Crear una dirección IP pública**|
   |Añada una dirección IP pública|Escriba **my-bstn-public-ip**|
   |SKU|Deje el valor predeterminado **Estándar**.|
   
8. Seleccione **Aceptar**.

9. Seleccione **Siguiente** para ir a la pestaña **Seguridad**.

10. Seleccione **Siguiente** para continuar a la pestaña **Direcciones IP**.

11. En el cuadro espacio de direcciones de la columna Subredes, seleccione la palabra subred **predeterminada**.

12. En la plantilla **Editar subred**, escriba o seleccione la siguiente información:

   |Configuración|Valor|
   |---|---|
   |Propósito de la subred|Deje el valor predeterminado **Predeterminado**.|
   |Nombre|Escriba **mysubnet1a**|
   |Intervalo de direcciones IPv4|Deje el valor predeterminado **10.0.0/16**|
   |Dirección inicial|Deje el valor predeterminado **/24 (256 direcciones)**|

13. Seleccione **Guardar**.

14. Seleccione **Revisar y crear** en la parte inferior de la pantalla y, cuando se supere la validación, seleccione **Crear**.

    >**Nota**: La implementación de Bastion puede tardar hasta 15 minutos en completar la creación de instancias.
 
### Cree una máquina virtual.

>**Nota**: En esta tarea, crearás una máquina virtual que se usará para probar el punto de conexión privado.

1. En el menú de Azure Portal, selecciona + **Crear un recurso** > **Proceso** > **Máquina virtual** o busca **Máquina virtual** en el cuadro de búsqueda del portal.
   
2. En **Crear una máquina virtual**, escriba o seleccione los valores en la pestaña **Básico**:

   |Configuración|Value|
   |---|---|
   |**Detalles del proyecto**|
   |Suscripción|Seleccione la suscripción.|
   |Resource group|Seleccione **CreateSQLEndpointTutorial**.|
   |**Detalles de instancia**|
   |Nombre de la máquina virtual|Escriba **myVM**.|
   |Region|Seleccione **(EE. UU.) Este de EE. UU.** .|
   |Opciones de disponibilidad|Deje el valor predeterminado **No se requiere redundancia de la infraestructura**.|
   |Tipo de seguridad|Deje el valor predeterminado **Estándar**.|
   |Imagen|Seleccione **Windows Server 2022 Datacenter - x64 Gen2**.|
   |Arquitectura VM|Seleccione **x64**.|
   |Ejecución de Azure Spot con descuento|Deja esta casilla desactivada, tal y como está de forma predeterminada|
   |Size|Deja el valor predeterminado **tandard_D2s_v3-2 vcpus, 8 GiB de memoria.**|
   |**Cuenta de administrador**|
   |Tipo de autenticación|Seleccione **Contraseña**.|
   |Nombre de usuario|Escribe **Tenantadmin2.**|
   |Contraseña|Introduce **Superuser#170.**|
   |Confirmar contraseña|Vuelve a introducir **Superuser#170.**|
   |**Reglas de puerto de entrada**|
   |Selección de puertos de entrada|Seleccione **Ninguno**.|

4. Seleccione la pestaña **Redes** o seleccione **Siguiente: Discos** y, después, **Siguiente: Redes**.
  
5. En la pestaña **Redes**, escriba o seleccione esta información:

   |Configuración|Valor|
   |---|---|
   |**Interfaz de red**|
   |Red virtual|Selecciona **myVNet1a.**|
   |Subnet|Selecciona **mySubnet1a.**|
   |Dirección IP pública|Seleccione **Ninguno**.|
   |Grupo de seguridad de red de NIC|Seleccione **Básica**.|
   |Puertos de entrada públicos|Seleccione **Ninguno**.|
  
6. Seleccione **Revisar + crear**.

7. Revise la configuración y, a continuación, seleccione **Crear**.

### Creación de un servidor SQL de Azure y un punto de conexión privado

>**Nota**: En esta tarea, crearás un SQL Server en Azure.

1. En el menú de Azure Portal, selecciona + **Crear un recurso** > **Bases de datos** > **Base de datos de SQL.**
   
2. En la pestaña **Básico** de **Crear base de datos SQL**, escriba o seleccione esta información:

   |Configuración|Value|
   |---|---|
   |**Detalles del proyecto**|
   |Subscription|Seleccione su suscripción.|
   |Resource group|Seleccione **CreateSQLEndpointTutorial**.|
   |**Detalles de la base de datos**|
   |Nombre de la base de datos|Escriba **mysqldatabase**.|
   |Servidor|Seleccione **Crear nuevo**.|  

3. En **Crear un servidor de SQL Database**, escriba o seleccione esta información:
  
   |Configuración|Valor|
   |---|---|
   |**Detalles del servidor**|
   |Nombre de servidor|Escribe **mysqlserver1a.** Si el nombre ya existe, cree uno único.|
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
   |¿Quiere usar un grupo elástico de SQL?|así que seleccione **No**.|
   |Proceso y almacenamiento|Tome las opciones predeterminadas o seleccione **Configurar base de datos** para configurar los valores de proceso y almacenamiento.|
   |**Redundancia del almacenamiento de copia de seguridad**|
   |Redundancia del almacenamiento de copia de seguridad|Seleccione **Almacenamiento de copias de seguridad con redundancia local**.|
   
5. Seleccione la pestaña **Redes** o el botón **Siguiente: Redes**.

6. En la pestaña **Redes**, escriba o seleccione esta información:

   |Configuración|Valor|
   |---|---|
   |**Conectividad de red**|
   |Método de conectividad|Seleccione **Punto de conexión privado**.|

7. Seleccione **+ Agregar punto de conexión privado** en **Puntos de conexión privados**.

8. En **Crear un punto de conexión privado**, escriba o seleccione esta información:

   |Configuración|Valor|
   |---|---|
   |Suscripción|Seleccione su suscripción.|
   |Resource group|Seleccione **CreateSQLEndpointTutorial**.|
   |Location|Seleccione **Este de EE. UU**.|
   |Nombre|Escriba **myPrivateSQLendpoint**.|
   |Recurso secundario de destino|Selecciona **mysqlserver1a.**|
   |**Redes**|
   |Virtual network|Selecciona **myVNet1a.**|
   |Subnet|Selecciona **mySubnet1a.**|
   |**Integración de DNS privado**|
   |Integración con una zona DNS privada|Deje el valor predeterminado **Sí**.|
   |Zona DNS privada|Deje el valor predeterminado **(nuevo) privatelink.database.windows.net**.|

 9. Seleccione **Aceptar**.

 10. Seleccione **Revisar + crear**.

 11. Seleccione **Crear**.

### Deshabilitación del acceso público al servidor lógico de Azure SQL

>**Nota**: Para este escenario, supongamos que quieres deshabilitar todo el acceso público a Azure SQL Server y permitir solo las conexiones desde tu red virtual.

1. En el cuadro de búsqueda de Azure Portal, escriba **mysqlserver** o el nombre del servidor que especificó en los pasos anteriores.

2. En la página **Redes**, seleccione la pestaña **Acceso público** y, luego, seleccione **Deshabilitar** para **Acceso a una red pública**.

   ![image](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/44ff5c24-70cf-49ed-b2ab-5e210c478b3a)


4. Seleccione **Guardar**.

### Prueba de la conectividad con el punto de conexión privado

>**Nota**: En esta tarea, utilizarás la máquina virtual que has creado en los pasos anteriores para conectarte a SQL Server con el punto de conexión privado.

1. En el panel de navegación de la izquierda, seleccione **Grupos de recursos**.

2. Seleccione **CreateSQLEndpointTutorial**.

3. Seleccione **myVM**.

4. En la página de información general de **myVM,** selecciona Conectar y después **Bastión.**

5. Introduce el nombre de usuario **Tenantadmin2** y la contraseña **Superuser#170** que has introducido durante la creación de la máquina virtual.

   **Importante:** Ve a la configuración de Edge/elementos emergentes y redirige/y cambia el conmutador Bloqueado a **desactivado,** antes de seleccionar Conectar.

7. Seleccione el botón **Conectar**.
  
8. Abra Windows PowerShell en el servidor después de conectarse.

9. Introduce `nslookup sqlserver-name.database.windows.net.` Sustituir **sqlserver-name** por el nombre de SQL Server que has creado en los pasos anteriores. Recibirá un mensaje similar al que se muestra a continuación:

   ````  
   Server:  UnKnown
   Address:  168.63.129.16
   
   Non-authoritative answer:
   Name:    mysqlserver1a.privatelink.database.windows.net
   Address:  10.1.0.5
   Aliases:  mysqlserver1a.database.windows.net
   ````
    
>**Nota**: se devuelve una dirección IP privada de 10.1.0.5 para el nombre de SQL Server. Esta se encuentra en la subred **miSubred1a** de la red virtual **miVNet1a** que has creado anteriormente.

9. Instale [SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&view=sql-server-2017) en **myVM**.
 
10. Abra **SQL Server Management Studio**.

11. En **Conectar con el servidor**, escriba o seleccione esta información:

    |Configuración|Value|
    |---|---|
    |Tipo de servidor|Seleccione **Motor de base de datos**.|
    |Nombre de servidor|Escribe **sqlserver1a.database.windows.net.**|
    |Autenticación|Seleccione **Autenticación de SQL Server**.|
    |Nombre de usuario|Escribe **Tenantadmin2**.|
    |Contraseña|Introduce **Superuser#170**.|
    |Recordar contraseña|Seleccione **Sí**.|
   
12. Seleccione **Conectar**.

13. Examine las bases de datos en el menú izquierdo.

14. (Opcionalmente) Cree o consulte información de mysqldatabase.

15. Cierre la conexión de Escritorio remoto a myVM.
  
> **Resultados**: te has conectado a un Azure SQL Server con un punto de conexión privado de Azure con Azure Portal.
