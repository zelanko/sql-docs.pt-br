---
title: "Gerenciador de Conexão do Gerenciador de recursos do Azure | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: dd1dbf668bf3ac24d9d6598b0ff9e2256d897c42
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="azure-resource-manager-connection-manager"></a>Gerenciador de Conexão do Gerenciador de recursos do Azure
O **Gerenciador de Conexão do Azure Resource Manager** permite que um pacote do SSIS gerenciar recursos do Azure usando um [entidade de serviço](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal).

O **Gerenciador de Conexão do Azure Resource Manager** é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para criar e configurar um **Gerenciador de Conexão do Azure Resource Manager**, siga as etapas abaixo:

1. No **adicionar Gerenciador de Conexão SSIS** caixa de diálogo, selecione **AzureResourceManager**e clique em **adicionar**.
2. No **Editor do Gerenciador de recursos do Gerenciador de Conexão do Azure** caixa de diálogo, especifique o **ID do aplicativo**, **chave de aplicativo**, e **ID de locatário** da entidade de serviço. Para obter detalhes sobre essas propriedades, consulte [isso](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) artigo.
3. Clique em **OK** para fechar a caixa de diálogo.
4. Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .

