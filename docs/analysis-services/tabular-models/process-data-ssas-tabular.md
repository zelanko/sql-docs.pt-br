---
title: Processar dados (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6fc5d0e934ae7fe4d7f9a00594c2f1ffd21bda1c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="process-data-ssas-tabular"></a>Processar dados (SSAS tabular)
  Ao importar dados para um modelo de tabela, no modo Cache, você está capturando um instantâneo desses dados no momento da importação. Em alguns casos, esses dados podem nunca serem alterados e não precisam ser atualizados no modelo. Porém, é mais provável que os dados de que você está importando sejam alterados regularmente. Para que seu modelo reflita os dados mais recentes das fontes de dados, é necessário processar (atualizar) os dados e recalcular os dados calculados. Para atualizar os dados em seu modelo, você executa uma ação de processo em todas as tabelas, em uma tabela individual, por uma partição, ou por uma conexão da fonte de dados.  
  
 Ao criar seu projeto de modelo, inicie as ações de processamento manualmente no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Após a implantação de um modelo, as operações de processamento podem ser executadas usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou programadas usando um script. As tarefas descritas aqui todas pertencem a ações de processo que você pode fazer durante a criação do modelo no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações sobre ações de processo para um modelo implantado, consulte [Processar banco de dados, tabela ou partição &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Processando os dados manualmente &#40;SSAS Tabular&#41;](../../analysis-services/tabular-models/manually-process-data-ssas-tabular.md)|Descreve como processar manualmente dados de espaço de trabalho modelo.|  
|[Solucionar problemas de dados de processo &#40;SSAS tabular&#41;](../../analysis-services/troubleshoot-process-data-ssas-tabular.md)|Descreve como solucionar problemas de operações de processo.|  
  
  
