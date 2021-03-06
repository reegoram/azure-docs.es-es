---
title: Configuración de puntos de conexión en una máquina virtual de Windows clásica | Microsoft Docs
description: Aprenda a configurar los puntos de conexión de una máquina virtual Windows clásica en Azure Portal para permitir la comunicación con una máquina virtual Windows en Azure.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: cca9adb40557cf7bf9e1d4129fc6bd61cbf0df4f
ms.sourcegitcommit: 0a84b090d4c2fb57af3876c26a1f97aac12015c5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38618246"
---
# <a name="how-to-set-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a>Configuración de puntos de conexión en una máquina virtual de Windows clásica en Azure
Todas las máquinas virtuales de Windows que se crean en Azure con el modelo de implementación clásico se pueden comunicar automáticamente a través de un canal de red privado con otras máquinas virtuales del mismo servicio en la nube o la misma red virtual. Sin embargo, los equipos en Internet o en otras redes virtuales necesitan extremos para dirigir el tráfico de red entrante a una máquina virtual. Este artículo también está disponible para [máquinas virtuales Linux](../../linux/classic/setup-endpoints.md).

> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). En este artículo se trata el modelo de implementación clásico. Microsoft recomienda que las implementaciones más recientes usen el modelo de Resource Manager.
> [!INCLUDE [virtual-machines-common-classic-createportal](../../../../includes/virtual-machines-classic-portal.md)]

En el modelo de implementación de **Resource Manager**, los puntos de conexión se configuran mediante **grupos de seguridad de red (NSG)**. Para más información, consulte [Permitir el acceso a la máquina virtual mediante Azure Portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Al crear una máquina virtual Windows en Azure Portal, los puntos de conexión comunes, como los de Escritorio remoto y Windows PowerShell Remoting se suelen crear automáticamente. Puede configurar extremos adicionales al crear la máquina virtual o posteriormente, según sea necesario.

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a>Pasos siguientes
* Para usar un cmdlet de Azure PowerShell para configurar un punto de conexión de máquina virtual, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).
* Para usar un cmdlet de Azure PowerShell para gestionar una ACL en un punto de conexión, consulte [Administración de listas de control de acceso (ACL) para puntos de conexión mediante PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).
* Si ha creado una máquina virtual en el modelo de implementación de Resource Manager, también puede usar Azure PowerShell para [crear grupos de seguridad de red](../../../virtual-network/tutorial-filter-network-traffic.md) con el fin de controlar el tráfico en la máquina virtual.
