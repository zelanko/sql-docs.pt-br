---
title: "Alterar as propriedades de um modelo de mineração | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- mining models [Analysis Services], properties
- properties [data mining]
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ccfd17eb10b11052f24cf18f9b0e94649b5030af
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="change-the-properties-of-a-mining-model"></a>Alterar as propriedades de um modelo de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Algumas propriedades de modelo de mineração se aplicam ao modelo como um todo, e outras propriedades de modelo se aplicam a colunas individuais. Exemplos de propriedades que se aplicam ao modelo inteiro seriam a propriedade **Drillthrough** , que especifica se os dados de caso devem estar disponíveis para consulta, e a propriedade **Description** . Propriedades que se aplicam à coluna incluem **Usage** e **ModelingFlags**, que controlam como os dados na coluna são usados no modelo.  
  
 As propriedades modelo a seguir têm editores avançados que você pode usar para criar expressões ou configurar propriedades de modelo complexas. Estas propriedades oferecem:  
  
-   Propriedade **Filtro**: abre a [Caixa de Diálogo Filtro de Conjunto de Dados ou Filtro de Modelo](http://msdn.microsoft.com/library/a9602174-b7e2-4e16-8ded-dfd8eb9264d7).  
  
-   Propriedade **AlgorithmParameters**: abre a [Caixa de diálogo de Parâmetros de Algoritmo &#40;Exibição de Modelos de Mineração&#41;](http://msdn.microsoft.com/library/57f9f6f8-8ca4-4a6e-8f18-85f0571b7060).  
  
 Para obter informações sobre como definir as propriedades em um modelo de mineração, consulte [Colunas do modelo de mineração](../../analysis-services/data-mining/mining-model-columns.md).  
  
### <a name="to-change-the-properties-of-a-mining-model"></a>Para alterar as propriedades de um modelo de mineração  
  
1.  Na guia **Modelos de Mineração** do Designer de Data Mining, clique com o botão direito do mouse no cabeçalho da coluna que contém o nome do modelo de mineração ou na linha da grade que contém o nome do algoritmo de mineração e selecione **Propriedades**.  
  
2.  Na janela **Propriedades** na lateral direita da tela, realce o valor que corresponde à propriedade que você deseja alterar e digite o novo valor.  
  
     O novo valor entrará em vigor quando você selecionar um elemento diferente no designer.  
  
### <a name="to-change-the-properties-of-a-mining-model-column"></a>Para alterar as propriedades de uma coluna de modelo de mineração  
  
1.  Na guia **Modelos de Mineração** no Designer de Data Mining, clique com o botão direito do mouse na célula da grade na interseção da coluna da estrutura de mineração e do modelo de mineração e selecione **Propriedades**.  
  
2.  Na janela **Propriedades** na lateral direita da tela, realce o valor que corresponde à propriedade que você deseja alterar e digite o novo valor.  
  
    > [!NOTE]  
    >  Se o uso da coluna for definido como **Ignorar**, a janela **Propriedades** da coluna ficará em branco.  
  
     O novo valor entrará em vigor quando você selecionar um elemento diferente no designer.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
