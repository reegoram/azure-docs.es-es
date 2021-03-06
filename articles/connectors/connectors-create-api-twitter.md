---
title: Conexión a Twitter desde Azure Logic Apps | Microsoft Docs
description: Automatice tareas y flujos de trabajo que supervisan y administran tweets, además de obtener datos sobre los seguidores, los usuarios a los que sigue, otros usuarios, escalas de tiempo y mucho más desde su cuenta de Twitter con Azure Logic Apps.
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.topic: article
tags: connectors
ms.date: 08/25/2018
ms.openlocfilehash: eea70d979a69a4855b6eeb892d1705ecadaa8434
ms.sourcegitcommit: ebb460ed4f1331feb56052ea84509c2d5e9bd65c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2018
ms.locfileid: "42918652"
---
# <a name="monitor-and-manage-twitter-by-using-azure-logic-apps"></a>Supervisión y administración de Twitter con Azure Logic Apps

Con Azure Logic Apps y el conector de Twitter, puede crear tareas automatizadas y flujos de trabajo que supervisan y administran los datos que le interesan en Twitter como tweets, seguidores, usuarios y usuarios a los que sigue, escalas de tiempo y mucho más, junto con otras acciones, por ejemplo:

* Supervisar, publicar y buscar tweets
* Obtener datos como seguidores, usuarios seguidos, escalas de tiempo y mucho más

Puede usar desencadenadores que obtengan respuestas de su cuenta de Twitter y permitan que la salida esté disponible para otras acciones. Puede usar acciones que realicen tareas con su cuenta de Twitter. También puede hacer que otras acciones usen la salida de las acciones de Twitter. Por ejemplo, cuando aparezca un nuevo tweet con un hashtag específico, puede enviar mensajes con el conector de Slack. Si no está familiarizado con las aplicaciones lógicas, consulte [¿Qué es Azure Logic Apps?](../logic-apps/logic-apps-overview.md)

## <a name="prerequisites"></a>Requisitos previos

* Una suscripción de Azure. Si no tiene una suscripción de Azure, <a href="https://azure.microsoft.com/free/" target="_blank">regístrese para obtener una cuenta gratuita de Azure</a>. 

* Las credenciales de usuario y la cuenta de Twitter

   Las credenciales autorizan a la aplicación lógica a crear una conexión con la cuenta de Twitter y acceder a ella.

* Conocimientos básicos acerca de [cómo crear aplicaciones lógicas](../logic-apps/quickstart-create-first-logic-app-workflow.md)

* La aplicación lógica desde donde quiere acceder a la cuenta de Twitter. Para comenzar con un desencadenador de Twitter, [cree una aplicación lógica en blanco](../logic-apps/quickstart-create-first-logic-app-workflow.md). Para usar una acción de Twitter, inicie la aplicación lógica con otro desencadenador, por ejemplo, **Recurrence**.

## <a name="connect-to-twitter"></a>Conexión a Twitter

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. Si aún no lo ha hecho, inicie sesión en [Azure Portal](https://portal.azure.com) y abra la aplicación lógica en el Diseñador de aplicaciones lógicas.

1. Elija una ruta de acceso: 

   * Para las aplicaciones lógicas en blanco, en el cuadro de búsqueda, escriba "twitter" como filtro. 
   En la lista de desencadenadores, seleccione el que desee. 

     O bien

   * Para las aplicaciones lógicas existentes: 
   
     * En el último paso para agregar una acción, elija **Nuevo paso**. 

       O bien

     * Entre los pasos en los que desee agregar una acción, mueva el puntero sobre la flecha. 
     Elija el signo más (**+**) que aparece y seleccione **Agregar una acción**.
     
       En el cuadro de búsqueda, escriba "twitter" como filtro. 
       En la lista de acciones, seleccione la acción que desee.

1. Si se le solicita que inicie sesión en Twitter, inicie sesión ahora para que pueda autorizar el acceso a la aplicación lógica.

1. Proporcione los detalles necesarios para el desencadenador o la acción seleccionados y continúe con la compilación del flujo de trabajo de la aplicación lógica.

## <a name="examples"></a>Ejemplos

### <a name="twitter-trigger-when-a-new-tweet-is-posted"></a>Desencadenador de Twitter: cuando se publica un nuevo tweet

Este desencadenador inicia un flujo de trabajo de la aplicación lógica cuando detecta un nuevo tweet, por ejemplo, con el hashtag #Seattle. Por ejemplo, cuando se detectan estos tweets, puede agregar un archivo con el contenido de los tweets al almacenamiento, por ejemplo, una cuenta de Dropbox mediante el conector de Dropbox. 

Opcionalmente, puede incluir una condición de que los tweets válidos deben provenir de los usuarios con al menos un número especificado de seguidores.

**Ejemplo empresarial**: puede usar este desencadenador para supervisar los tweets sobre su empresa y cargar el contenido de los tweets en una base de datos SQL.

### <a name="twitter-action-post-a-tweet"></a>Acción de Twitter: publicación de un tweet

Esta acción publica un tweet, pero puede configurarla para que el tweet incluya el contenido de los tweets encontrados por el desencadenador descrito anteriormente. 

## <a name="connector-reference"></a>Referencia de conectores

Para conocer los detalles técnicos sobre desencadenadores, acciones y límites, que se incluyen en la descripción de OpenAPI (antes Swagger) del conector, consulte la [página de referencia](/connectors/twitterconnector/) del conector.

## <a name="get-support"></a>Obtención de soporte técnico

* Si tiene alguna duda, visite el [foro de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).
* Para enviar ideas sobre características o votar sobre ellas, visite el [sitio de comentarios de los usuarios de Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Pasos siguientes

* Obtenga más información sobre otros [conectores de Logic Apps](../connectors/apis-list.md)
