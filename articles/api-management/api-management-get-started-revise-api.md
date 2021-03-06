---
title: Uso de revisiones para realizar cambios que no producen interrupciones de forma segura en Azure API Management | Microsoft Docs
description: Siga los pasos de este tutorial para obtener información sobre cómo realizar cambios que no producen interrupciones a través de revisiones en API Management.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.custom: mvc
ms.topic: tutorial
ms.date: 06/15/2018
ms.author: apimpm
ms.openlocfilehash: c1c884e05d357db7e23574dbd31f206d6c3fe23c
ms.sourcegitcommit: 17fe5fe119bdd82e011f8235283e599931fa671a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/11/2018
ms.locfileid: "41921017"
---
# <a name="use-revisions-to-make-non-breaking-changes-safely"></a>Uso de revisiones para realizar cambios que no producen interrupciones de forma segura
Cuando la API esté lista y los desarrolladores empiecen a usarla, tendrá que realizar cambios en dicha API y, al mismo tiempo, no interrumpir a quienes la llaman. También resulta útil informar a los desarrolladores de los cambios realizados. Esto se logra en Azure API Management con las **revisiones**. Para más información, consulte [Versions & revisions](https://blogs.msdn.microsoft.com/apimanagement/2017/09/14/versions-revisions/) (Versiones y revisiones) y [API Versioning with Azure API Management](https://blogs.msdn.microsoft.com/apimanagement/2017/09/13/api-versioning-with-azure-api-management/) (Control de versiones con Azure API Management).

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Agregar una nueva revisión
> * Realizar cambios que no producen interrupciones en la revisión
> * Convertir la revisión en actual y agregar una entrada en el registro de cambios
> * Examinar el portal para desarrolladores para ver los cambios y registro de cambios

![Registro de cambios en el portal para desarrolladores](media/api-management-getstarted-revise-api/azure_portal.PNG)

## <a name="prerequisites"></a>Requisitos previos

+ Completar la guía de inicio rápido siguiente: [Creación de una instancia de Azure API Management](get-started-create-service-instance.md).
+ Además, completar el tutorial siguiente: [Importación y publicación de la primera API](import-and-publish.md).

## <a name="add-a-new-revision"></a>Agregar una nueva revisión

1. Seleccione la página **API**.
2. Seleccione **Demo Conference API** en la lista de API (u otra API a la que desee agregar revisiones).
3. Haga clic en la pestaña **Revisiones** en el menú junto a la parte superior de la página.
4. Seleccione **+ Agregar revisión**.

    > [!TIP]
    > También puede seleccionar **Agregar revisión** en el menú contextual (**...**) de la API.
    
    ![Menú Revisiones cerca de la parte superior de la pantalla](media/api-management-getstarted-revise-api/TopMenu.PNG)

5. Incluya una descripción de la nueva revisión que ayude a saber para qué va a servir.
6. Seleccione **Crear**
7. Ya tenemos creada la revisión.

    > [!NOTE]
    > La API original permanece en **Revisión 1**. Esta es la revisión que los usuarios siguen llamando hasta que decida convertir otra en actual.

## <a name="make-non-breaking-changes-to-your-revision"></a>Realizar cambios que no producen interrupciones en la revisión

1. Seleccione **Demo Conference API** en la lista de API.
2. Seleccione la pestaña **Diseño** situada junto a la parte superior de la pantalla.
3. Fíjese en que el **selector de revisiones** (que está inmediatamente encima de la pestaña de diseño) muestra que la revisión seleccionada es **Revisión 2**.

    > [!TIP]
    > Use el selector de revisión para alternar entre las revisiones con las que vaya a trabajar.

4. Seleccione **+ Agregar operación**.
5. Establezca que la nueva operación sea **POST** y especifique **test** como nombre, nombre para mostrar y dirección URL de la operación.
6. **Guarde** la nueva operación.
7. Ya hemos hecho un cambio en **Revisión 2**. Use el **selector de revisión** junto a la parte superior de la página para volver a **Revisión 1**.
8. Observe que la nueva operación no figura en **Revisión 1**. 

## <a name="make-your-revision-current-and-add-a-change-log-entry"></a>Convertir la revisión en actual y agregar una entrada en el registro de cambios

1. Seleccione la pestaña **Revisiones** en el menú junto a la parte superior de la página.

    ![El menú de revisión en la pantalla de revisión.](media/api-management-getstarted-revise-api/RevisionsMenu.PNG)
2. Abra el menú contextual (**...**) de **Revisión 2**.
3. Seleccione **Convertir en actual**.
4. Active la casilla **Post to Public Change log for this API** (Publicar en el registro de cambios público de esta API), si quiere publicar notas sobre este cambio. Especifique una descripción del cambio que puedan ver los desarrolladores, por ejemplo: **Testing revisions. Se agregó una nueva operación de "prueba".**
5. **Revisión 2** es ahora la revisión actual.

## <a name="browse-the-developer-portal-to-see-changes-and-change-log"></a>Examinar el portal para desarrolladores para ver los cambios y registro de cambios

1. En Azure Portal, seleccione **API**.
2. Seleccione **Portal para desarrolladores** en el menú superior.
3. Seleccione **API** y, después, **Demo Conference API**.
4. Observe que la nueva operación **prueba** ahora aparece disponible.
5. Seleccione **API Change History** (Historial de cambios de la API) debajo del nombre de la API.
6. Vea que la entrada en el registro de cambios aparece en esta lista.

    ![Portal para desarrolladores](media/api-management-getstarted-revise-api/developer_portal.PNG)

## <a name="next-steps"></a>Pasos siguientes

En este tutorial aprendió lo siguiente:

> [!div class="checklist"]
> * Agregar una nueva revisión
> * Realizar cambios que no producen interrupciones en la revisión
> * Convertir la revisión en actual y agregar una entrada en el registro de cambios
> * Examinar el portal para desarrolladores para ver los cambios y registro de cambios

Avance hasta el siguiente tutorial:

> [!div class="nextstepaction"]
> [Publicación de varias versiones de la API](api-management-get-started-publish-versions.md)
