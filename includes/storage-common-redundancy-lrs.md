---
title: archivo de inclusión
description: archivo de inclusión
services: storage
author: tamram
ms.service: storage
ms.topic: include
ms.date: 03/26/2018
ms.author: tamram
ms.custom: include file
ms.openlocfilehash: 58d81bd4c1ce4b3af91a335039f62df08b340576
ms.sourcegitcommit: d4c076beea3a8d9e09c9d2f4a63428dc72dd9806
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2018
ms.locfileid: "39399998"
---
El almacenamiento con redundancia local (LRS) está diseñado para proporcionar al menos el 99,999999999 % (once nueves) de durabilidad de objetos a lo largo de un año determinado. Para ello, replica los datos dentro de una unidad de escalado de almacenamiento. Una unidad de escalado de almacenamiento se hospeda en un centro de datos de la región en la que se creó su cuenta de almacenamiento. Una solicitud de escritura a una cuenta de almacenamiento de LRS se devuelve correctamente solo después de que los datos se escriben en todas las réplicas. Cada una de estas réplicas reside en dominios de error y dominios de actualización independientes dentro de una unidad de escalado de almacenamiento.

Una unidad de escalado de almacenamiento es una colección de estanterías de nodos de almacenamiento. Un dominio de error (FD) es un grupo de nodos que representan una unidad física de error y se pueden considerar como nodos pertenecientes a la misma estantería. Un dominio de actualización (UD) es un grupo de nodos que se actualizan en conjunto durante el proceso de actualización de un servicio (implementación). Las réplicas se distribuyen entre dominios de actualización y dominios de error dentro de una unidad de escalado de almacenamiento. Esta arquitectura garantiza que los datos están disponibles si un error de hardware afecta a único bastidor o cuando los nodos se actualizan durante una implementación.

LRS es la opción de replicación de costo más bajo y ofrece la menor durabilidad en comparación con otras opciones. Si se produce un desastre en el nivel de centro de datos (por ejemplo, un incendio o una inundación), es posible que todas las réplicas se pierdan o que no se puedan recuperar. Para mitigar este riesgo, Microsoft recomienda el uso del almacenamiento con redundancia de zona (ZRS) o del almacenamiento con redundancia geográfica (GRS).

* Si la aplicación almacena los datos que se pueden reconstruir fácilmente si se produce una pérdida de datos, puede optar por LRS.
* Algunas aplicaciones están restringidas a la replicación de datos solo dentro de un país debido a requisitos de gobernanza de datos. En algunos casos, las regiones emparejadas en las que los datos se replican para las cuentas de GRS pueden estar en otro país. Para más información sobre las regiones emparejadas, consulte [Regiones de Azure](https://azure.microsoft.com/regions/).
