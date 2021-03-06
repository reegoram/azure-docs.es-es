---
title: Localizadores de streaming en Azure Media Services | Microsoft Docs
description: En este artículo se explica qué son los localizadores de streaming y cómo los usa Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 10/22/2018
ms.author: juliako
ms.openlocfilehash: 56e9a0b4eec347d2367c38ab00c6c9d9dca60752
ms.sourcegitcommit: c2c279cb2cbc0bc268b38fbd900f1bac2fd0e88f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2018
ms.locfileid: "49986906"
---
# <a name="streaming-locators"></a>Localizadores de streaming

Para proporcionar a los clientes una dirección URL que pueden usar para reproducir archivos de audio o vídeo codificados, debe crear un elemento [StreamingLocator](https://docs.microsoft.com/rest/api/media/streaminglocators) y compilar las direcciones URL de streaming. Para obtener más información, consulte [Stream a file](stream-files-dotnet-quickstart.md) (Hacer streaming de un archivo).

## <a name="streaminglocator-definition"></a>Definición de StreamingLocator

En la tabla siguiente se muestran las propiedades de StreamingLocator y se proporcionan sus definiciones.

|NOMBRE|Escriba|DESCRIPCIÓN|
|---|---|---|
|id |string|Identificador de recurso completo del recurso.|
|Nombre   |string|Nombre del recurso.|
|properties.alternativeMediaId  |string|Id. de medios alternativo de este localizador de streaming.|
|properties.assetName   |string|Nombre de recurso|
|properties.contentKeys |StreamingLocatorContentKey[]|Claves de contenido que usa este localizador de streaming.|
|properties.created |string|Hora de creación del localizador de streaming.|
|properties.defaultContentKeyPolicyName |string|Nombre del elemento ContentKeyPolicy predeterminado que usa este localizador de streaming.|
|properties.endTime |string|Hora de finalización del localizador de streaming.|
|properties.startTime   |string|Hora de inicio del localizador de streaming.|
|properties.streamingLocatorId  |string|Elemento StreamingLocatorId del localizador de streaming.|
|properties.streamingPolicyName |string|Nombre de la directiva de streaming que usa este localizador de streaming. Especifique el nombre de la directiva de streaming que creó o use una de las directivas de streaming predefinidas. Las directivas de streaming predefinidas que están disponibles son: "Predefined_DownloadOnly", "Predefined_ClearStreamingOnly", "Predefined_DownloadAndClearStreaming", "Predefined_ClearKey", "Predefined_MultiDrmCencStreaming" y "Predefined_ MultiDrmStreaming".|
|Tipo   |string|Tipo de recurso.|

Para conocer la definición completa, consulte [Localizadores de streaming](https://docs.microsoft.com/rest/api/media/streaminglocators).

## <a name="filtering-ordering-paging"></a>Filtrado, ordenación, paginación

Media Services admite las siguientes opciones de consulta de OData para los localizadores de streaming: 

* $filter 
* $orderby 
* $top 
* $skiptoken 

Descripción del operador:

* Eq = es igual que
* Ne = no es igual que
* Ge = es mayor o igual que
* Le = es menor o igual que
* Gt = es mayor que
* Lt = es menor que

### <a name="filteringordering"></a>Filtrado y ordenación

En la tabla siguiente se muestra cómo pueden aplicarse estas opciones a las propiedades de StreamingLocator: 

|NOMBRE|Filtrar|Orden|
|---|---|---|
|id |||
|Nombre|Eq, ne, ge, le, gt, lt|Ascendente y descendente|
|properties.alternativeMediaId  |||
|properties.assetName   |||
|properties.contentKeys |||
|properties.created |Eq, ne, ge, le, gt, lt|Ascendente y descendente|
|properties.defaultContentKeyPolicyName |||
|properties.endTime |Eq, ne, ge, le, gt, lt|Ascendente y descendente|
|properties.startTime   |||
|properties.streamingLocatorId  |||
|properties.streamingPolicyName |||
|Tipo   |||

### <a name="pagination"></a>Paginación

La paginación se admite para cada uno de los cuatro criterios de ordenación habilitados. En este momento, el tamaño de página es 10.

> [!TIP]
> Siempre debe usar el vínculo siguiente para enumerar la colección y así no tener que depender de un tamaño de página determinado.

Si una respuesta de consulta contiene muchos elementos, el servicio devuelve una propiedad "\@odata.nextLink" para obtener la siguiente página de resultados. Esto se puede utilizar para pasar de página en el conjunto de resultados completo. No puede configurar el tamaño de página. 

Si se crean o eliminan los elementos StreamingLocators durante la paginación a través de la colección, los cambios se ven reflejados en los resultados que se devuelven (si esos cambios se encuentran en la parte de la colección que no se ha descargado). 

En el ejemplo de C# siguiente se muestra cómo enumerar todos los elementos StreamingLocators de la cuenta.

```csharp
var firstPage = await MediaServicesArmClient.StreamingLocators.ListAsync(CustomerResourceGroup, CustomerAccountName);

var currentPage = firstPage;
while (currentPage.NextPageLink != null)
{
    currentPage = await MediaServicesArmClient.StreamingLocators.ListNextAsync(currentPage.NextPageLink);
}
```

Para obtener ejemplos de REST, consulte [Streaming Locators - List](https://docs.microsoft.com/rest/api/media/streaminglocators/list) (Lista de localizadores de streaming).

## <a name="next-steps"></a>Pasos siguientes

[Streaming de un archivo](stream-files-dotnet-quickstart.md)
