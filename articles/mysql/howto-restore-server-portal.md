---
title: "Restauración de un servidor en Azure Database for MySQL | Microsoft Docs"
description: "En este artículo se describe cómo restaurar un servidor en Azure Database for MySQL mediante Azure Portal."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.translationtype: Human Translation
ms.sourcegitcommit: 71fea4a41b2e3a60f2f610609a14372e678b7ec4
ms.openlocfilehash: 0603119da20e74b423072ce6afdb8c9f20830383
ms.contentlocale: es-es
ms.lasthandoff: 05/10/2017

---

# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a>Copia de seguridad y restauración de un servidor en Azure Database for MySQL mediante Azure Portal

## <a name="backup-happens-automatically"></a>Las copias de seguridad se realizan automáticamente
Cuando se usa Azure Database for MySQL, el servicio de base de datos realiza automáticamente una copia de seguridad del servicio de cada 5 minutos. 

Las copias de seguridad están disponibles durante 7 días en el nivel Básico y 35 días en el nivel Estándar. Para más información, consulte [Niveles de servicio de Azure Database for MySQL](concepts-service-tiers.md)

Con esta característica de copia de seguridad automática, puede restaurar el servidor y todas sus bases de datos en un servidor nuevo a un momento dado anterior.

## <a name="restore-in-the-azure-portal"></a>Restauración en Azure Portal
Azure Database for MySQL permite restaurar el servidor a un momento dado y en una nueva copia del servidor. Puede usar este nuevo servidor para recuperar los datos. 

Por ejemplo, si una tabla se quitó accidentalmente a mediodía de hoy, podría restaurar al momento justo antes de mediodía y recuperar la tabla y los datos que faltan desde esa copia nueva del servidor.

Los siguientes pasos restauran el servidor de ejemplo a un momento dado:

1. Inicie sesión en [Azure Portal](https://portal.azure.com/).

2. Localice su servidor de Azure Database for MySQL. En el panel izquierdo, seleccione **Todos los recursos** y seleccione el servidor en la lista.

3.  En la parte superior de la hoja de información general del servidor, haga clic en **Restaurar** en la barra de herramientas. Se abre la hoja Restaurar.
![haga clic en el botón restaurar](./media/howto-restore-server-portal/click-restore-button.png)

4. Rellene el formulario Restaurar con la información necesaria:

- **Punto de restauración (UTC)**: use el selector de fecha y el selector de tiempo para seleccionar el momento al que se restaurará. La hora especificada está en formato UTC, por lo que es probable que deba convertir la hora local a UTC.
- **Restaurar en el servidor nuevo**: especifique el nombre del nuevo servidor donde se restaurará el servidor existente.
- **Ubicación**: la opción de región se rellena automáticamente con la región del servidor de origen, y no se puede cambiar.
- **Plan de tarifa**: la opción de plan de tarifa se rellena automáticamente con el mismo plan de tarifa que el servidor de origen, y no se puede cambiar aquí. 
![Restauración de PITR](./media/howto-restore-server-portal/pitr-restore.png)

5. Haga clic en **Aceptar** para restaurar el servidor a un momento dado. 

6. Una vez finalizada la restauración, busque el nuevo servidor que se crea para comprobar que las bases de datos se restauraron del modo esperado.

## <a name="next-steps"></a>Pasos siguientes
- [Bibliotecas de conexiones de Azure Database for MySQL](concepts-connection-libraries.md)
