---
title: "Azure AD Connect: inicio de sesión único de conexión directa | Microsoft Docs"
description: "En este tema se describe el inicio de sesión único de conexión directa de Azure Active Directory (Azure AD) y cómo permite proporcionar un verdadero inicio de sesión único a los usuarios de equipos de escritorio corporativos dentro de la red de la empresa."
services: active-directory
keywords: "qué es Azure AD Connect, instalar Active Directory, componentes necesarios para Azure AD, SSO, inicio de sesión único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.translationtype: HT
ms.sourcegitcommit: bfd49ea68c597b109a2c6823b7a8115608fa26c3
ms.openlocfilehash: c4cd80c50dca5b97c36f1c9785d8ea347b35285c
ms.contentlocale: es-es
ms.lasthandoff: 07/25/2017

---

# <a name="azure-active-directory-seamless-single-sign-on"></a>Inicio de sesión único de conexión directa de Azure Active Directory

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>¿Qué es el inicio de sesión único de conexión directa de Azure Active Directory?

El inicio de sesión único de conexión directa de Azure Active Directory (SSO de conexión directa de Azure AD) permite iniciar sesión automáticamente a los usuarios en dispositivos corporativos conectados a la red de la empresa. Si se habilita, los usuarios no tienen que escribir la contraseña para iniciar sesión en Azure AD y, generalmente, ni siquiera los nombres de usuario. Esta característica proporciona a los usuarios un acceso sencillo a las aplicaciones en la nube sin necesidad de componentes locales adicionales.

SSO de conexión directa se puede combinar con los métodos de inicio de sesión mediante [sincronización de hash de contraseñas](active-directory-aadconnectsync-implement-password-synchronization.md) o [autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md).

![Inicio de sesión único de conexión directa](./media/active-directory-aadconnect-sso/sso1.png)

>[!NOTE]
>Esta característica _no_ se puede aplicar a Active Directory Federation Services (ADFS), que ya ofrece esta funcionalidad.

## <a name="key-benefits"></a>Ventajas principales

- *Mejor experiencia del usuario*
  - Los usuarios inician sesión automáticamente tanto en las aplicaciones basadas en la nube como en las locales.
  - Los usuarios no tienen que escribir sus contraseñas varias veces.
- *Es fácil de implementar y administrar*
  - No se necesitan componentes adicionales en local para que esto funcione.
  - Funciona con cualquier método de autenticación en la nube, ya sea [sincronización de hash de contraseña](active-directory-aadconnectsync-implement-password-synchronization.md) o [autenticación de paso a través](active-directory-aadconnect-pass-through-authentication.md).
  - Puede extenderse a algunos o a todos los usuarios mediante la directiva de grupo.
  - Registre los dispositivos que no son de Windows 10 con Azure AD. Se necesita la versión 2.1 o posterior del [cliente para unirse al área de trabajo](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="feature-highlights"></a>Características destacadas

- El nombre de usuario de inicio de sesión puede ser el predeterminado local (`userPrincipalName`) u otro atributo `Alternate ID`) configurado en Azure AD Connect.
- SSO de conexión directa es una característica oportunista. Si, por algún motivo, genera un error, la experiencia de inicio de sesión del usuario se revierte a su comportamiento habitual; es decir, el usuario deberá escribir su contraseña en la página de inicio de sesión.
- Si una aplicación envía un parámetro `domain_hint` (que identifica el inquilino) o `login_hint` (que identifica el usuario) en su solicitud de inicio de sesión de Azure AD, los usuarios inician sesión automáticamente sin que tengan que escribir nombres de usuario ni contraseñas.
- Puede habilitarse a través de Azure AD Connect.
- Es una característica gratuita y no es necesario usar ninguna versión de pago de Azure AD para usarla.
- Se admite en clientes basados en el explorador web y en clientes de Office que admiten la [autenticación moderna](https://aka.ms/modernauthga) en plataformas con la funcionalidad de autenticación de Kerberos:

| SO\Explorador |Internet Explorer|perimetral|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|Sí|Sí|Sí|Sí\*|N/D
|Windows 8.1|Sí|N/D|Sí|Sí\*|N/D
|Windows 8|Sí|N/D|Sí|Sí\*|N/D
|Windows 7|Sí|N/D|Sí|Sí\*|N/D
|Mac OS X|N/D|N/D|Sí\*|Sí\*|Sí\*

\*Requiere [configuración adicional](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!NOTE]
>En el caso de Windows 10, la recomendación es usar [Azure AD Join](../active-directory-azureadjoin-overview.md) para que la experiencia de inicio de sesión único con Azure AD sea óptima.

## <a name="next-steps"></a>Pasos siguientes

- [**Inicio rápido** ](active-directory-aadconnect-sso-quick-start.md): desarrollo y ejecución de SSO de conexión directa de Azure AD.
- [**Profundización técnica** ](active-directory-aadconnect-sso-how-it-works.md): descripción del funcionamiento de esta característica.
- [**Preguntas más frecuentes**](active-directory-aadconnect-sso-faq.md): obtenga respuestas a las preguntas más frecuentes.
- [**Solución de problemas**](active-directory-aadconnect-troubleshoot-sso.md): aprenda a resolver problemas comunes de esta característica.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): para la tramitación de solicitudes de nuevas características.

