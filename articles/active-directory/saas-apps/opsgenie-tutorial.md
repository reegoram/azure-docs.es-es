---
title: 'Tutorial: Integración de Azure Active Directory con OpsGenie | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y OpsGenie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: 715035072ddc2ceb087d003dd5da5bc47572e9b9
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39444358"
---
# <a name="tutorial-azure-active-directory-integration-with-opsgenie"></a>Tutorial: Integración de Azure Active Directory con OpsGenie

En este tutorial, aprenderá a integrar Pluralsight con Azure Active Directory (Azure AD).

La integración de OpsGenie con Azure AD le proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a OpsGenie.
- Puede permitir que los usuarios inicien sesión automáticamente en OpsGenie (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con OpsGenie, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en Pluralsight

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Adición de OpsGenie desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-opsgenie-from-the-gallery"></a>Adición de OpsGenie desde la galería
Para configurar la integración de OpsGenie en Azure AD, deberá agregar OpsGenie desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar OpsGenie desde la galería, realice los pasos siguientes:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro de búsqueda, escriba **OpsGenie**.

    ![Creación de un usuario de prueba de Azure AD](./media/opsgenie-tutorial/tutorial_opsgenie_search.png)

1. En el panel de resultados, seleccione **OpsGenie** y luego haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/opsgenie-tutorial/tutorial_opsgenie_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con OpsGenie con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de OpsGenie para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de OpsGenie.

Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de OpsGenie.

Para configurar y probar el inicio de sesión único de Azure AD con OpsGenie, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
1. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Creación de un usuario de prueba de OpsGenie](#creating-a-opsgenie-test-user)**: el objetivo es tener un homólogo de Britta Simon en OpsGenie que esté vinculado a la representación del usuario en Azure AD.
1. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en el portal de Azure y lo configurará en la aplicación OpsGenie.

**Para configurar el inicio de sesión único de Azure AD con OpsGenie, realice los pasos siguientes:**

1. En la página de integración de la aplicación **OpsGenie** de Azure Portal, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/opsgenie-tutorial/tutorial_opsgenie_samlbase.png)

1. En la sección **Dominio y direcciones URL de OpsGenie**, lleve a cabo los pasos siguientes:

    ![Configurar inicio de sesión único](./media/opsgenie-tutorial/tutorial_opsgenie_url.png)

    En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL: `https://app.opsgenie.com/auth/login`

1. En la sección **Certificado de firma de SAML**, haga clic en el botón Copiar para copiar la **dirección URL de metadatos de federación de la aplicación** y péguela en el Bloc de notas.

    ![Vínculo de descarga del certificado](./media/opsgenie-tutorial/tutorial_opsgenie_certificate.png)

1. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/opsgenie-tutorial/tutorial_general_400.png)

1. En la sección **Configuración de OpsGenie**, haga clic en **Configurar OpsGenie** para abrir la ventana **Configurar inicio de sesión**. Copie la **dirección URL del servicio de inicio de sesión único de SAML** de la sección Referencia rápida.

    ![Configurar inicio de sesión único](./media/opsgenie-tutorial/tutorial_opsgenie_configure.png)

1. Abra otra instancia del explorador y después inicie sesión en OpsGenie como administrador.

1. Haga clic en **Configuración** y después en la pestaña **Inicio de sesión único**.
   
    ![Inicio de sesión único de OpsGenie](./media/opsgenie-tutorial/tutorial_opsgenie_06.png)

1. Para habilitar SSO, seleccione **Habilitado**.
   
    ![Configuración de OpsGenie](./media/opsgenie-tutorial/tutorial_opsgenie_07.png) 

1. En la sección **Proveedor**, haga clic en la pestaña **Azure Active Directory**.
   
    ![Configuración de OpsGenie](./media/opsgenie-tutorial/tutorial_opsgenie_08.png) 

1. En la página de diálogo de Azure Active Directory, realice los siguientes pasos:
   
    ![Configuración de OpsGenie](./media/opsgenie-tutorial/tutorial_opsgenie_09.png)
    
    a. En el cuadro de texto **SAML 2.0 Endpoint** (Punto de conexión SAML 2.0), pegue el valor de la **dirección URL del servicio de inicio de sesión único** que ha copiado de Azure Portal.
    
    b. En el cuadro de texto **URL de metadatos**, pegue el valor de **Dirección URL de metadatos de federación de la aplicación** que copió en Azure Portal.
    
    c. Haga clic en **Guardar cambios**.

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/opsgenie-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/opsgenie-tutorial/create_aaduser_02.png) 

1. Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/opsgenie-tutorial/create_aaduser_03.png) 

1. En la página de diálogo **Usuario**, realice los siguientes pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/opsgenie-tutorial/create_aaduser_04.png) 

    a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="creating-a-opsgenie-test-user"></a>Creación de un usuario de prueba de OpsGenie

El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en OpsGenie. 

1. En una ventana del explorador web, inicie sesión en el inquilino de OpsGenie como administrador.

1. Vaya a la lista Usuarios haciendo clic en **Usuario** en el panel izquierdo.
   
   ![Configuración de OpsGenie](./media/opsgenie-tutorial/tutorial_opsgenie_10.png) 

1. Haga clic en **Agregar usuario**.

1. En el cuadro de diálogo **Agregar usuario** , realice los pasos siguientes:
   
   ![Configuración de OpsGenie](./media/opsgenie-tutorial/tutorial_opsgenie_11.png)
   
   a. En el cuadro de texto **Email** (Correo electrónico), escriba la dirección de correo electrónico de BrittaSimon en Azure Active Directory.
   
   b. En el cuadro de texto **Nombre completo**, escriba **Britta Simon**.
   
   c. Haga clic en **Save**(Guardar). 

>[!NOTE]
>Britta recibirá un correo electrónico con instrucciones sobre cómo configurar su perfil.

### <a name="assigning-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a OpsGenie.

![Asignar usuario][200] 

**Para asignar a Britta Simon a OpsGenie, realice los pasos siguientes:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **OpsGenie**.

    ![Configurar inicio de sesión único](./media/opsgenie-tutorial/tutorial_opsgenie_app.png) 

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202] 

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.

Al hacer clic en el icono de OpsGenie en el panel de acceso, debería iniciar sesión automáticamente en su aplicación OpsGenie.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/opsgenie-tutorial/tutorial_general_01.png
[2]: ./media/opsgenie-tutorial/tutorial_general_02.png
[3]: ./media/opsgenie-tutorial/tutorial_general_03.png
[4]: ./media/opsgenie-tutorial/tutorial_general_04.png

[100]: ./media/opsgenie-tutorial/tutorial_general_100.png

[200]: ./media/opsgenie-tutorial/tutorial_general_200.png
[201]: ./media/opsgenie-tutorial/tutorial_general_201.png
[202]: ./media/opsgenie-tutorial/tutorial_general_202.png
[203]: ./media/opsgenie-tutorial/tutorial_general_203.png

