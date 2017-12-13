---
title: "Excluir um modelo de mineração de uma estrutura de mineração | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], mining models
- deleting mining models
- removing mining models
- mining models [Analysis Services], deleting
ms.assetid: 9ab1506b-856e-4762-a663-5adf15ac71e3
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 470e1d74434261b08c47f93c060c4ac4da143cb2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>Excluir um modelo de mineração de uma estrutura de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Você pode excluir modelos de mineração usando o Designer de mineração de dados, usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ou usando instruções DMX.  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>Exclua um modelo de mineração usando as Ferramentas de Dados do SQL Server  
  
1.  Selecione a guia **Modelos de Mineração** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no modelo a ser excluído e selecione **Excluir**.  
  
     A caixa de diálogo **Excluir Objetos** é aberta.  
  
3.  Clique em **OK**.  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>Exclua um modelo de mineração usando o SQL Server Management Studio  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém o modelo.  
  
2.  Expanda **Estruturas de Mineração**e, depois, **Modelos de Mineração**.  
  
3.  Clique com o botão direito do mouse no modelo a ser excluído e selecione **Excluir**.  
  
     A exclusão do modelo não leva à exclusão dos dados de treinamento, mas apenas dos metadados e de quaisquer padrões criados durante o treinamento do modelo.  
  
### <a name="delete-a-mining-model-using-dmx"></a>Excluir um modelo de mineração usando DMX  
  
-   [DROP MINING MODEL &#40;DMX&#41;](../../dmx/drop-mining-model-dmx.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
