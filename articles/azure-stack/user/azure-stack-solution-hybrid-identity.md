---
title: Configuración de la identidad de nube híbrida con aplicaciones de Azure y Azure Stack | Microsoft Docs
description: Aprenda a configurar la identidad de nube híbrida con aplicaciones de Azure y Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 09/28/2018
ms.author: mabrigg
ms.reviewer: Anjay.Ajodha
ms.openlocfilehash: 7cea11f448f20ace2dd50454834e60ce3a3c3b70
ms.sourcegitcommit: 5843352f71f756458ba84c31f4b66b6a082e53df
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47584275"
---
# <a name="tutorial-configure-hybrid-cloud-identity-for-azure-and-azure-stack-applications"></a>Tutorial: Configuración de la identidad de nube híbrida para aplicaciones de Azure y Azure Stack

*Se aplica a: sistemas integrados de Azure Stack y Kit de desarrollo de Azure Stack*

Aprenda a configurar la identidad de nube híbrida para sus aplicaciones de Azure y Azure Stack.

Tiene dos opciones para conceder acceso a sus aplicaciones tanto en Azure global como en Azure Stack.

 * Cuando Azure Stack tiene conexión continua a Internet, puede usar Azure Active Directory (Azure AD).
 * Cuando Azure Stack se desconecta de Internet, puede usar los Servicios de federación de Active Directory (AD FS).

Usará entidades de servicio para conceder acceso a las aplicaciones de Azure Stack, con el fin de realizar una implementación o configuración mediante Azure Resource Manager en Azure Stack.

En este tutorial, creará un entorno de ejemplo para:

> [!div class="checklist"]
> - Establecer una identidad híbrida en Azure global y Azure Stack
> - Recuperar un token para acceder a la API de Azure Stack.

Para seguir los pasos de este tutorial debe tener permisos de operador de Azure Stack.

> [!Tip]  
> ![hybrid-pillars.png](./media/azure-stack-solution-cloud-burst/hybrid-pillars.png)  
> Microsoft Azure Stack es una extensión de Azure. Azure Stack aporta la agilidad y la innovación de la informática en la nube a su entorno local y hace posible la única nube híbrida que le permite crear e implementar aplicaciones híbridas en cualquier parte.  
> 
> En las notas del producto [Consideraciones de diseño para aplicaciones híbridas](https://aka.ms/hybrid-cloud-applications-pillars) se revisan los pilares de la calidad de software (selección de ubicación, escalabilidad, disponibilidad, resistencia, capacidad de administración y seguridad) para diseñar, implementar y usar aplicaciones híbridas. Las consideraciones de diseño ayudan a optimizar el diseño de aplicaciones híbridas y reducen los desafíos en los entornos de producción.


## <a name="create-a-service-principal-for-azure-ad-in-the-portal"></a>Crear a una entidad de servicio para Azure AD en el portal

Si ha implementado Azure Stack con Azure AD como el almacén de identidades, puede crear entidades de servicio igual que hace para Azure. El artículo sobre la [creación de entidades de servicio](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-azure-ad) muestra cómo realizar los pasos en el portal. Compruebe que tiene los [permisos de Azure AD necesarios](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#required-permissions) antes de comenzar.

## <a name="create-a-service-principal-for-ad-fs-using-powershell"></a>Creación de una entidad de servicio para AD FS mediante PowerShell

Si ha implementado Azure Stack con AD FS, puede usar PowerShell para crear una entidad de servicio, asignar un rol para el acceso e iniciar sesión en Powershell con dicha identidad. En la sección [Creación de una entidad de servicio para AD FS](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-create-service-principals#create-service-principal-for-ad-fs) se muestra cómo realizar los pasos necesarios con PowerShell.

## <a name="using-the-azure-stack-api"></a>Uso de la API de Azure Stack

El tutorial de la [API de Azure Stack](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-rest-api-use) le guía por el proceso de recuperación de un token de acceso a la API de Azure Stack.

## <a name="connect-to-azure-stack-using-powershell"></a>Conexión a Azure Stack con Powershell

La guía de inicio rápido para [empezar a trabajar con PowerShell en Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-powershell-configure-quickstart) le guía por los pasos necesarios para instalar Azure PowerShell y conectarse a su instalación de Azure Stack.

### <a name="prerequisites"></a>Requisitos previos

Una instalación de Azure Stack conectada a Azure Active Directory con una suscripción a la que puede acceder. Si no tiene una instalación de Azure Stack, puede usar estas instrucciones para configurar un [Kit de desarrollo de Azure Stack](https://docs.microsoft.com/azure/azure-stack/asdk/asdk-deploy).

#### <a name="connect-to-azure-stack-using-code"></a>Conexión a Azure Stack mediante código

Para conectarse a Azure Stack mediante código, use la API de los puntos de conexión de Azure Resource Manager para obtener los puntos de conexión de autenticación y Graph para la instalación de Azure Stack y, luego, autentíquese mediante solicitudes de REST. Puede encontrar una aplicación cliente de ejemplo en [GitHub](https://github.com/shriramnat/HybridARMApplication).

>[!Note]
>A menos que el SDK de Azure correspondiente al lenguaje seleccionado admita perfiles de API de Azure, puede que el SDK no funcione con Azure Stack. Para más información acerca de los perfiles de la API de Azure, consulte el artículo [Administración de los perfiles de la versión de API](https://docs.microsoft.com/da-dk/azure/azure-stack/user/azure-stack-version-profiles).

## <a name="next-steps"></a>Pasos siguientes

 - Para más información sobre cómo se trata la identidad en Azure Stack, consulte [Arquitectura de identidad para Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-identity-architecture).
 - Para más información sobre los patrones de nube de Azure, consulte [Patrones de diseño en la nube](https://docs.microsoft.com/azure/architecture/patterns).
