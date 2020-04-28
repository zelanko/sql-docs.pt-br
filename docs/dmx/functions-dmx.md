---
title: Funções (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f68a66e778d44059a83ca6eca3cee35b4dffca9c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892760"
---
# <a name="functions-dmx"></a>Funções (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ao usar o DMX (Data Mining Extensions) para consultar objetos no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você pode usar funções para retornar mais informações do que apenas os valores nas colunas no modelo de Data Mining ou no conjunto de dados de entrada. Por exemplo, use consultas DMX para retornar não apenas o valor de previsão de uma coluna, como também a probabilidade de que a previsão esteja correta. Não somente funções DMX podem ser usadas, como também funções do Microsoft Visual Basic for Applications (VBA), Microsoft Excel e procedimentos armazenados.  
  
## <a name="dmx-functions"></a>Funções DMX  
 Você pode utilizar funções DMX para executar as tarefas a seguir:  
  
-   Retornar previsões.  
  
-   Retornar estatísticas sobre a previsão, como probabilidade e suporte.  
  
-   Filtrar seus resultados de consulta.  
  
-   Reordenar uma expressão de tabela.  
  
 A maioria das funções DMX retornam um valor escalar, como suporte para previsão, mas algumas retornam de resultado tabular. Por exemplo, a função PredictHistogram retorna uma tabela que contém o suporte e a probabilidade para cada Estado da coluna previsível especificada. Os resultados são exibidos como nova coluna de tabela.  
  
 **Para obter mais informações:** [funções de previsão gerais &#40;&#41;DMX ](../dmx/general-prediction-functions-dmx.md), [extensões de Data Mining &#40;referência de função DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Funções do Visual Basic for Applications (VBA) e do Excel  
 Além das funções DMX, é possível chamar também uma série de funções VBA e Excel de instruções DMX. Por exemplo, você pode usar a função lCase para modificar como a coluna de Attribute_Name no conteúdo do modelo de TM_Decision_Tree é exibida. Isso é demonstrado no exemplo de código a seguir.  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 Se a mesma função existir no VBA e no Excel, você deverá prefixar o nome da função em sua instrução DMX com o **VBA** ou o **Excel**. Por exemplo, você usaria `VBA!Log` ou `Excel!Log`. Se a função VBA ou Excel a ser usada também existir em expressões DMX ou MDX (Multidimensional Expressions), ou se a função contiver um caractere de cifrão ($), será preciso usar os colchetes ([]) para escapar a função. Por exemplo, a chamada de função seria `[VBA!Format]`.  
  
## <a name="stored-procedures"></a>Procedimentos armazenados  
 Use as linguagens CLR (Common Language Runtime) para criar procedimentos armazenados que estendem a funcionalidade de DMX. Por exemplo, um modelo de mineração de árvore de regressão retorna coeficientes, como A, B e assim por diante, que descrevem a equação de regressão, mas o modelo não retorna a equação em si, como um + BX = y. Entretanto, é possível gravar um procedimento armazenado que utilize o objeto do modelo de mineração de dados para pesquisar o esquema de conteúdo, e retornar a equação de regressão como saída. Por isso, uma instrução DMX pode retornar a lista das equações de regressão como parte de um resultado de consulta.  
  
 **Para obter mais informações:** [Gerenciamento de assemblies de modelo multidimensional](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-assemblies-management)  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referência de instrução&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-statements.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;&#41;DMX](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
