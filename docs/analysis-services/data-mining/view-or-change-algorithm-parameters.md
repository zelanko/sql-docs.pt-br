---
title: Exibir ou alterar parâmetros do algoritmo | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58b512d726d45a8ceabb76a4ce2b1e6c8c62815b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209563"
---
# <a name="view-or-change-algorithm-parameters"></a>Exibir ou alterar parâmetros do algoritmo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Você pode alterar os parâmetros fornecidos com os algoritmos usados para criar modelos de mineração de dados para personalizar os resultados do modelo.  
  
 Os parâmetros de algoritmo fornecidos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não alteram apenas as propriedades no modelo: eles podem ser usados para alterar significativamente a maneira como dados são processados, agrupados e exibidos. Por exemplo, você pode usar parâmetros de algoritmo para fazer o seguinte:  
  
-   Alterar o método de análise, como o método de clustering.  
  
-   Controlar o comportamento da seleção de recursos.  
  
-   Especificar o tamanho de conjuntos de itens ou a probabilidade de regras.  
  
-   Controlar a ramificação e a profundidade de árvores de decisão.  
  
-   Especificar um valor de semente ou o tamanho do conjunto de controle interno usado na criação de modelo.  
  
 Os parâmetros fornecidos para cada algoritmo variam muito; Para obter uma lista dos parâmetros que podem ser definidas para cada algoritmo, consulte os tópicos de referência técnica nesta seção: [Algoritmos de mineração de dados &#40;Analysis Services - mineração de dados&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
### <a name="change-an-algorithm-parameter"></a>Alterar um parâmetro de algoritmo  
  
1.  Na guia **Modelos de Mineração** do Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse no tipo de modelo de mineração para o qual você quer ajustar o algoritmo e selecione **Definir Parâmetros de Algoritmo**.  
  
     A caixa de diálogo **Parâmetros do Algoritmo** é exibida.  
  
2.  Na coluna **Valor** , defina um novo valor para o algoritmo que você deseja alterar.  
  
     Se você não digitar um valor na coluna **Valor** , o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará o valor de parâmetro padrão. A coluna **Intervalo** descreve os possíveis valores que você pode digitar.  
  
3.  Clique em **OK**.  
  
     O parâmetro de algoritmo será definido com o novo valor. A alteração de parâmetro não será refletida no modelo de mineração até que você processe o modelo novamente.  
  
### <a name="view-the-parameters-used-in-an-existing-model"></a>Exibir os parâmetros usados em um modelo existente  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra uma janela de consulta DMX.  
  
2.  Digite uma consulta como esta:  
  
    ```  
    select MINING_PARAMETERS   
    from $system.DMSCHEMA_MINING_MODELS  
    WHERE MODEL_NAME = '<model name>'  
  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas e instruções do modelo de mineração](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
