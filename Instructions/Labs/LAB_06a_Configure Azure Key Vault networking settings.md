---
lab:
  title: 'Ejercicio 06a: Configuración de las opciones de red de Azure Key Vault'
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tiene acceso administrativo. 


Puede usar Azure Portal para configurar las opciones de red de Azure Key Vault para trabajar con otras aplicaciones y servicios de Azure. 

---

## Tareas de aptitudes

- Crear un almacén de claves mediante Azure Portal.

- Agregar una red virtual existente a un firewall y reglas de red virtual.

- Configuración de una red y subred virtuales para permitir el acceso a un almacén de claves.

## Instrucciones del ejercicio 

### Uso de Azure Portal para crear una instancia de Azure Key Vault.

1. Inicie una sesión en el explorador e inicie sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. En el cuadro de búsqueda de Azure Portal, escriba **Key Vault.**

3. En la lista de resultados, elija **Key Vault**.

4. En la sección Key Vaults, elija **Crear.**

5. En la pestaña **Aspectos Básicos** de **Crear almacén de claves**, escriba o seleccione esta información:
   
   |Configuración|Value|
   |---|---|
   |**Detalles del proyecto**|
   |Subscription|Seleccione su suscripción.|
   |Resource group|Escribe **az-rg-1.** Seleccione **Aceptar**.|
   |**Detalles de instancia**|
   |Nombre del almacén de claves|Escribe **AZAPLKeyVault.**|
   |Region|Seleccione **Este de EE. UU**.|
   |Plan de tarifa|Valor predeterminado del sistema **Estándar**|
   |Días durante los cuales se conservarán los almacenes eliminados|Valor predeterminado del sistema **90**|

7. Seleccione la **pestaña Revisar y crear** o seleccione el botón azul Revisar y crear situado en la parte inferior de la página.
  
8. Seleccione **Crear**.

### Configuración de firewall y redes virtuales de Key Vault.

1. En el cuadro de búsqueda de Azure Portal, escriba **Key Vault.**

2. Ve al almacén de claves que has creado anteriormente.

3. Seleccione **Redes** y, luego, elija la pestaña **Firewalls and virtual networks** (Firewalls y redes virtuales).

4. En Permitir acceso desde, selecciona **Permitir el acceso público desde redes virtuales y direcciones IP específicas.**

5. En la sección Redes virtuales, selecciona + **Añadir una red virtual,** y después selecciona + **Añadir redes virtuales existentes.**

6. En la plantilla Agregar redes, selecciona tu red virtual creada previamente de la lista desplegable **Redes virtuales** y **Subredes**.

7. En la parte inferior de la plantilla Agregar redes, haz clic en **Agregar.**

  > **Resultados**: has creado un almacén de claves y configurado el firewall y red virtual del almacén de claves de Azure Portal.
