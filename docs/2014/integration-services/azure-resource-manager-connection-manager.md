---
title: Gerenciador de Conexões do Azure Resource Manager | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPARMCM.F1
- SQL11.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: a2380258-0418-4a8c-a731-5071a44ddf1e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1dce4def11f14072295dbf3cde9d5ab77304fe74
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439343"
---
# <a name="azure-resource-manager-connection-manager"></a>Gerenciador de Conexões do Azure Resource Manager
O **Gerenciador de Conexões do Azure Resource Manager** permite que um pacote do SSIS gerencie recursos do Azure usando uma [entidade de serviço](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).

Para criar e configurar um **gerenciador de conexões do Azure Resource Manager**, siga as etapas abaixo:

1. Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS**, selecione **AzureResourceManager** e clique em **Adicionar**.
2. Na caixa de diálogo **Editor do gerenciador de conexões do Azure Resource Manager**, especifique a **ID do Aplicativo**, a **Chave do Aplicativo** e a **ID do Locatário** da entidade de serviço. Para obter detalhes sobre essas propriedades, consulte [este](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) artigo.
3. Clique em **OK** para fechar a caixa de diálogo.
4. Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .
