---
lab:
  title: "Ejercicio 06: Habilitación de la eliminación temporal en Azure Key\_Vault"
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tienes acceso administrativo. 


Si se elimina un almacén de claves que no tenga habilitada la eliminación temporal, se eliminarán permanentemente todos los secretos, claves y certificados almacenados en ese almacén de claves. La eliminación accidental de un almacén de claves puede provocar una pérdida de datos permanente. La eliminación temporal permite recuperar un almacén de claves eliminado accidentalmente durante un período de retención configurable.

---

## Tareas de aptitudes

- Comprobar si la eliminación temporal está habilitada en un almacén de claves y habilitarla.

## Instrucciones del ejercicio 

### Comprobar si la eliminación temporal está habilitada en un almacén de claves y habilitarla

1. Inicia una sesión en el explorador e inicia sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. Selecciona el almacén de claves.

3. En la hoja **Configuración**, selecciona **Propiedades**.

4. Comprueba si el botón de selección situado junto a la eliminación temporal está establecido en **Habilitar protección de purga (aplique un período de retención obligatorio para almacenes eliminados y objetos de almacén).**

5. Si la eliminación temporal no está habilitada en el almacén de claves, haz clic en el botón de selección **Habilitar protección de purga (aplicar un período de retención obligatorio para almacenes eliminados y objetos de almacén)** para habilitar la eliminación temporal y haz clic en **Guardar.**

![imagen](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/06131a60-7f00-4764-a424-87ea41a78394)

> **Resultados**: has habilitado correctamente la eliminación temporal, lo que garantiza que los recursos eliminados se conservan durante 90 días (de forma predeterminada) y se pueden recuperar, deshacer eficazmente la eliminación a través de Azure Portal.