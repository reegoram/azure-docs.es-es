---
title: 'Guía de inicio rápido: Creación de una cuenta de Azure Media Services con la CLI de Azure | Microsoft Docs'
description: Siga los pasos de este inicio rápido para crear una cuenta de Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: quickstart
ms.custom: mvc
ms.date: 10/15/2018
ms.author: juliako
ms.openlocfilehash: de54571308b737b9160a39ee4ba5d4b2d9f15775
ms.sourcegitcommit: 3a7c1688d1f64ff7f1e68ec4bb799ba8a29a04a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2018
ms.locfileid: "49376540"
---
# <a name="quickstart-create-an-azure-media-services-account"></a>Inicio rápido: creación de una cuenta de Azure Media Services

Si es un desarrollador o un creador de contenido multimedia, tendrá que crear una cuenta de Media Services para la administración, el cifrado, la codificación, la administración y el streaming de contenido multimedia en Azure. Al crear una cuenta de Media Services, debe proporcionar el identificador de un recurso de cuenta de Azure Storage. La cuenta de almacenamiento especificada está asociada a su cuenta de Media Services. Este recurso de cuenta de almacenamiento debe ubicarse en la misma región geográfica que la cuenta de Media Services.  

En esta guía de inicio rápido se describen los pasos para crear una cuenta de Azure Media Services con la CLI de Azure.  

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a>Inicio de sesión en Azure

Inicie sesión en [Azure Portal](http://portal.azure.com) e inicie **CloudShell** para ejecutar comandos de la CLI, como se muestra en los siguientes pasos.

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

Si decide instalar y usar la CLI localmente, para este tema es preciso la CLI de Azure versión 2.0 o posterior. Ejecute `az --version` para encontrar la versión que tiene. Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure]( /cli/azure/install-azure-cli). 

## <a name="set-the-azure-subscription"></a>Establecimiento de la suscripción de Azure

En el siguiente comando, proporcione el identificador de suscripción de Azure que quiere usar para la cuenta de Media Services. Para ver una lista de las suscripciones a las que tiene acceso, vaya a [Suscripciones](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).

```azurecli-interactive
az account set --subscription <mySubscriptionId>
```

## <a name="create-an-azure-resource-group"></a>Crear un grupo de recursos de Azure

El comando siguiente crea un grupo de recursos en el que tendrá la cuenta de Storage y Media Services. Reemplace el marcador de posición *myresourcegroup* por el nombre que quiere usar para el grupo de recursos.

```azurecli-interactive
az group create -n <myresourcegroup> -l westus2
```

## <a name="create-an-azure-storage-account"></a>Creación de una cuenta de Azure Storage

Al crear una cuenta de Media Services, debe proporcionar el identificador de un recurso de cuenta de Azure Storage. La cuenta de almacenamiento especificada está asociada a su cuenta de Media Services. 

Debe tener una cuenta de almacenamiento **Principal** y puede tener cualquier número de cuentas de almacenamiento **Secundarias** asociadas a su cuenta de Media Services. Media Services admite cuentas de **Uso general v2** o **Uso general v1**. No se admiten las cuentas de Blob Storage como **Principales**. Para más información sobre las cuentas de almacenamiento, vea [Introducción a las cuentas de Azure Storage](../../storage/common/storage-account-overview.md). 

El siguiente comando crea la cuenta de Storage que se asociará a la cuenta de Media Services (principal). En el siguiente script, reemplace el marcador de posición *storageaccountforams*. El valor de "account_name" debe tener una longitud inferior a 24.

```azurecli-interactive
az storage account create -n <storageaccountforams> -g <myresourcegroup>
```

## <a name="create-an-azure-media-services-account"></a>Creación de una cuenta de Azure Media Services

A continuación, encontrará los comandos de CLI de Azure que crean una nueva cuenta de Media Services. Solo tiene que reemplazar los valores resaltados siguientes:

* *myamsaccountname*
* *myresourcegroup*
* *storageaccountforams*

```azurecli-interactive
az ams create -n <myamsaccountname> -g <myresourcegroup> --storage-account <storageaccountforams>
```

## <a name="clean-up-resources"></a>Limpieza de recursos

Si ya no necesita ningún recurso del grupo de recursos, incluida la cuenta de Media Services que ha creado en este inicio rápido, elimine el grupo de recursos.

En **CloudShell**, ejecute el siguiente comando:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Streaming de un archivo](stream-files-dotnet-quickstart.md)
