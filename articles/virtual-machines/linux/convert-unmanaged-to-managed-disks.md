---
title: "Conversión de una máquina virtual Linux en Azure con discos no administrados a discos administrados - Azure Managed Disks | Microsoft Docs"
description: "Conversión de una máquina virtual Linux con discos no administrados en discos administrados mediante la CLI de Azure 2.0 en el modelo de implementación de Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.translationtype: HT
ms.sourcegitcommit: f9003c65d1818952c6a019f81080d595791f63bf
ms.openlocfilehash: 3109da1dac6ebb6564c94b5c6635ded77ea9be8d
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---

# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-to-managed-disks"></a>Conversión de una máquina virtual Linux con discos no administrados en discos administrados

Si ya dispone de máquinas virtuales Linux que usan discos no administrados, puede convertirlas para usar discos administrados mediante el servicio [Azure Managed Disks](../../storage/storage-managed-disks-overview.md). Este proceso convierte el disco del SO y los discos de datos conectados.

En este artículo se muestra cómo convertir máquinas virtuales con la CLI de Azure. Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Antes de empezar

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Conversión de máquinas virtuales de instancia única
En esta sección se explica cómo convertir máquinas virtuales de Azure de instancia única de Unmanaged Disks a Managed Disks. (Si las máquinas virtuales se encuentran en un conjunto de disponibilidad, consulte la sección siguiente). Puede usar este proceso para convertir las máquinas virtuales de discos no administrados premium (SDD) a discos administrados premium, o bien de discos no administrados estándar (HDD) a discos administrados estándar.

1. Desasigne la máquina virtual mediante [az vm deallocate](/cli/azure/vm#deallocate). En el ejemplo siguiente se desasigna la VM `myVM` en el grupo de recursos denominado `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Convierta la máquina virtual en discos administrados con [az vm convert](/cli/azure/vm#convert). El proceso siguiente convierte la máquina virtual denominada `myVM`, incluidos el disco del SO y todos los discos de datos:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Inicie la máquina virtual después de la conversión a discos administrados con [az vm start](/cli/azure/vm#start). En el ejemplo siguiente se inicia la VM llamada `myVM` en el grupo de recursos `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Conversión de VM de un conjunto de disponibilidad

Si las VM que desea convertir en discos administrados se encuentran en un conjunto de disponibilidad, primero debe convertir el conjunto de disponibilidad en un conjunto de disponibilidad administrado.

Todas las VM del conjunto de disponibilidad deben desasignarse antes de convertir el conjunto de disponibilidad. Planee la conversión de todas las máquinas virtuales a discos administrados después de haber convertido el propio conjunto de disponibilidad en un conjunto de disponibilidad administrado. Después, inicie todas las máquinas virtuales y siga trabajando con normalidad.

1. Enumere todas las máquinas virtuales de un conjunto de disponibilidad con [az vm availability-set list](/cli/azure/vm/availability-set#list). En el ejemplo siguiente se enumeran todas las VM del conjunto de disponibilidad `myAvailabilitySet` en el grupo de recursos denominado `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Desasigne todas las máquinas virtuales con [az vm deallocate](/cli/azure/vm#deallocate). En el ejemplo siguiente se desasigna la VM `myVM` en el grupo de recursos denominado `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Convierta el conjunto de disponibilidad con [az vm availability-set convert](/cli/azure/vm/availability-set#convert). En el ejemplo siguiente se convierte el conjunto de disponibilidad `myAvailabilitySet` en el grupo de recursos denominado `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Convierta todas las máquinas virtuales a discos administrados con [az vm convert](/cli/azure/vm#convert). El proceso siguiente convierte la máquina virtual denominada `myVM`, incluidos el disco del SO y todos los discos de datos:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Inicie todas las máquinas virtuales después de la conversión a discos administrados con [az vm start](/cli/azure/vm#start). En el ejemplo siguiente se inicia la máquina virtual llamada `myVM` en el grupo de recursos `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="managed-disks-and-azure-storage-service-encryption"></a>Managed Disks y Azure Storage Service Encryption
No puede usar los pasos anteriores para convertir un disco no administrado en uno administrado si el disco no administrado se encuentra en una cuenta de Storage cifrada con el [cifrado del servicio Azure Storage](../../storage/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Los siguientes pasos explican cómo copiar y usar Unmanaged Disks que han estado en una cuenta de almacenamiento cifrada:

1. Copie el VHD con [az storage blob copy start](/cli/azure/storage/blob/copy#start) en una cuenta de almacenamiento que nunca se ha habilitado para el cifrado del servicio Azure Storage.

2. Use la VM copiada de alguna de las formas siguientes:

   * Cree una máquina virtual que use discos administrados y especifique el archivo VHD durante la creación con [az vm create](/cli/azure/vm#create).

   * Asocie el VHD copiado con [az vm disk attach](/cli/azure/vm/disk#attach) a una máquina virtual en ejecución que usa discos administrados.

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre las opciones de almacenamiento, vea [Introducción a Azure Managed Disks](../../storage/storage-managed-disks-overview.md).

