---
title: "Características de seguridad que se pueden usar con Azure Storage | Microsoft Docs"
description: " Este artículo ofrece una visión general de las principales características de seguridad de Azure que se pueden usar con Almacenamiento de Azure. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.translationtype: HT
ms.sourcegitcommit: bde1bc7e140f9eb7bb864c1c0a1387b9da5d4d22
ms.openlocfilehash: 1386d16cf0e7f6fd324d0779e9ad54ecd88b3166
ms.contentlocale: es-es
ms.lasthandoff: 07/21/2017

---
# <a name="azure-storage-security-overview"></a>Información general sobre seguridad de Almacenamiento de Azure
Almacenamiento de Azure es la solución de almacenamiento en la nube para las aplicaciones modernas que dependen de la durabilidad, la disponibilidad y la escalabilidad para satisfacer las necesidades de sus clientes. Almacenamiento de Azure proporciona un conjunto completo de funcionalidades de seguridad:

* La cuenta de almacenamiento se puede proteger mediante el control de acceso basado en rol y Azure Active Directory.
* Los datos se pueden proteger en tránsito entre una aplicación y Azure usando cifrado de cliente, HTTPS o SMB 3.0.
* Se puede establecer una configuración para que los datos se cifren automáticamente cuando se escriben en Almacenamiento de Azure mediante el Cifrado del servicio de Almacenamiento.
* Se puede establecer el cifrado de los discos de datos y del sistema operativo utilizados por máquinas virtuales mediante el Cifrado de discos de Azure.
* Se puede conceder acceso delegado a los objetos de datos de Almacenamiento de Azure mediante las Firmas de acceso compartido.
* El método de autenticación usado por alguien cuando accede a Almacenamiento puede seguirse mediante el análisis de almacenamiento.

Para obtener más información sobre la seguridad en Azure Storage, consulte la [guía de seguridad de Azure Storage](../storage/storage-security-guide.md). Esta guía proporciona una profundización en las características de seguridad de Almacenamiento de Azure, como las claves de cuenta de almacenamiento, el cifrado de datos en tránsito y en reposo y el análisis de almacenamiento.

Este artículo ofrece una visión general de las características de seguridad de Azure que se pueden usar con Azure Storage. Además, se incluyen vínculos a artículos que ofrecen detalles de cada característica para que pueda tener más información al respecto.

Estas son las características principales que se tratan en este artículo:

* Control de acceso basado en roles
* Acceso delegado a objetos de almacenamiento
* Cifrado en tránsito
* Cifrado en reposo/Cifrado del servicio de Almacenamiento
* Cifrado de disco de Azure
* Almacén de claves de Azure

## <a name="role-based-access-control-rbac"></a>Control de acceso basado en rol (RBAC)
Puede proteger su cuenta de almacenamiento con el control de acceso basado en rol (RBAC). En organizaciones que quieren aplicar directivas de seguridad para el acceso a los datos, es imperativo restringir el acceso en función de los principios de seguridad [necesidad de saber](https://en.wikipedia.org/wiki/Need_to_know) y [mínimo privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege). Estos derechos de acceso se conceden al asignar el rol RBAC adecuado a grupos y aplicaciones de un determinado ámbito. Puede aprovechar los [roles integrados de RBAC](../active-directory/role-based-access-built-in-roles.md), tales como el de colaborador de la cuenta de almacenamiento, para asignar privilegios a los usuarios.

Más información:

* [Control de acceso basado en roles de Azure Active Directory](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-to-storage-objects"></a>Acceso delegado a objetos de almacenamiento
Una Firma de acceso compartido (SAS) ofrece acceso delegado a los recursos en la cuenta de almacenamiento. Esto significa que puede conceder permisos limitados de los clientes a objetos en su cuenta de almacenamiento durante un período específico y con un conjunto determinado de permisos sin tener que compartir las claves de acceso a las cuentas. La SAS es un URI que incluye en sus parámetros de consulta toda la información necesaria para el acceso autenticado a un recurso de almacenamiento. Para obtener acceso a los recursos de almacenamiento con la SAS, el cliente solo tiene que pasar la SAS al método o constructor adecuados.

Más información:

* [Firmas de acceso compartido, Parte 1: Descripción del modelo SAS](../storage/storage-dotnet-shared-access-signature-part-1.md)
* [Firmas de acceso compartido, Parte 2: Creación y uso de una SAS con Almacenamiento de blobs](../storage/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>Cifrado en tránsito
Cifrado en tránsito es un mecanismo para proteger datos cuando se transmiten a través de redes. Con Almacenamiento de Azure, puede proteger los datos mediante:

* [Cifrado de nivel de transporte](../storage/storage-security-guide.md#encryption-in-transit), como HTTPS para transferir datos a Almacenamiento de Azure o desde este servicio.
* [Cifrado en el cable](../storage/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), como el cifrado SMB 3.0 para recursos compartidos de Azure File.
* [Cifrado de cliente](../storage/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), para cifrar los datos antes de transferirlos al almacenamiento y descifrarlos una vez transferidos desde este servicio.

Más información acerca del cifrado de cliente:

* [Cifrado del lado cliente para el Almacenamiento de Microsoft Azure (vista previa)](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [Cloud security controls series: Encrypting Data in Transit (Serie de controles de seguridad en la nube: cifrado de datos en tránsito)](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>Cifrado en reposo
Para muchas organizaciones, el [cifrado de los datos en reposo](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) es un paso obligatorio en lo que respecta a la privacidad de los datos, el cumplimiento y la soberanía de los datos. Hay tres características de Azure que proporcionan cifrado de datos "en reposo":

* [Cifrado del servicio de almacenamiento](../storage/storage-security-guide.md#encryption-at-rest) permite solicitar que el servicio de almacenamiento cifre automáticamente los datos al escribirlos en Almacenamiento de Azure.
* [Cifrado de cliente](../storage/storage-security-guide.md#client-side-encryption) también proporciona la característica de cifrado en reposo.
* [Cifrado de discos de Azure](../storage/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) permite cifrar los discos de datos y del sistema operativo usados por una máquina virtual de IaaS.

Más información acerca del Cifrado de servicio de almacenamiento:

* [Cifrado del servicio Azure Storage](https://azure.microsoft.com/services/storage/) está disponible para [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/). Para más información sobre otros tipos de almacenamiento de Azure, consulte [File Storage](https://azure.microsoft.com/services/storage/files/), [Premium Storage (disco)](https://azure.microsoft.com/services/storage/premium-storage/), [Table Storage](https://azure.microsoft.com/services/storage/tables/) y [Queue Storage](https://azure.microsoft.com/services/storage/queues/).
* [Cifrado del servicio Almacenamiento de Azure para datos en reposo (versión preliminar)](../storage/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Cifrado de disco de Azure
Cifrado de discos de Azure para máquinas virtuales (VM) le ayuda a solucionar los aspectos de seguridad y cumplimiento normativo de su organización, ya que cifra los discos de las máquinas virtuales (incluidos los discos de arranque y de datos) con claves y directivas que usted controla en el [Almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/).

Cifrado de discos para máquinas virtuales funciona en sistemas operativos Linux y Windows. También utiliza el Almacén de claves para ayudarle a proteger, administrar y auditar el uso de las claves de cifrado del disco. Todos los datos de los discos de máquinas virtuales se cifran en reposo con tecnología de cifrado estándar del sector en sus cuentas de Almacenamiento de Azure. La solución Cifrado de discos para Windows se basa en la tecnología de [Cifrado de unidad BitLocker de Microsoft](https://technet.microsoft.com/library/cc732774.aspx), y la solución de Linux se basa en [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Más información:

* [Azure Disk Encryption for Windows and Linux Azure Virtual Machines (Cifrado de discos de Azure para máquinas virtuales IaaS de Linux y Windows)](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>Almacén de claves de Azure
Azure Disk Encryption usa [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) para ayudarle a controlar y administrar las claves y los secretos de cifrado de discos en su suscripción del almacén de claves. Además, garantiza que todos los datos de los discos de las máquinas virtuales se cifren en reposo en Azure Storage. Debe usar el Almacén de claves de Azure para auditar el uso de la directiva y las claves.

Más información:

* [¿Qué es el Almacén de claves de Azure?](../key-vault/key-vault-whatis.md)
* [Introducción al Almacén de claves de Azure](../key-vault/key-vault-get-started.md)

