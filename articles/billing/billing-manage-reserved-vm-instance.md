---
title: Administrar Azure Reservations | Microsoft Docs
description: Aprenda a cambiar el ámbito de la suscripción y a administrar el acceso a Azure Reservations.
services: billing
documentationcenter: ''
author: yashesvi
manager: yashesvi
editor: ''
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2018
ms.author: cwatson
ms.openlocfilehash: 0b19bb0d77bb600258596ce369713464641a7d2f
ms.sourcegitcommit: 42405ab963df3101ee2a9b26e54240ffa689f140
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47423245"
---
# <a name="manage-reservations-for-azure-resources"></a>Administración de reservas para los recursos de Azure

Después de comprar una reserva de Azure, es posible que deba aplicar la reserva a otra suscripción, cambiar quién puede administrar la reserva, o cambiar el ámbito de la reserva. También puede dividir una reserva en dos para aplicar algunas de las instancias que compró a otra suscripción.

Si ha adquirido Azure Reserved Virtual Machine Instances, puede cambiar la configuración de optimización de la reserva. Puede aplicar el descuento de reserva a las máquinas virtuales de la misma serie o puede reservar la capacidad del centro de datos para un tamaño específico de máquina virtual.

## <a name="change-the-scope-for-a-reservation"></a>Cambio del ámbito de una reserva

 El descuento de la reserva se aplica a las máquinas virtuales, SQL Database, Azure Cosmos DB u otros recursos que se correspondan con la reserva y que se ejecuten dentro del ámbito de esta. El ámbito de una reserva puede ser una suscripción única o todas las suscripciones del contexto de facturación. Si establece que el ámbito es una suscripción única, la reserva se corresponderá con los recursos que se ejecuten en la suscripción seleccionada. Si establece que el ámbito es compartido, Azure asociará la reserva con los recursos que se ejecuten en todas las suscripciones dentro del contexto de facturación. El contexto de facturación depende de la suscripción que se usó para comprar la reserva.

Para cambiar el ámbito de una reserva:

1. Inicie sesión en el [Azure Portal](https://portal.azure.com).
2. Seleccione **Todos los servicios** > **Reservations**.
3. Seleccione la reserva.
4. Seleccione **Configuración** > **Configuración**.
5. Cambie el ámbito. 

Si cambia el ámbito para que pase de ser compartido a único, solo podrá seleccionar suscripciones de las que sea el propietario. Únicamente se pueden seleccionar las suscripciones que pertenezcan al mismo contexto de facturación que la reserva.

El ámbito solo se aplica a la oferta de pago por uso MS-AZR-0003P, la oferta Enterprise MS-AZR-0017P o a los tipos de suscripción de CSP. Las suscripciones de desarrollo y pruebas de contratos Enterprise no son aptas para obtener el descuento de reserva.

## <a name="add-or-change-users-who-can-manage-a-reservation"></a>Agregar o cambiar los usuarios que pueden administrar una reserva

Para delegar la administración de una reserva, agregue usuarios a roles en dicha reserva. De forma predeterminada, la persona que compró la reserva y el administrador de cuenta tienen el rol de propietario en la reserva.

Puede administrar el acceso a las reservas de forma independiente de las suscripciones que obtienen el descuento de reserva. El hecho de que a un usuario se le concedan permisos para administrar una reserva no implica que también se le otorguen derechos para administrar la suscripción. Y si a un usuario se le conceden permisos para administrar una suscripción dentro del ámbito de la reserva, no significa que se le otorguen derechos para administrar la reserva.

Para delegar la administración de acceso en una reserva:

1. Inicie sesión en el [Azure Portal](https://portal.azure.com).
2. Seleccione **Todos los servicios** > **Reservations** para enumerar las reservas a las que tiene acceso.
3. Seleccione la reserva cuyo acceso quiere delegar a otros usuarios.
4. Seleccione **Access Control (IAM)**.
5. Seleccione **Agregar** > **Rol** > **Propietario**. U otro rol si quiere conceder acceso limitado.
6. Escriba la dirección de correo electrónico del usuario al que desea agregar como propietario.
7. Seleccione el usuario y, después, **Guardar**.

## <a name="split-a-single-reservation-into-two-reservations"></a>División de una reserva única en dos

 Si se compran varias instancias de recursos en una reserva, se pueden asignar algunas de las instancias de la reserva a distintas suscripciones. De forma predeterminada, todas las instancias tienen un ámbito, que puede ser de suscripción única o compartida. Pongamos por ejemplo que se han comprado diez instancias de reserva y como ámbito se ha especificado la suscripción A. En caso de que le interese, se puede establecer el ámbito de siete reservas en la suscripción A y el de las tres restantes en la suscripción B. Dividir una reserva le permite distribuir las instancias para lograr una administración más precisa del ámbito. Si quiere simplificar la asignación a las suscripciones, elija el ámbito compartido. Sin embargo, para la administración de costos o fines presupuestarios, puede asignar las cantidades a suscripciones concretas.

 Una reserva se puede dividir en dos mediante PowerShell, CLI o la API.

### <a name="split-a-reservation-by-using-powershell"></a>División de una reserva con PowerShell

1. Ejecute el comando siguiente para obtener el identificador de pedido de reserva:

    ```powershell
    # Get the reservation orders you have access to
    Get-AzureRmReservationOrder
    ```

2. Obtenga los detalles de una reserva:

    ```powershell
    Get-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId b8be062a-fb0a-46c1-808a-5a844714965a
    ```

3. Divida la reserva en dos y distribuya las instancias:

    ```powershell
    # Split the reservation. The sum of the reservations, the quantity, must equal the total number of instances in the reservation that you're splitting.
    Split-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId b8be062a-fb0a-46c1-808a-5a844714965a -Quantity 3,2
    ```
4. Si quiere actualizar el ámbito, ejecute el siguiente comando:

    ```powershell
    Update-AzureRmReservation -ReservationOrderId a08160d4-ce6b-4295-bf52-b90a5d4c96a0 -ReservationId 5257501b-d3e8-449d-a1ab-4879b1863aca -AppliedScopeType Single -AppliedScope /subscriptions/15bb3be0-76d5-491c-8078-61fe3468d414
    ```

## <a name="cancellations-and-exchanges"></a>Cancelaciones e intercambios

Según el tipo de reserva, es posible que pueda cancelar o intercambiar una reserva. Para más información, vea las secciones sobre cancelación y e intercambios en estos temas:

- [Pago por adelantado de máquinas virtuales con Azure Reserved VM Instances](..//virtual-machines/windows/prepay-reserved-vm-instances.md#cancellations-and-exchanges)
- [Pago por adelantado para planes de software SUSE con Azure Reservations](../virtual-machines/linux/prepay-suse-software-charges.md#cancellation-and-exchanges-not-allowed)
- [Pago por adelantado por recursos de proceso de SQL Database con capacidad reservada de Azure SQL Database](../sql-database/sql-database-reserved-capacity.md#cancellations-and-exchanges)

## <a name="change-optimize-setting-for-reserved-vm-instances"></a>Cambiar la configuración de optimización para instancias reservadas de máquina virtual

 Al comprar una instancia reservada de máquina virtual, puede elegir entre la flexibilidad de tamaño de instancia o la prioridad de capacidad. En la opción de flexibilidad del tamaño de instancia se aplica el descuento por la reserva a otras máquinas virtuales del mismo [grupo](https://aka.ms/RIVMGroups). La prioridad de capacidad da preferencia a la capacidad del centro de datos para las implementaciones. Esta opción le ofrece una mayor confianza en su capacidad para iniciar instancias de máquinas virtuales cuando las necesite.

De forma predeterminada, cuando se comparte el ámbito de la reserva, la flexibilidad de tamaño de instancia está activada. La capacidad del centro de datos no tiene prioridad en las implementaciones de máquina virtual.

En las reservas donde el ámbito es único, puede optimizar la reserva para la prioridad de capacidad en lugar de la flexibilidad del tamaño de instancia de máquina virtual.

Para actualizar la configuración de optimización de la reserva:

1. Inicie sesión en el [Azure Portal](https://portal.azure.com).
2. Seleccione **Todos los servicios** > **Reservations**.
3. Seleccione la reserva.
4. Seleccione **Configuración** > **Configuración**.
5. Cambie la configuración de la **optimización**.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de Azure Reservations, consulte los siguientes artículos:

- [¿Qué es Azure Reservations?](billing-save-compute-costs-reservations.md)
- [Pago por adelantado de máquinas virtuales con Azure Reserved VM Instances](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [Pago por adelantado por recursos de proceso de SQL Database con capacidad reservada de Azure SQL Database](../sql-database/sql-database-reserved-capacity.md)
- [Pago por adelantado para recursos de Azure Cosmos DB con capacidad reservada de Azure Cosmos DB](../cosmos-db/cosmos-db-reserved-capacity.md)
- [Pago por adelantado para planes de software SUSE con Azure Reservations](../virtual-machines/linux/prepay-suse-software-charges.md)
- [Información sobre cómo se aplica el descuento por la reserva de máquinas virtuales](billing-understand-vm-reservation-charges.md)
- [Descubra cómo se aplica el descuento del plan de software SUSE Linux Enterprise](../billing/billing-understand-suse-reservation-charges.md)
- [Descubra cómo se aplican otros descuentos por reservas](billing-understand-reservation-charges.md)
- [Información sobre el uso de reservas para suscripciones de pago por uso](billing-understand-reserved-instance-usage.md)
- [Información sobre el uso de reservas para la inscripción Enterprise](billing-understand-reserved-instance-usage-ea.md)
- [Costos de software de Windows no incluidos con Reservations](billing-reserved-instance-windows-software-costs.md)

## <a name="need-help-contact-support"></a>¿Necesita ayuda? Ponerse en contacto con soporte técnico

Si tiene más preguntas, [póngase en contacto con el soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver el problema rápidamente.
