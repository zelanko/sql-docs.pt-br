---
title: Modificando e processando o modelo de cesta de compras (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 96eb44713cd34fdcea81a7e5e4daf26739afdec1
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36311904"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>Modificando e processando o modelo de cesta de compras (Tutorial de mineração de dados intermediário)
  Antes de processar o modelo de mineração de associação que você criou, você deve alterar os valores padrão de dois parâmetros: *suporte* e *probabilidade*.  
  
-   *Suporte* define a porcentagem de casos em que uma regra deve existir antes de ser considerado válido. Você especificará que uma regra deve ser encontrada em pelo menos 1 por cento dos casos.  
  
-   *Probabilidade* define como provavelmente uma associação deve ser antes de ser considerado válido. Você vai considerar qualquer associação com a probabilidade de pelo menos 10 por cento.  
  
 Para obter mais informações sobre os efeitos de aumentar ou diminuir a probabilidade e suporte, consulte [Microsoft Association Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md).  
  
 Depois de definir a estrutura e os parâmetros para o **associação** modelo de mineração, você processará o modelo.  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>Para ajustar os parâmetros do modelo de Associação  
  
1.  Abra o **modelos de mineração** guia do Designer de mineração de dados.  
  
2.  Clique com botão direito do **associação** coluna da grade no designer e selecione **definir parâmetros de algoritmo para abrir os parâmetros do algoritmo** caixa de diálogo.  
  
3.  No **valor** coluna o **parâmetros de algoritmo** caixa de diálogo caixa, defina os seguintes parâmetros:  
  
     MINIMUM_PROBABILITY = 0.1  
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>Para processar o modelo de mineração  
  
1.  Sobre o **modelo de mineração** menu [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], selecione **processar estrutura de mineração e todos os modelos.**  
  
2.  No aviso que pergunta se você deseja construir e implantar o projeto, clique em **Sim**.  
  
     O **processar estrutura de mineração - associação** caixa de diálogo é aberta.  
  
3.  Clique em **Executar**.  
  
     A caixa de diálogo **Andamento do Processo** é aberta para exibir informações sobre o processamento do modelo. O processamento da estrutura e do modelo novos pode demorar algum tempo.  
  
4.  Depois que o processamento estiver completo, clique em **Fechar** para sair da caixa de diálogo **Progresso do Processo** .  
  
5.  Clique em **fechar** novamente para sair do **processar estrutura de mineração - associação** caixa de diálogo.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Explorando os modelos de cesta de compras &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e considerações de processamento &#40;mineração de dados&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  