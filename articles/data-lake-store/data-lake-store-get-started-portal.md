---
title: Uso de Azure Portal como introducción a Azure Data Lake Storage Gen1 | Microsoft Docs
description: Use Azure Portal para crear una cuenta de Azure Data Lake Storage Gen1 y realizar operaciones básicas en la cuenta de Data Lake Storage Gen1.
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: nitinme
ms.openlocfilehash: fba62a7838ad4b8f349e233eef5e8d82450f1453
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46949026"
---
# <a name="get-started-with-azure-data-lake-storage-gen1-using-the-azure-portal"></a>Introducción a Azure Data Lake Storage Gen1 con Azure Portal

> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [CLI de Azure](data-lake-store-get-started-cli-2.0.md)
>
> 

[!INCLUDE [data-lake-storage-gen1-rename-note.md](../../includes/data-lake-storage-gen1-rename-note.md)]

Aprenda a usar Azure Portal para crear una cuenta de Azure Data Lake Storage Gen1 y realizar operaciones básicas como crear carpetas, cargar y descargar archivos de datos, eliminar la cuenta, etc. Para más información, consulte [Introducción a Azure Data Lake Storage Gen1](data-lake-store-overview.md).

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar este tutorial, debe contar con lo siguiente:

* **Una suscripción de Azure**. Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-storage-gen1-account"></a>Creación de una cuenta de Data Lake Storage Gen1

1. Inicie sesión en el nuevo [Azure Portal](https://portal.azure.com).
2. Haga clic en **Crear un recurso > Storage > Data Lake Storage Gen1**.
3. En la hoja **Nuevo Data Lake Storage Gen1**, proporcione los valores como se muestra en la captura de pantalla siguiente:
   
    ![Creación de una nueva cuenta de Data Lake Storage Gen1](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Create a new Data Lake Storage Gen1 account")
   
   * **Nombre**. Escriba un nombre único para la cuenta de Data Lake Storage Gen1.
   * **Suscripción**. Seleccione la suscripción con la que desea crear una cuenta de Data Lake Storage Gen1.
   * **Grupo de recursos**. Seleccione un grupo de recursos existente, o bien seleccione la opción **Crear nuevo** para crearlo. Un grupo de recursos es un contenedor que incluye los recursos relacionados de una aplicación. Para más información, consulte [Grupos de recursos en Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Ubicación**: seleccione la ubicación donde desea crear la cuenta de Data Lake Storage Gen1.
   * **Configuración de cifrado**. Hay tres opciones:
     
     * **No habilitar el cifrado**.
     * Seleccione **Usar claves administradas por Data Lake Storage Gen1** si desea que Azure Data Lake Storage Gen1 administre las claves de cifrado.
     * **Usar claves de su propia instancia de Key Vault**. Puede seleccionar una instancia de Azure Key Vault existente o crear una nueva. Si utiliza las claves de un almacén de claves, debe asignar permisos para que la cuenta de Data Lake Storage Gen1 acceda a ese almacén Azure Key Vault. Para obtener instrucciones, consulte [Asignación de permisos a Azure Key Vault](#assign-permissions-to-azure-key-vault).
       
        ![Cifrado de Data Lake Storage Gen1](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Data Lake Storage Gen1 encryption")
       
        Haga clic en **Aceptar** en la hoja **Configuración de cifrado**.

        Para más información, consulte [Cifrado de datos en Azure Data Lake Storage Gen1](./data-lake-store-encryption.md).

4. Haga clic en **Create**(Crear). Si elige anclar la cuenta al panel, volverá a este, donde podrá ver el progreso del aprovisionamiento de la cuenta de Data Lake Storage Gen1. Una vez aprovisionada la cuenta de Data Lake Storage Gen1, aparece la hoja de la cuenta.

## <a name="assign-permissions-to-azure-key-vault"></a>Asignación de permisos para Azure Key Vault
Si utiliza las claves de Azure Key Vault para configurar el cifrado de la cuenta de Data Lake Storage Gen1, debe configurar el acceso entre la cuenta de Data Lake Storage Gen1 y la de Azure Key Vault. Para ello, siga los pasos que se indican a continuación.

1. Si ha usado claves de Azure Key Vault, la hoja de la cuenta de Data Lake Storage Gen1 muestra una advertencia en la parte superior. Haga clic en la advertencia para abrir **Cifrado**.
   
    ![Cifrado de Data Lake Storage Gen1](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Data Lake Storage Gen1 encryption")
2. La hoja muestra dos opciones para configurar el acceso.

    ![Cifrado de Data Lake Storage Gen1](./media/data-lake-store-get-started-portal/adls-encryption-4.png "Data Lake Storage Gen1 encryption")
   
   * En la primera opción, haga clic en **Conceder permisos** para configurar el acceso. La primera opción solo está habilitada si el usuario que creó la cuenta de Data Lake Storage Gen1 es también administrador de Azure Key Vault.
   * La otra opción consiste en ejecutar el cmdlet de PowerShell que se muestra en la hoja. Es preciso ser propietario de Azure Key Vault o tener capacidad para conceder permisos en Azure Key Vault. Después de ejecutar el cmdlet, vuelva a la hoja y haga clic en **Habilitar** para configurar el acceso.

> [!NOTE]
> También puede crear una cuenta de Data Lake Storage Gen1 con plantillas de Azure Resource Manager. Estas plantillas son accesibles desde las [plantillas de inicio rápido de Azure](https://azure.microsoft.com/resources/templates/?term=data+lake+store):
    - Sin cifrado de datos: [Implementación de la cuenta de Azure Data Lake Storage Gen1 sin cifrado de datos](https://azure.microsoft.com/resources/templates/101-data-lake-store-no-encryption/).
    - Con cifrado de datos mediante Data Lake Storage Gen1: [Implementación de la cuenta de Data Lake Storage Gen1 con cifrado (Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/).
    - Con cifrado de datos mediante Azure Key Vault: [Implementación de la cuenta de Data Lake Storage Gen1 con cifrado (Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/).
> 
> 



## <a name="createfolder"></a>Creación de carpetas en una cuenta de Azure Data Lake Storage Gen1
Puede crear carpetas en la cuenta de Data Lake Storage Gen1 para administrar y almacenar datos.

1. Abra la cuenta de Data Lake Storage Gen1 que creó. En el panel izquierdo, haga clic en **Todos los recursos** y, en la hoja que se abre, haga clic en el nombre de la cuenta en la que quiere crear carpetas. Si ancló la cuenta al Panel de inicio, haga clic en ese icono de cuenta.
2. En la hoja de su cuenta de Data Lake Storage Gen1, haga clic en **Explorador de datos**.
   
    ![Creación de carpetas en una cuenta de Data Lake Storage Gen1](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Create folders in a Data Lake Storage Gen1 account")
3. En la hoja de Explorador de datos, haga clic en **Nueva carpeta**, escriba un nombre para la nueva carpeta y haga clic en **Aceptar**.
   
    ![Creación de carpetas en una cuenta de Data Lake Storage Gen1](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Create folders in a Data Lake Storage Gen1 account")
   
    La carpeta recién creada se muestra en la hoja **Explorador de datos** . Puede crear carpetas anidadas hasta cualquier nivel.
   
    ![Creación de carpetas en una cuenta de Data Lake](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Create folders in a Data Lake accoun")

## <a name="uploaddata"></a>Carga de datos en una cuenta de Data Lake Storage Gen1
Puede cargar los datos en una cuenta de Data Lake Storage Gen1 directamente en el nivel raíz o en una carpeta que creara en la cuenta. 

1. Desde la hoja **Explorador de datos**, haga clic en **Carga**. 
2. En la hoja **Cargar archivos**, vaya a los archivos que desee cargar y haga clic en **Agregar archivos seleccionados**. También puede seleccionar más de un archivo para cargar.

    ![Cargar datos](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Cargar datos")

Si busca datos de ejemplo para cargar, puede obtener la carpeta **Ambulance Data** en el [repositorio Git de Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="properties"></a>Acciones disponibles con los datos almacenados
Haga clic en el icono de puntos suspensivos en un archivo y, en el menú emergente, en la acción que desee realizar con los datos.

![Propiedades de los datos](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "Propiedades de los datos") 

## <a name="secure-your-data"></a>Protección de los datos
Puede proteger los datos almacenados en su cuenta de Data Lake Storage Gen1 con Azure Active Directory y el control de acceso (ACL). Para obtener instrucciones sobre cómo hacerlo, consulte [Protección de los datos almacenados en Azure Data Lake Storage Gen1](data-lake-store-secure-data.md).

## <a name="delete-a-data-lake-storage-gen1-account"></a>Eliminación de una cuenta de Data Lake Storage Gen1
Para eliminar una cuenta de Data Lake Storage Gen1, en la hoja de Data Lake Storage Gen1, haga clic en **Eliminar**. Para confirmar la acción, se le pedirá que escriba el nombre de la cuenta que desea eliminar. Escriba el nombre de la cuenta y después haga clic en **Eliminar**.

![Eliminación de una cuenta de Data Lake Storage Gen1](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Eliminación de una cuenta de Data Lake")

## <a name="next-steps"></a>Pasos siguientes
* [Uso de Azure Data Lake Storage Gen1 para requisitos de macrodatos](data-lake-store-data-scenarios.md) 
* [Protección de datos en Data Lake Storage Gen1](data-lake-store-secure-data.md)
* [Uso de Azure Data Lake Analytics con Data Lake Storage Gen1](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de Azure HDInsight con Data Lake Storage Gen1](data-lake-store-hdinsight-hadoop-use-portal.md)

