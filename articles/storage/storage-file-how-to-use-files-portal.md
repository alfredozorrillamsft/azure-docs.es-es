---
title: "Administración de Azure File Storage desde Azure Portal | Microsoft Docs"
description: Aprenda a usar Azure Portal para administrar Azure File Storage.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.translationtype: HT
ms.sourcegitcommit: bde1bc7e140f9eb7bb864c1c0a1387b9da5d4d22
ms.openlocfilehash: d8ffb4359b0efe8da2f3bccb81c987bdeedf1a39
ms.contentlocale: es-es
ms.lasthandoff: 07/21/2017

---

# <a name="how-to-use-azure-file-storage-from-the-azure-portal"></a>Uso de Azure File Storage desde Azure Portal
[Azure Portal](https://portal.azure.com) ofrece una interfaz de usuario para la administración de Azure File Storage. Puede realizar las siguientes acciones desde el explorador web:

* Creación de un recurso compartido de archivos
* Cargar y descargar archivos al recurso compartido de archivos y desde este.
* Supervisar el uso real de cada recurso compartido de archivos.
* Ajustar la cuota de tamaño del recurso compartido de archivos.
* Copiar los comandos necesarios para montar el recurso compartido de archivos desde un cliente Windows o Linux.

## <a name="create-file-share"></a>Creación de un recurso compartido de archivos
1. Inicie sesión en el Portal de Azure.
2. En el menú de navegación, haga clic en **Cuentas de almacenamiento** o **Cuentas de almacenamiento (clásico)**.
    
    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Elija la cuenta de almacenamiento.

    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. Elija el servicio "Archivos".

    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. Haga clic en "Recursos compartidos de archivos" y siga el vínculo para crear su primer recurso compartido de archivos.

    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Rellene el nombre del recurso compartido de archivos y su tamaño (hasta 5120 GB) para crear su primer recurso compartido de archivos. Una vez que se ha creado el recurso compartido de archivos, se puede montar desde cualquier sistema de archivos que admita SMB 2.1 o SMB 3.0. Puede hacer clic en **Cuota** en el recurso compartido de archivos para cambiar el tamaño del archivo hasta 5120 GB. Consulte la [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/) para estimar el costo de almacenamiento con Azure File Storage.

    ![Captura de pantalla que muestra cómo crear un recurso compartido de archivos en el portal](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Carga y descarga de archivos
1. Elija un recurso compartido de archivos creado previamente.

    ![Captura de pantalla que muestra cómo cargar y descargar archivos desde el portal](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Haga clic en **Cargar** para abrir la interfaz de usuario para cargar los archivos.

    ![Captura de pantalla que muestra cómo cargar archivos desde el portal](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-to-file-share"></a>Conexión al recurso compartido de archivos
-  Haga clic en **Conectar** para obtener la línea de comandos necesaria para montar el recurso compartido de archivos desde Windows y Linux. Los usuarios de Linux también pueden hacer referencia a [Uso de Azure File Storage con Linux](storage-how-to-use-files-linux.md) para obtener instrucciones adicionales de montaje para otras distribuciones de Linux.

    ![Captura de pantalla que muestra cómo montar el recurso compartido de archivos](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  Puede copiar los comandos para el montaje del recurso compartido de archivos en Windows o Linux y ejecutarlos desde la máquina virtual de Azure o el equipo local.

    ![Captura de pantalla que muestra los comandos de montaje para Windows y Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**Sugerencia:**  
Para obtener la clave de acceso de la cuenta de almacenamiento necesaria para el montaje, haga clic en **Ver las claves de acceso de esta cuenta de almacenamiento** en la parte inferior de la página Conectar.

## <a name="see-also"></a>Otras referencias
Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.

* [Preguntas más frecuentes](storage-files-faq.md)
* [Solución de problemas](storage-troubleshoot-file-connection-problems.md)
