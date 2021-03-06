---
title: "Planeamiento de la capacidad y el escalado para la replicación de VMware en Azure con Azure Site Recovery | Microsoft Docs"
description: "Use este artículo para planear la capacidad y el escalado cuando replique máquinas virtuales VMware en Azure con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.translationtype: Human Translation
ms.sourcegitcommit: 138f04f8e9f0a9a4f71e43e73593b03386e7e5a9
ms.openlocfilehash: f5b334e594e3d002e1862b25c4faba7163efa7d4
ms.contentlocale: es-es
ms.lasthandoff: 06/29/2017


---
# <a name="step-3-plan-capacity-and-scaling-for-vmware-to-azure-replication"></a>Paso 3: Planeamiento de la capacidad y el escalado de VMware para la replicación en Azure

Use este artículo para averiguar cómo planear la capacidad y el escalado cuando se replican máquinas virtuales VMware locales y servidores físicos en Azure con [Azure Site Recovery](site-recovery-overview.md).

Publique cualquier comentario o pregunta en la parte inferior de este artículo, o bien en el [foro de Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="how-do-i-start-capacity-planning"></a>¿Cómo se puede iniciar el planeamiento de la capacidad?

Recopile información sobre su entorno de replicación y luego planee la capacidad con esta información, junto con las consideraciones que se resaltan en este artículo.


## <a name="gather-information"></a>Recopilación de información

1. Descargue la [herramienta Deployment Planner para la replicación de VMware](https://aka.ms/asr-deployment-planner).
2. [Lea este artículo](site-recovery-deployment-planner.md) para aprender a ejecutar la herramienta.
3. Con la herramienta puede recopilar información sobre máquinas virtuales compatibles e incompatibles, discos por máquina virtual y la actividad de datos por disco. Esta herramienta también se encarga de los requisitos de ancho de banda de red y de la infraestructura de Azure necesaria para una replicación y conmutación por error de prueba correctas.

## <a name="replication-considerations"></a>Consideraciones sobre la replicación

Tenga en cuenta estas consideraciones antes de iniciar la implementación:

**Componente** | **Detalles** |
--- | --- | ---
**Replicación** | **Tasa máxima de cambios diaria**: una máquina protegida solo puede usar un servidor de procesos, y un servidor de procesos puede gestionar una tasa de cambios diaria de hasta 2 TB. Por lo tanto, la tasa máxima de cambios diaria que admite una máquina protegida es de 2 TB.<br/><br/> **Rendimiento máximo**: una máquina replicada puede pertenecer a una cuenta de almacenamiento en Azure. Una cuenta de almacenamiento estándar puede controlar un máximo de 20 000 solicitudes por segundo y se recomienda mantener la cantidad de operaciones de entrada/salida por segundo (IOPS) en una máquina de origen en 20 000. Por ejemplo, si tiene una máquina de origen con 5 discos y cada disco genera 120 E/S por segundo (8 K de tamaño) en la máquina de origen, se encontrará dentro del límite de 500 de Azure por E/S por segundo por disco. (El número de cuentas de almacenamiento necesario es igual al IOPS de máquina de origen total dividido por 20 000).

## <a name="configuration-server-capacity"></a>Capacidad del servidor de configuración

El servidor de configuración debe poder controlar la capacidad de tasa de cambios diaria en todas las cargas de trabajo que se ejecutan en máquinas protegidas, y necesita el ancho de banda suficiente para realizar una replicación continua de los datos en el Azure Storage.

Como procedimiento recomendado, localice el servidor de configuración en la misma red y mismo segmento de LAN que las máquinas que desea proteger. De todos modos, puede estar en una red distinta, pero las máquinas que desea proteger deben contar con la visibilidad de red de nivel L3 en ella.

## <a name="sizing-recommendations"></a>Recomendaciones de tamaño

En la tabla se resumen las recomendaciones de ajuste de tamaño en función de la CPU.

**CPU** | **Memoria** | **Tamaño del disco de caché** | **Frecuencia de cambio de datos** | **Máquinas protegidas**
--- | --- | --- | --- | ---
8 vCPU (2 sockets * 4 núcleos @ 2,5 gigahercios [GHz]) | 16 GB | < 300 GB | 500 GB o menos | Replicar menos de 100 máquinas.
12 vCPUs (2 sockets * 6 núcleos @ 2,5 GHz) | 18 GB | 600 GB | 500 GB a 1 TB | Replicar entre 100 y 150 máquinas.
16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz) | 32 GB | 1 TB | 1 TB a 2 TB | Replicar entre 150 y 200 máquinas.
Implementar otro servidor de procesos | | | 2 TB | Implemente servidores de procesos adicionales si replica más de 200 máquinas o si la tasa de cambios de datos diaria supera los 2 TB.

Donde:

* Cada máquina de origen está configurada con 3 discos de 100 GB cada una.
* Usamos almacenamiento de pruebas comparativas de 8 unidades SAS de 10 K RPM con RAID 10 para las mediciones de disco de caché.

## <a name="process-server-capacity"></a>Capacidad del servidor de procesos


El servidor de procesos recibe datos de replicación provenientes de las máquinas protegidas y los optimiza con almacenamiento en caché, compresión y cifrado. A continuación, envía los datos a Azure.

- La máquina del servidor de procesos debe tener los recursos suficientes para realizar estas tareas.
- El primer servidor de procesos está instalado en el servidor de configuración de forma predeterminada. Puede implementar servidores de procesos adicionales para escalar el entorno.
- El servidor de procesos utiliza una caché basada en disco. Utilice un disco de caché independiente con 600 GB o más de capacidad para controlar los cambios en los datos almacenados ante la eventualidad de una interrupción o un cuello de botella en la red.
- Si necesita proteger más de 200 máquinas, o si la tasa de cambios diaria es mayor que 2 TB, puede agregar servidores de procesos para controlar la carga de replicación. Para escalar horizontalmente, puede:
    - Aumentar el número de servidores de configuración. Por ejemplo, puede proteger hasta 400 máquinas con dos servidores de configuración.
    - Agregar más servidores de procesos y utilizarlos para controlar el tráfico en lugar (o además) del servidor de configuración.


### <a name="example-process-server-scaling"></a>Ejemplo de escalado de los servidores de procesos

La tabla siguiente describe un escenario en el cual:

* No pretende utilizar el servidor de configuración como un servidor de procesos.
* Ha configurado un servidor de procesos adicional.
* Ha configurado máquinas virtuales protegidas para utilizar el servidor de procesos adicional.
* Cada máquina de origen protegida está configurada con tres discos de 100 GB cada uno.

**Servidor de configuración** | **Servidores de procesos adicionales** | **Tamaño del disco de caché** | **Frecuencia de cambio de datos** | **Máquinas protegidas**
--- | --- | --- | --- | ---
8 vCPU (2 sockets * 4 núcleos a 2,5 GHz), 16 GB de memoria | 4 vCPU (2 sockets * 2 núcleos a 2,5 GHz), 8 GB de memoria | < 300 GB | 250 GB o menos | Replicar 85 máquinas o menos.
8 vCPU (2 sockets * 4 núcleos a 2,5 GHz), 16 GB de memoria | 8 vCPU (2 sockets * 4 núcleos a 2,5 GHz), 12 GB de memoria | 600 GB | 250 GB a 1 TB | Replicar entre 85 y 150 máquinas.
12 vCPU (2 sockets * 6 núcleos a 2,5 GHz), 18 GB de memoria | 12 vCPU (2 sockets * 6 núcleos a 2,5 GHz), 24 GB de memoria | 1 TB | 1 TB a 2 TB | Replicar entre 150 y 225 máquinas.

La manera en la que escalará los servidores depende de su preferencia con respecto a un modelo de escalado vertical u horizontal.  Puede escalar verticalmente con la implementación de algunos servidores de procesos y de configuración de alto nivel, mientras que, para escalar horizontalmente, debe implementar más servidores con menos recursos. Por ejemplo, si necesita proteger 220 máquinas, podría elegir una de las siguientes opciones:

* Configurar el servidor de configuración con 12 vCPU, 18 GB de memoria y un servidor de procesos adicional con 12 vCPU, 24 GB de memoria. Configurar máquinas protegidas para que utilicen solo el servidor de procesos adicional.
* Configurar dos servidores de configuración (2 x 8 vCPU, 16 GB de RAM) y dos servidores de procesos adicionales (1 x 8 vCPU y 4 vCPU x 1 para controlar 135 + 85 [220] máquinas). Configurar máquinas protegidas para que utilicen solo servidores de procesos adicionales.

## <a name="deploy-additional-process-servers"></a>Implementar servidores de procesos adicionales

Siga estas instrucciones para configurar un servidor de procesos adicional. Después de configurar el servidor, debe migrar las máquinas de origen para que lo utilicen.

1. En **Site Recovery servers** (Servidores de Site Recovery), haga clic en el servidor de configuración > **+ Servidor de procesos**.
2. En **Tipo de servidor**, haga clic en **Servidor de procesos (local)**.

    ![Servidor de proceso](./media/vmware-walkthrough-capacity/migrate-ps2.png)
3. Descargue el archivo de instalación unificada de Site Recovery.
4. Ejecute el programa de instalación para instalar al servidor de procesos y registrarlo en el almacén.
5. En **Antes de comenzar**, seleccione **Add additional process servers to scale out deployment** (Agregar servidores de procesos adicionales para el escalado horizontal de la implementación).
6. En **Configuration Server Details** (Detalles del servidor de configuración), especifique la dirección IP del servidor de configuración y la frase de contraseña. Si no tiene frase de contraseña, ejecute **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe –n** en el servidor de configuración para obtener una.

    ![Servidor de configuración](./media/vmware-walkthrough-capacity/add-ps2.png)
7. Complete el resto de la instalación tal y como lo hizo cuando instaló el servidor de configuración.

### <a name="migrate-machines-to-use-the-process-server"></a>Migración de máquinas para usar el servidor de procesos

1. En **Configuración** > **Site Recovery servers** (Servidores de Site Recovery), haga clic en el servidor de configuración > **Servidor de procesos**.
2. Haga clic con el botón derecho en el servidor de procesos que se utiliza actualmente y haga clic en > **Cambiar**.

    ![Cambio del servidor de procesos](./media/vmware-walkthrough-capacity/migrate-ps3.png)
3. En **Select target process server** (Seleccionar servidor de procesos de destino), elija el servidor de procesos que quiere usar y las máquinas virtuales que controlará el servidor.
4. Haga clic en el icono de información. El espacio promedio que se necesita para replicar cada máquina virtual seleccionada en el nuevo servidor de procesos aparecerá para ayudarlo a tomar decisiones relacionadas con la carga.
5. Haga clic en la marca de verificación para comenzar a replicar en el nuevo servidor de procesos.

## <a name="control-network-bandwidth"></a>Ancho de banda de red de control

Después de ejecutar la [herramienta Deployment Planner](site-recovery-deployment-planner.md) para calcular el ancho de banda necesario para la replicación (la replicación inicial y la diferencial), puede controlar la cantidad de ancho de banda utilizado para la replicación mediante un par de opciones:

* **Limitar ancho de banda**: el tráfico de VMware que se replica en Azure pasa a través de un servidor de procesos específico. También puede limitar el ancho de banda en las máquinas que se ejecutan como servidores de procesos.
* **Influir en el ancho de banda**: puede influir en el ancho de banda utilizado para la replicación mediante un par de claves del Registro:
  * El valor del Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** especifica el número de subprocesos que se utilizan para la transferencia de datos (replicación inicial o diferencial) de un disco. Un valor mayor aumenta el ancho de banda de red utilizado para la replicación.
  * **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** especifica el número de subprocesos usados para la transferencia de datos durante la conmutación por recuperación.

### <a name="throttle-bandwidth"></a>Limitar ancho de banda

1. Abra el complemento MMC de Azure Backup en la máquina que actúa como el servidor de procesos. De manera predeterminada, hay disponible un acceso directo para Backup en el escritorio o en la siguiente carpeta: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. En el complemento, haga clic en **Cambiar propiedades**.
3. En la pestaña **Limitación**, seleccione la opción **Habilitar el límite de uso del ancho de banda de Internet para operaciones de copia de seguridad**.
4. Establezca los límites para las horas laborables y no laborables. Los intervalos válidos van de 512 Kbps a 102 Mbps por segundo.

    ![Limitación](./media/vmware-walkthrough-capacity/throttle2.png)

También puede utilizar el cmdlet [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) para establecer la limitación. Aquí tiene un ejemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que no se requiere ninguna limitación.

### <a name="influence-network-bandwidth-for-a-vm"></a>Control del uso de ancho de banda de red para una VM

1. En el Registro de la máquina virtual, vaya a **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * Para influir en el tráfico de ancho de banda en un disco de replicación, modifique el valor de **UploadThreadsPerVM** o cree la clave en caso de que no exista.
   * Para influir en el ancho de banda para el tráfico de conmutación por recuperación de Azure, modifique el valor de **DownloadThreadsPerVM**.
2. El valor predeterminado es 4. En una red sobreaprovisionada, se deben cambiar los valores de estas claves del Registro. El valor máximo es 32. Supervise el tráfico para optimizar el valor.




## <a name="next-steps"></a>Pasos siguientes

Vaya a [Paso 4: Planeamiento de las redes](vmware-walkthrough-network.md).

