---
title: 'Tutorial: integración de Azure Active Directory con Freshservice | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Freshservice.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: eb848ede258d8d25d4734664bd500235f34359e7
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39440667"
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a>Tutorial: integración de Azure Active Directory con Freshservice

En este tutorial, aprenderá a integrar Freshservice con Azure Active Directory (Azure AD).

La integración de Freshservice con Azure AD proporciona las siguientes ventajas:

- En Azure AD se puede controlar quién tiene acceso a Freshservice
- Puede permitir que los usuarios inicien sesión automáticamente en Freshservice (inicio de sesión único) con sus cuentas de Azure AD
- Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con Freshservice, se necesitan los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Freshservice

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Agregar Freshservice desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-freshservice-from-the-gallery"></a>Agregar Freshservice desde la galería
Para configurar la integración de Freshservice en Azure AD, deberá agregar Freshservice desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar Freshservice desde la galería, siga estos pasos:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro de búsqueda, escriba **Freshservice**.

    ![Creación de un usuario de prueba de Azure AD](./media/freshservice-tutorial/tutorial_freshservice_search.png)

1. En el panel de resultados, seleccione **Freshservice** y luego haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Freshservice con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Freshservice para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Freshservice.

Para establecer la relación de vínculo, en Freshservice, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.

Para configurar y probar el inicio de sesión único de Azure AD con Freshservice, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
1. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Creación de un usuario de prueba de Freshservice](#creating-a-freshservice-test-user)**: para tener un homólogo de Britta Simon en Freshservice que esté vinculado a la representación de Azure AD de usuario.
1. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Freshservice.

**Para configurar el inicio de sesión único de Azure AD con Freshservice, realice los pasos siguientes:**

1. En Azure Portal, en la página de integración de la aplicación **Freshservice**, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/freshservice-tutorial/tutorial_freshservice_samlbase.png)

1. En la sección **Dominio y direcciones URL de Freshservice**, siga estos pasos:

    ![Configurar inicio de sesión único](./media/freshservice-tutorial/tutorial_freshservice_url.png)

    a. En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<democompany>.freshservice.com`.

    b. En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<democompany>.freshservice.com`

    > [!NOTE] 
    > Estos valores no son reales. Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión. Para obtener estos valores, póngase en contacto con el [equipo de soporte técnico de clientes de Freshservice](https://support.freshservice.com/). 
 
1. En la sección **Certificado de firma de SAML**, copie el valor de **HUELLA DIGITAL** del certificado.

    ![Configurar inicio de sesión único](./media/freshservice-tutorial/tutorial_freshservice_certificate.png)

1. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/freshservice-tutorial/tutorial_general_400.png)

1. En la sección **Configuración de Freshservice**, haga clic en **Configurar Freshservice** para abrir la ventana **Configurar inicio de sesión**. Copie los valores **Sign-Out URL y SAML Single Sign-On Service URL** (Dirección URL de cierre de sesión y Dirección URL del servicio de inicio de sesión único de SAML) de la **sección de referencia rápida**.

    ![Configurar inicio de sesión único](./media/freshservice-tutorial/tutorial_freshservice_configure.png) 

1. En otra ventana del explorador web, inicie sesión en el sitio de la compañía de Freshservice como administrador.

1. En el menú de la parte superior, haga clic en **Administrador**.
   
    ![Administración](./media/freshservice-tutorial/ic790814.png "Administración")

1. En el **Portal del cliente**, haga clic en **Seguridad**.
   
    ![Seguridad](./media/freshservice-tutorial/ic790815.png "Seguridad")

1. En la sección **Seguridad** , realice estos pasos:
   
    ![Inicio de sesión único](./media/freshservice-tutorial/ic790816.png "Inicio de sesión único")
   
    a. Cambie a **Inicio de sesión único**.

    b. Seleccione **Inicio de sesión único de SAML**.

    c. En el cuadro de texto **SAML Login URL** (Dirección URL de inicio de sesión de SAML), pegue el valor de **SAML Single Sign-On Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) que ha copiado de Azure Portal.

    d. En el cuadro de texto **URL de cierre de sesión**, pegue el valor de **Sign-Out URL** (Dirección URL de cierre de sesión) que copió de Azure Portal.

    e. En el cuadro de texto **Security Certificate Fingerprint** (Huella digital de certificado de seguridad), pegue el valor de **HUELLA DIGITAL** del certificado que haya copiado de Azure Portal.

    f. Haga clic en **Guardar**

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/freshservice-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/freshservice-tutorial/create_aaduser_02.png) 

1. Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/freshservice-tutorial/create_aaduser_03.png) 

1. En la página de diálogo **Usuario**, realice los siguientes pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/freshservice-tutorial/create_aaduser_04.png) 

    a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="creating-a-freshservice-test-user"></a>Creación de un usuario de prueba de Freshservice

Para permitir que los usuarios de Azure AD inicien sesión en FreshService, deben aprovisionarse en FreshService. En el caso de FreshService, el aprovisionamiento es una tarea manual.

**Para aprovisionar una cuenta de usuario, realice estos pasos:**

1. Inicie sesión en el sitio de la compañía de **FreshService** como administrador.

1. En el menú de la parte superior, haga clic en **Administrador**.
   
    ![Administración](./media/freshservice-tutorial/ic790814.png "Administración")

1. En la sección **User Management** (Administración de usuarios), haga clic en **Requesters** (Solicitantes).
   
    ![Solicitantes](./media/freshservice-tutorial/ic790818.png "Solicitantes")

1. Haga clic en **Nuevo solicitante**.
   
    ![Nuevos solicitantes](./media/freshservice-tutorial/ic790819.png "Nuevos solicitantes")

1. En la sección **New Requester** (Nuevo solicitante), lleve a cabo estos pasos:
   
    ![Nuevo solicitante](./media/freshservice-tutorial/ic790820.png "Nuevo solicitante")   

    a. Escriba los atributos **First Name** (Nombre) y **Email** (Correo electrónico) de una cuenta de Azure Active Directory válida que desee aprovisionar en los cuadros de texto relacionados.

    b. Haga clic en **Save**(Guardar).
   
    >[!NOTE]
    >El titular de la cuenta de Azure Active Directory recibe un mensaje de correo electrónico con un vínculo para confirmar la cuenta antes de que se active.
    >  

>[!NOTE]
>Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de FreshService que proporcione FreshService para aprovisionar cuentas de usuario de AAD.
>  

![Asignar usuario][200] 

**Para asignar Britta Simon a Freshservice, siga estos pasos:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **Freshservice**.

    ![Configurar inicio de sesión único](./media/freshservice-tutorial/tutorial_freshservice_app.png) 

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202] 

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.

Al hacer clic en el icono de Freshservice en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Freshservice.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/freshservice-tutorial/tutorial_general_01.png
[2]: ./media/freshservice-tutorial/tutorial_general_02.png
[3]: ./media/freshservice-tutorial/tutorial_general_03.png
[4]: ./media/freshservice-tutorial/tutorial_general_04.png

[100]: ./media/freshservice-tutorial/tutorial_general_100.png

[200]: ./media/freshservice-tutorial/tutorial_general_200.png
[201]: ./media/freshservice-tutorial/tutorial_general_201.png
[202]: ./media/freshservice-tutorial/tutorial_general_202.png
[203]: ./media/freshservice-tutorial/tutorial_general_203.png

