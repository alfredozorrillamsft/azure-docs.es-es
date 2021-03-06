---
title: "Configuración de un entorno de desarrollo para microservicios de Azure | Microsoft Docs"
description: "Instale las herramientas, el SDK y el motor en tiempo de ejecución y cree un clúster de desarrollo local. Después de completar esta instalación, estará listo para crear aplicaciones."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/20/2017
ms.author: ryanwi, mikhegn
ms.translationtype: Human Translation
ms.sourcegitcommit: f7479260c7c2e10f242b6d8e77170d4abe8634ac
ms.openlocfilehash: 926dfe3de0715f855e6d5b57f10c2366cda8583b
ms.contentlocale: es-es
ms.lasthandoff: 06/21/2017


---
<a id="prepare-your-development-environment" class="xliff"></a>

# Preparación del entorno de desarrollo
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md) 
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
> 
> 

 Para compilar y ejecutar [aplicaciones de Azure Service Fabric][1] en la máquina de desarrollo, debe instalar el motor en tiempo de ejecución, el SDK y las herramientas. También es preciso que habilite la ejecución de los scripts de Windows PowerShell que se incluyen en el SDK.

<a id="prerequisites" class="xliff"></a>

## Requisitos previos
<a id="supported-operating-system-versions" class="xliff"></a>

### Versiones de sistemas operativos compatibles
Se admiten las siguientes versiones de sistemas operativos para desarrollo:

* Windows 7
* Windows 8/Windows 8.1
* Windows Server 2012 R2
* Windows Server 2016
* Windows 10

> [!NOTE]
> Windows 7 solo incluye de forma predeterminada Windows PowerShell 2.0. Los cmdlets de PowerShell de Service Fabric requieren PowerShell 3.0 o superior. Puede [descargar Windows PowerShell 5.0][powershell5-download] desde el Centro de descarga de Microsoft.
> 
> 

<a id="install-the-sdk-and-tools" class="xliff"></a>

## Instalación de SDK y herramientas
<a id="to-use-visual-studio-2017" class="xliff"></a>

### Cómo usar Visual Studio 2017
Las herramientas de Service Fabric forman parte de la carga de trabajo de Azure Development and Management de Visual Studio 2017. Habilite esta carga de trabajo durante la instalación de Visual Studio.
Además, debe instalar el SDK de Microsoft Azure Service Fabric mediante el Instalador de plataforma web.

* [Instalación del SDK de Microsoft Azure Service Fabric][core-sdk]

<a id="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later" class="xliff"></a>

### Para utilizar Visual Studio 2015 (es necesario usar Visual Studio 2015 Update 2 o versiones posteriores)
En Visual Studio 2015, las herramientas de Service Fabric se instalan con el SDK mediante el Instalador de plataforma web:

* [Instalación del SDK y las herramientas de Microsoft Azure Service Fabric][full-bundle-vs2015]

<a id="sdk-installation-only" class="xliff"></a>

### Para instalar solamente el SDK
Si únicamente necesita el SDK, puede instalar este paquete:
* [Instalación del SDK de Microsoft Azure Service Fabric][core-sdk]

Las versiones actuales son:
* SDK de Service Fabric 2.6.220
* Runtime de Service Fabric 5.6.220
* Herramientas de Visual Studio 2015 1.6.50508.2
* Visual Studio 2017 Update 2

Las versiones preliminares actuales son:
* SDK de Service Fabric 255.255.2718.255
* Runtime de Service Fabric 255.255.5718.255
* Herramientas de Visual Studio 2015 1.6.50509.5
* Microsoft Visual Studio 2017 Update 3 Preview 1

Para obtener una lista de las versiones admitidas, consulte [Compatibilidad con Service Fabric](service-fabric-support.md).

<a id="enable-powershell-script-execution" class="xliff"></a>

## Habilitar la ejecución del script de PowerShell
Service Fabric usa scripts de Windows PowerShell para crear un clúster de desarrollo local e implementar aplicaciones desde Visual Studio. De forma predeterminada, Windows bloquea la ejecución de estos scripts. Para habilitarlos, debe modificar la directiva de ejecución de PowerShell. Abra PowerShell como administrador y escriba el siguiente comando:

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

<a id="next-steps" class="xliff"></a>

## Pasos siguientes
Ahora que ha terminado la configuración del entorno de desarrollo, puede empezar a compilar y ejecutar aplicaciones.

* [Creación de la primera aplicación de Service Fabric en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
* [Introducción a la implementación y actualización de aplicaciones en un clúster local](service-fabric-get-started-with-a-local-cluster.md)
* [Más información sobre los modelos de programación: Reliable Services y Reliable Actors](service-fabric-choose-framework.md)
* [Consulta de los ejemplos de código de Service Fabric en GitHub](https://aka.ms/servicefabricsamples)
* [Visualización del clúster mediante el Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md)
* [Siga la ruta de aprendizaje de Service Fabric para obtener una amplia introducción a la plataforma](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Página de campaña de Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Vínculo de WebPI de VS 2015"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Vínculo de WebPI de Dev15"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Vínculo de WebPI de SDK de núcleo"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395

