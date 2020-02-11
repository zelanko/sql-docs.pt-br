---
title: Modificando a estrutura de previsão (tutorial de mineração de dados intermediário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a86ddf0a715fc3a2313f555e898b3bd94cf66d8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63301297"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>Modificando a estrutura de previsão (Tutorial de mineração de dados intermediário)
  A estrutura de mineração criada na tarefa anterior contém um modelo de previsão único. Antes de processar e explorar o modelo, você deve alterar sua estrutura ligeiramente e modificar uma de suas propriedades.  
  
## <a name="modifying-the-mining-structure"></a>Modificando a estrutura de mineração  
 Você pode alterar a estrutura de mineração usando a guia **estrutura de mineração** do designer de mineração de dados. Ao criar o modelo com o Assistente de Mineração de Dados, você usou três colunas: ReportingDate, ModelRegion e Quantidade. No entanto, a tabela de **previsão** também contém uma coluna de valor, que pode ser usada para prever a quantidade de vendas. Usando a guia **estrutura de mineração** , você pode adicionar essa coluna da exibição da fonte de dados à estrutura de mineração.  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>Para adicionar a coluna Valor à estrutura de mineração de previsão  
  
1.  Na guia **estrutura de mineração** do designer de data mining, no painel **exibição da fonte de dados** , selecione a coluna valor na tabela vTimeSeries.  
  
2.  Arraste a coluna valor do painel **exibição da fonte de dados** para a lista de colunas da estrutura de **previsão** .  
  
     A coluna de valor agora está incluída na estrutura de mineração de **previsão** .  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>Modificando as colunas do modelo de mineração  
 Como você adicionou uma nova coluna à estrutura, é preciso definir como o modelo a usará. Você pode especificar como a coluna será usada na guia **modelos de mineração** do designer de mineração de dados.  
  
 A guia **modelos de mineração** lista as colunas que a estrutura de mineração contém na coluna **estrutura** da grade e lista as colunas que o modelo de mineração contém na coluna que tem o nome do modelo, neste caso, **previsão**. Clique nos nomes das colunas para fazer modificações. No modelo de mineração de **previsão** , a coluna valor é usada como uma coluna de entrada e também é usada para prever vendas futuras. Portanto, é preciso definir as propriedades da coluna de forma que ela possa ser usada como uma coluna de entrada e uma coluna previsível.  
  
> [!NOTE]  
>  Na guia **modelos de mineração** , você também pode criar novos modelos com base na mesma estrutura e pode ajustar as propriedades de algoritmo e coluna para cada modelo. No entanto, você deverá processar o modelo antes que essas alterações entrem em vigor.  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>Para definir a coluna Valor que será usada  
  
1.  Na coluna **previsão** da grade na guia **modelos de mineração** , clique na célula da linha valor.  
  
2.  Selecione **prever** na lista.  
  
     Agora, a coluna Valor passa a ser uma coluna de entrada e uma coluna previsível.  
  
 Você também pode alterar as propriedades de colunas individuais selecionando a coluna e abrindo a janela **Propriedades** . Para abrir a janela **Propriedades** , clique com o botão direito do mouse no nome da coluna e selecione **Propriedades**. Se você alterar uma propriedade dentro da coluna de um modelo individual, só será possível alterar as propriedades deste modelo. No entanto, quando você altera uma propriedade dentro da coluna de **estrutura** , a alteração afeta todos os modelos associados à estrutura. Sempre que você fizer alterações no modelo ou na estrutura, deverá processá-los novamente para ver os efeitos.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Personalizando e processando o modelo de previsão &#40;tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Estruturas de mineração &#40;Analysis Services de mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelos de mineração &#40;Analysis Services de mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
