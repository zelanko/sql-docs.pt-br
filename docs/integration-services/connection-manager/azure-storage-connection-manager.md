---
title: Gerenciador de Conexões do Armazenamento do Azure | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03acf5db82c21a66e2fbd8337713b6989ce36a31
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403067"
---
# <a name="azure-storage-connection-manager"></a>Gerenciador de conexões do Armazenamento do Azure

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  O **gerenciador de conexões do Armazenamento do Azure** habilita a conexão de um pacote do SSIS com uma conta do Armazenamento do Azure.
   
 O **gerenciador de conexões do Armazenamento do Azure** é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS** , selecione **AzureStorage**e clique em **Adicionar**.  
  
As seguintes propriedades estão disponíveis.

- **Serviço:** especifica o serviço de armazenamento ao qual se conectar.
- **Nome da conta:** especifica o nome da conta de armazenamento.
- **Autenticação:** especifica o método de autenticação a ser usado. As autenticações **AccessKey** e **ServicePrincipal** são compatíveis.
    - **AccessKey:** para esse método de autenticação, especifique a **chave de conta**.
    - **ServicePrincipal:** para esse método de autenticação, especifique a **ID do aplicativo**, a **Chave do aplicativo** e a **ID do locatário** da entidade de serviço.
      A entidade de serviço deve ser atribuída à função de **Colaborador de Dados do Storage Blob** para a conta de armazenamento.
      Confira [esta](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) página para saber mais detalhes.
- **Ambiente:** especifica o ambiente de nuvem que hospeda a conta de armazenamento.
