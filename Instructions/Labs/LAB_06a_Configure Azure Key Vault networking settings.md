---
lab:
  title: 'Ejercicio 06a: Configuración de las opciones de red de Azure Key Vault'
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tienes acceso administrativo. 


Puedes usar Azure Portal para configurar las opciones de red de Azure Key Vault para trabajar con otras aplicaciones y servicios de Azure. 

---

## Tareas de aptitudes

- Crear un almacén de claves mediante Azure Portal.

- Agregar una red virtual existente a un firewall y reglas de red virtual.

- Configuración de una red y subred virtuales para permitir el acceso a un almacén de claves.

## Instrucciones del ejercicio 

### Uso de Azure Portal para crear una instancia de Azure Key Vault.

1. Inicia una sesión en el explorador e inicia sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. En el cuadro de búsqueda de Azure Portal, escribe **Key Vault.**

3. En la lista de resultados, elige **Key Vault**.

4. En la sección Key Vaults, elige **Crear.**

5. En la pestaña **Aspectos Básicos** de **Crear almacén de claves**, escribe o selecciona esta información:
   
   |Configuración|Valor|
   |---|---|
   |**Detalles del proyecto**|
   |Suscripción|Selecciona tu suscripción.|
   |Grupo de recursos|Escribe **az-rg-1.** Selecciona **Aceptar**.|
   |**Detalles de instancia**|
   |Nombre del almacén de claves|El nombre del almacén solo debe contener caracteres alfanuméricos y guiones y no puede empezar por un número. *Ejemplo: az-securevault150*|
   |Región|Selecciona **Este de EE. UU**.|
   |Plan de tarifa|Deja la configuración predeterminada en Estándar.|
   |Días durante los cuales se conservarán los almacenes eliminados|Deja la configuración predeterminada en 90.|

7. Selecciona la **pestaña Revisar y crear** o selecciona el botón azul Revisar y crear situado en la parte inferior de la página.
  
8. Selecciona **Crear.**

### Configuración de firewall y redes virtuales de Key Vault.

1. En el cuadro de búsqueda de Azure Portal, escribe **Key Vault.**

2. Ve al almacén de claves que has creado anteriormente.

3. Selecciona **Configuración,** después, **Redes** y, a continuación, la pestaña **Firewalls y redes virtuales**.
   
4. En Permitir acceso desde, selecciona **Permitir el acceso público desde redes virtuales y direcciones IP específicas.**

5. En la sección Redes virtuales, selecciona + **Añadir una red virtual,** y después selecciona + **Añadir redes virtuales existentes.**

6. En la plantilla **Agregar redes**, selecciona tu red virtual creada previamente de la lista desplegable **Redes virtuales** y **Subredes**.

7. En la parte inferior de la plantilla **Agregar redes**, selecciona **Habilitar** y, después, **Agregar**. 

8. En la parte inferior de la página **Firewalls y redes virtuales**, selecciona **Aplicar.**

  > **Resultados**: has creado un almacén de claves y configurado el firewall y red virtual del almacén de claves de Azure Portal.
