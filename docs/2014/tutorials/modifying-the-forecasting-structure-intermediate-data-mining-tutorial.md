---
title: Modificando a estrutura de previsão (Tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4252f9885070067278a24db266ce58714366e69b
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312124"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>Modificando a estrutura de previsão (Tutorial de mineração de dados intermediário)
  A estrutura de mineração criada na tarefa anterior contém um modelo de previsão único. Antes de processar e explorar o modelo, você deve alterar sua estrutura ligeiramente e modificar uma de suas propriedades.  
  
## <a name="modifying-the-mining-structure"></a>Modificando a estrutura de mineração  
 Você pode alterar a estrutura de mineração usando o **estrutura de mineração** guia do Designer de mineração de dados. Ao criar o modelo com o Assistente de Mineração de Dados, você usou três colunas: ReportingDate, ModelRegion e Quantidade. No entanto, o **previsão** tabela também contém uma coluna de valor, que pode ser usado para prever a quantidade de vendas. Usando o **estrutura de mineração** guia, você pode adicionar essa coluna da exibição da fonte de dados para a estrutura de mineração.  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>Para adicionar a coluna Valor à estrutura de mineração de previsão  
  
1.  No **estrutura de mineração** guia do Designer de mineração de dados, no **exibição da fonte de dados** painel, selecione a coluna valor na tabela vTimeSeries.  
  
2.  Arraste a coluna de quantidade do **exibição da fonte de dados** painel na lista de colunas para o **previsão** estrutura.  
  
     A coluna de quantidade agora está incluída no **previsão** estrutura de mineração.  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>Modificando as colunas do modelo de mineração  
 Como você adicionou uma nova coluna à estrutura, é preciso definir como o modelo a usará. Você pode especificar como a coluna será usada no **modelos de mineração** guia do Designer de mineração de dados.  
  
 O **modelos de mineração** guia lista as colunas que contém a estrutura de mineração a **estrutura** coluna da grade e lista as colunas que contém o modelo de mineração na coluna que tem o nome da modelo, nesse caso **previsão**. Clique nos nomes das colunas para fazer modificações. No **previsão** modelo de mineração, a coluna de valor é usada como uma coluna de entrada e também é usada para prever vendas futuras. Portanto, é preciso definir as propriedades da coluna de forma que ela possa ser usada como uma coluna de entrada e uma coluna previsível.  
  
> [!NOTE]  
>  No **modelos de mineração** guia, você também pode criar novos modelos baseados na mesma estrutura, e você pode ajustar as propriedades de algoritmo e da coluna para cada modelo. No entanto, você deverá processar o modelo antes que essas alterações entrem em vigor.  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>Para definir a coluna Valor que será usada  
  
1.  No **previsão** coluna da grade no **modelos de mineração** guia, clique na célula na linha de quantidade.  
  
2.  Selecione **prever** da lista.  
  
     Agora, a coluna Valor passa a ser uma coluna de entrada e uma coluna previsível.  
  
 Você também pode alterar as propriedades das colunas individuais selecionando a coluna e abrindo o **propriedades** janela. Para abrir o **propriedades** janela, clique no nome da coluna e, em seguida, selecione **propriedades**. Se você alterar uma propriedade dentro da coluna de um modelo individual, só será possível alterar as propriedades deste modelo. No entanto, quando você alterar uma propriedade dentro de **estrutura** coluna, a alteração afeta todo o modelo é associado à estrutura. Sempre que você fizer alterações no modelo ou na estrutura, deverá processá-los novamente para ver os efeitos.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Personalizando e processando o modelo de previsão &#40;intermediário de Tutorial de mineração de dados&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas de mineração &#40;Analysis Services – mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelos de mineração &#40;Analysis Services – mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  