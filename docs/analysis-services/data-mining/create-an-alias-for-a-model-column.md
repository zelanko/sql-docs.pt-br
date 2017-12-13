---
title: Criar um Alias para uma coluna de modelo | Microsoft Docs
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
- data mining [Analysis Services], how-to topics
- mining models [Analysis Services], columns
- column names [Analysis Services]
ms.assetid: c80ebe66-a8f8-4f24-9fe8-8288de9d13bc
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 579b9aedecce2df549e93459ccd368120d75ae3b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="create-an-alias-for-a-model-column"></a>Criar um alias para uma coluna de modelo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], você pode criar um alias para uma coluna de modelo. Isso é útil quando o nome da estrutura de mineração é muito comprido, dificultando o trabalho, ou quando é necessário renomear a coluna para uma descrição mais detalhada de seu conteúdo ou uso no modelo. Por exemplo, se fizer uma cópia da coluna de estrutura e em seguida diferenciar a coluna para um modelo específico, você poderá renomear a coluna de modo a refletir o conteúdo com maior exatidão.  
  
 Para criar um alias para uma coluna de modelo, use o painel **Propriedades** e defina a propriedade [Nome](../../analysis-services/scripting/properties/name-element-assl.md) da coluna.  
  
 Na guia **Modelos de Mineração** do Designer de Data Mining, o alias aparece entre parênteses próximo ao rótulo de uso da coluna.  
  
 Para obter informações sobre como definir as propriedades em um modelo de mineração, consulte [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md).  
  
### <a name="to-add-an-alias-to-a-mining-model-column"></a>Para adicionar um alias a uma coluna de modelo de mineração  
  
1.  Na guia **Modelos de Mineração** no Designer de Data Mining, clique com o botão direito do mouse na célula no modelo da coluna de mineração que desejar alterar e, em seguida, selecione **Propriedades**.  
  
2.  Na janela **Propriedades** , no lado direito da tela, clique na célula ao lado da propriedade Nome e exclua o valor atual. Digite um novo nome para a coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Propriedades do modelo de mineração](../../analysis-services/data-mining/mining-model-properties.md)  
  
  
