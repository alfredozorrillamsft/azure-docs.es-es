---
title: "Ejemplo de la CLI para mover una instancia de Azure SQL Database a un grupo elástico de SQL | Microsoft Docs"
description: "Script de ejemplo de la CLI de Azure para mover una instancia de SQL Database a un grupo elástico de SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/05/2017
ms.author: janeng
ms.translationtype: Human Translation
ms.sourcegitcommit: bb794ba3b78881c967f0bb8687b1f70e5dd69c71
ms.openlocfilehash: 1dc31a0b20f36e28a58896ed63a5e0395ae1d3af
ms.contentlocale: es-es
ms.lasthandoff: 07/06/2017

---

# <a name="use-cli-to-move-an-azure-sql-database-in-a-sql-elastic-pool"></a>Uso de la CLI para mover una instancia de Azure SQL Database a un grupo elástico de SQL

Este script de ejemplo de la CLI de Azure crea dos grupos elásticos y traslada una instancia de Azure SQL Database de un grupo elástico de SQL a otro grupo elástico de SQL y, a continuación, traslada una base de datos fuera de un grupo elástico a un nivel de rendimiento de base de datos única de Azure. 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si decide instalar y usar la CLI localmente, para este tema es preciso que ejecute la CLI de Azure versión 2.0 o posterior. Ejecute `az --version` para encontrar la versión. Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Script de ejemplo

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Traslado de una base de datos de un grupo a otro")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Después de ejecutar el script de ejemplo, se puede usar el comando siguiente para quitar el grupo de recursos y todos los recursos asociados.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script usa los siguientes comandos. Cada comando de la tabla crea un vínculo a documentación específica del comando.

| Comando | Notas |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [az sql server create](https://docs.microsoft.com/cli/azure/sql/server#create) | Crea un servidor lógico que hospeda una base de datos o un grupo elástico. |
| [az sql elastic-pools create](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | Crea un grupo elástico en el servidor lógico. |
| [az sql db create](https://docs.microsoft.com/cli/azure/sql/db#create) | Crea una base de datos en un servidor lógico como una base de datos única o agrupada. |
| [az sql db update](https://docs.microsoft.com/cli/azure/sql/db#update) | Actualiza las propiedades de la base de datos o traslada una base de datos a un grupo elástico, fuera de este o entre grupos elásticos. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina un grupo de recursos, incluidos todos los recursos anidados. |

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).

Encontrará más ejemplos de scripts de la CLI de SQL Database en la [documentación de Azure SQL Database](../sql-database-cli-samples.md).



