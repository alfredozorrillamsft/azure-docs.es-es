---
title: "Conexión de Excel a Hadoop con Power Query - Azure HDInsight | Microsoft Docs"
description: "Vea cómo aprovechar las ventajas de los componentes de inteligencia empresarial y usar Power Query para Excel a fin de acceder a los datos almacenados en Hadoop en HDInsight."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 01ad2f90-7520-44d9-8c16-4d936faaff9b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jgao
ms.translationtype: HT
ms.sourcegitcommit: bde1bc7e140f9eb7bb864c1c0a1387b9da5d4d22
ms.openlocfilehash: 6a15efb091b4faaa7305bb8faa362c62fac595cb
ms.contentlocale: es-es
ms.lasthandoff: 07/21/2017

---
# <a name="connect-excel-to-hadoop-by-using-power-query"></a>Conexión de Excel a Hadoop con Power Query
Una de las características clave de la solución para Big Data de Microsoft es la integración de los componentes de Microsoft Business Intelligence (BI) con los clústeres de Hadoop en Azure HDInsight. Un ejemplo importante es la capacidad de conectar Excel a la cuenta de Azure Storage que contiene los datos asociados a su clúster de Hadoop mediante el complemento de Microsoft Power Query para Excel. En este artículo se describen las pautas para configurar y usar Power Query para consultar los datos asociados con un clúster de Hadoop administrado con HDInsight.

### <a name="prerequisites"></a>Requisitos previos
Antes de empezar este artículo, debe tener los siguientes elementos:

* **Un clúster de HDInsight**. Para configurarlo, consulte [Introducción a Azure HDInsight][hdinsight-get-started].
* **Una estación de trabajo** que ejecute Windows 7, Windows Server 2008 R2 o un sistema operativo posterior.
* **Office 2016, Office Profesional Plus 2013, Office 365 ProPlus, Excel 2013 Standalone u Office Professional Plus 2010**.

## <a name="install-power-query"></a>Instalación de Power Query
Power Query puede importar datos ofrecidos o generados por un trabajo de Hadoop ejecutado en un clúster de HDInsight.

En Excel 2016, Power Query se ha integrado en la cinta de Datos en la sección Obtener y transformar. Para versiones anteriores de Excel, descargue Microsoft Power Query para Excel desde el [Centro de descarga de Microsoft][powerquery-download] e instálelo.

## <a name="import-hdinsight-data-into-excel"></a>Importación de datos de HDInsight a Excel
El complemento de Power Query para Excel facilita la importación de datos desde el clúster de HDInsight hasta Excel, donde se pueden usar herramientas de BI como PowerPivot y Power Map para la inspección, el análisis y la presentación de los datos.

**Para importar datos desde un clúster de HDInsight**

1. Abra Excel.
2. Cree un libro vacío.
3. Siga los pasos siguientes en función de la versión de Excel:

    - Excel 2016

        - Haga clic en el menú **Datos**, haga clic en **Obtener datos** desde la cinta **Obtener y transformar datos**, haga clic en **Desde Azure** y, después, en **Desde Azure HDInsight (HDFS)**.

        ![HDI.PowerQuery.SelectHdiSource](./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.excel2016.png)

    - Excel 2013/2010

        - Haga clic en el menú **Power Query**, en **De Azure** y, luego, en **De HDInsight de Microsoft Azure** .
   
        ![HDI.PowerQuery.SelectHdiSource][image-hdi-powerquery-hdi-source]
       
        **Nota**: Si no ve el menú **Power Query**, vaya a **Archivo** > **Opciones** > **Complementos** y seleccione **Complementos COM** en el cuadro desplegable **Administrador** situado al final de la página. Elija el botón **Go...** y compruebe que la casilla del complemento de Power Query para Excel esté activada.
       
        **Nota:** Power Query también permite importar datos de HDFS haciendo clic **De otros orígenes**.
4. En **Nombre de cuenta**, escriba el nombre de la cuenta de Azure Blob Storage asociada con su clúster y, a continuación, haga clic en **Aceptar**. Esta puede ser una [cuenta de almacenamiento predeterminada](hdinsight-administer-use-management-portal.md#find-the-default-storage-account) o una cuenta de almacenamiento vinculada.  El formato es *https://&lt;NombreDeCuentaDeAlmacenamiento>.blob.core.windows.net/*.
5. En **Clave de cuenta**, escriba la clave de cuenta para la cuenta deBlob Storage y, a continuación, haga clic en **Guardar**. (Solo tiene que escribir la información de la cuenta la primera vez que tenga acceso a este almacén).
6. En el panel del **navegador** situado a la izquierda del Editor de consultas, haga doble clic en el nombre del contenedor de almacenamiento de blobs. De forma predeterminada, el nombre del contenedor es el mismo que el del clúster.
7. Busque **HiveSampleData.txt** en la columna **Nombre** (la ruta de acceso de la carpeta es **../hive/warehouse/hivesampletable/)**, y haga clic en **Binario** a la izquierda de HiveSampleData.txt. HiveSampleData.txt incluye todo el clúster. Opcionalmente, puede utilizar su propio archivo.
   
    ![HDI.PowerQuery.ImportData][image-hdi-powerquery-importdata]
8. Si quiere, puede cambiar el nombre de las columnas. Cuando haya terminado, haga clic en **Aplicar y cerrar**.  Los datos se han cargado en el libro:
   
    ![HDI.PowerQuery.ImportedTable][image-hdi-powerquery-imported-table]

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido a usar Power Query para recuperar datos de HDInsight en Excel. Del mismo modo, puede recuperar datos de HDInsight en Base de datos SQL de Azure. También se pueden cargar los datos en HDInsight. Para obtener más información, consulte los artículos siguientes:

* [Conexión de Excel a HDInsight con Microsoft Hive ODBC Driver][hdinsight-ODBC]
* [Carga de datos en HDInsight][hdinsight-upload-data]

[hdinsight-ODBC]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[image-hdi-powerquery-hdi-source]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.selecthdisource.png
[image-hdi-powerquery-importdata]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importdata.png
[image-hdi-powerquery-imported-table]: ./media/hdinsight-connect-excel-power-query/hdi.powerquery.importedtable.PNG

[powerquery-download]: http://go.microsoft.com/fwlink/?LinkID=286689

