---
title: Configuración de un laboratorio con Azure Lab Services | Microsoft Docs
description: En este tutorial, va a configurar un laboratorio para usarlo en una clase.
services: devtest-lab, lab-services, virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 10/05/2018
ms.author: spelluru
ms.openlocfilehash: 6696d6e7e53e98dfab2a65c7c66825936020f33c
ms.sourcegitcommit: 67abaa44871ab98770b22b29d899ff2f396bdae3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2018
ms.locfileid: "48856647"
---
# <a name="tutorial-set-up-a-classroom-lab"></a>Tutorial: Configuración de un laboratorio de clase 
En este tutorial, se va a configurar un laboratorio de clase con las máquinas virtuales que van a utilizar los estudiantes de la clase.  

En este tutorial realizará lo siguiente:

> [!div class="checklist"]
> * Creación de un laboratorio educativo
> * Configuración del laboratorio de clase
> * Envío del vínculo de registro a los estudiantes

## <a name="prerequisites"></a>Requisitos previos
Para configurar un laboratorio de clase en una cuenta de laboratorio, debe ser miembro del rol **Creador de laboratorio** en la cuenta de laboratorio. La cuenta que usó para crear una cuenta de laboratorio se agrega automáticamente a este rol. Un propietario de laboratorio puede agregar otros usuarios al rol de Creador de laboratorio mediante los pasos descritos en el siguiente artículo: [Incorporación de un usuario al rol de Creador de laboratorio](tutorial-setup-lab-account.md#add-a-user-to-the-lab-creator-role).


## <a name="create-a-classroom-lab"></a>Creación de un laboratorio educativo

1. Vaya al [sitio web de Azure Lab Services](https://labs.azure.com). 
2. Seleccione **Iniciar sesión** y escriba las credenciales. Azure Lab Services es compatible con cuentas profesionales y cuentas Microsoft. 
3. En la ventana **Nuevo laboratorio**, lleve a cabo las siguientes acciones: 
    1. Especifique un **nombre** para el laboratorio. 
    2. Especifique el máximo **número de usuarios** permitidos en el laboratorio. 
    6. Seleccione **Guardar**.

        ![Creación de un laboratorio educativo](../media/tutorial-setup-classroom-lab/new-lab-window.png)
4. En la página **Seleccionar especificaciones de máquina virtual**, realice los pasos siguientes:
    1. Seleccione un **tamaño** para las máquinas virtuales (VM) creadas en el laboratorio. 
    2. Seleccione la **región** en la que quiere que se creen las máquinas virtuales. 
    3. Seleccione la **imagen de máquina virtual** que se usará para crear máquinas virtuales en el laboratorio. 
    4. Seleccione **Next** (Siguiente).

        ![Especificaciones de máquina virtual](../media/tutorial-setup-classroom-lab/select-vm-specifications.png)    
5. En la página **Establecer credenciales**, especifique las credenciales predeterminadas de todas las máquinas virtuales del laboratorio. 
    1. Especifique el **nombre del usuario** para todas las máquinas virtuales del laboratorio.
    2. Especifique la **contraseña** del usuario. 

        > [!IMPORTANT]
        > Tome nota de ambos. No se volverán a mostrar.
    3. Seleccione **Crear**. 

        ![Establecer credenciales](../media/tutorial-setup-classroom-lab/set-credentials.png)
6. En la página **Configurar plantilla**, puede ver el estado del proceso de creación del laboratorio. La creación de la plantilla en el laboratorio tarda un máximo de 20 minutos. 

    ![Configurar plantilla](../media/tutorial-setup-classroom-lab/configure-template.png)
7. Una vez completada la configuración de la plantilla, verá la siguiente página: 

    ![Página Configurar plantilla una vez terminada](../media/tutorial-setup-classroom-lab/configure-template-after-complete.png)
8. Los pasos siguientes son opcionales para este tutorial: 
    1. Seleccione **Iniciar** para iniciar la plantilla de máquina virtual.
    2. Seleccione **Conectar** para conectarse a la plantilla de máquina virtual. 
    3. Instale y configure el software en la plantilla de máquina virtual. 
    4. **Pare** la máquina virtual.  
    5. Escriba una **descripción** para la plantilla.

        ![Siguiente en la página Configurar plantilla](../media/tutorial-setup-classroom-lab/configure-template-next.png)
9. Seleccione **Siguiente** en la página de plantilla. 
10. En la página **Publicar la plantilla**, realice las acciones siguientes. 
    1. Para publicar la plantilla inmediatamente, seleccione la casilla *I understand I can't modify the template after publishing. This process can only be done once and can take up to an hour* (Comprendo que no puedo modificar la plantilla después de la publicación. Este proceso solo se puede realizar una vez y puede tardar hasta una hora), y seleccione **Publicar**.  

        > [!WARNING]
        > Una vez que publique, no se puede cancelar la publicación. 
    2. Para publicar más adelante, seleccione **Guardar para más adelante**. Puede publicar la plantilla de máquina virtual una vez finalizado el asistente. Para más información sobre cómo configurar y publicar una vez finalizado el asistente, consulte la sección [Publicación de la plantilla](how-to-manage-classroom-labs.md#publish-the-template) del artículo [Administración de laboratorios educativos](how-to-manage-classroom-labs.md).

        ![Publicar plantilla](../media/tutorial-setup-classroom-lab/publish-template.png)
11. Puede ver el **progreso de la publicación** de la plantilla. Este proceso puede tardar hasta una hora. 

    ![Publicar plantilla: progreso](../media/tutorial-setup-classroom-lab/publish-template-progress.png)
12. Podrá ver la página siguiente cuando la plantilla se haya publicado correctamente. Seleccione **Listo**.

    ![Publicar plantilla: correctamente](../media/tutorial-setup-classroom-lab/publish-success.png)
1. Verá el **panel** del laboratorio. 
    
    ![Panel del laboratorio de clase](../media/tutorial-setup-classroom-lab/classroom-lab-home-page.png)
4. Cambie a la página **Máquinas virtuales** y confirme que ve las máquinas virtuales que tienen el estado **Sin asignar**. Estas máquinas virtuales no están asignadas a los alumnos todavía. Deberían estar en estado **Detenida**. En esta pagina, puede iniciar una máquina virtual de un alumno, conectarse a la máquina virtual, detener la máquina virtual y eliminar la máquina virtual. Puede iniciarlas en esta página o dejar que los alumnos inicien las máquinas virtuales. 

    ![Máquinas virtuales en estado detenido](../media/tutorial-setup-classroom-lab/virtual-machines-stopped.png)

## <a name="send-registration-link-to-students"></a>Envío del vínculo de registro a los estudiantes

1. Cambie a la vista **Panel** seleccionando **Panel** en el menú de la izquierda. 
2. Seleccione el icono **Registro de usuario**.

    ![Vínculo de registro del estudiante](../media/tutorial-setup-classroom-lab/dashboard-user-registration-link.png)
1. En el cuadro de diálogo **Registro de usuario**, seleccione el botón **Copiar**. El vínculo se copia en el Portapapeles. Péguelo en un editor de correo electrónico y envíe un correo electrónico al estudiante. 

    ![Vínculo de registro del estudiante](../media/tutorial-setup-classroom-lab/registration-link.png)
2. En el cuadro de diálogo **Registro de usuario**, seleccione **Cerrar**. 
3. Comparta el vínculo de registro con un alumno para que este se pueda registrar para la clase. 


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha creado un laboratorio de clase y ha configurado el laboratorio. Para saber cómo el estudiante puede acceder a una máquina virtual en el laboratorio con el enlace de registro, avance al siguiente tutorial:

> [!div class="nextstepaction"]
> [Conexión a una máquina virtual en el laboratorio de clase](tutorial-connect-virtual-machine-classroom-lab.md)

