---
title: Modificando e processando o modelo de cesta de mercado (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4987e3497b7d52ff11f8f52bc403105340f7f508
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63301368"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>Modificando e processando o modelo de cesta de compras (Tutorial de mineração de dados intermediário)
  Antes de processar o modelo de mineração de associação que você criou, você deve alterar os valores padrão de dois dos parâmetros: *suporte* e *probabilidade*.  
  
-   O *suporte* define a porcentagem de casos em que uma regra deve existir antes de ser considerada válida. Você especificará que uma regra deve ser encontrada em pelo menos 1 por cento dos casos.  
  
-   *Probabilidade* define a probabilidade de que uma associação deve ser antes de ser considerada válida. Você vai considerar qualquer associação com a probabilidade de pelo menos 10 por cento.  
  
 Para obter mais informações sobre os efeitos de aumentar ou diminuir o suporte e a probabilidade, consulte [referência técnica do algoritmo de associação da Microsoft](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md).  
  
 Depois de definir a estrutura e os parâmetros para o modelo de mineração de **Associação** , você processará o modelo.  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>Para ajustar os parâmetros do modelo de Associação  
  
1.  Abra a guia **modelos de mineração** do designer de mineração de dados.  
  
2.  Clique com o botão direito do mouse na coluna **Associação** na grade no designer e selecione **definir parâmetros de algoritmo para abrir a caixa de diálogo parâmetros de algoritmo** .  
  
3.  Na coluna **valor** da caixa de diálogo **parâmetros do algoritmo** , defina os seguintes parâmetros:  
  
     MINIMUM_PROBABILITY = 0.1  
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>Para processar o modelo de mineração  
  
1.  No menu **modelo de mineração** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], selecione **estrutura de mineração de processo e todos os modelos.**  
  
2.  No aviso que pergunta se você deseja construir e implantar o projeto, clique em **Sim**.  
  
     A caixa de diálogo **processar estrutura de mineração-Associação** é aberta.  
  
3.  Clique em **Executar**.  
  
     A caixa de diálogo **Andamento do Processo** é aberta para exibir informações sobre o processamento do modelo. O processamento da estrutura e do modelo novos pode demorar algum tempo.  
  
4.  Depois que o processamento estiver completo, clique em **Fechar** para sair da caixa de diálogo **Progresso do Processo** .  
  
5.  Clique em **fechar** novamente para sair da caixa de diálogo **processar estrutura de mineração-Associação** .  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Explorando os modelos de cesta de mercado &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos e considerações de processamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
