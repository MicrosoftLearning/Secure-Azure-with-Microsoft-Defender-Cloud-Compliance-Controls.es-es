---
lab:
  title: 'Ejercicio 06b: Realice la eliminación temporal y la recuperación del almacén de claves de protección contra purga'
  module: Module 07 - Configure Azure Key Vault networking settings
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tiene acceso administrativo. 


Puedes usar la protección contra purga para prevenir la eliminación de tu almacén de claves, claves, secretos y certificados por parte de un interno malintencionado. Considere esto como una papelera de reciclaje con un bloqueo basado en el tiempo. Puede recuperar los elementos en cualquier momento durante el período de retención que haya configurado. Recuerde que no podrá eliminar o purgar un almacén de claves permanentemente hasta que transcurra el período de retención. Una vez que transcurra el período de retención establecido, el objeto del almacén de claves se purgará automáticamente.

---

## Tareas de aptitudes

- Comprobar si la eliminación temporal está habilitada en un almacén de claves y habilitarla.

- Enumerar, recuperar o purgar un almacén de claves eliminado temporalmente.

- Enumerar, recuperar o purgar secretos, claves y certificados eliminados temporalmente.

## Instrucciones del ejercicio 

### Comprobar si la eliminación temporal está habilitada en un almacén de claves y habilitarla

1. Inicie una sesión en el explorador e inicie sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. Seleccione el almacén de claves.

3. Haz clic en la hoja **Propiedades**.

4. Comprueba si el botón de radio situado junto a la opción de borrado temporal está configurado como **Habilitar protección contra purga.**

5. Si la eliminación temporal no está habilitada en el almacén de claves, haz clic en el botón de radio para habilitar la eliminación temporal y haz clic en **Guardar.**

![imagen](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/06131a60-7f00-4764-a424-87ea41a78394)


### Enumerar, recuperar o purgar un almacén de claves eliminado temporalmente.

1. Inicie una sesión en el explorador e inicie sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. Haga clic en la barra de búsqueda de la parte superior de la página.

3. Busca el servicio **Key Vault**. No haga clic en un almacén de claves individual.

4. En la parte superior de la pantalla, haga clic en la opción "Administrar almacenes eliminados"

5. Se abrirá un panel de contexto en el lado derecho de la pantalla.

6. Seleccione su suscripción.

7. Si el almacén de claves se ha eliminado temporalmente, aparecerá en el panel de contexto de la derecha.

8. Si hay demasiados almacenes, puede hacer clic en "Cargar más" en la parte inferior del panel de contexto o usar la CLI o PowerShell para obtener los resultados.

9. Una vez que encuentres el almacén que deseas **recuperar** o **purgar,** selecciona la **casilla** que aparece después.

10. Seleccione la opción de recuperación en la parte inferior del panel de contexto si quiere recuperar el almacén de claves.

11. Si por el contrario quiere eliminar de forma permanente el almacén de claves, seleccione la opción de purga.

![imagen](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/f41c0673-3832-4d3f-8b05-48e46e6c2282)


### Enumerar, recuperar o purgar secretos, claves y certificados eliminados temporalmente.

1. Inicie una sesión en el explorador e inicie sesión en el [menú de Azure Portal.](https://portal.azure.com/)
   
2. Seleccione el almacén de claves.

3. Seleccione la hoja correspondiente al tipo de secreto que quiera administrar (claves, secretos o certificados).

4. En la parte superior de la pantalla, haga clic en "Manage deleted (keys, secrets, or certificates)" (Administrar eliminados [claves, secretos o certificados]).

5. Aparecerá un panel de contexto en el lado derecho de la pantalla.

6. Si el secreto, la clave o el certificado no aparecen en la lista, esto quiere decir que no se encuentra en el estado de eliminación temporal.

7. Seleccione el secreto, la clave o el certificado que quiera administrar.

8. Seleccione la opción para recuperar o purgar situada en la parte inferior del panel de contexto.

![imagen](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Cloud-Security-Benchmark/assets/91347931/dab95f78-1642-4883-b56f-70e1e5320d45)


  > **Resultados**: has realizado la administración de recuperación de Azure Key Vault con protección contra purga y eliminación temporal en Azure Portal.
