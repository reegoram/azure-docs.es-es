---
title: archivo de inclusión
description: archivo de inclusión
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 605533f25b36a92a660301d28aa63cb2ecdd44f4
ms.sourcegitcommit: 11321f26df5fb047dac5d15e0435fce6c4fde663
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2018
ms.locfileid: "37909957"
---
Al crear una puerta de enlace de red virtual, debe especificar la SKU de la puerta de enlace que desea usar. Seleccione las SKU que cumplan sus requisitos en función de los tipos de cargas de trabajo, rendimientos, características y Acuerdos de Nivel de Servicio.

###  <a name="benchmark"></a>SKU de puerta de enlace por túnel, conexión y rendimiento

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

###  <a name="feature"></a>SKU de puerta de enlace por conjunto de características

Las nueva SKU de puerta de enlace de VPN simplifican los conjuntos de características que se ofrecen en las puertas de enlace:

| **SKU**| **Características**|
| ---    | ---         |
|**Basic** (\*\*)   | **VPN basada en ruta**: 10 túneles con P2S, sin autenticación RADIUS, sin P2S, sin IKEv2 para P2S<br>**VPN basada en directivas**: (IKEv1): 1 túnel; sin P2S|
| **VpnGw1, VpnGw2 y VpnGw3** | **VPN basada en ruta**: hasta 30 túneles (\*), P2S, BGP, activo-activo, directiva de IPsec/IKE personalizada, coexistencia de VPN y ExpressRoute |
|        |             |

( * ) Se puede configurar "PolicyBasedTrafficSelectors" para conectar una puerta de enlace de VPN Gateway basada en ruta (VpnGw1, VpnGw2, VpnGw3) a varios dispositivos de firewall locales basados en directivas. Consulte [Connect VPN gateways to multiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) (Conexión de puertas de enlace VPN Gateway a varios dispositivos de VPN locales basados en directivas con PowerShell) para más información.

(\*\*) La SKU Basic se considera una SKU heredada. La SKU Basic tiene ciertas limitaciones de características. No se puede cambiar el tamaño de una puerta de enlace que utiliza una SKU Basic a una de las SKU de puerta de enlace nuevas, sino que debe cambiar a una SKU nueva, lo que implica eliminar y volver a crear la puerta de enlace VPN.

###  <a name="workloads"></a>SKU de puerta de enlace: producción frente a cargas de desarrollo y pruebas

Dadas las diferencias en los Acuerdos de Nivel de Servicio y los conjuntos de características, se recomiendan las siguientes SKU para la producción, en comparación el desarrollo y las pruebas:

| **Carga de trabajo**                       | **SKU**               |
| ---                                | ---                    |
| **Cargas de trabajo de producción, críticas** | VpnGw1, VpnGw2, VpnGw3 |
| **Desarrollo y pruebas o prueba de concepto**   | Basic (\*\*)                 |
|                                    |                        |

(\*\*) La SKU Basic se considera una SKU heredada y tiene limitaciones de características. Compruebe que se admite la característica que necesita antes de usar la SKU Basic.

Si continúa utilizando las SKU antiguas (heredadas), las recomendaciones de SKU de producción son Standard y HighPerformance. Para obtener información e instrucciones para las SKU antiguas, consulte [Trabajo con SKU de puerta de enlace de red virtual (SKU antiguas)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).
