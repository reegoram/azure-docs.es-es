---
title: Actualización y administración de VM con Azure Stack | Microsoft Docs
description: Obtenga información sobre cómo usar las soluciones Update Management, Change Tracking e Inventario en Azure Automation para administrar máquinas VM Windows que se implementan en Azure Stack.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/15/2018
ms.author: jeffgilb
ms.reviewer: rtiberiu
ms.openlocfilehash: 1ef20dc35b069c5f12c2f31d0979949be27271e0
ms.sourcegitcommit: 74941e0d60dbfd5ab44395e1867b2171c4944dbe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/15/2018
ms.locfileid: "49323649"
---
# <a name="azure-stack-vm-update-and-management"></a>Administración y actualización de VM en Azure Stack
Puede usar las siguientes características de solución de Azure Automation para administrar VM Windows que se implementan mediante Azure Stack:

- **[Update Management](https://docs.microsoft.com/azure/automation/automation-update-management)**. Con la solución Update Management, puede evaluar rápidamente el estado de las actualizaciones disponibles en todos los equipos agente y administrar el proceso de instalación de las actualizaciones necesarias para estas VM Windows.

- **[Change Tracking](https://docs.microsoft.com/azure/automation/automation-change-tracking)**. Los cambios en el Registro y los archivos de Windows, en los servicios de Windows y en el software instalado en los servidores supervisados se envían al servicio de Log Analytics en la nube para su procesamiento. Se aplica la lógica a los datos recibidos y el servicio de nube registra los datos. Con la información en el panel de seguimiento de cambios, puede ver fácilmente los cambios realizados en la infraestructura de servidores.

- **[Inventario](https://docs.microsoft.com/azure/automation/automation-vm-inventory)**. El seguimiento de Inventario para una máquina virtual Windows en Azure Stack proporciona una interfaz de usuario basada en explorador para instalar y configurar la recopilación de inventario. 

> [!IMPORTANT]
> Estas soluciones son las mismas que las que se usan para administrar VM de Azure. Tanto las VM Windows de Azure como de Azure Stack se administran de la misma manera, desde la misma interfaz, con las mismas herramientas. Las VM de Azure Stack también tienen el mismo precio que las VM de Azure cuando se usan las soluciones Update Management, Change Tracking e Inventario con Azure Stack.

## <a name="prerequisites"></a>Requisitos previos
Deben cumplirse varios requisitos previos antes de usar estas características para actualizar y administrar VM Windows de Azure Stack. Entre otros, se incluyen pasos que deben darse en Azure Portal, así como en el portal de administración de Azure Stack.

### <a name="in-the-azure-portal"></a>En el Portal de Azure
Para usar las características de Azure Automation Inventario, Change Tracking y Update Management para VM Windows de Azure Stack, primero deberá habilitar estas soluciones en Azure.

> [!TIP]
> Si ya tiene estas características habilitadas para VM de Azure, puede usar sus credenciales preexistentes del área de trabajo de Log Analytics. Si ya tiene un id. de área de trabajo de Log Analytics y la clave principal que quiere usar, vaya directamente a la [sección siguiente](.\vm-update-management.md#in-the-azure-stack-administration-portal). De lo contrario, continúe en esta sección para crear una nueva cuenta de Automation y el área de trabajo de Log Analytics.

El primer paso para habilitar estas soluciones es [crear un área de trabajo de Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace) en su suscripción de Azure. Un área de trabajo de Log Analytics es un entorno de Log Analytics único, con su propio repositorio de datos, sus propios orígenes de datos y sus propias soluciones. Después de haber creado un área de trabajo, anote el id. del área de trabajo y la clave. Para ver esta información, vaya a la hoja del área de trabajo, haga clic en **Configuración avanzada**y revise los valores **Id. del área de trabajo** y **Clave principal**. 

Luego, debe [crear una cuenta de Automation](https://docs.microsoft.com/azure/automation/automation-create-standalone-account). Una cuenta de Automation es un contenedor para los recursos de Azure Automation. Proporciona una manera de separar los entornos u organizar aún más los flujos de trabajo y recursos de Automation. Una vez que cree la cuenta de Automation, debe habilitar las características de Inventario, Change Tracking y Update Management. Para ello, siga estos pasos para habilitar cada característica:

1. En Azure Portal, vaya a la cuenta de Automation que va a usar.

2. Seleccione la solución que va a habilitar (ya sea **Inventario**, **Change Tracking** o **Update Management**).

3. Use la lista desplegable **Seleccionar área de trabajo...** para seleccionar el área de trabajo de Log Analytics que va a usar.

4. Compruebe que toda la información restante sea correcta y, luego, haga clic en **Habilitar** para habilitar la solución.

5. Repita los pasos del 2 al 4 para habilitar las tres soluciones. 

   [![](media/vm-update-management/1-sm.PNG "Habilitación de las características de una cuenta de Automation")](media/vm-update-management/1-lg.PNG#lightbox)

### <a name="in-the-azure-stack-administration-portal"></a>En el portal de administración de Azure Stack
Después de habilitar las soluciones de Azure Automation en Azure Portal, debe iniciar sesión en el portal de administración de Azure Stack como administrador en la nube y descargar la extensión **Azure Update and Configuration Management** de Marketplace de Azure Stack. 

   ![Extensión Azure Update and Configuration Management en Marketplace](media/vm-update-management/2.PNG) 

## <a name="enable-update-management-for-azure-stack-virtual-machines"></a>Habilitación de Update Management en máquinas virtuales de Azure Stack
Siga estos pasos para habilitar Update Management para VM Windows de Azure Stack.

1. Inicie sesión en el portal de usuarios de Azure Stack.

2. En el portal de usuarios de Azure Stack, vaya a la hoja Extensiones de las máquinas virtuales Windows para las que quiere habilitar estas soluciones, haga clic en **+ Agregar**, seleccione la extensión **Azure Update and Configuration Management** y haga clic en **Crear**:

   [![](media/vm-update-management/3-sm.PNG "Hoja de extensión de VM Windows")](media/vm-update-management/3-lg.PNG#lightbox)

3. Proporcione el id. del área de trabajo y la clave principal creados anteriormente para vincular el agente con el área de trabajo de Log Analytics y haga clic en **Aceptar** para implementar la extensión.

   [![](media/vm-update-management/4-sm.PNG "Introducción del id. del área de trabajo y la clave")](media/vm-update-management/4-lg.PNG#lightbox) 

4. Como se describe en la [documentación de administración de Update Management](https://docs.microsoft.com/azure/automation/automation-update-management), deberá habilitar la solución Update Management para cada VM que quiera administrar. Para habilitar la solución para todas las VM que informan al área de trabajo, seleccione **Update Management**, haga clic en **Administrar las máquinas** y, luego, seleccione la opción **Habilitar en todas las máquinas disponibles y futuras**.

   [![](media/vm-update-management/5-sm.PNG "Introducción del id. del área de trabajo y la clave")](media/vm-update-management/5-lg.PNG#lightbox) 

   > [!TIP]
   > Repita este paso para habilitar cada solución para las VM Windows de Azure Stack que informan al área de trabajo. 
  
Después de habilitar la extensión Azure Update and Configuration Management, se realiza un examen dos veces al día para cada VM Windows administrada. Se llama a la API de Windows cada 15 minutos para consultar la hora de la última actualización y determinar si ha cambiado el estado. Si ha cambiado el estado, se inicia un examen de cumplimiento.

Después de que se analizan las VM, aparecen en la cuenta de Azure Automation en la solución Update Management: 

   [![](media/vm-update-management/6-sm.PNG "Introducción del id. del área de trabajo y la clave")](media/vm-update-management/6-lg.PNG#lightbox) 

> [!IMPORTANT]
> Puede que transcurran entre 30 minutos y 6 horas antes de que se muestren los datos actualizados de los equipos administrados.

Las VM Windows de Azure Stack ahora pueden incluirse en las implementaciones de actualización programadas junto con VM de Azure.

## <a name="enable-update-management-using-a-resource-manager-template"></a>Habilitación de Update Management con una plantilla de Resource Manager
Si tiene un gran número de VM Windows de Azure Stack, puede usar [esta plantilla de Azure Resource Manager](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/MicrosoftMonitoringAgent-ext-win) para implementar más fácilmente la solución en VM Windows. La plantilla implementa la extensión Microsoft Monitoring Agent en una VM Windows existente y la agrega a un área de trabajo de Azure Log Analytics existente.
 
## <a name="next-steps"></a>Pasos siguientes
[Optimización del rendimiento de SQL Server](azure-stack-sql-server-vm-considerations.md)
