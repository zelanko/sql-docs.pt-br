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
manager: kfile
ms.openlocfilehash: 3f0fce34f57591d9c6c3f3a9c7382266d655f364
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37985443"
---
# <a name="functions-dmx"></a>Funções (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Quando você usa extensões DMX (Data Mining) para consultar objetos no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você pode usar funções para retornar informações mais do que apenas os valores nas colunas no modelo de mineração de dados ou conjunto de dados de entrada. Por exemplo, use consultas DMX para retornar não apenas o valor de previsão de uma coluna, como também a probabilidade de que a previsão esteja correta. Não somente funções DMX podem ser usadas, como também funções do Microsoft Visual Basic for Applications (VBA), Microsoft Excel e procedimentos armazenados.  
  
## <a name="dmx-functions"></a>Funções DMX  
 Você pode utilizar funções DMX para executar as tarefas a seguir:  
  
-   Retornar previsões.  
  
-   Retornar estatísticas sobre a previsão, como probabilidade e suporte.  
  
-   Filtrar seus resultados de consulta.  
  
-   Reordenar uma expressão de tabela.  
  
 A maioria das funções DMX retornam um valor escalar, como suporte para previsão, mas algumas retornam de resultado tabular. Por exemplo, a função PredictHistogram retorna uma tabela que contém o suporte e probabilidade para cada estado da coluna previsível especificada. Os resultados são exibidos como nova coluna de tabela.  
  
 **Para obter mais informações:** [funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md), [extensões &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Funções do Visual Basic for Applications (VBA) e do Excel  
 Além das funções DMX, é possível chamar também uma série de funções VBA e Excel de instruções DMX. Por exemplo, você pode usar a função lCase para modificar como a coluna Attribute_Name no conteúdo do modelo TM_Decision_Tree é exibida. Isso é demonstrado no exemplo de código a seguir.  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 Se a mesma função existir no VBA e Excel, você deve prefixar o nome da função na instrução DMX com um **VBA** ou **Excel**. Por exemplo, você usaria `VBA!Log` ou `Excel!Log`. Se a função VBA ou Excel a ser usada também existir em expressões DMX ou MDX (Multidimensional Expressions), ou se a função contiver um caractere de cifrão ($), será preciso usar os colchetes ([]) para escapar a função. Por exemplo, a chamada de função seria `[VBA!Format]`.  
  
## <a name="stored-procedures"></a>Procedimentos armazenados  
 Use as linguagens CLR (Common Language Runtime) para criar procedimentos armazenados que estendem a funcionalidade de DMX. Por exemplo, um modelo de mineração de árvore de regressão retorna coeficientes, como A, B e assim por diante, que descrevem a equação de regressão, mas o modelo não retorna a equação em si, como um + Bx = y. Entretanto, é possível gravar um procedimento armazenado que utilize o objeto do modelo de mineração de dados para pesquisar o esquema de conteúdo, e retornar a equação de regressão como saída. Por isso, uma instrução DMX pode retornar a lista das equações de regressão como parte de um resultado de consulta.  
  
 **Para obter mais informações:** [gerenciamento de Assemblies de modelo Multidimensional](../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; referência](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40;DMX&#41; referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensões de mineração de dados &#40;DMX&#41; convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40;DMX&#41; elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funções de previsão gerais &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estrutura e uso de consultas de previsão DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Compreendendo a instrução DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
