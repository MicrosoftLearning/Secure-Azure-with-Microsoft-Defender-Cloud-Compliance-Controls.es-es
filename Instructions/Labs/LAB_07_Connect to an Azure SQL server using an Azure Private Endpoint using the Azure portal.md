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
  
- Crea una máquina virtual.
  
- Crear un servidor SQL de Azure y un punto de conexión privado.
  
- Probar la conectividad con el punto de conexión privado del servidor SQL.

## Instrucciones del ejercicio 

### Creación de un grupo de recursos y una red virtual.

>**Nota**: el host bastión se utilizará para conectarse de forma segura a la máquina virtual a fin de probar el punto de conexión privado. 

1. Inicia una sesión en el explorador e inicia sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. En el cuadro de búsqueda de la parte superior del portal, escribe **redes virtuales.** En los resultados de la búsqueda, selecciona **Redes virtuales**.

3. En la página **Redes virtuales**, selecciona **+ Crear**.

4. En la pestaña **Aspectos básicos** de **Crear red virtual**, escribe o selecciona esta información:
   
   |Configuración|Valor|
   |---|---|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Selecciona **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre de la red virtual|Escribe **vnet-2.**|
   |Región|Selecciona **(EE. UU.) Este de EE. UU.** .|  
    
5. Selecciona **Siguiente** para ir a la pestaña **Seguridad**.
  
6. Selecciona **Habilitar Azure Bastion** en la sección Azure Bastion de la pestaña Seguridad.

>**Nota**: Azure Bastion es un servicio de pago que proporciona conectividad RDP y SSH segura a las máquinas virtuales a través de TLS. Cuando se conecta a través de Azure Bastion, las máquinas virtuales no necesitan una dirección IP pública. 

7. Escribe o selecciona la siguiente información en el campo **Azure Bastion**:

   |Configuración|Valor|
   |---|---|
   |Host de Azure Bastion |Escribe **az-bastionhost-1a.**|
   |Nombre de la dirección IP pública de Azure Bastion|Selecciona **Crear una dirección IP pública**|
   |Incorporación de una dirección IP pública|Seleccione **Aceptar**|

8. Selecciona **Siguiente** para continuar a la pestaña **Direcciones IP**.

9. En el cuadro **espacio de direcciones IPv4** configurado existente debajo de la columna **Subredes**, haz clic en la entrada **predeterminada**.

10. En la plantilla **Editar subred**, escribe o selecciona la siguiente información:

    |Configuración|Valor|
    |---|---|
    |Propósito de subred|Deja la configuración predeterminada en Predeterminada.|
    |Nombre|**subnet-2**|
    |Incluir un espacio de direcciones IPv4|Deja la configuración predeterminada con la marca de verificación.|
    |Intervalo de direcciones IPv4|Deja la configuración predeterminada en 10.0.0.0/16.|
    |Dirección inicial|10.0.0.0.|
    |Tamaño|Deja la configuración predeterminada en /24 (256 direcciones).|
    |Intervalo de direcciones de subred|10.0.0.0-10.0.0.255.|

11. En la parte inferior de la página **Editar subred**, selecciona **Guardar.**

12. En la parte inferior de la página **Direcciones IP**, selecciona **Revisar + crear.**

13. En la parte inferior de la página **Revisar + crear**, selecciona **Crear.**

>**Nota**: La implementación de Bastion puede tardar hasta 15 minutos en completar la creación de instancias.
 
### Cree una máquina virtual.

>**Nota**: en esta tarea, crearás una máquina virtual que se usará para probar el punto de conexión privado.

1. En el portal, busca y selecciona **máquinas virtuales.**

2. En **Máquinas virtuales**, selecciona **+ Crear** y, después, **Máquina virtual de Azure**.

3. En Crear una máquina virtual, escribe o selecciona esta información en la página **Aspectos básicos**:

   |Configuración|Valor|
   |---|---|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Selecciona **az-rg-1.**|
   |**Detalles de instancia**|
   |Nombre de la máquina virtual|Escribe **vm-3.**|
   |Región|Selecciona **(EE. UU.) Este de EE. UU.** .|
   |Opciones de disponibilidad|En el menú desplegable Zona de disponibilidad, selecciona **No se necesita redundancia de la infraestructura**.|
   |Tipo de seguridad|En el menú desplegable Tipo de seguridad, selecciona **Estándar**.|
   |Imagen|Selecciona **Windows Server 2022 Datacenter - x64 Gen2.**|
   |Arquitectura VM|Selecciona **x64.**|
   |Ejecución de Azure Spot con descuento|Deja la configuración predeterminada en desactivada.|
   |Tamaño|Deja la configuración predeterminada en Standard_D2s_v3-2 VCPU, 8 GiB de memoria.|
   |**Cuenta de administrador**|
   |Nombre de usuario|Escribe **Tenantadmin2.**|
   |Contraseña|Introduce **Superuser#170.**|
   |Confirmar contraseña|Vuelve a introducir **Superuser#170.**|
   |**Reglas de puerto de entrada**|
   |Puertos de entrada públicos|Selecciona **Ninguno**.|
   |Selección de puertos de entrada|La configuración predeterminada está atenuada.|

4. Selecciona **Siguiente: Discos** y, luego, **Siguiente: Redes**.
  
5. En la página **Redes**, escribe o selecciona esta información:

   |Configuración|Valor|
   |---|---|
   |**Interfaz de red**|
   |Red virtual|Selecciona **vnet-2.**|
   |Subred|Deja la configuración predeterminada en subnet-2 (10.0.0.0/24).|
   |Dirección IP pública|Deja la configuración predeterminada en (new) vm-3-ip.|
   |Grupo de seguridad de red de NIC|Deja la configuración predeterminada en Ninguno.|
   |Eliminar NIC al eliminar la VM|Deja activada la configuración predeterminada en Habilitar redes aceleradas.|
   |Equilibrio de carga|Deja la configuración predeterminada en Ninguno.|
  
6. Selecciona **Revisar + crear.**

7. Revisa la configuración y, a continuación, selecciona **Crear.**

### Creación de un servidor SQL de Azure y un punto de conexión privado

>**Nota**: en esta tarea, crearás un SQL Server en Azure.

1. En el cuadro de búsqueda de la parte superior del portal, escribe **SQL Database.** Selecciona **Bases de datos SQL** en los resultados de la búsqueda.

2. En la página **Bases de datos SQL**, selecciona **+Crear.**
   
3. En la pestaña **Aspectos básicos** de **Crear base de datos SQL**, escribe o selecciona esta información:

   |Configuración|Valor|
   |---|---|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Selecciona **az-rg-1.**|
   |**Detalles de la base de datos**|
   |Nombre de la base de datos|Escribe **az-sql-db1a.**|
   |Server|Seleccione **Crear nuevo**.|
   |**Detalles del servidor**|
   |Nombre de servidor|Escribe **az-sql-srv1a.**|
   |Location|Deja la configuración predeterminada en (EE. UU.) Este de EE. UU.|
   |**Autenticación**|
   |Método de autenticación|Selecciona **Uso de la autenticación de SQL**.|  
   |Inicio de sesión del administrador del servidor|Escribe **Tenantadmin2.**|
   |Contraseña|Introduce **Superuser#170.**|
   |Confirmación de la contraseña|Introduce **Superuser#170.**|

4. Seleccione **Aceptar**.
    
   |Configuración|Valor|
   |---|---|
   |**Detalles de la base de datos**|
   |¿Quieres usar un grupo elástico de SQL?|Deja la configuración predeterminada en No.|
   |Entorno de la carga de trabajo|Deja la configuración predeterminada en Desarrollo.|
   |Proceso y almacenamiento|Deja la configuración predeterminada en Uso general: sin servidor.|
   |**Redundancia del almacenamiento de copia de seguridad**|
   |Redundancia del almacenamiento de copia de seguridad|Selecciona **Almacenamiento de copias de seguridad con redundancia local.**|
   
5. Selecciona la pestaña **Redes** o el botón **Siguiente: Redes**.

6. En la pestaña **Redes**, escribe o selecciona esta información:

   |Configuración|Valor|
   |---|---|
   |**Conectividad de red**|
   |Método de conectividad|Selecciona **Punto de conexión privado.**|
   |Directiva de conexión|Deja la configuración predeterminada en Predeterminado: usa la directiva Redirigir para todas las conexiones de cliente que se originan dentro de Azure (excepto las conexiones de punto de conexión privado) y Proxy para todas las conexiones de cliente que se originan fuera de Azure.|
   |Conexiones de cifrado|Deja la configuración predeterminada en TLS.12|

7. En la sección **Puntos de conexión privados**, selecciona **+ Agregar punto de conexión privado.**

8. Selecciona **Revisar + crear.**

9. Seleccione **Crear**.

10. En **Crear un punto de conexión privado**, escribe o selecciona esta información:

       |Configuración|Valor|
       |---|---|
       |Suscripción|Selecciona tu suscripción.|
       |Grupo de recursos|Selecciona **az-rg-1.**|
       |Ubicación|Selecciona **Este de EE. UU**.|
       |Nombre|Escribe **az-pe1a.**|
       |Recurso secundario de destino|Deja la configuración predeterminada en SqlServer.|
       |**Redes**|
       |Red virtual|Selecciona **vnet-2.**|
       |Subred|Selecciona **subnet-2.**|
       |**Integración de DNS privado**|
       |Integración con una zona DNS privada|Deja la configuración predeterminada en Sí.|
       |Zona DNS privada|Deja la configuración predeterminada (nuevo) privatelink.database.windows.net.|

12. Selecciona **Aceptar.**

13. Selecciona **Revisar + crear.**

14. Seleccione **Crear**.

>**Nota**: la implementación de un punto de conexión privado y un servidor de Azure SQL puede tardar hasta 10 minutos en completar la creación de instancias.

### Permite que determinadas direcciones IP de Internet públicas accedan a tu servidor lógico de Azure SQL.

>**Nota**: para esta tarea, supongamos que quieres habilitar el acceso público a tu servidor de Azure SQL y permitir conexiones solo desde tu red virtual. La configuración de Acceso público puede tener como valor predeterminado **Deshabilitado.**

1. En el cuadro de búsqueda de Azure Portal, escribe **az-sql-svr1a** o el nombre del servidor que especificaste en los pasos anteriores.
   
2. Selecciona **Redes** en la sección **Seguridad** de **az-sql-svr1a.**
  
3. En la página **Redes**, ve a la pestaña **Acceso público**.
  
4. Comprueba si **Acceso a la red pública** está deshabilitado. Si está deshabilitado, selecciona **Redes seleccionadas** para Acceso a la red pública.

>**Nota**: las conexiones procedentes de las direcciones IP configuradas en la sección Reglas de firewall, más abajo, tendrán acceso a esta base de datos. De manera predeterminada, no se permiten direcciones IP públicas.

5. Si es necesario, ve a la sección **Reglas de firewall** de la página **Redes** y selecciona **+ Agregar la dirección IPv4 de cliente** si tu dirección IP de cliente no se ha rellenado aún en los campos **Nombre de regla,****Dirección IPv4 inicial** y **Dirección IPv4 final**.

   ![imagen](https://github.com/user-attachments/assets/fff5bfb1-53fd-40ea-9a31-5a095e7f3dbc) 

7. Selecciona **Guardar.**

### Prueba de la conectividad con el punto de conexión privado

>**Nota**: en esta tarea, utilizarás la máquina virtual que has creado en los pasos anteriores para conectarte a SQL Server con el punto de conexión privado.

1. En el cuadro de búsqueda de Azure Portal, escribe **vm-3** y selecciónalo en la lista desplegable Recursos.

2. En la página **Información general** de vm-3, selecciona **Conectar** y, después, selecciona **Bastion.**

3. Introduce el nombre de usuario **Tenantadmin2** y la contraseña **Superuser#170** que has introducido durante la creación de la máquina virtual.

   **Importante:** Importante: ve a Configuración de Edge y ve a **Elementos emergentes y redirecciones.** Selecciona la opción radial etiquetada **Permitir siempre elementos emergentes y redireccionamientos desde https://portal.azure.com** y, después, haz clic en **Listo.**

4. Selecciona el botón **Conectar**.
  
5. Abre Windows PowerShell en el servidor después de conectarte.

6. Para comprobar la resolución de nombres del punto de conexión privado, escriba el siguiente comando en la ventana del terminal:

   ```bash
   nslookup server-name.database.windows.net

>**Note**: Replace **sqlserver-name** with the name of the SQL server you created in the previous steps. For example, enter **nslookup az-sql-srv1a.database.windows.net** You’ll receive a message similar to the one shown below:

   ````
   
   Server:  UnKnown Address:  168.63.129.16
   
   Non-authoritative answer: Name:    az-sql-srv1a.privatelink.database.windows.net Address:  10.1.0.5 Aliases:  az-sql-srv1a.database.windows.net
   ````
   
>**Note**: A  private IP address of 10.1.0.5 is returned for the SQL server name. This address is in **az-sql-srv1a** subnet of **vnet-2** virtual network you created previously.

7. Install [SQL Server Management Studio (SSMS)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?preserve-view=true&amp;view=sql-server-2017) on **vm-3.**
 
8. Open **SQL Server Management Studio.**

9. In **Connect to server,** enter or select this information:

    |Setting|Value|
    |---|---|
    |Server type|Leave the default setting as Database Engine.|
    |Server name|Enter **az-sql-srv1a.database.windows.net.**|
    |Authentication|Select **SQL Server Authentication.**|
    |User name|Enter **Tenantadmin2**.|
    |Password|Enter **Superuser#170**.|
    |Remember password|Select **Yes.**|
    |Connectivity Security|
    |Encryption|Leave the default setting as Mandatory.|
   
10. Select **Connect.**

11. Browse databases from left menu.

12. Close the remote desktop connection to vm-3.
  
> **Results**: You have connected to an Azure SQL server using an Azure Private Endpoint using the Azure portal.
