---
lab:
  title: 'Ejercicio 05: Habilitar el acceso Just-In-Time en máquinas virtuales'
  module: Module 06 - Explore just-in-time VM access
---


>**Nota**: para completar este laboratorio, necesitarás una [suscripción de Azure.](https://azure.microsoft.com/en-us/free/?azure-portal=true) al que tiene acceso administrativo. 


Puedes usar el acceso Just-In-Time (JIT) de Microsoft Defender for Cloud para proteger las máquinas virtuales (VM) de Azure frente a un acceso de red no autorizado. Muchas veces, los firewalls contienen reglas de permisos por las que las máquinas virtuales quedan vulnerables a ataques. Con JIT puedes permitir el acceso a las máquinas virtuales solo cuando sea necesario, en los puertos necesarios y durante el período de tiempo necesario. 

---

## Tareas de aptitudes

- Habilitación de JIT en tus máquinas virtuales desde Azure Portal.

- Solicitud de acceso a una máquina virtual con JIT habilitado desde Azure Portal.

## Instrucciones del ejercicio 

### Habilitación de JIT en las máquinas virtuales desde máquinas virtuales de Azure

>**Nota**: puedes habilitar JIT en una máquina virtual desde las páginas de máquinas virtuales de Azure de Azure Portal.

1. En el cuadro de búsqueda que aparece en la parte superior del portal, escribe **máquina virtual**. En los resultados de la búsqueda, selecciona **Máquinas virtuales**.

2. Selecciona **vm-1.**
 
3. Selecciona **Configuración** en la sección **Configuración** de vm-1.
   
4. En **Acceso de máquina virtual Just-In-Time**, selecciona **Habilitar Just-In-Time.**

5. En **Acceso de máquina virtual Just-In-Time,** haz clic en el vínculo que dice **Abrir Microsoft Defender for Cloud.**

6. De forma predeterminada, el acceso Just-In-Time para la máquina virtual usa esta configuración:

   - Máquinas de Windows
   
     - Puerto RDP: 3389
     - Acceso máximo permitido: tres horas
     - Direcciones IP de origen permitidas: cualquiera

   - Equipos con Linux
     - Puerto SSH: 22
     - Acceso máximo permitido: tres horas
     - Direcciones IP de origen permitidas: cualquiera
   
7. De forma predeterminada, el acceso Just-In-Time para la máquina virtual usa esta configuración:

   - En la pestaña **Configurado**, haz clic con el botón derecho en la máquina virtual a la que deseas agregar un puerto y selecciona Editar.
  
 ![imagen](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/66cf98b6-2ce0-43c7-a7be-b5d69bcfac1d)

   - En **Configuración de acceso de máquina virtual JIT** , puedes modificar la configuración existente de un puerto protegido, o bien agregar un puerto personalizado.
   - Cuando hayas terminado de editar los puertos, selecciona **Guardar**.   

### Solicitud de acceso a una máquina virtual habilitada para JIT desde la página de conexión de la máquina virtual de Azure.

>**Nota**: cuando una máquina virtual tiene JIT habilitado, tienes que solicitar acceso para conectarte a ella. Puedes solicitar acceso de cualquiera de las maneras admitidas, independientemente de cómo hayas habilitado JIT.
   
1. En Azure Portal, abre las páginas de máquinas virtuales.

2. Selecciona la máquina virtual a la que deseas conectarte y abre la página **Conectar**.

   - Azure comprueba si JIT está habilitado en esa máquina virtual.

        - Si JIT no está habilitado para la máquina virtual, se te pedirá que lo habilites.
    
        - Si JIT está habilitado, selecciona **Solicitar acceso** para pasar una solicitud de acceso con la dirección IP de solicitud, el intervalo de tiempo y los puertos que se configuraron para esa máquina virtual.

![imagen](https://github.com/MicrosoftLearning/Secure-Azure-services-and-workloads-with-Microsoft-Defender-for-Cloud-regulatory-compliance-controls/assets/91347931/7e454150-bc04-47bc-afa1-e0a1e8af17f9)






> **Resultados**: has explorado varios métodos sobre cómo habilitar JIT en las máquinas virtuales y cómo solicitar acceso a las máquinas virtuales que tienen JIT habilitado en Microsoft Defender for Cloud.
