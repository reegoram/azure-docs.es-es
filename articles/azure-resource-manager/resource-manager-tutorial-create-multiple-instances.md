---
title: Creación de varias instancias con Azure Resource Manager | Microsoft Docs
description: Obtenga información sobre cómo crear una plantilla de Azure Resource Manager para crear varias instancias de recursos de Azure.
services: azure-resource-manager
documentationcenter: ''
author: mumian
manager: dougeby
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/10/2018
ms.topic: tutorial
ms.author: jgao
ms.openlocfilehash: 63a18a6ae0ee4c6e0a01bd7ac4a26a4fb89746c2
ms.sourcegitcommit: 3150596c9d4a53d3650cc9254c107871ae0aab88
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47419498"
---
# <a name="tutorial-create-multiple-resource-instances-using-resource-manager-templates"></a>Tutorial: Creación de varias instancias de recursos con plantillas de Resource Manager

Obtenga información sobre cómo iterar la plantilla de Azure Resource Manager para crear varias instancias de un recurso de Azure. En el último tutorial, modificó una plantilla existente para crear una cuenta de Azure Storage cifrada. En este tutorial, modificará la misma plantilla para crear tres instancias de cuenta de almacenamiento.

> [!div class="checklist"]
> * Apertura de una plantilla de inicio rápido
> * Edición de la plantilla
> * Implementación de la plantilla

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.

## <a name="prerequisites"></a>Requisitos previos

Para completar este artículo, necesitará lo siguiente:

* [Visual Studio Code](https://code.visualstudio.com/)
* Extensión de herramientas de Resource Manager Para realizar la instalación, consulte [Instalación de la extensión de herramientas de Resource Manager](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#prerequisites).

## <a name="open-a-quickstart-template"></a>Abra una plantilla de inicio rápido.

La plantilla usada en esta guía de inicio rápido se denomina [Crear una cuenta de almacenamiento estándar](https://azure.microsoft.com/resources/templates/101-storage-account-create/). La plantilla define un recurso de la cuenta de almacenamiento de Azure.

1. En Visual Studio Code, seleccione **Archivo**>**Abrir archivo**.
2. En **Nombre de archivo**, pegue el código URL siguiente:

    ```url
    https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
    ```
3. Seleccione **Abrir** para abrir el archivo.
4. Seleccione **Archivo**>**Guardar como** para guardar el archivo como **azuredeploy.json** en el equipo local.

## <a name="edit-the-template"></a>Edición de la plantilla

El objetivo de este tutorial es usar la iteración de recursos para crear tres cuentas de almacenamiento.  La misma plantilla solo crea una cuenta de almacenamiento. 

En Visual Studio Code, haga estos cuatro cambios:

![Azure Resource Manager crea varias instancias](./media/resource-manager-tutorial-create-multiple-instances/resource-manager-template-create-multiple-instances.png)

1. Agregue un elemento `copy` a la definición de recurso de la cuenta de almacenamiento. En el elemento de copia, especifique el número de iteraciones y un nombre para este bucle. El valor de recuento debe ser un número entero positivo y no puede ser superior a 800.
2. La función `copyIndex()` devuelve la iteración actual en el bucle. `copyIndex()` es de base cero. Para desplazar el valor de índice, puede pasar un valor de la función copyIndex(). Por ejemplo, *copyIndex(1)*.
3. Elimine el elemento **variables**, porque no se volverá a usar.
4. Elimine el elemento **outputs**.

La plantilla completada tiene este aspecto:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "[resourceGroup().location]",
      "metadata": {
        "description": "Location for all resources."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
      "apiVersion": "2018-02-01",
      "location": "[parameters('location')]",
      "sku": {
        "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage",
      "properties": {},
      "copy": {
        "name": "storagecopy",
        "count": 3
      }
    }
  ]
}
```

Para más información sobre cómo crear varias instancias, consulte [Implementación de varias instancias de un recurso o una propiedad en plantillas de Azure Resource Manager](./resource-group-create-multiple.md).

## <a name="deploy-the-template"></a>Implementación de la plantilla

Consulte la sección [Implementación de la plantilla](./resource-manager-quickstart-create-templates-use-visual-studio-code.md#deploy-the-template) de la guía de inicio rápido de Visual Studio Code para el procedimiento de implementación.

Para mostrar las tres cuentas de almacenamiento, omita el parámetro --name:

# <a name="clitabcli"></a>[CLI](#tab/CLI)
```cli
az storage account list --resource-group <ResourceGroupName>
```

# <a name="powershelltabpowershell"></a>[PowerShell](#tab/PowerShell)

```powershell
Get-AzureRmStorageAccount -ResourceGroupName <ResourceGroupName>
```

---

Compare los nombres de las cuentas de almacenamiento con la definición del nombre de la plantilla.

## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando los recursos de Azure ya no sean necesarios, limpie los recursos que implementó eliminando el grupo de recursos.

1. En Azure Portal, seleccione **Grupos de recursos** en el menú de la izquierda.
2. Escriba el nombre del grupo de recursos en el campo **Filtrar por nombre**.
3. Seleccione el nombre del grupo de recursos.  Verá un total de seis recursos en el grupo de recursos.
4. Seleccione **Eliminar grupo de recursos** del menú superior.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, aprendió a crear varias instancias de cuenta de almacenamiento. Hasta ahora, ha creado una cuenta de almacenamiento o varias instancias de cuenta de almacenamiento. En el tutorial siguiente, desarrollará una plantilla con varios recursos y varios tipos de recursos. Algunos de los recursos tienen recursos dependientes.

> [!div class="nextstepaction"]
> [Creación de plantillas de Azure Resource Manager con recursos dependientes](./resource-manager-tutorial-create-templates-with-dependent-resources.md)
