---
title: "Dominios personalizados del proxy de aplicación de Azure AD | Microsoft Docs"
description: "Administre los dominios personalizados del proxy de aplicación de Azure AD para que la dirección URL de la aplicación sea la mismo independientemente de dónde accedan los usuarios."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.translationtype: HT
ms.sourcegitcommit: 22aa82e5cbce5b00f733f72209318c901079b665
ms.openlocfilehash: d0abd789d47b34f3dad206b9862c289d6683a83b
ms.contentlocale: es-es
ms.lasthandoff: 07/24/2017

---

# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Uso de dominios personalizados en el proxy de la aplicación de Azure AD

Al publicar una aplicación a través del proxy de la aplicación de Azure Active Directory, se crea una dirección URL externa a la que los usuarios se desplazan cuando trabajan de forma remota. Esta dirección URL obtiene el dominio predeterminado *yourtenant-msappproxy.net*. Si quiere usar su propio nombre de dominio, configure un dominio personalizado para la aplicación. 

Se recomienda que configure dominios personalizados para las aplicaciones siempre que sea posible. Algunas de las ventajas de los dominios personalizados son:

- Los usuarios pueden acceder a la aplicación con la misma dirección URL, ya estén trabajando dentro o fuera de la red.
- Si todas las aplicaciones tienen las mismas direcciones URL internas y externas, los vínculos de una aplicación que señalan a otra seguirán funcionando fuera de la red corporativa. 
- Puede controlar la personalización de marca y crear las direcciones URL que quiera. 


## <a name="configure-a-custom-domain"></a>Configuración de un dominio personalizado

Antes de configurar un dominio personalizado, asegúrese de que tener preparados los siguientes requisitos: 
- Un [dominio comprobado agregado a Azure Active Directory](active-directory-domains-add-azure-portal.md).
- Un certificado personalizado para el dominio, en forma de un archivo PFX. 
- Una aplicación local [publicada a través del proxy de la aplicación](application-proxy-publish-azure-portal.md).

Cuando tenga listos estos tres requisitos, siga estos pasos para configurar el dominio personalizado:

1. Inicie sesión en el [Portal de Azure](https://portal.azure.com).
2. Vaya a **Azure Active Directory** > **Aplicaciones empresariales** > **Todas las aplicaciones** y elija la aplicación que quiere administrar.
3. Seleccione **Proxy de la aplicación**. 
4. En el campo de dirección URL externa, use la lista desplegable para seleccionar el dominio personalizado. Si no ve su dominio en la lista, es que no se ha comprobado todavía. 
5. El campo **Certificado** que se deshabilitó se habilita. Seleccione este campo. 

   ![Haga clic para cargar un certificado.](./media/active-directory-application-proxy-custom-domains/certificate.png)

   Si este campo permanece deshabilitado, es probable que un certificado ya esté cargado para ese dominio. 

6. Cargue el certificados PFX y escriba su contraseña. 
7. Haga clic en **Guardar** para guardar los cambios. 
8. Agregue un registro DNS que redirija la nueva dirección URL externa al dominio msappproxy.net. 

>[!TIP] 
>Solo es necesario cargar un certificado por dominio personalizado. Después de cargar un certificado, puede elegir el dominio personalizado cuando publique una nueva aplicación y no tiene que configurar nada más excepto el registro DNS. 

## <a name="manage-certificates"></a>Administración de certificados

### <a name="certificate-format"></a>Formato del certificado
No hay ninguna restricción sobre los métodos de firma del certificado. Se admiten ECC, SAN y otros tipos comunes de certificado. También puede usar certificados con caracteres comodín. Si usa un certificado comodín, asegúrese de que el carácter comodín coincida con la dirección URL externa deseada. También se aceptan certificados autofirmados. Si usa una entidad de certificación privada, el CDP (punto de distribución de lista de revocación de certificados) del certificado debe ser público.

### <a name="changing-the-domain"></a>Cambio del dominio
Todos los dominios comprobados aparecen en la lista desplegable de direcciones URL externas de la aplicación. Para cambiar el dominio, actualice ese campo de la aplicación. Si selecciona un dominio que no tiene un certificado asociado, siga los pasos del 5 al 7 para agregarlo. Si el dominio que desea no está en la lista, [agréguelo como dominio comprobado](active-directory-domains-add-azure-portal.md). A continuación, asegúrese de actualizar el registro DNS para redirigirlo desde la nueva dirección URL externa. 

### <a name="certificate-management"></a>Administración de certificados
Puede usar el mismo certificado para varias aplicaciones a menos que las aplicaciones compartan un host externo. 

Cuando un certificado expira, recibirá una advertencia que le indica que cargue otro certificado mediante el portal. Si se revoca el certificado, los usuarios pueden ver una advertencia de seguridad al acceder a la aplicación. No se realizan comprobaciones de revocación de los certificados.  Para actualizar el certificado en una aplicación dada, vaya a la aplicación y siga los pasos del 5 al 7 para configurar dominios personalizados en aplicaciones publicadas y cargar un nuevo certificado. Si no se usa un certificado antiguo con otras aplicaciones, se elimina automáticamente. 

Actualmente, toda la administración de certificados es a través de páginas de aplicación individuales, por lo que deberá administrar los certificados en el contexto de las aplicaciones pertinentes. 

## <a name="next-steps"></a>Pasos siguientes
* [Habilitar el inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md) en las aplicaciones publicadas con la autenticación de Azure AD.
* [Habilitar el acceso condicional](active-directory-application-proxy-conditional-access.md) a las aplicaciones publicadas.
* [Incorporación de su nombre de dominio personalizado a Azure AD](active-directory-domains-add-azure-portal.md)



