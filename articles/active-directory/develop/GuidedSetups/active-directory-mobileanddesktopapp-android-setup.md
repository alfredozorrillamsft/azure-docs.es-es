---
title: "Introducción a Android en Azure AD v2: instalación | Microsoft Docs"
description: "Cómo puede una aplicación de Android obtener un token de acceso y llamar a las API Graph que requieren tokens de acceso desde el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.translationtype: Human Translation
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.openlocfilehash: a43d7e30a6f4176afba27f0de2c2c116df741080
ms.contentlocale: es-es


---

## <a name="set-up-your-project"></a>Configurar su proyecto

> ¿Prefiere descargar este proyecto de Android Studio de ejemplo en su lugar? [Descargue un proyecto](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) y vaya al [paso de configuración](#create-an-application-express) para configurar el código de ejemplo antes de ejecutarlo.


### <a name="create-a-new-project"></a>Crear un nuevo proyecto 
1.  Abra Android Studio, vaya a `File` > `New` > `New Project`.
2.  Asigne un nombre a la aplicación y haga clic en `Next`.
3.  Asegúrese de seleccionar *API 21 o posterior (Android 5.0)* y haga clic en`Next`
4.  Salga de `Empty Activity`, haga clic en `Next` y luego en `Finish`.


### <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a>Adición de la biblioteca de autenticación de Microsoft (MASL) a su proyecto
1.  En Android Studio, vaya a `Gradle Scripts` > `build.gradle (Module: app)`.
2.  Copie y pegue el código siguiente en `Dependencies`:

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a>Acerca de este paquete

El paquete anterior instala la biblioteca de autenticación de Microsoft (MSAL). MSAL controla la adquisición, el almacenamiento en caché y la actualización de los tokens de usuario que se utilizan para tener acceso a las API protegidas por el punto de conexión de Azure Active Directory v2.
<!--end-collapse-->

## <a name="create-your-applications-ui"></a>Creación de la IU de la aplicación

1.  Abra `activity_main.xml` en `res` > `layout`.
2.  Cambie el diseño de la actividad de `android.support.constraint.ConstraintLayout` u otro a `LinearLayout`.
3.  Agregue la propiedad `android:orientation="vertical"` al nodo `LinearLayout`.
4.  Copie y pegue el código siguiente en el nodo `LinearLayout`, reemplazando el contenido actual:

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```


