---
title: "Gerenciador de Conexões do Armazenamento do Azure | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09368733d9df6a7750c9b782ba45ae129b204b8b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="azure-storage-connection-manager"></a>Gerenciador de conexões do Armazenamento do Azure
  O **gerenciador de conexões do Armazenamento do Azure** permite que um pacote SSIS se conecte a uma conta do Armazenamento do Azure usando os valores especificados para as propriedades: Nome da Conta de Armazenamento e Chave de Conta.  
   
 O **gerenciador de conexões do Armazenamento do Azure** é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md). 
  
1.  Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS** , selecione **AzureStorage**e clique em **Adicionar**.  
  
2.  Na caixa de diálogo Editor do Gerenciador de Conexão do Armazenamento do Azure, escolha **Usar conta do Azure** para se conectar a um Serviço de Armazenamento do Azure por meio da Internet ou escolha **Usar conta de desenvolvedor local** para se conectar ao serviço local hospedado pelo Emulador de Armazenamento do Azure.  
  
3.  Se você tiver escolhido a opção **Usar conta do Azure** , faça o seguinte:  
  
    1.  Especifique valores para os campos **Nome da conta de armazenamento** e **Chave de conta** . Esses valores serão armazenados como dados confidenciais no pacote SSIS.  
  
    2.  Escolha **Usar HTTPS** se quiser usar HTTPS em vez de HTTP para se conectar ao Serviço de Armazenamento do Azure.  
  
4.  Clique em **OK** para fechar a caixa de diálogo.  
  
5.  Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .  
  
  
