---
title: "Ejemplo de PowerShell de grupo de conmutación por error de replicación geográfica para una instancia única de Azure SQL Database | Microsoft Docs"
description: "Script de ejemplo de Azure PowerShell para configurar la replicación geográfica activa para una instancia única de Azure SQL Database"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.translationtype: Human Translation
ms.sourcegitcommit: 857267f46f6a2d545fc402ebf3a12f21c62ecd21
ms.openlocfilehash: 0fcddfd7e224fc763616573e5cd8b3345cc46ded
ms.contentlocale: es-es
ms.lasthandoff: 06/28/2017

---

# <a name="use-powershell-to-configure-an-active-geo-replication-failover-group-for-a-single-azure-sql-database"></a>Usar PowerShell para configurar un grupo de conmutación por error de replicación geográfica activa para una instancia única de Azure SQL Database

En este ejemplo de script de PowerShell se configura un grupo de conmutación por error de replicación geográfica activa para una única instancia de Azure SQL Database y se conmuta por error a una réplica secundaria de Azure SQL Database.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a>Scripts de ejemplo

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Configurar grupo de conmutación por error para base de datos única")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a>Explicación del script

Este script usa los siguientes comandos. Cada comando de la tabla crea un vínculo a documentación específica del comando.

| Comando | Notas |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Crea un servidor lógico que hospeda una base de datos o un grupo elástico. |
| [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | Crea un grupo elástico en un servidor lógico. |
| [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase) | Actualiza las propiedades de la base de datos o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos. |
| [New-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| Crea una base de datos secundaria para una base de datos existente e inicia la replicación de datos. |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)| Obtiene una o más bases de datos. |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| Convierte una base de datos secundaria en principal para iniciar la conmutación por error.|
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | Obtiene los vínculos de replicación geográfica entre una Base de datos SQL de Azure y un grupo de recursos o SQL Server. |
| [Remove-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | Finaliza una replicación de datos entre una base de datos SQL y la base de datos secundaria especificada. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |
|||

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).

Encontrará más ejemplos de scripts de PowerShell de SQL Database en los [scripts de PowerShell de Azure SQL Database](../sql-database-powershell-samples.md).

