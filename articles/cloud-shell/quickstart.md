---
title: "Guía de inicio rápido de Azure Cloud Shell (versión preliminar) | Microsoft Docs"
description: "Guía de inicio rápido de Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.translationtype: HT
ms.sourcegitcommit: bde1bc7e140f9eb7bb864c1c0a1387b9da5d4d22
ms.openlocfilehash: 7a2ed1c890eb22b3aff9aaadf2b420eeb21dd207
ms.contentlocale: es-es
ms.lasthandoff: 07/21/2017

---

# <a name="quickstart-for-using-the-azure-cloud-shell"></a>Guía de inicio rápido de Azure Cloud Shell

En este documento se detalla cómo usar Azure Cloud Shell en [Azure Portal](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Inicio de Cloud Shell
1. Inicie **Cloud Shell** en la navegación superior de Azure Portal <br>
![](media/shell-icon.png)
2. Seleccione una suscripción para crear una cuenta de almacenamiento y un recurso compartido de archivos de Azure
3. Seleccione "Create storage" (Creación de almacenamiento)

> [!TIP]
> Usted se autentica automáticamente para la CLI de Azure 2.0 en todas las sesiones.

### <a name="set-your-subscription"></a>Establecimiento de la suscripción
1. Enumere las suscripciones a las que tiene acceso: <br>
`az account list`
2. Establezca su suscripción preferida: <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> La suscripción se recordará para sesiones futuras mediante `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Crear un grupo de recursos
Cree un nuevo grupo de recursos en WestUS llamado "MyRG": <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Creación de una máquina virtual Linux
Cree una máquina virtual con Ubuntu en su nuevo grupo de recursos. La CLI de Azure 2.0 creará claves SSH y configurará la máquina virtual con ellas. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> La CLI de Azure 2.0 coloca las claves públicas y privadas usadas para autenticar la máquina virtual en `/User/.ssh/id_rsa` y `/User/.ssh/id_rsa.pub` de forma predeterminada. La carpeta .ssh se conserva en la imagen de 5 GB adjunta del recurso compartido de archivos de Azure.

Su nombre de usuario en esta máquina virtual será el nombre de usuario utilizado en Cloud Shell ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>Conexión SSH con la máquina virtual Linux
1. Busque el nombre de la máquina virtual en la barra de búsqueda de Azure Portal
2. Haga clic en "Conectar" y ejecute: `ssh username@ipaddress`

![](media/sshcmd-copy.png)

Al establecer la conexión SSH, debería ver el aviso de bienvenida de Ubuntu.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Limpiar 
Elimine el grupo de recursos y cualquier recurso dentro del mismo: <br>
Ejecute `az group delete -n MyRG`

## <a name="next-steps"></a>Pasos siguientes
[Obtenga información sobre la persistencia del almacenamiento en Cloud Shell](persisting-shell-storage.md) <br>
[Más información sobre la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/) <br>
[Información sobre Azure File Storage](../storage/storage-files-introduction.md) <br>
