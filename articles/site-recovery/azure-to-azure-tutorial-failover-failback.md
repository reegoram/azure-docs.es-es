---
title: Conmutación por error y conmutación por recuperación de las máquinas virtuales de Azure replicadas en una región secundaria de Azure con Azure Site Recovery
description: Aprenda a conmutar por error y por recuperación la replicación de las máquinas virtuales de Azure en una región secundaria de Azure con Azure Site Recovery
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.topic: tutorial
ms.date: 10/10/2018
ms.author: raynew
ms.custom: mvc
ms.openlocfilehash: 1c9af5c94aa05f60220080b779921a2c79c322f3
ms.sourcegitcommit: 7b0778a1488e8fd70ee57e55bde783a69521c912
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2018
ms.locfileid: "49067438"
---
# <a name="fail-over-and-fail-back-azure-vms-between-azure-regions"></a>Conmutación por error y por recuperación de máquinas virtuales de Azure entre regiones de Azure

El servicio [Azure Site Recovery](site-recovery-overview.md) contribuye a su estrategia de recuperación ante desastres mediante la administración y la coordinación de la replicación, la conmutación por error y la conmutación por recuperación de máquinas locales y máquinas virtuales (VM) de Azure.

Este tutorial describe cómo conmutar por error una sola máquina virtual de Azure en una región de Azure secundaria. Después de conmutar por error, conmutará por recuperación a la región principal cuando esté disponible. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Conmutar por error la máquina virtual de Azure
> * Volver a proteger la máquina virtual de Azure secundaria, de modo que se replique en la región principal
> * Realizar la conmutación por recuperación de la máquina virtual secundaria
> * Volver a proteger la máquina virtual principal a la región secundaria



## <a name="prerequisites"></a>Requisitos previos

- Asegúrese de que ha completado una [exploración de la recuperación ante desastres](azure-to-azure-tutorial-dr-drill.md) para comprobar que todo funciona según lo previsto.
- Compruebe las propiedades de la máquina virtual antes de ejecutar la conmutación por error de prueba. La máquina virtual debe cumplir los [requisitos de Azure](azure-to-azure-support-matrix.md#support-for-replicated-machine-os-versions).

## <a name="run-a-failover-to-the-secondary-region"></a>Ejecución de una conmutación por error en la región secundaria

1. En **Elementos replicados**, seleccione la máquina virtual que desea conmutar por error > **Conmutar por error**

   ![Conmutación por error](./media/azure-to-azure-tutorial-failover-failback/failover.png)

2. En **Conmutación por error**, seleccione un **Punto de recuperación** en el que realizar la conmutación por error. Puede seleccionar una de las siguientes opciones:

   * **Latest** (Más reciente) (valor predeterminado): esta opción procesa todos los datos en el servicio Site Recovery y proporciona el objetivo de punto de recuperación (RPO) más bajo.
   * **Latest processed** (Último procesado): esta opción revierte la máquina virtual al punto de recuperación más reciente que el servicio Site Recovery haya procesado.
   * **Personalizado**: use esta opción para conmutar por error a un punto de recuperación concreto. Esta opción es útil para realizar una conmutación por error de prueba.

3. Seleccione **Shut down machine before beginning failover** (Apagar la máquina antes de comenzar la conmutación por error) si desea que Site Recovery intente apagar las máquinas virtuales de origen antes de desencadenar la conmutación por error. La conmutación por error continúa aunque se produzca un error de cierre.

4. Siga el progreso de la conmutación por error en la página **Trabajos**.

5. Después de la conmutación por error, valide la máquina virtual iniciando sesión en ella. Si desea volver a otro punto de recuperación para la máquina virtual, puede usar la opción **Cambiar punto de recuperación**.

6. Realice la acción **Confirmar** una vez que quede satisfecho con la conmutación por error de la máquina virtual.
   Al confirmar, se eliminan todos los puntos de recuperación disponibles con el servicio. La opción **Cambiar punto de recuperación** ya no está disponible.

## <a name="reprotect-the-secondary-vm"></a>Volver a proteger la máquina virtual secundaria

Después de la conmutación por error de la máquina virtual, debe volver a protegerla para que se replique de nuevo en la región principal.

1. Asegúrese de que la máquina virtual está en el estado **Conmutación por error confirmada** y compruebe que la región principal está disponible, y puede crear y tener acceso a los recursos nuevos en ella.
2. En **Almacén** > **Elementos replicados**, haga clic con el botón derecho en la máquina virtual que ha sido objeto de la conmutación por error y seleccione **Volver a proteger**.

   ![Haga clic con el botón derecho para volver a proteger](./media/azure-to-azure-tutorial-failover-failback/reprotect.png)

2. Tenga en cuenta que la dirección de la protección, de la región secundaria a la principal, ya está seleccionada.
3. Revise la información de **Grupo de recursos, red, almacenamiento y conjuntos de disponibilidad**. Los recursos marcados (nuevos) se crean como parte de la operación de repetición de la protección.
4. Haga clic en **Aceptar** para desencadenar un trabajo de repetición de la protección. Este trabajo inicializa el sitio de destino con los datos más recientes. A continuación, replica las diferencias en la región principal. La máquina virtual está ahora en un estado protegido.

## <a name="fail-back-to-the-primary-region"></a>Conmutación por recuperación a la región principal

Tras volver a proteger las máquinas virtuales, puede conmutar por recuperación a la región principal, si es preciso. Para ello, configurar una conmutación por error de la región secundaria a la primaria, como se describe en este artículo.
