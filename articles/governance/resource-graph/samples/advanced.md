---
title: Consultas avanzadas de Azure Resource Graph
description: Utilice Azure Resource Graph para ejecutar algunas consultas avanzadas.
services: resource-graph
author: DCtheGeek
ms.author: dacoulte
ms.date: 09/18/2018
ms.topic: quickstart
ms.service: resource-graph
manager: carmonm
ms.custom: mvc
ms.openlocfilehash: 934dff93b9a7f5d6755f55ad1073e01e586b1ca7
ms.sourcegitcommit: ccdea744097d1ad196b605ffae2d09141d9c0bd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49647840"
---
# <a name="advanced-resource-graph-queries"></a>Consultas avanzadas de Resource Graph

El primer paso para entender las consultas con Azure Resource Graph es el reconocimiento básico del [lenguaje de consultas](../concepts/query-language.md). Si aún no está familiarizado con [Azure Data Explorer](../../../data-explorer/data-explorer-overview.md), se recomienda repasar los conceptos básicos para entender cómo componer solicitudes para los recursos que está buscando.

Le guiaremos por las siguientes consultas avanzadas:

> [!div class="checklist"]
> - [Obtención del tamaño y la capacidad de VMSS](#vmss-capacity)
> - [Enumeración de todos los nombres de etiquetas](#list-all-tags)
> - [Máquinas virtuales que coinciden con regex](#vm-regex)

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free) antes de empezar.

## <a name="language-support"></a>Compatibilidad con idiomas

La CLI de Azure (mediante una extensión) y Azure PowerShell (mediante un módulo) admiten Azure Resource Graph. Antes de realizar cualquiera de las siguientes consultas, compruebe que el entorno está listo. Consulte la [CLI de Azure](../first-query-azurecli.md#add-the-resource-graph-extension) y [Azure PowerShell](../first-query-powershell.md#add-the-resource-graph-module) para conocer los pasos para instalar y validar el entorno de shell que prefiera.

## <a name="vmss-capacity"></a>Obtención del tamaño y la capacidad de VMSS

Esta consulta busca los recursos del conjunto de escalado de máquinas virtuales (VMSS) y obtiene varios detalles, incluido el tamaño de la máquina virtual y la capacidad del conjunto de escalado. Esta información usa la función `toint()` para convertir la capacidad en un número para que se pueda ordenar. Esto también cambia el nombre de los valores devueltos en propiedades con nombre personalizadas.

```Query
where type=~ 'microsoft.compute/virtualmachinescalesets'
| where name contains 'contoso'
| project subscriptionId, name, location, resourceGroup, Capacity = toint(sku.capacity), Tier = sku.name
| order by Capacity desc
```

```azurecli-interactive
az graph query -q "where type=~ 'microsoft.compute/virtualmachinescalesets' | where name contains 'contoso' | project subscriptionId, name, location, resourceGroup, Capacity = toint(sku.capacity), Tier = sku.name | order by Capacity desc"
```

```azurepowershell-interactive
Search-AzureRmGraph -Query "where type=~ 'microsoft.compute/virtualmachinescalesets' | where name contains 'contoso' | project subscriptionId, name, location, resourceGroup, Capacity = toint(sku.capacity), Tier = sku.name | order by Capacity desc"
```

## <a name="list-all-tags"></a>Enumeración de todos los nombres de etiquetas

Esta consulta comienza con la etiqueta y crea un objeto JSON que enumera todos los nombres de etiqueta únicos y sus tipos correspondientes.

```Query
project tags
| summarize buildschema(tags)
```

```azurecli-interactive
az graph query -q "project tags | summarize buildschema(tags)"
```

```azurepowershell-interactive
Search-AzureRmGraph -Query "project tags | summarize buildschema(tags)"
```

## <a name="vm-regex"></a>Máquinas virtuales que coinciden con regex

Esta consulta busca las máquinas virtuales que coincidan con una [expresión regular](/dotnet/standard/base-types/regular-expression-language-quick-reference) (conocida como _regex_).
**matches regex @** nos permite definir regex para coincidir, que es **^Contoso(.*)[0-9]+$**. Esa definición de regex se explica como:

- `^` - La coincidencia debe empezar al principio de la cadena.
- `Contoso` - La cadena principal con la que buscamos la coincidencia (distingue entre mayúsculas y minúsculas).
- `(.*)` - Una coincidencia de subexpresión:
  - `.` - Coincide con cualquier carácter individual (excepto saltos de línea).
  - `*` - Coincide con el elemento anterior cero o más veces.
- `[0-9]` - Coincidencia de grupo caracteres para los números del 0 al 9.
- `+` - Coincide con el elemento anterior una o más veces.
- `$` - La coincidencia del elemento anterior se debe producir al final de la cadena.

Después de la coincidencia del nombre, la consulta proyecta el nombre y ordena por nombre de forma ascendente.

```Query
where type =~ 'microsoft.compute/virtualmachines' and name matches regex @'^Contoso(.*)[0-9]+$'
| project name
| order by name asc
```

```azurecli-interactive
az graph query -q "where type =~ 'microsoft.compute/virtualmachines' and name matches regex @'^Contoso(.*)[0-9]+$' | project name | order by name asc"
```

```azurepowershell-interactive
Search-AzureRmGraph -Query "where type =~ 'microsoft.compute/virtualmachines' and name matches regex @'^Contoso(.*)[0-9]+$' | project name | order by name asc"
```

## <a name="next-steps"></a>Pasos siguientes

- Consulte ejemplos de [consultas de inicio](starter.md)
- Más información sobre el [lenguaje de consulta](../concepts/query-language.md)
- Más información sobre la [exploración de recursos](../concepts/explore-resources.md)