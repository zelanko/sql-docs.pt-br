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
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5e2605e5ab2c36c282adec778f6f20ebb2e37f1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189413"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>Modificando a estrutura de previsão (Tutorial de mineração de dados intermediário)
  A estrutura de mineração criada na tarefa anterior contém um modelo de previsão único. Antes de processar e explorar o modelo, você deve alterar sua estrutura ligeiramente e modificar uma de suas propriedades.  
  
## <a name="modifying-the-mining-structure"></a>Modificando a estrutura de mineração  
 Você pode alterar a estrutura de mineração usando o **estrutura de mineração** guia do Designer de mineração de dados. Ao criar o modelo com o Assistente de Mineração de Dados, você usou três colunas: ReportingDate, ModelRegion e Quantidade. No entanto, o **Forecasting** tabela também contém uma coluna de valor, que pode ser usado para prever o volume de vendas. Usando o **estrutura de mineração** guia, você pode adicionar essa coluna da exibição da fonte de dados para a estrutura de mineração.  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>Para adicionar a coluna Valor à estrutura de mineração de previsão  
  
1.  Sobre o **estrutura de mineração** guia do Designer de mineração de dados, no **exibição da fonte de dados** painel, selecione a coluna valor na tabela vTimeSeries.  
  
2.  Arraste a coluna Quantidade a **exibição da fonte de dados** painel para a lista de colunas para o **Forecasting** estrutura.  
  
     A coluna valor agora está incluída na **Forecasting** estrutura de mineração.  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>Modificando as colunas do modelo de mineração  
 Como você adicionou uma nova coluna à estrutura, é preciso definir como o modelo a usará. Você pode especificar como a coluna será usada na **modelos de mineração** guia do Designer de mineração de dados.  
  
 O **modelos de mineração** guia lista as colunas contidas na estrutura de mineração na **estrutura** coluna da grade e lista as colunas que o modelo de mineração contém a coluna que tem o nome das modelo, nesse caso **Forecasting**. Clique nos nomes das colunas para fazer modificações. No **Forecasting** modelo de mineração, a coluna de valor é usada como uma coluna de entrada e também é usada para prever vendas futuras. Portanto, é preciso definir as propriedades da coluna de forma que ela possa ser usada como uma coluna de entrada e uma coluna previsível.  
  
> [!NOTE]  
>  No **modelos de mineração** guia, você também pode criar novos modelos com base na mesma estrutura, e você pode ajustar as propriedades de algoritmo e da coluna para cada modelo. No entanto, você deverá processar o modelo antes que essas alterações entrem em vigor.  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>Para definir a coluna Valor que será usada  
  
1.  No **Forecasting** coluna da grade, na **modelos de mineração** guia, clique na célula na linha de quantidade.  
  
2.  Selecione **Predict** na lista.  
  
     Agora, a coluna Valor passa a ser uma coluna de entrada e uma coluna previsível.  
  
 Você também pode alterar as propriedades das colunas individuais selecionando a coluna e abrindo o **propriedades** janela. Para abrir o **propriedades** janela, clique com botão direito no nome da coluna e, em seguida, selecione **propriedades**. Se você alterar uma propriedade dentro da coluna de um modelo individual, só será possível alterar as propriedades deste modelo. No entanto, quando você altera uma propriedade dentro de **estrutura** coluna, a alteração afetará todo o modelo que está associado com a estrutura. Sempre que você fizer alterações no modelo ou na estrutura, deverá processá-los novamente para ver os efeitos.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Personalizando e processando o modelo de previsão &#40;Tutorial de mineração de dados intermediário&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Estruturas de mineração &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelos de mineração &#40;Analysis Services - mineração de dados&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
