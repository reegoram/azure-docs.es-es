---
title: archivo de inclusión
description: archivo de inclusión
services: digital-twins
author: dsk-2015
ms.service: digital-twins
ms.topic: include
ms.date: 09/17/2018
ms.author: dkshir
ms.custom: include file
ms.openlocfilehash: 7bac2b291bec2ceda118c877cde997a2fa9f9f37
ms.sourcegitcommit: 74941e0d60dbfd5ab44395e1867b2171c4944dbe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2018
ms.locfileid: "49322980"
---
1. Inicie sesión en el [Azure Portal](http://portal.azure.com).

1. En el panel de navegación izquierdo, haga clic en **Crear un recurso**. Busque *Digital Twins* y seleccione **Digital Twins (preview)** (Digital Twins [versión preliminar]). Haga clic en **Crear** para iniciar el proceso de implementación.

    ![Creación de una instancia de Digital Twins](./media/create-digital-twins-portal/create-digital-twins.png)

1. En el panel **Digital Twins**, escriba la siguiente información:
   * **Nombre del recurso**: cree un nombre único para la instancia de Digital Twins.
   * **Suscripción**: elija la suscripción que quiere usar para crear esta instancia de Digital Twins. 
   * **Grupo de recursos**: seleccione o cree un [grupo de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) para la instancia de Digital Twins.
   * **Ubicación**: seleccione la ubicación más cercana a sus dispositivos.

    ![Creación de una instancia de Digital Twins](./media/create-digital-twins-portal/create-digital-twins-param.png)

1. Revise la información de Digital Twins y, luego, haga clic en **Crear**. La instancia de Digital Twins podría tardar unos minutos en crearse. Puede ver el progreso en el panel **Notificaciones**.

1. Abra el panel **Información general** de la instancia de Digital Twins. Observe el vínculo que se muestra en la sección **API de administración**.

    1. La dirección URL de la **API de administración** se formatea como: **_https://yourDigitalTwinsName.yourLocation.azuresmartspaces.net/management/swagger_**. Esta dirección URL le lleva a la documentación de la API REST de Azure Digital Twins que se aplica a la instancia. Lea [Uso de Azure Digital Twins Swagger](../articles/digital-twins/how-to-use-swagger.md) para aprender a leer y usar esta documentación de API.

    1. Modifique la dirección URL de la **API de administración** a este formato: **_https://yourDigitalTwinsName.yourLocation.azuresmartspaces.net/management/api/v1.0/_**. La aplicación usará la dirección URL modificada como dirección URL base para acceder a la instancia. Copie esta dirección URL modificada en un archivo temporal. La necesitará en la próxima sección.

    ![API de administración](./media/create-digital-twins-portal/digital-twins-management-api.png)