---
title: Comprar un nombre de dominio personalizado para Azure Web Apps
description: "Obtenga información sobre cómo comprar un nombre de dominio personalizado con una aplicación web en el servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: robmcm
ms.translationtype: HT
ms.sourcegitcommit: 79bebd10784ec74b4800e19576cbec253acf1be7
ms.openlocfilehash: c42e419984ee4b7f30c8423b9a0c420e2c981949
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Comprar un nombre de dominio personalizado para Azure Web Apps

Los dominios de App Service (versión preliminar) son dominios de nivel superior que se administran directamente en Azure. Facilitan la administración de dominios personalizados para [Azure Web Apps](app-service-web-overview.md). En este tutorial se muestra cómo comprar un dominio de App Service y asignar nombres DNS a Azure Web Apps.

Este artículo trata sobre el Servicio de aplicaciones de Azure (aplicaciones web, aplicaciones de API, aplicaciones móviles, Logic Apps); para Servicios en la nube, consulte [Configuración de un nombre de dominio personalizado para un servicio en la nube de Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial:

* [Cree una aplicación de App Service](/azure/app-service/) o use alguna aplicación que haya creado para otro tutorial.

## <a name="prepare-the-app"></a>Preparación de la aplicación

Para usar dominios personalizados en Azure Web Apps, el [plan de App Service](https://azure.microsoft.com/pricing/details/app-service/) de la aplicación web debe ser un nivel de pago (**Compartido**, **Básico**, **Estándar** o **Premium**). En este paso, asegúrese de que la aplicación web se encuentra en el plan de tarifa admitido.

### <a name="sign-in-to-azure"></a>Inicio de sesión en Azure

Abra [Azure Portal](https://portal.azure.com) e inicie sesión con su cuenta de Azure.

### <a name="navigate-to-the-app-in-the-azure-portal"></a>Navegue hasta la aplicación en Azure Portal

En el menú izquierdo, seleccione **App Services** y, después, el nombre de la aplicación.

![Navegación en el portal a la aplicación de Azure](./media/app-service-web-tutorial-custom-domain/select-app.png)

Consulte la página de administración de la aplicación de App Service.  

### <a name="check-the-pricing-tier"></a>Comprobar el plan de tarifa

En el panel de navegación izquierdo de la página de la aplicación, desplácese hasta la sección **Configuración** y seleccione **Escalar verticalmente (plan de App Service)**.

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

El nivel actual de la aplicación aparece resaltado con un cuadro azul. Asegúrese de que la aplicación web no está en el nivel **Gratis**. No se admiten DNS personalizados en el nivel **Gratis**. 

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Si el plan de App Service no es **Gratuito**, cierre la página **Elegir un plan de tarifa** y vaya a [Comprar un dominio](#buy-the-domain).

### <a name="scale-up-the-app-service-plan"></a>Escalado verticalmente del plan de App Service

Seleccione alguno de los niveles de pago (**Compartido**, **Básico**, **Estándar** o **Premium**). 

Haga clic en **Seleccionar**.

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Cuando vea la siguiente notificación, significará que la operación de escalado se habrá completado.

![Confirmación de la operación de escalado](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-the-domain"></a>Comprar el dominio

### <a name="sign-in-to-azure"></a>Inicio de sesión en Azure
Abra [Azure Portal](https://portal.azure.com/) e inicie sesión con su cuenta de Azure.

### <a name="launch-buy-domains"></a>Iniciar Comprar dominios
En la pestaña **Web Apps**, haga clic en el nombre de la aplicación web, seleccione **Configuración** y elija **Dominios personalizados**.
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

En la página **Dominios personalizados**, haga clic en **Comprar dominios**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-the-domain-purchase"></a>Configurar la compra del dominio

En la página **Dominio de App Service**, escriba el nombre de dominio que quiere comprar en el cuadro **Buscar dominio** y escriba `Enter`. Los dominios disponibles sugeridos se muestran justo debajo del cuadro de texto. Seleccione uno o varios dominios que quiera comprar. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Haga clic en **Información de contacto** y rellene el formulario de información de contacto del dominio. Cuando termine, haga clic en **Aceptar** para volver a la página Dominio de App Service.
   
Es importante que rellene todos los campos obligatorios con la mayor precisión posible. Los datos incorrectos para la información de contacto pueden producir un error al comprar los dominios. 

A continuación, seleccione las opciones que quiera para el dominio. Para obtener explicaciones, vea la tabla siguiente:

| Configuración | Valor sugerido | Descripción |
|-|-|-|
|Renovación automática | **Habilitación** | Renueva automáticamente el dominio de App Service cada año. En el momento de la renovación se cargará el mismo precio de compra en su tarjeta de crédito. |
|Protección de la privacidad | Habilitar | Participe en "Protección de la privacidad", que se incluye en el precio de compra _gratuitamente_ (excepto para los dominios de nivel superior cuyo registro no admite la protección de la privacidad, como _.co.in_, _.co.uk_ y así sucesivamente). |
| Asignar nombres de host predeterminados | **www** y **@** | Seleccione los enlaces de nombre de host deseados, si quiere. Una vez completada la operación de compra de dominio, puede tener acceso a la aplicación web en los nombres de host seleccionados. Si la aplicación web está detrás de [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), no verá la opción para asignar el dominio raíz (@), ya que Traffic Manager no admite registros A. Puede realizar cambios en las asignaciones de nombre de host una vez completada la compra del dominio. |

### <a name="accept-terms-and-purchase"></a>Aceptar los términos y comprar

Haga clic en **Condiciones legales** para consultar las condiciones y los gastos y, después, haga clic en **Comprar**.

> [!NOTE]
> Los dominios de App Service usan DNS de Azure para hospedar los dominios. Además de la tarifa de registro del dominio, se aplican cargos de uso de DNS de Azure. Para obtener más información, vea [DNS de Azure Precios](https://azure.microsoft.com/pricing/details/dns/).
>
>

De nuevo en la hoja **Dominio de App Service**, haga clic en **Aceptar**. Mientras la operación está en curso, verá las notificaciones siguientes:

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-the-hostnames"></a>Probar los nombres de host

Si ha asignado nombres de host predeterminados a la aplicación web, también verá una notificación de operación correcta para cada nombre de host seleccionado. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

También verá los nombres de host seleccionados en la página **Dominios personalizados**, en la sección **Nombres de host**. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

Para probar los nombres de host, vaya a los nombres de host enumerados en el explorador. En el ejemplo de la captura de pantalla anterior, intente navegar a _kontoso.net_ y _www.kontoso.net_.

## <a name="assign-hostnames-to-web-app"></a>Asignar nombres de host a la aplicación web

Si decide no asignar uno o varios nombres de host predeterminados a la aplicación web durante el proceso de compra, o si tiene que asignar un nombre de host que no aparece, puede asignar un nombre de host en cualquier momento.

También puede asignar nombres de host en el dominio de App Service a cualquier otra aplicación web. Los pasos dependen de si el dominio de App Service y la aplicación web pertenecen a la misma suscripción.

- Suscripción diferente: asigne los registros DNS personalizados desde el dominio de App Service a la aplicación web como un dominio comprado de forma externa. Para obtener información sobre cómo agregar nombres DNS personalizados a un dominio de App Service, vea [Administrar los registros DNS personalizados](#custom). Para asignar un dominio comprado externo a una aplicación web, vea [Asignar un nombre DNS personalizado a Azure Web Apps](app-service-web-tutorial-custom-domain.md). 
- La misma suscripción: siga los pasos que hay a continuación.

### <a name="launch-add-hostname"></a>Iniciar Agregar nombre de host
En la página **App Services**, seleccione el nombre de la aplicación web a la que quiere asignar los nombres de host, seleccione **Configuración** y después **Dominios personalizados**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Asegúrese de que el dominio comprado aparece en la sección **Dominios de App Service**, pero no lo seleccione. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Todos los dominios de App Service de la misma suscripción se muestran en la página **Dominios personalizados** de la aplicación web. Si el dominio está en la suscripción de la aplicación web, pero no puede verlo en la página **Dominios personalizados** de la aplicación web, intente volver a abrir la página **Dominios personalizados** o actualice la página web. Compruebe también la campana de notificación situada en la parte superior de Azure Portal para ver el progreso o los errores de creación.
>
>

Seleccione **Agregar nombre de host**.

### <a name="configure-hostname"></a>Configurar el nombre de host
En el cuadro de diálogo **Agregar nombre de host**, escriba el nombre de dominio completo de su dominio de App Service o cualquier subdominio. Por ejemplo:

- kontoso.net
- www.kontoso.net
- abc.kontoso.net

Cuando termine, seleccione **Validar**. El tipo de registro de nombre de host se selecciona automáticamente.

Seleccione **Agregar nombre de host**.

Una vez completada la operación, verá una notificación de operación correcta para el nombre de host asignado.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>Cerrar Agregar nombre de host
En la página **Agregar nombre de host**, asigne otros nombres de host a la aplicación web, según sea necesario. Cuando termine, cierre la página **Agregar nombre de host**.

Ahora debería ver el nombre de host recién asignado en la página **Dominios personalizados** de la aplicación.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-the-hostnames"></a>Probar los nombres de host

Vaya a los nombres de host enumerados en el explorador. En el ejemplo de la captura de pantalla anterior, intente navegar a _abc.kontoso.net_.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>Administrar los registros DNS personalizados

En Azure, los registros DNS para un dominio de App Service se administran mediante [DNS de Azure](https://azure.microsoft.com/services/dns/). Puede agregar, quitar y actualizar los registros DNS, al igual que para un dominio comprado de forma externa.

### <a name="open-app-service-domain"></a>Abrir Dominio de App Service

En Azure Portal, en el menú de la izquierda, seleccione **Más servicios** > **Dominios de App Service**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Seleccione el dominio que se va a administrar. 

### <a name="access-dns-zone"></a>Obtener acceso a la zona DNS

En el menú de la izquierda del dominio, seleccione **Zona DNS**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Esta acción abre la página [Zona DNS](../dns/dns-zones-records.md) de su dominio de App Service en DNS de Azure. Para obtener información sobre cómo editar los registros DNS, vea [Administración de zonas DNS en Azure Portal](../dns/dns-operations-dnszones-portal.md).

## <a name="cancel-purchase-delete-domain"></a>Cancelar la compra (eliminar el dominio)

Después de comprar el dominio de App Service, dispone de cinco días para cancelar la compra para obtener un reembolso completo. Después de cinco días, puede eliminar el dominio de App Service, pero no puede recibir un reembolso.

### <a name="open-app-service-domain"></a>Abrir Dominio de App Service

En Azure Portal, en el menú de la izquierda, seleccione **Más servicios** > **Dominios de App Service**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Seleccione el dominio que quiera cancelar o eliminar. 

### <a name="delete-hostname-bindings"></a>Eliminación de enlaces de nombre de host

En el menú de la izquierda del dominio, seleccione **Enlaces de nombre de host**. Aquí se enumeran los enlaces de nombre de host de todos los servicios de Azure.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

No se puede eliminar el dominio de App Service hasta que se eliminen todos los enlaces de nombre de host.

Para eliminar todos los enlaces de nombre de host, seleccione **...** > **Eliminar**. Después de eliminarlos todos, haga clic en **Guardar**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>Cancelar o eliminar

En el menú de la izquierda del dominio, seleccione **Información general**. 

Si no ha transcurrido el período de cancelación en el dominio comprado, haga clic en **Cancelar compra**. De lo contrario, en su lugar verá el botón **Eliminar**. Para eliminar el dominio sin un reembolso, haga clic en **Eliminar**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

Haga clic en **Aceptar** para confirmar la operación. Si no quiere continuar, haga clic en cualquier lugar fuera del cuadro de diálogo de confirmación.

Una vez completada la operación, el dominio se libera de la suscripción y vuelve a estar disponible para que otros usuarios lo compren. 

